# SSZ Test Architecture - WICHTIG!

**Datum:** 2025-10-28  
**Status:** KRITISCHE INFORMATION FÜR ENTWICKLER

---

## ⚠️ WICHTIG: KEINE PYTEST-TESTS!

### Die Tests sind NORMALE Python-Skripte!

**FALSCH angenommen:**
```bash
pytest tests/  # ❌ Das sind KEINE pytest-Tests!
```

**RICHTIG:**
```bash
python tests/test_segwave_core.py  # ✓ Normale Python-Skripte
python scripts/tests/test_ssz_kernel.py  # ✓ Direkt ausführbar
```

---

## 🔍 WARUM DAS WICHTIG IST

### 1. Test-Files sind normale .py Dateien

**Alle diese sind NORMALE Python-Skripte:**
- `tests/test_segwave_core.py`
- `tests/cosmos/test_multi_body_sigma.py`
- `scripts/tests/test_ssz_kernel.py`
- `scripts/tests/test_ssz_invariants.py`
- `scripts/tests/test_segmenter.py`
- `scripts/tests/test_cosmo_fields.py`
- `scripts/tests/test_cosmo_multibody.py`

**Sie enthalten:**
- Normale Python-Funktionen
- `if __name__ == "__main__":` Blöcke
- Direkte print() Statements
- KEINE pytest fixtures
- KEINE pytest decorators (@pytest.mark.*)

---

## ✅ WIE MAN SIE AUSFÜHRT

### Methode 1: Direkt als Python-Skript (EMPFOHLEN)

```bash
# Einzelner Test
python tests/test_segwave_core.py

# Mit vollem Pfad
python /home/error/Segmented-Spacetime-Mass-Projection-Unified-Results/tests/test_segwave_core.py

# Alle Tests in einem Verzeichnis
for f in tests/*.py; do python "$f"; done
```

### Methode 2: Via pytest (FUNKTIONIERT AUCH, aber nicht nötig)

```bash
# pytest kann normale Python-Skripte auch ausführen
pytest tests/test_segwave_core.py -v

# ABER: Das ist overhead, da es keine pytest-Features nutzt
```

---

## 📋 TEST-STRUKTUR

### Typisches Test-File:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Test Description
"""

def test_something():
    """Normal Python function"""
    print("Testing...")
    result = calculate_something()
    assert result > 0, "Test failed"
    print("✓ Test passed")

if __name__ == "__main__":
    print("="*80)
    print("RUNNING TESTS")
    print("="*80)
    
    test_something()
    
    print("="*80)
    print("ALL TESTS PASSED")
    print("="*80)
```

**Das ist KEIN pytest-Test, sondern ein normales Python-Skript!**

---

## 🎯 WARUM DIESE ARCHITEKTUR?

### Vorteile:

1. **Keine pytest-Abhängigkeit**
   - Tests laufen ohne pytest-Installation
   - Weniger Dependencies

2. **Direkt ausführbar**
   - `python test.py` funktioniert immer
   - Keine pytest-Konfiguration nötig

3. **Einfacher zu debuggen**
   - Normale Python-Ausgabe
   - Keine pytest-Magic

4. **Cross-Platform**
   - Funktioniert überall wo Python läuft
   - Keine pytest-Versionsunterschiede

---

## 📊 WIE run_full_suite.py ARBEITET

### Das Master-Script:

```python
# run_full_suite.py führt Tests als Subprozesse aus:

subprocess.run([sys.executable, "tests/test_segwave_core.py"])
# NICHT: pytest.main(["tests/test_segwave_core.py"])
```

**Es startet jedes Test-File als normales Python-Skript!**

---

## ⚠️ PYTEST.INI IST OPTIONAL

### Die pytest.ini Datei existiert, ABER:

```ini
[pytest]
testpaths = tests scripts/tests
python_files = test_*.py
python_classes = Test*
python_functions = test_*
# timeout = 300  # COMMENTED OUT - pytest-timeout ist optional
```

**Diese Datei ist NUR für den Fall dass jemand pytest benutzt.**

**Die Tests selbst brauchen sie NICHT!**

---

## 🔧 FÜR ENTWICKLER

### Wenn du einen neuen Test schreibst:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Dein neuer Test
"""

def test_my_feature():
    """Normale Python-Funktion"""
    # Dein Test-Code
    assert something == expected
    print("✓ Test passed")

if __name__ == "__main__":
    # Mach es direkt ausführbar
    test_my_feature()
