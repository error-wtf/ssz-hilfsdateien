# Pytest Crash Fix - "I/O operation on closed file"

## Problem

Bei Ausführung von pytest in PowerShell oder durch PowerShell Extension:

```
ValueError: I/O operation on closed file.
  File "...\pytest\capture.py", line 591, in snap
    self.tmpfile.seek(0)
```

**Ursache:** PowerShell Extension parst pytest's Output und schließt dabei File-Handles, während pytest noch darauf zugreift.

---

## Schnelle Lösung

### Option 1: Safe Batch-Wrapper (Empfohlen)

```cmd
run_tests_safe.bat tests/test_ssz_real_data_comprehensive.py
```

**Vorteile:**
- ✅ Umgeht PowerShell komplett
- ✅ UTF-8 encoding
- ✅ Korrekte pytest Flags
- ✅ Keine Output-Capture-Probleme

### Option 2: Pytest Flags verwenden

```cmd
python -X utf8 -m pytest tests/ -s --tb=short -v
```

**Wichtig:** `-s` Flag deaktiviert Output-Capture!

### Option 3: CMD statt PowerShell

```cmd
cmd /c "python -m pytest tests/ -v"
```

---

## Detaillierte Analyse

### Was passiert:

1. **Pytest startet** und aktiviert Output-Capture
2. **Tests laufen** und produzieren Output (stdout/stderr)
3. **PowerShell Extension** versucht Output zu parsen
4. **Extension schließt** File-Handles während Parsing
5. **Pytest versucht** Capture zu beenden (`tmpfile.seek(0)`)
6. **CRASH:** File ist bereits geschlossen

### Warum bei comprehensive tests?

Die neuen comprehensive tests (`test_ssz_real_data_comprehensive.py`) geben **viel Output**:

```python
print("="*80)
print("PPN PARAMETER β")
print("="*80)
print(f"Calculated β:  {beta:.12f}")
# ... 20+ Zeilen pro Test
```

**Mehr Output = Höhere Wahrscheinlichkeit für PowerShell Parsing-Konflikt**

---

## Lösungen im Detail

### 1. run_tests_safe.bat

**Neu erstellt:** Safe Test Runner

```batch
@echo off
REM Bypasses PowerShell Extension

chcp 65001 >nul 2>&1
set PYTHONUTF8=1
set PYTHONIOENCODING=utf-8

python -X utf8 -m pytest "%TEST_PATH%" -s --tb=short -v %EXTRA_ARGS%
```

**Verwendung:**

```cmd
# Alle comprehensive tests
run_tests_safe.bat tests/test_ssz_real_data_comprehensive.py

# Nur PPN tests
run_tests_safe.bat tests/test_ssz_real_data_comprehensive.py -k "PPN"

# Nur Sgr A*
run_tests_safe.bat tests/test_ssz_real_data_comprehensive.py -k "SgrA"

# Mit verbose output
run_tests_safe.bat tests/test_ssz_real_data_comprehensive.py -v -s
```

### 2. Pytest Flags

**Kritischer Flag:** `-s` (no capture)

```cmd
python -m pytest tests/ -s           # ← Kein Capture
python -m pytest tests/ --tb=short   # ← Kurze Tracebacks
python -m pytest tests/ -v           # ← Verbose
```

**Kombiniert:**
```cmd
python -X utf8 -m pytest tests/test_ssz_real_data_comprehensive.py -s -v --tb=short
```

### 3. Comprehensive Test Runner

**Bereits existiert:** `run_comprehensive_tests.py`

```bash
python run_comprehensive_tests.py --verbose
```

Dieser verwendet bereits sichere subprocess-Aufrufe mit UTF-8 encoding.

---

## Für verschiedene Test-Typen

### Comprehensive Real Data Tests:

```cmd
# Safe wrapper
run_tests_safe.bat tests/test_ssz_real_data_comprehensive.py

# Oder Python runner
python run_comprehensive_tests.py --verbose

# Oder direkt (mit -s flag!)
python -X utf8 -m pytest tests/test_ssz_real_data_comprehensive.py -s -v
```

### Scripts/tests:

```cmd
# Safe wrapper
run_tests_safe.bat scripts/tests/

# Oder direkt
python -m pytest scripts/tests/ -s -v
```

### Alle Tests:

