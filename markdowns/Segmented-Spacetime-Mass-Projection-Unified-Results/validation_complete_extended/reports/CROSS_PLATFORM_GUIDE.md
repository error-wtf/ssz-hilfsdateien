# Cross-Platform Testing Guide

## Übersicht

Alle Tests funktionieren auf **Linux** und **Windows**!

---

## 🐧 Linux / macOS

### Setup:

```bash
# Executable machen
chmod +x run_verbose_tests.sh
chmod +x run_tests_safe.sh
chmod +x run_comprehensive_tests.sh

# Python 3 benötigt
python3 --version  # Should be >= 3.8
```

### Tests ausführen:

```bash
# Verbose tests
./run_verbose_tests.sh scripts/tests/test_ssz_kernel.py

# Safe runner
./run_tests_safe.sh tests/test_ssz_real_data_comprehensive.py -s -v

# Comprehensive tests
./run_comprehensive_tests.sh --verbose
```

### Direkt mit pytest:

```bash
# Mit UTF-8 (wichtig für Sonderzeichen)
python3 -X utf8 -m pytest scripts/tests/ -s -v

# Spezifische Tests
python3 -m pytest tests/test_ssz_real_data_comprehensive.py -k "PPN" -s -v
```

---

## 🪟 Windows

### Setup:

```cmd
REM Python 3 benötigt
python --version  REM Should be >= 3.8

REM UTF-8 Encoding setzen
set PYTHONUTF8=1
set PYTHONIOENCODING=utf-8
```

### Tests ausführen:

```cmd
REM Verbose tests
run_verbose_tests.bat scripts\tests\test_ssz_kernel.py

REM Safe runner
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -s -v

REM Comprehensive tests
python run_comprehensive_tests.py --verbose
```

### Direkt mit pytest:

```cmd
REM Mit UTF-8 (wichtig für Sonderzeichen)
python -X utf8 -m pytest scripts\tests\ -s -v

REM Spezifische Tests
python -m pytest tests\test_ssz_real_data_comprehensive.py -k "PPN" -s -v
```

---

## 🔄 Plattform-Unterschiede

### Pfad-Separatoren:

```python
# ✅ RICHTIG (plattform-unabhängig):
from pathlib import Path
test_file = Path("tests") / "test_ssz_kernel.py"

# ❌ FALSCH (nur Windows):
test_file = "tests\\test_ssz_kernel.py"

# ❌ FALSCH (nur Linux):
test_file = "tests/test_ssz_kernel.py"
```

### UTF-8 Encoding:

```python
# ✅ RICHTIG (plattform-unabhängig):
with open(file, 'r', encoding='utf-8') as f:
    content = f.read()

# Python Flag:
# Linux:   python3 -X utf8 script.py
# Windows: python -X utf8 script.py

# Environment:
# Linux:   export PYTHONUTF8=1
# Windows: set PYTHONUTF8=1
```

### Shell-Scripts:

| Feature | Linux (.sh) | Windows (.bat) |
|---------|-------------|----------------|
| **Shebang** | `#!/usr/bin/env bash` | N/A |
| **Variablen** | `$VAR` oder `${VAR}` | `%VAR%` oder `!VAR!` |
| **If-Bedingung** | `if [ -z "$VAR" ]` | `if "%VAR%"==""` |
| **Pfade** | `/` | `\` oder `/` |
| **Python** | `python3` | `python` |
| **Exit Code** | `$?` | `%errorlevel%` |

---

## 📝 Test-Scripts

### Verfügbar für beide Plattformen:

| Script | Linux | Windows | Funktion |
|--------|-------|---------|----------|
| **Verbose Tests** | `run_verbose_tests.sh` | `run_verbose_tests.bat` | Tests mit physikalischen Interpretationen |
| **Safe Runner** | `run_tests_safe.sh` | `run_tests_safe.bat` | Verhindert PowerShell-Crashes |
| **Comprehensive** | `run_comprehensive_tests.sh` | `run_comprehensive_tests.py` | Umfassende Real-Data Tests |

---

## 🧪 Pytest-Parameter (identisch auf beiden Plattformen)

```bash
# Grundlegende Flags:
-v            # Verbose (zeigt Test-Namen)
-s            # No capture (zeigt print() Output)
--tb=short    # Kurze Tracebacks
-k "PATTERN"  # Filtert Tests nach Pattern

# Output-Formate:
--junitxml=junit.xml           # JUnit XML Report
--html=report.html             # HTML Report (benötigt pytest-html)
--self-contained-html          # HTML mit embedded CSS/JS

# Parallel (benötigt pytest-xdist):
-n auto       # Nutzt alle CPU-Kerne
-n 4          # Nutzt 4 Kerne
```

---

## 🐛 Plattform-spezifische Probleme

### Windows:

#### Problem 1: PowerShell Extension Crash
```
ValueError: I/O operation on closed file
```

**Lösung:**
```cmd
REM Verwende Safe Runner:
run_tests_safe.bat tests\ -s -v

REM Oder CMD statt PowerShell:
cmd /c "python -m pytest tests\ -s -v"
```

#### Problem 2: Encoding-Fehler
```
'charmap' codec can't encode character
```

**Lösung:**
```cmd
REM UTF-8 erzwingen:
set PYTHONUTF8=1
python -X utf8 -m pytest tests\
```

### Linux:

#### Problem 1: Permission Denied
```bash
bash: ./run_verbose_tests.sh: Permission denied
```

**Lösung:**
```bash
chmod +x run_verbose_tests.sh
./run_verbose_tests.sh
```

#### Problem 2: python vs python3
```bash
python: command not found
```

**Lösung:**
```bash
# Verwende python3 statt python:
python3 -m pytest tests/

