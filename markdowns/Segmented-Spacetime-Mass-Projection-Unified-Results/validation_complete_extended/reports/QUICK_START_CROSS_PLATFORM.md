# Quick Start - Cross-Platform

## 🚀 Schnellstart für Linux und Windows

---

## 🐧 **LINUX / macOS**

### Setup:
```bash
# Scripts executable machen
chmod +x run_verbose_tests.sh run_tests_safe.sh run_comprehensive_tests.sh

# Dependencies installieren
pip3 install -r requirements.txt
```

### Tests ausführen:
```bash
# Option 1: Shell-Script (empfohlen)
./run_verbose_tests.sh scripts/tests/

# Option 2: Python-Script (plattform-unabhängig)
python3 run_comprehensive_tests.py --verbose

# Option 3: Direkt pytest
python3 -X utf8 -m pytest scripts/tests/ -s -v
```

---

## 🪟 **WINDOWS**

### Setup:
```cmd
REM Dependencies installieren
pip install -r requirements.txt

REM UTF-8 Encoding setzen
set PYTHONUTF8=1
```

### Tests ausführen:
```cmd
REM Option 1: Batch-Script (empfohlen)
run_verbose_tests.bat scripts\tests\

REM Option 2: Python-Script (plattform-unabhängig)
python run_comprehensive_tests.py --verbose

REM Option 3: Direkt pytest
python -X utf8 -m pytest scripts\tests\ -s -v
```

---

## 🌍 **PLATTFORM-UNABHÄNGIG**

### Diese Commands funktionieren ÜBERALL:

```bash
# Comprehensive Real Data Tests
python run_comprehensive_tests.py --verbose

# Mit HTML Report
python run_comprehensive_tests.py --html --output results

# Spezifische Tests
python -X utf8 -m pytest tests/test_ssz_real_data_comprehensive.py -s -v

# Mit Filter
python -X utf8 -m pytest tests/ -k "PPN or gamma" -s -v

# JUnit XML Output
python -X utf8 -m pytest tests/ --junitxml=junit.xml
```

---

## 📋 Test-Suite Übersicht

| Test Suite | Linux Command | Windows Command | Plattform-unabhängig |
|------------|---------------|-----------------|---------------------|
| **Verbose Tests** | `./run_verbose_tests.sh scripts/tests/` | `run_verbose_tests.bat scripts\tests\` | `python -X utf8 -m pytest scripts/tests/ -s -v` |
| **Safe Runner** | `./run_tests_safe.sh tests/` | `run_tests_safe.bat tests\` | `python -X utf8 -m pytest tests/ -s -v` |
| **Comprehensive** | `./run_comprehensive_tests.sh --verbose` | `python run_comprehensive_tests.py --verbose` | `python run_comprehensive_tests.py --verbose` |

---

## 🎯 Häufige Anwendungsfälle

### 1. Alle Tests mit physikalischen Interpretationen:

**Linux:**
```bash
./run_verbose_tests.sh scripts/tests/
```

**Windows:**
```cmd
run_verbose_tests.bat scripts\tests\
```

**Beide:**
```bash
python -X utf8 -m pytest scripts/tests/ -s -v
```

### 2. Nur SSZ Kernel Tests:

**Linux:**
```bash
./run_verbose_tests.sh scripts/tests/test_ssz_kernel.py
```

**Windows:**
```cmd
run_verbose_tests.bat scripts\tests\test_ssz_kernel.py
```

**Beide:**
```bash
python -X utf8 -m pytest scripts/tests/test_ssz_kernel.py -s -v
```

### 3. Comprehensive Tests mit HTML Report:

**Linux:**
```bash
./run_comprehensive_tests.sh --html --verbose
```

**Windows:**
```cmd
python run_comprehensive_tests.py --html --verbose
```

**Beide:**
```bash
python run_comprehensive_tests.py --html --verbose
```

### 4. Tests für spezifisches Objekt (z.B. Sgr A*):

**Beide Plattformen:**
```bash
python run_comprehensive_tests.py --object "SgrA" --verbose
python -X utf8 -m pytest tests/ -k "SgrA" -s -v
```

---

## 🔧 Troubleshooting

### Linux: "Permission denied"

```bash
# Lösung: Script executable machen
chmod +x run_verbose_tests.sh
```

### Linux: "python: command not found"

```bash
# Lösung: python3 verwenden
python3 -X utf8 -m pytest tests/
```

### Windows: "PowerShell Extension Crash"

```cmd
REM Lösung: CMD verwenden statt PowerShell
cmd /c "python -m pytest tests\ -s -v"