```

**NICHT:**
```python
import pytest  # ❌ Nicht nötig!

@pytest.mark.parametrize(...)  # ❌ Nicht nötig!
def test_my_feature():
    ...
```

---

## 📝 DOKUMENTATION IN ANDEREN FILES

### Wo das erwähnt wird:

1. **README.md** - Sollte erwähnen: "Tests sind normale Python-Skripte"
2. **TEST_SUITE_README.md** - Sollte Ausführung erklären
3. **INSTALL_README.md** - pytest ist optional
4. **requirements.txt** - pytest ist NICHT drin (optional)

---

## 🎯 PRAKTISCHE BEISPIELE

### Beispiel 1: Alle Tests laufen

```bash
# Methode A: Via Master-Script (EMPFOHLEN)
python run_full_suite.py

# Methode B: Manuell alle Tests
for test in tests/*.py scripts/tests/*.py; do
    echo "Running $test..."
    python "$test"
done

# Methode C: Via pytest (funktioniert, aber overhead)
pytest tests/ scripts/tests/ -v
```

### Beispiel 2: Einzelner Test debuggen

```bash
# Direkt ausführen
python tests/test_segwave_core.py

# Mit Python-Debugger
python -m pdb tests/test_segwave_core.py

# Mit Ausgabe-Umleitung
python tests/test_segwave_core.py > output.log 2>&1
```

---

## ⚠️ HÄUFIGE FEHLER

### Fehler 1: pytest als Requirement

```txt
# requirements.txt
pytest>=7.0.0  # ❌ FALSCH - nicht nötig!
```

**Richtig:**
```txt
# requirements.txt
# pytest ist OPTIONAL für Test-Ausführung
# Tests sind normale Python-Skripte
```

### Fehler 2: pytest-spezifische Features nutzen

```python
import pytest  # ❌ FALSCH

@pytest.fixture
def my_fixture():  # ❌ FALSCH - funktioniert nicht ohne pytest
    ...
```

**Richtig:**
```python
# Keine pytest-Imports
# Normale Python-Funktionen
def setup_test_data():  # ✓ RICHTIG
    ...
```

### Fehler 3: Annahme dass pytest installiert ist

```python
# In einem Script:
import pytest  # ❌ FALSCH - könnte fehlen
pytest.main([...])
```

**Richtig:**
```python
import subprocess
subprocess.run([sys.executable, "tests/test.py"])  # ✓ RICHTIG
```

---

## 📊 VERGLEICH

### pytest-Tests vs. Unsere Tests

| Feature | pytest-Tests | Unsere Tests |
|---------|--------------|--------------|
| Ausführung | `pytest tests/` | `python tests/test.py` |
| Dependencies | pytest required | Nur Python |
| Fixtures | Ja | Nein (normale Funktionen) |
| Parametrize | Ja | Nein (normale Loops) |
| Plugins | Ja | Nein |
| Debugging | pytest --pdb | python -m pdb |
| CI/CD | pytest --junitxml | Exit codes |

---

## ✅ ZUSAMMENFASSUNG

### Die 3 wichtigsten Punkte:

1. **Tests sind normale Python-Skripte**
   - Keine pytest-Abhängigkeit
   - Direkt mit `python test.py` ausführbar

2. **pytest ist OPTIONAL**
   - Kann benutzt werden, muss aber nicht
   - Tests funktionieren ohne pytest

3. **run_full_suite.py startet Tests als Subprozesse**
   - Nicht via pytest.main()
   - Via subprocess.run([sys.executable, ...])

---

## 🎯 FÜR CI/CD

### GitHub Actions / GitLab CI:

```yaml
# .github/workflows/tests.yml
- name: Run Tests
  run: |
    # NICHT: pytest tests/
    # SONDERN:
    python run_full_suite.py
    
    # ODER einzeln:
    python tests/test_segwave_core.py
    python scripts/tests/test_ssz_kernel.py
```

---

## 📚 REFERENZEN

**Siehe auch:**
- `run_full_suite.py` - Master test runner
- `run_all_validations.py` - Pipeline runner
- `TEST_SUITE_README.md` - Test documentation
- Memory: SYSTEM-RETRIEVED-MEMORY[138930ac-ba12-4c02-b925-8d034fb2c7ac]

---

**© 2025 Carmen Wrede & Lino Casu**  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Status:** ✅ KRITISCHE ARCHITEKTUR-INFO DOKUMENTIERT
