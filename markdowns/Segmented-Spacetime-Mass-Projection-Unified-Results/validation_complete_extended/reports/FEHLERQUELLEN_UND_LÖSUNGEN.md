# SSZ Projekt - Fehlerquellen & Lösungen

**Erstellt:** 2025-10-28  
**Status:** Komplette Übersicht aller gefundenen und gelösten Fehler

---

## 🔴 KRITISCHE FEHLER (GELÖST)

### 1. **IndentationError in test_segwave_core.py**

**Problem:**
```python
E     File "tests/test_segwave_core.py", line 77
E       print(f"  Current ring: T_curr = {T_curr:.1f} K")
E   IndentationError: unexpected indent
```

**Ursache:**
- File wurde durch vorherige Commits korrupt
- Dreifache Wiederholungen von Code-Blöcken
- Falsche Einrückung (4 statt 0 spaces)

**Lösung:**
```bash
git checkout a203d4c -- tests/test_segwave_core.py
```

**Commit:** `8c7d0fa`  
**Verhindert durch:** Python Cache löschen nach git operations

---

### 2. **SyntaxError in test_multi_body_sigma.py**

**Problem:**
```python
E     File "tests/cosmos/test_multi_body_sigma.py", line 50
E       print(f"  • Bot
E             ^
E   SyntaxError: unterminated string literal (detected at line 50)
```

**Ursache:**
- Unterminated f-string
- File-Korruption durch Edits

**Lösung:**
```bash
git checkout a203d4c -- tests/cosmos/test_multi_body_sigma.py
```

**Commit:** `2c3b82f`  
**Verhindert durch:** Syntax validation vor commit

---

### 3. **NameError: numpy nicht importiert**

**Problem:**
```python
E   NameError: name 'np' is not defined
# in scripts/tests/test_data_validation.py line 243
```

**Ursache:**
- Fehlender `import numpy as np`

**Lösung:**
```python
# In test_data_validation.py hinzufügen:
import numpy as np
```

**Commit:** `215da6b`  
**Verhindert durch:** Import-Check vor Test-Run

---

### 4. **Git LFS Error in Colab**

**Problem:**
```
error: external filter 'git-lfs filter-process' failed
fatal: assets/ssz_animations/blackhole_segmented_spacetime.gif: smudge filter lfs failed
```

**Ursache:**
- Colab hat kein Git LFS installiert
- Repo nutzt LFS für große GIF-Files (10+ MB)

**Lösung:**
```python
# Neue Colab-Zelle VOR dem Clone:
!curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
!apt-get install -y git-lfs
!git lfs install

# Im Clone-Cell:
!git clone https://github.com/...
%cd ...
!git lfs pull  # WICHTIG!
```

**Commit:** `0829ec4`  
**Verhindert durch:** Colab-Setup dokumentiert

---

### 5. **JSON Serialization: numpy.bool_ Error**

**Problem:**
```python
TypeError: Object of type bool is not JSON serializable
# in run_ssz_theory_validation.py line 464
```

**Ursache:**
- NumPy types (np.bool_, np.int64, etc.) sind nicht JSON-serializable
- Python's `json.dump()` kann nur native Python types

**Lösung:**
```python
def convert_numpy(obj):
    """Convert numpy types to Python types for JSON serialization"""
    import numpy as np
    if isinstance(obj, np.bool_):
        return bool(obj)
    elif isinstance(obj, np.integer):
        return int(obj)
    elif isinstance(obj, np.floating):
        return float(obj)
    elif isinstance(obj, np.ndarray):
        return obj.tolist()
    elif isinstance(obj, dict):
        return {k: convert_numpy(v) for k, v in obj.items()}
    elif isinstance(obj, (list, tuple)):
        return [convert_numpy(item) for item in obj]
    return obj

# Vor json.dump():
results_converted = convert_numpy(results)
json.dump(results_converted, f, indent=2, ensure_ascii=False)
```

**Commit:** `0909104`  
**Verhindert durch:** NumPy type conversion Standard-Template

---

## ⚠️ AKTUELLE FEHLER (ZU FIXEN)

### 6. **Missing pyarrow/fastparquet in requirements.txt**

**Problem:**
```python
ImportError: Unable to find a usable engine; tried using: 'pyarrow', 'fastparquet'.
A suitable version of pyarrow or fastparquet is required for parquet support.
```

**Betrifft:**
- `scripts/tests/test_ssz_invariants.py` (4 tests)
- Alle Tests die `pd.read_parquet()` verwenden

**Ursache:**
- `pyarrow` fehlt in requirements.txt
- Parquet-Support ist optional in pandas