REM Oder Safe Runner:
run_tests_safe.bat tests\
```

### Windows: "charmap codec error"

```cmd
REM Lösung: UTF-8 erzwingen
set PYTHONUTF8=1
python -X utf8 -m pytest tests\
```

### Beide: "No module named pytest"

```bash
# Lösung: Dependencies installieren
pip install -r requirements.txt

# Oder nur pytest:
pip install pytest pytest-html
```

---

## 📊 Beispiel-Outputs

### Gamma Bounds Test:

```
================================================================================
GAMMA SEGMENT FIELD TEST
================================================================================
Density range: ρ = [0.0, 100.0]

Gamma values:
  ρ =    0.0 → γ = 1.000000
  ρ =  100.0 → γ = 0.020000

Physical Interpretation:
  • γ decreases with density (segment saturation)
  • Bounded between floor and 1.0 (physical limits)
================================================================================
PASSED
```

### SSZ Ring Velocity:

```
================================================================================
SSZ RING VELOCITY: Two-Shell Propagation
================================================================================
Configuration:
  Ring 1: T = 100.0 K, v = 10.0 km/s (initial)
  Ring 2: T = 80.0 K

Velocity Propagation:
  v_2 = 11.1803 km/s

Physical Interpretation:
  • Cooler ring → Higher velocity
  • SSZ predicts velocity increase of 11.8%
================================================================================
PASSED
```

---

## 💡 Pro-Tipps

### 1. Verwende Python-Scripts für maximale Kompatibilität:

```bash
# Funktioniert auf Linux UND Windows:
python run_comprehensive_tests.py --verbose
```

### 2. Speichere Results in plattform-unabhängigem Format:

```bash
# JUnit XML (Standard-Format)
python -X utf8 -m pytest tests/ --junitxml=results.xml

# HTML Report
python -X utf8 -m pytest tests/ --html=report.html --self-contained-html
```

### 3. Nutze pytest-Parameter statt Shell-Scripts:

```bash
# Diese Parameter funktionieren identisch auf beiden Plattformen:
-s                  # Show print() output
-v                  # Verbose
-k "PATTERN"        # Filter tests
--tb=short          # Short tracebacks
--junitxml=FILE     # JUnit XML
--html=FILE         # HTML report
```

---

## 📚 Weitere Dokumentation

- **CROSS_PLATFORM_GUIDE.md** - Detaillierte Plattform-Unterschiede
- **VERBOSE_TESTS_GUIDE.md** - Anleitung für verbose tests
- **VERBOSE_TESTS_STATUS.md** - Status aller Tests
- **PYTEST_CRASH_FIX.md** - PowerShell-Crash-Lösungen

---

## ✅ Checkliste

### Vor dem Testen:

- [ ] Python >= 3.8 installiert
- [ ] Dependencies installiert (`pip install -r requirements.txt`)
- [ ] (Linux) Scripts executable (`chmod +x *.sh`)
- [ ] (Windows) UTF-8 Encoding gesetzt

### Nach dem Testen:

- [ ] Alle Tests PASSED
- [ ] Physikalische Interpretationen sichtbar (mit `-s` flag)
- [ ] Reports generiert (JUnit XML / HTML)
- [ ] Keine Encoding-Fehler
- [ ] Keine Pfad-Probleme

---

**🎯 Empfehlung:**

**Für maximale Cross-Platform Kompatibilität:**

```bash
# Verwende immer Python-Scripts:
python run_comprehensive_tests.py --verbose

# Oder pytest direkt mit -X utf8:
python -X utf8 -m pytest tests/ -s -v
```

**Diese Commands funktionieren identisch auf Linux, macOS und Windows!**

---

**© 2025 Carmen Wrede, Lino Casu**  
**Anti-Capitalist Software License (v 1.4)**
