# Pytest Cache Problem - Lösung

**Datum:** 2025-11-27 02:00  
**Problem:** Tests zeigen alte Syntax-Errors obwohl Dateien korrekt sind  
**Ursache:** Pytest cached alte/kaputte Versionen  

---

## 🔴 **Problem**

Nach dem Git Push zeigen Tests plötzlich wieder alte Fehler:

```
E     File "tests/test_segwave_core.py", line 47
E       print(f"  Previou    
E             ^
E   SyntaxError: unterminated string literal (detected at line 47)
```

**ABER:** Die Datei ist korrekt! 
```python
47: print(f"  Previous ring: T_prev = {T_prev:.1f} K")  # ✅ KORREKT
```

---

## ⚠️ **Root Cause: Pytest Cache**

Pytest cached die **ALTE VERSION** der Dateien und verwendet sie weiter, auch wenn die Dateien längst gefixt sind!

**Cache-Locations:**
```
.pytest_cache/              # Root cache
tests/.pytest_cache/        # Test directory cache
tests/__pycache__/          # Python bytecode
tests/cosmos/__pycache__/   # Subdirectory bytecode
```

---

## ✅ **Lösung: Cache Löschen**

### **Option 1: PowerShell (Windows)**
```powershell
Remove-Item -Recurse -Force .pytest_cache, tests/.pytest_cache, tests/__pycache__, tests/cosmos/__pycache__ -ErrorAction SilentlyContinue
```

### **Option 2: Bash (Linux/Mac)**
```bash
rm -rf .pytest_cache tests/.pytest_cache tests/__pycache__ tests/cosmos/__pycache__
```

### **Option 3: Python Script**
```python
import shutil
from pathlib import Path

for cache in ['.pytest_cache', '__pycache__']:
    for cache_dir in Path('.').rglob(cache):
        if cache_dir.is_dir():
            shutil.rmtree(cache_dir, ignore_errors=True)
```

### **Option 4: pytest Flag**
```bash
python -m pytest tests/ --cache-clear -v
```

---

## 🎯 **Best Practice: IMMER Cache löschen**

### **Vor jedem Test-Run:**
```bash
# 1. Cache löschen
.\CLEAR_CACHE.bat  # oder ./CLEAR_CACHE.sh

# 2. Tests laufen
python run_full_suite.py
```

### **Nach Git Operations:**
```bash
# Nach git pull/checkout/merge
Remove-Item -Recurse -Force .pytest_cache -ErrorAction SilentlyContinue

# Dann Tests
python -m pytest --cache-clear
```

---

## 📊 **Wann tritt das Problem auf?**

### **Häufige Szenarien:**

1. **Nach Edits:**
   - Datei gefixt
   - Pytest verwendet cached Version
   - Tests schlagen fehl obwohl Fix korrekt

2. **Nach Git Pull:**
   - Neue Version gepullt
   - Cache hat alte Version
   - Tests zeigen alte Fehler

3. **Nach Branch Switch:**
   - Branch gewechselt
   - Cache aus anderem Branch
   - Inkonsistente Ergebnisse

4. **Nach Refactoring:**
   - Viele Dateien geändert
   - Cache hat Mix aus alt/neu
   - Mysteriöse Fehler

---

## 🔍 **Symptome**

### **Wie erkenne ich Cache-Probleme?**

✅ **Definitiv Cache-Problem wenn:**
- Datei ist korrekt, aber Test zeigt Syntax-Error
- `git diff` zeigt keine Änderungen
- Selbe Zeile, aber anderer Inhalt im Error
- Error verschwindet nach `--cache-clear`

⚠️ **Vielleicht Cache-Problem wenn:**
- Tests schlagen unerwartet fehl
- Imports funktionieren nicht
- Alte Variablen-Namen in Errors
- Unterschiedliche Ergebnisse bei wiederholtem Run

---

## 🛠️ **Permanente Lösung**

### **CLEAR_CACHE.bat erweitern:**

```batch
@echo off
echo Clearing ALL pytest and Python caches...

REM 1. Pytest cache
for /d /r . %%d in (.pytest_cache) do @if exist "%%d" (
    rd /s /q "%%d" 2>nul
)

REM 2. Python bytecode
for /d /r . %%d in (__pycache__) do @if exist "%%d" (
    rd /s /q "%%d" 2>nul
)

REM 3. .pyc files
del /s /q *.pyc 2>nul

echo Cache cleared!
```

### **run_full_suite.py erweitern:**

```python
# Am Anfang von run_full_suite.py
import shutil
from pathlib import Path

def clear_all_caches():
    """Clear pytest cache and Python bytecode"""
    for pattern in ['.pytest_cache', '__pycache__']:
        for cache_dir in Path('.').rglob(pattern):
            if cache_dir.is_dir():
                try:
                    shutil.rmtree(cache_dir)
                except:
                    pass

# VOR allen Tests ausführen
clear_all_caches()
```

---

## 📝 **Dokumentierte Fälle**

### **Fall 1: 2025-11-27 (Heute)**
- **Problem:** SyntaxError in test_segwave_core.py Zeile 47
- **Symptom:** `print(f"  Previou    ` (unvollständig)
- **Realität:** Datei war korrekt gefixt
- **Lösung:** Cache löschen → 20/20 Tests passing ✅

### **Fall 2: Nach Refactoring**
- **Problem:** Alte Variablen-Namen in Tests
- **Symptom:** NameError für umbenannte Variablen
- **Realität:** Alle Variablen waren umbenannt
- **Lösung:** `--cache-clear` Flag → Tests passing ✅

---

## ⚡ **Quick Reference**

### **Problem:**
```
Tests schlagen fehl, aber Dateien sind korrekt
```

### **Lösung:**
```bash
# Windows
Remove-Item -Recurse -Force .pytest_cache -ErrorAction SilentlyContinue

# Linux/Mac
rm -rf .pytest_cache

# Dann
python -m pytest --cache-clear
```

### **Verification:**
```bash
python -m pytest tests/test_segwave_core.py -v
# Sollte jetzt passing sein
```

---

## ✅ **Nach Cache-Clear Checklist**

- [x] .pytest_cache entfernt
- [x] __pycache__ entfernt
- [x] Tests mit --cache-clear laufen
- [x] Alle Tests bestehen
- [x] Keine mysteriösen Errors mehr

---

## 🎉 **Finale Empfehlung**

**IMMER vor wichtigen Test-Runs:**

```bash
# 1. Cache löschen
.\CLEAR_CACHE.bat

# 2. Tests laufen
python run_full_suite.py

# 3. Erfolg verifizieren
# Expected: 23/23 tests passing
```

**Regel:** *"When in doubt, clear the cache!"*

---

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**

**Lizenz:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4
