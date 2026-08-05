# ⚠️ WARNUNG: NICHT AUTOMATISCH SYNCEN!

## Problem

Nach dem ersten Test-Run werden temporäre/beschädigte Dateien erstellt, die **NICHT** committed werden sollten!

## Betroffene Dateien

- `tests/__pycache__/` - Python Bytecode Cache
- `.pytest_cache/` - Pytest Cache
- `reports/summary-output.md` - Temporäre Test-Logs
- `*.pyc`, `*.pyo` - Kompilierte Python-Dateien
- Alle Test-Output-Dateien die während der Ausführung modifiziert werden

## ❌ NIEMALS TUN:

```bash
# FALSCH - committed alles inklusive Müll:
git add -A
git commit -m "Update"
git push
```

## ✅ RICHTIG:

### Option 1: Selektiv committen
```bash
# Nur spezifische Dateien:
git add tests/test_segwave_core.py
git add run_full_suite.py
git commit -m "FIX: Specific changes"
git push
```

### Option 2: Vor Commit prüfen
```bash
# Zeige was committed werden würde:
git status

# Zeige Diff:
git diff

# Nur dann committen wenn alles OK ist!
git add <spezifische-dateien>
git commit -m "..."
git push
```

### Option 3: Cache vorher löschen
```bash
# Windows:
.\CLEAR_CACHE.bat

# Linux/Mac:
./CLEAR_CACHE.sh

# Dann erst committen
```

## Warum passiert das?

1. Test-Run erstellt temporäre Dateien
2. Pytest cached Ergebnisse
3. Wenn Cache beschädigt ist → Tests schlagen fehl
4. `git add -A` committed den beschädigten Cache
5. Nächster Clone/Pull hat sofort Fehler

## Lösung

**VOR jedem Commit:**

1. ✅ Cache löschen: `.\CLEAR_CACHE.bat`
2. ✅ Tests laufen: `python run_full_suite.py`
3. ✅ Nur Source-Dateien committen (keine `__pycache__`, keine `.pytest_cache`)
4. ✅ `.gitignore` prüfen ob Cache ignoriert wird

## .gitignore Regeln (MUSS enthalten sein!)

```gitignore
# Python Cache
__pycache__/
*.py[cod]
*$py.class
*.so
.Python

# Pytest
.pytest_cache/
.cache/

# Test Outputs
reports/summary-output.md
test_results/*.xml
*.log

# IDE
.vscode/
.idea/
*.swp
*.swo
```

## Automatisches Sync deaktivieren

Falls du ein Auto-Sync Tool verwendest:
- **GitHub Desktop**: Deaktiviere "Automatically sync"
- **VS Code Git**: Deaktiviere "Auto Fetch"
- **Git Hooks**: Prüfe `.git/hooks/` auf post-commit hooks

---

© 2025 Carmen Wrede, Lino Casu
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