```cmd
# CI Suite (safe)
.\ci\run_suite_safe.bat

# Oder safe wrapper
run_tests_safe.bat tests/ scripts/tests/
```

---

## Warum "no tests ran"?

Wenn pytest **keine Tests findet**, prüfen:

### 1. Test-Discovery

```python
# Tests müssen mit test_ beginnen oder _test enden:
def test_something():  # ✓ Wird gefunden
    pass

def something_test():  # ✓ Wird gefunden
    pass

def check_something():  # ✗ Wird NICHT gefunden
    pass
```

### 2. Klassen-Namen

```python
class TestSomething:  # ✓ Muss mit Test beginnen
    def test_method(self):
        pass

class MySuite:  # ✗ Wird NICHT gefunden
    def test_method(self):
        pass
```

### 3. Datei-Namen

```python
# ✓ Diese Dateien werden gefunden:
test_example.py
test_ssz_real_data_comprehensive.py
example_test.py

# ✗ Diese werden IGNORIERT:
example.py
check_tests.py
validate_data.py
```

### 4. Import-Fehler

Wenn Import fehlschlägt, werden Tests übersprungen:

```cmd
# Prüfen mit --collect-only
python -m pytest tests/ --collect-only

# Zeigt:
# - Welche Tests gefunden wurden
# - Oder: Import-Fehler
```

---

## Für CI/CD

### GitHub Actions / GitLab CI:

```yaml
# Kein PowerShell-Problem in Linux CI
- name: Run comprehensive tests
  run: |
    python -m pytest tests/test_ssz_real_data_comprehensive.py -v --junitxml=junit.xml
```

### Windows CI:

```yaml
# Muss safe flags verwenden
- name: Run comprehensive tests (Windows)
  shell: cmd
  run: |
    python -X utf8 -m pytest tests/test_ssz_real_data_comprehensive.py -s -v --junitxml=junit.xml
```

---

## Best Practices

### 1. Immer UTF-8 verwenden:

```cmd
python -X utf8 -m pytest ...
```

### 2. Bei viel Output: -s Flag:

```cmd
python -m pytest tests/test_ssz_real_data_comprehensive.py -s
```

### 3. In CI: Shell explizit setzen:

```yaml
shell: cmd  # oder bash
```

### 4. Safe Wrapper nutzen:

```cmd
run_tests_safe.bat <test-path>
```

---

## Troubleshooting

### Problem: Tests werden nicht gefunden

```cmd
# Prüfen was pytest sieht:
python -m pytest tests/ --collect-only

# Prüfen mit verbose:
python -m pytest tests/ -v --collect-only
```

### Problem: Import-Fehler

```cmd
# Python path prüfen:
python -c "import sys; print('\n'.join(sys.path))"

# Modul importieren testen:
python -c "from tests import test_ssz_real_data_comprehensive"
```

### Problem: Encoding-Fehler

```cmd
# UTF-8 erzwingen:
set PYTHONUTF8=1
set PYTHONIOENCODING=utf-8
python -X utf8 -m pytest ...
```

### Problem: PowerShell Crash

```cmd
# Lösung 1: CMD verwenden
cmd /c "python -m pytest tests/ -v"

# Lösung 2: -s Flag
python -m pytest tests/ -s -v

# Lösung 3: Safe wrapper
run_tests_safe.bat tests/
```

---

## Zusammenfassung

### ✅ VERWENDEN:

```cmd
# Option 1: Safe Wrapper (Empfohlen)
run_tests_safe.bat tests/test_ssz_real_data_comprehensive.py

# Option 2: Mit -s Flag
python -X utf8 -m pytest tests/ -s -v

# Option 3: Comprehensive Runner
python run_comprehensive_tests.py --verbose
```

### ❌ VERMEIDEN:

```cmd
# NICHT ohne -s flag bei viel Output:
python -m pytest tests/test_ssz_real_data_comprehensive.py

# NICHT in PowerShell Extension bei langen Tests:
# (Extension wird Output parsen und crashen)
```

---

## Neue Dateien

- ✅ `run_tests_safe.bat` - Safe Test Runner
- ✅ `PYTEST_CRASH_FIX.md` - Diese Dokumentation

---

## Lizenz

Anti-Capitalist Software License (v 1.4)
© 2025 Carmen Wrede, Lino Casu