# Oder erstelle Alias:
alias python=python3
```

---

## 🎯 Best Practices

### 1. Plattform-unabhängige Pfade:

```python
from pathlib import Path
import os

# ✅ RICHTIG:
base_dir = Path(__file__).parent
test_file = base_dir / "tests" / "test_example.py"

# ✅ RICHTIG:
data_path = os.path.join("data", "results", "output.csv")

# ❌ FALSCH:
test_file = "tests\\test_example.py"  # Nur Windows
test_file = "tests/test_example.py"   # Nur Linux
```

### 2. UTF-8 immer explizit:

```python
# ✅ RICHTIG:
with open(file, 'r', encoding='utf-8') as f:
    content = f.read()

Path(file).read_text(encoding='utf-8')

# ❌ FALSCH:
with open(file, 'r') as f:  # Platform-dependent encoding
    content = f.read()
```

### 3. Subprocess mit Encoding:

```python
# ✅ RICHTIG:
subprocess.run(
    cmd,
    capture_output=True,
    text=True,
    encoding='utf-8',
    errors='replace'
)

# ❌ FALSCH:
subprocess.run(cmd, capture_output=True, text=True)
```

### 4. Shell-Scripts für beide Plattformen:

```bash
# Erstelle BEIDE:
run_tests.sh   # Für Linux/macOS
run_tests.bat  # Für Windows

# Oder verwende Python-Script (plattform-unabhängig):
run_tests.py   # Funktioniert überall
```

---

## 🚀 Quick Commands

### Linux:

```bash
# Alle Tests
./run_verbose_tests.sh scripts/tests/

# Spezifische Tests
./run_tests_safe.sh tests/test_ssz_real_data_comprehensive.py -k "PPN"

# Mit HTML Report
./run_comprehensive_tests.sh --html --verbose
```

### Windows:

```cmd
REM Alle Tests
run_verbose_tests.bat scripts\tests\

REM Spezifische Tests
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "PPN"

REM Mit HTML Report
python run_comprehensive_tests.py --html --verbose
```

### Plattform-unabhängig (Python):

```bash
# Funktioniert auf Linux UND Windows:
python -X utf8 -m pytest tests/ -s -v
python run_comprehensive_tests.py --verbose
python extend_all_tests.py --dry-run
```

---

## 📦 CI/CD Integration

### GitHub Actions (Linux):

```yaml
name: SSZ Tests
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - run: pip install -r requirements.txt
      - run: chmod +x run_verbose_tests.sh
      - run: ./run_verbose_tests.sh scripts/tests/ --junitxml=junit.xml
```

### GitHub Actions (Windows):

```yaml
name: SSZ Tests (Windows)
on: [push, pull_request]

jobs:
  test:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - run: pip install -r requirements.txt
      - run: run_verbose_tests.bat scripts\tests\ --junitxml=junit.xml
        shell: cmd
```

### GitHub Actions (Matrix - Beide):

```yaml
name: SSZ Tests (Matrix)
on: [push, pull_request]

jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        python-version: ['3.8', '3.9', '3.10', '3.11']
    
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      - run: pip install -r requirements.txt
      
      # Plattform-unabhängig:
      - run: python -X utf8 -m pytest tests/ -s -v --junitxml=junit.xml
```

---

## ✅ Checkliste: Cross-Platform Kompatibilität

### Code:

- [x] `pathlib.Path()` statt String-Pfade
- [x] `encoding='utf-8'` in allen File-Operations
- [x] `subprocess.run(..., encoding='utf-8')`
- [x] Keine hardcoded `\` oder `/` in Pfaden
- [x] `python3` (Linux) vs `python` (Windows) handling

### Scripts:

- [x] `.sh` Scripts für Linux/macOS
- [x] `.bat` Scripts für Windows
- [x] `.py` Scripts als plattform-unabhängige Alternative
- [x] Executable permissions (`chmod +x`) dokumentiert

### Tests:

- [x] UTF-8 Output in allen print() Statements
- [x] Plattform-unabhängige Assertions
- [x] Keine OS-spezifischen Imports ohne Guards

### Dokumentation:

- [x] Linux-Beispiele
- [x] Windows-Beispiele
- [x] Plattform-Unterschiede dokumentiert
- [x] Troubleshooting für beide Plattformen

---

## 🎉 Zusammenfassung

### ✅ Was funktioniert auf beiden Plattformen:

- **Alle Python-Tests** (mit `-X utf8`)
- **Pytest-Parameter** (identisch)
- **Print-Output** (mit UTF-8 encoding)
- **Physikalische Interpretationen** (alle Tests)
- **JUnit XML / HTML Reports** (identisch)

### ⚠️ Plattform-spezifisch:

- **Shell-Scripts** (.sh vs .bat)
- **Python-Command** (python3 vs python)
- **Pfad-Separatoren** (verwende `pathlib.Path()`)

### 🚀 Empfehlung:

**Für maximale Kompatibilität:**
```bash
# Verwende Python-Scripts (funktioniert überall):
python run_comprehensive_tests.py --verbose

# Oder pytest direkt:
python -X utf8 -m pytest tests/ -s -v
```

---

**© 2025 Carmen Wrede, Lino Casu**  
**Anti-Capitalist Software License (v 1.4)**