**Lösung:**
```bash
# In requirements.txt hinzufügen:
pyarrow>=10.0.0
```

**Alternative:**
```python
# Wenn pyarrow nicht verfügbar ist, CSV als Fallback:
try:
    df = pd.read_parquet(field_path)
except ImportError:
    csv_path = field_path.replace('.parquet', '.csv')
    df = pd.read_csv(csv_path)
```

**Status:** ❌ TO DO  
**Priorität:** HOCH (betrifft Linux-Installationen)

---

## 🐛 HÄUFIGE PROBLEME

### 7. **Python Cache Issues**

**Problem:**
- Tests schlagen fehl obwohl Code korrekt ist
- pytest lädt alte .pyc Files
- Änderungen werden nicht erkannt

**Symptome:**
```
ERROR collecting tests/test_segwave_core.py
IndentationError: unexpected indent
# Obwohl File korrekt ist!
```

**Lösung:**
```bash
# Windows PowerShell:
Remove-Item -Recurse -Force __pycache__,.pytest_cache,tests\__pycache__,tests\cosmos\__pycache__,scripts\tests\__pycache__

# Linux:
find . -type d -name __pycache__ -exec rm -rf {} +
find . -type d -name .pytest_cache -exec rm -rf {} +
```

**Wann auftreten:**
- Nach git checkout
- Nach git pull
- Nach manuellen File-Edits
- Nach fehlgeschlagenen Tests

**Verhindert durch:**
- Cache löschen VOR jedem Test-Run
- Cache löschen NACH git operations
- .gitignore für __pycache__

---

### 8. **UTF-8 Encoding (Windows)**

**Problem:**
```python
UnicodeEncodeError: 'charmap' codec can't encode character '\u2713'
```

**Ursache:**
- Windows nutzt cp1252 statt UTF-8
- subprocess.run() ohne encoding parameter
- Griechische Buchstaben (β, γ, α, φ) in Output

**Lösung:**
```python
# Template für alle Scripts:
import os
import sys

# UTF-8 Setup
os.environ['PYTHONIOENCODING'] = 'utf-8:replace'

if sys.platform.startswith('win'):
    try:
        sys.stdout.reconfigure(encoding='utf-8', errors='replace')
        sys.stderr.reconfigure(encoding='utf-8', errors='replace')
    except:
        pass

# subprocess IMMER mit encoding:
subprocess.run(
    cmd,
    capture_output=True,
    text=True,
    encoding='utf-8',      # KRITISCH!
    errors='replace',      # KRITISCH!
    timeout=timeout
)
```

**Betrifft:**
- Alle Test-Scripts mit Physical Interpretations
- Alle Scripts mit griechischen Variablen
- Windows-Systeme

---

### 9. **Missing Columns in DataFrames**

**Problem:**
```python
AssertionError: Expected column 'mass_msun' not found
```

**Ursache:**
- Verschiedene CSV-Versionen nutzen andere Spaltennamen
- Alte: `M_msun`, Neue: `mass_msun`, Alternative: `M_solar`

**Lösung:**
```python
# Flexible column checks:
mass_columns = ['mass_msun', 'M_msun', 'M_solar']
assert any(col in df.columns for col in mass_columns), f"No mass column found. Available: {df.columns.tolist()}"

# Get the actual column:
mass_col = next(col for col in mass_columns if col in df.columns)
mass = df[mass_col]
```

**Verhindert durch:**
- Flexible column lookups
- Clear error messages with available columns

---

## 📋 CHECKLISTE VOR COMMIT

### Pre-Commit Checks:

```bash
# 1. Python Syntax
python -m py_compile file.py

# 2. Imports vorhanden
grep -n "^import\|^from" file.py

# 3. Cache löschen
find . -type d -name __pycache__ -exec rm -rf {} +

# 4. pytest dry-run
pytest --collect-only

# 5. Git status
git status
git diff
```

### Pre-Push Checks:

```bash
# 1. Alle Tests lokal
pytest tests/ scripts/tests/ -v

# 2. Requirements aktuell
pip freeze > requirements-freeze.txt
diff requirements.txt requirements-freeze.txt

# 3. Git LFS Status
git lfs status

# 4. UTF-8 Encoding Check
file -i *.py | grep -v utf-8

# 5. Final validation
python run_all_validations.py
```

---

## 🔧 AUTOMATISCHE FIXES

### Script: `cleanup.sh` (Linux)

