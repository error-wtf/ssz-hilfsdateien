# Safe Commit System

## Problem

Nach Test-Runs werden temporäre Dateien erstellt, die **NICHT** ins Repository gehören. Wenn diese versehentlich committed werden, führt das zu Fehlern beim nächsten Clone/Pull.

## Lösung: 3 neue Scripts

### 1. `safe_commit.ps1` - Sicheres Committen (EMPFOHLEN)

**Verwendung:**
```powershell
.\safe_commit.ps1
```

**Was es tut:**
1. ✅ Löscht automatisch Cache-Dateien
2. ✅ Zeigt Git-Status
3. ✅ Fragt welche Dateien committed werden sollen:
   - **Option 1 (EMPFOHLEN)**: Nur Source-Dateien (*.py, *.md, etc.)
   - Option 2: Spezifische Dateien manuell auswählen
   - Option 3: Alles (GEFÄHRLICH!)
4. ✅ Führt Pre-Commit Checks aus
5. ✅ Erstellt Commit nur wenn alles OK ist

**Beispiel:**
```powershell
PS> .\safe_commit.ps1

[1/5] Cache löschen...
  ✓ Cache gelöscht

[2/5] Git Status:
  M tests/test_segwave_core.py
  M run_full_suite.py

[3/5] Dateien zum Committen:
Welche Dateien sollen committed werden?
  1) Alle Source-Dateien (*.py, *.md, *.txt - EMPFOHLEN)
  2) Spezifische Dateien (manuell auswählen)
  3) Alles (GEFÄHRLICH - nicht empfohlen!)
  4) Abbrechen

Auswahl (1-4): 1

[4/5] Pre-Commit Check...
  ✓ Keine Cache-Dateien gefunden
  ✓ Syntax-Check bestanden

[5/5] Commit erstellen...
Commit Message: FIX: Corrected test indentation

✓ Commit erfolgreich erstellt!
```

---

### 2. `check_before_commit.ps1` - Pre-Commit Validation

**Verwendung:**
```powershell
.\check_before_commit.ps1
```

**Was es tut:**
1. ✅ Prüft ob Cache/Temp-Dateien gestaged wurden
2. ✅ Blockiert Commit wenn gefährliche Dateien gefunden werden
3. ✅ Führt Python Syntax-Check aus
4. ✅ Zeigt Warnungen und Lösungsvorschläge

**Blockierte Dateien:**
- `__pycache__/` - Python Bytecode Cache
- `.pytest_cache/` - Pytest Cache
- `*.pyc`, `*.pyo`, `*.pyd` - Kompilierte Python-Dateien
- `summary-output.md` - Temporäre Test-Logs
- `*.log` - Log-Dateien

**Beispiel (Fehler gefunden):**
```powershell
PS> .\check_before_commit.ps1

[1/3] Prüfe gestagte Dateien...
  Gestagte Dateien:
    tests/test_segwave_core.py
    tests/__pycache__/test_segwave_core.cpython-310.pyc

[2/3] Prüfe auf Cache/Temp-Dateien...
  ⚠️  WARNUNG: Cache/Temp-Dateien gefunden!
    Pattern: __pycache__
      tests/__pycache__/test_segwave_core.cpython-310.pyc

❌ COMMIT BLOCKIERT!

Diese Dateien sollten NICHT ins Repository:
  - __pycache__/ (Python Bytecode)
  - .pytest_cache/ (Test Cache)

Lösung:
  1. Cache löschen: .\CLEAR_CACHE.bat
  2. Dateien unstagen: git reset HEAD <datei>
  3. Nur Source-Dateien stagen: git add <spezifische-datei>
```

---

### 3. `DONT_AUTO_SYNC.md` - Dokumentation

Erklärt das Problem und zeigt Best Practices.

---

## Workflow: Richtig Committen

### ✅ RICHTIG (mit safe_commit.ps1):

```powershell
# 1. Änderungen machen
# ... Code editieren ...

# 2. Tests laufen lassen
python run_full_suite.py

# 3. Safe Commit verwenden
.\safe_commit.ps1

# 4. Pushen
git push origin main
```

### ✅ RICHTIG (manuell):

```powershell
# 1. Cache löschen
.\CLEAR_CACHE.bat

# 2. Status prüfen
git status

# 3. Nur Source-Dateien stagen
git add tests/test_segwave_core.py
git add run_full_suite.py

# 4. Pre-Commit Check
.\check_before_commit.ps1

# 5. Committen
git commit -m "FIX: Corrected test indentation"

# 6. Pushen
git push origin main
```

### ❌ FALSCH:

```powershell
# NIEMALS SO:
git add -A                    # ❌ Staged ALLES (inkl. Cache!)
git commit -m "Update"        # ❌ Kein Check!
git push                      # ❌ Pushed beschädigte Dateien!
```

---

## Warum ist das wichtig?

### Problem-Szenario:

1. **Test-Run:** `python run_full_suite.py`
   - Erstellt `__pycache__/`, `.pytest_cache/`
   - Generiert temporäre Logs

2. **Falsches Commit:** `git add -A && git commit`
   - Committed Cache-Dateien
   - Committed beschädigte Test-Dateien

3. **Push:** `git push`
   - Beschädigte Dateien landen auf GitHub

4. **Nächster Clone/Pull:**
   - Tests schlagen sofort fehl
   - IndentationError in test_segwave_core.py
   - Cache-Konflikte

### Lösung:

**IMMER `safe_commit.ps1` verwenden!**

---

## Integration in Workflow

### Option 1: Alias erstellen

```powershell
# In PowerShell Profile ($PROFILE):
function sc { .\safe_commit.ps1 @args }

# Dann einfach:
sc
```

### Option 2: Git Alias

```bash
git config --global alias.safe '!powershell -File safe_commit.ps1'

# Dann:
git safe
```

### Option 3: Pre-Commit Hook (automatisch)

```bash
# .git/hooks/pre-commit erstellen:
#!/bin/sh
powershell -File check_before_commit.ps1
```

---

## Fehlerbehebung

### "Commit blockiert - Cache-Dateien gefunden"

**Lösung:**
```powershell
# 1. Cache löschen
.\CLEAR_CACHE.bat

# 2. Dateien unstagen
git reset HEAD

# 3. Nur Source-Dateien stagen
git add *.py *.md

# 4. Erneut versuchen
.\safe_commit.ps1
```

### "Syntax-Fehler in Python-Datei"

**Lösung:**
```powershell
# 1. Datei prüfen
python -m py_compile tests/test_segwave_core.py

# 2. Fehler beheben

# 3. Erneut versuchen
.\safe_commit.ps1
```

### "Keine Änderungen zu committen"

Das ist OK! Bedeutet Repository ist bereits synchronisiert.

---

## Best Practices

### ✅ DO:
- Verwende `safe_commit.ps1` für alle Commits
- Lösche Cache vor jedem Commit
- Stage nur Source-Dateien
- Prüfe `git status` vor dem Commit
- Führe Tests aus vor dem Push

### ❌ DON'T:
- Verwende NIEMALS `git add -A` ohne Check
- Committe NIEMALS direkt nach Test-Run
- Skippe NIEMALS Pre-Commit Checks
- Pushe NIEMALS ohne lokale Tests

---

## Zusammenfassung

**Ein Befehl für sicheres Committen:**

```powershell
.\safe_commit.ps1
```

Das war's! 🎉

---

© 2025 Carmen Wrede, Lino Casu
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
