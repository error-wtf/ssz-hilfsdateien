# UTF-8 Encoding Fix — Windows PowerShell

**Problem**: `'charmap' codec can't decode byte 0x90` Fehler bei Suite-Runs

**Lösung**: UTF-8 dauerhaft aktivieren

---

## 🔧 Einmalige Systemeinrichtung

### PowerShell (als Administrator):
```powershell
# Umgebungsvariablen dauerhaft setzen
setx PYTHONIOENCODING UTF-8
setx LC_ALL C.UTF-8
setx LANG C.UTF-8

# Konsolen-Codepage auf UTF-8
chcp 65001
```

### PowerShell-Profil (optional, für automatisches chcp):
```powershell
# Öffnen:
notepad $PROFILE

# Hinzufügen:
chcp 65001 > $null
$env:PYTHONIOENCODING="UTF-8"
$env:LC_ALL="C.UTF-8"
$env:LANG="C.UTF-8"
```

---

## 📝 Code-Fixes (bereits implementiert)

### 1. Alle File-Writes mit encoding="utf-8"
```python
# ✓ RICHTIG
with open(path, "w", encoding="utf-8") as f:
    f.write(content)

# ✓ RICHTIG
Path(file).write_text(content, encoding="utf-8")

# ✗ FALSCH (nutzt System-Default)
with open(path, "w") as f:  # BAD
    f.write(content)
```

### 2. Subprocess mit UTF-8 Environment
```python
import subprocess
import os

def _utf8_env():
    env = dict(os.environ)
    env["PYTHONIOENCODING"] = "UTF-8"
    env["LC_ALL"] = "C.UTF-8"
    env["LANG"] = "C.UTF-8"
    return env

# Aufruf
subprocess.run(
    cmd,
    env=_utf8_env(),
    encoding="utf-8",
    errors="replace",  # Fallback für invalid chars
)
```

### 3. sys.stdout reconfigure (Start von Scripts)
```python
import sys

# Am Anfang von run_all_ssz_terminal.py, etc.
sys.stdout.reconfigure(encoding="utf-8", errors="replace")
sys.stderr.reconfigure(encoding="utf-8", errors="replace")
```

---

## ✅ Verification

### Test ausführen:
```powershell
pytest scripts/tests/test_utf8_encoding.py -v
```

**Erwartete Ausgabe**:
```
test_utf8_environment PASSED
test_stdout_encoding PASSED
test_utf8_file_write_read PASSED
test_json_utf8 PASSED
```

---

## 🐛 Troubleshooting

### Problem: Test schlägt fehl mit "PYTHONIOENCODING not UTF-8"
**Lösung**: 
1. PowerShell neu starten (damit setx wirkt)
2. Prüfen: `$env:PYTHONIOENCODING` → sollte "UTF-8" sein

### Problem: Konsole zeigt Fragezeichen statt Sonderzeichen
**Lösung**: `chcp 65001` in PowerShell ausführen

### Problem: Git zeigt Encoding-Warnings
**Lösung**: `.gitattributes` setzen:
```
*.py text eol=lf
*.md text eol=lf
*.json text eol=lf
*.csv text eol=lf
```

---

**Status**: ✅ Implementiert in Suite (seit 2025-10-18)