```bash
#!/bin/bash
# Cleanup Script für SSZ Projekt

echo "🧹 Cleaning Python cache..."
find . -type d -name __pycache__ -exec rm -rf {} + 2>/dev/null
find . -type d -name .pytest_cache -exec rm -rf {} + 2>/dev/null
find . -type f -name "*.pyc" -delete
find . -type f -name "*.pyo" -delete

echo "✅ Cache cleaned"

echo "🔍 Checking for syntax errors..."
python3 -m py_compile tests/*.py scripts/tests/*.py 2>&1 | grep -v "File contains no section headers"

echo "✅ Syntax check complete"
```

### Script: `cleanup.ps1` (Windows)

```powershell
# Cleanup Script für SSZ Projekt

Write-Host "🧹 Cleaning Python cache..." -ForegroundColor Yellow
Get-ChildItem -Path . -Include __pycache__,.pytest_cache -Recurse -Force -ErrorAction SilentlyContinue | Remove-Item -Recurse -Force
Get-ChildItem -Path . -Include *.pyc,*.pyo -Recurse -Force -ErrorAction SilentlyContinue | Remove-Item -Force

Write-Host "✅ Cache cleaned" -ForegroundColor Green

Write-Host "🔍 Checking for syntax errors..." -ForegroundColor Yellow
Get-ChildItem -Path tests,scripts\tests -Filter *.py -Recurse | ForEach-Object {
    python -m py_compile $_.FullName 2>&1 | Out-Null
    if ($LASTEXITCODE -eq 0) {
        Write-Host "  ✓ $($_.Name)" -ForegroundColor Green
    } else {
        Write-Host "  ✗ $($_.Name)" -ForegroundColor Red
    }
}

Write-Host "✅ Syntax check complete" -ForegroundColor Green
```

---

## 📚 DEPENDENCY UPDATES NEEDED

### requirements.txt Ergänzungen:

```txt
# Aktuelle requirements.txt +

# Parquet Support (für test_ssz_invariants.py)
pyarrow>=10.0.0

# Optional: Fastparquet als Alternative
# fastparquet>=0.8.0

# Colab-spezifisch (bereits via Git LFS Cell gelöst):
# git-lfs (nicht via pip, via apt)
```

---

## 🎯 BEST PRACTICES

### 1. **File Edits:**
- IMMER Syntax-Check nach Edit
- IMMER Cache löschen nach git operations
- IMMER backup vor großen Changes

### 2. **Git Operations:**
```bash
# Nach jedem checkout/pull:
find . -type d -name __pycache__ -exec rm -rf {} +

# Vor jedem commit:
python -m py_compile file.py
```

### 3. **Test Runs:**
```bash
# Cache löschen
# Dann erst:
pytest tests/ -v

# Bei Failures:
# 1. Cache nochmal löschen
# 2. Git status prüfen
# 3. Syntax-Check
```

### 4. **Colab Notebooks:**
```python
# IMMER am Anfang:
# Cell 1: Git LFS install
# Cell 2: Clone + lfs pull
# Cell 3: Requirements install
```

---

## 📊 STATUS ÜBERSICHT

| Fehler | Status | Commit | Priorität |
|--------|--------|--------|-----------|
| IndentationError test_segwave_core | ✅ GEFIXT | 8c7d0fa | KRITISCH |
| SyntaxError test_multi_body_sigma | ✅ GEFIXT | 2c3b82f | KRITISCH |
| NameError numpy import | ✅ GEFIXT | 215da6b | HOCH |
| Git LFS Colab | ✅ GEFIXT | 0829ec4 | HOCH |
| JSON numpy.bool_ | ✅ GEFIXT | 0909104 | HOCH |
| pyarrow requirements.txt | ❌ TO DO | - | HOCH |
| Python Cache | ⚠️ WORKAROUND | - | MITTEL |
| UTF-8 Windows | ✅ GEFIXT | - | MITTEL |

---

## 🚀 NÄCHSTE SCHRITTE

### Sofort (HOCH):
1. ✅ pyarrow zu requirements.txt hinzufügen
2. ✅ cleanup.sh / cleanup.ps1 erstellen
3. ✅ Diese Dokumentation committen

### Später (MITTEL):
1. Pre-commit hooks einrichten
2. CI/CD um Cache-Cleanup erweitern
3. Automatische Syntax-Checks

### Optional (NIEDRIG):
1. Parquet → CSV Fallback implementieren
2. Column-Name-Aliasing standardisieren
3. Test-Suite Refactoring

---

## 📞 KONTAKT

Bei neuen Fehlern:
1. Screenshot + Error-Message dokumentieren
2. Prüfen ob in dieser Liste
3. Wenn neu: Issue erstellen mit Context

---

**© 2025 Carmen Wrede & Lino Casu**  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Last Updated:** 2025-10-28  
**Version:** 1.0  
**Commits today:** 26 total
