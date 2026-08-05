# SSZ Pipeline - Automatische Schutzmaßnahmen

## ✅ Implementierte Guardrails (2025-10-17)

### 1. **Repo-Root-Wächter**
- **Datei**: `ci/autorun_suite.py`
- **Funktion**: Prüft beim Start automatisch, ob das Script aus dem korrekten Verzeichnis ausgeführt wird
- **Verhalten**: Bricht sofort mit klarer Fehlermeldung ab, falls falsches Verzeichnis
- **Vorteil**: Keine "file not found" Fehler mehr, keine versehentlichen Läufe im falschen Ordner

```python
# Wird automatisch in main() aufgerufen
ensure_correct_repo_root()
```

### 2. **UTF-8 Erzwingung überall** ⭐ VOLLSTÄNDIG
- **Problem behoben**: `'charmap' codec can't decode byte 0x90` Crashes (z.B. bei µ, —, etc.)
- **Umsetzung**:
  - `run_all_ssz_terminal.py`: stdout/stderr direkt auf UTF-8 rekonfiguriert (Zeilen 19-33)
  - `ci/autorun_suite.py`: UTF-8 für **ALLE** Subprozesse (git, pytest, sweep, terminal scripts)
  - Neue Hilfsfunktion: `_utf8_env()` für konsistente Umgebungsvariablen
  - Alle `subprocess.run()` und `subprocess.Popen()` mit `encoding="utf-8", errors="replace"`
  - `run_suite.cmd` verwendet `-X utf8` Flag für maximale Kompatibilität

### 3. **Absolute Pytest-Pfade**
- **Problem behoben**: "no tests ran" bei falschem Arbeitsverzeichnis
- **Umsetzung**: Tests werden jetzt über absoluten Pfad gefunden:
```python
tests_dir = str(ROOT / "scripts" / "tests")
```

### 4. **Quarantäne des alten Ordners**
- **Alter Name**: `H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results`
- **Neuer Name**: `H:\WINDSURF\___quarantined_DO_NOT_USE`
- **Vorteil**: Nur noch ein aktives Repo → keine Verwechslungsgefahr

### 5. **Convenience Launcher**
- **Datei**: `run_suite.cmd`
- **Verwendung**: 
  - Doppelklick im Explorer, oder
  - Terminal: `run_suite`
- **Vorteil**: 
  - Läuft immer im korrekten Verzeichnis
  - Kein PowerShell nötig
  - Keine CD-Befehle notwendig

### 6. **Automatische Summary-Generierung** ⭐ NEU
- **Script**: `summary-all-tests.py`
- **Ausgabe**: `output-summary.md` (automatisch nach jedem Suite-Lauf)
- **Funktion**: Aggregiert alle Test-Ergebnisse, PyTest-Stats, SSZ/GAIA Reports
- **Integration**: Wird automatisch in `ci/autorun_suite.py` aufgerufen
- **Vorteil**: 
  - Komplette Übersicht ohne manuelle Aggregation
  - Markdown-Format (leicht lesbar, versionierbar)
  - Keine Plots (nur Text/Daten für schnelle Review)

## 🚀 Verwendung

### Einfacher Start (empfohlen)
```cmd
run_suite
```
oder einfach `run_suite.cmd` im Explorer doppelklicken.

### Manueller Start
```powershell
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python ci/autorun_suite.py
```

### Einzelne Tests
```powershell
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python -m pytest scripts/tests/test_gaia_required_columns.py -q
```

## 🛡️ Was passiert bei Fehlern?

### Falsches Verzeichnis
```
======================================================================
FEHLER: Falsches Arbeitsverzeichnis!
======================================================================
  Gefunden     : H:\WINDSURF\___quarantined_DO_NOT_USE
  Erwartet endet mit: _bak_2025-10-17_17-03-00

Bitte wechseln Sie in den korrekten Backup-Ordner:
  cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
======================================================================
```
→ Script beendet sich sofort mit Exit-Code 2

### UTF-8 Probleme
→ Werden automatisch abgefangen durch `errors="replace"`  
→ Sonderzeichen werden als Platzhalter dargestellt statt Crash

## 📋 Technische Details

### Subprocess-Aufrufe (alle UTF-8 sicher)
```python
subprocess.run(
    cmd,
    capture_output=True,
    text=True,
    encoding="utf-8",
    errors="replace",
    env=_utf8_env(os.environ),
)
```

### Logger (UTF-8 sicher)
```python
FileHandler(log_path, encoding="utf-8")
```

### Umgebungsvariablen (automatisch gesetzt)
- `PYTHONUTF8=1`
- `PYTHONIOENCODING=utf-8`
- `LC_ALL=C.UTF-8`
- `LANG=C.UTF-8`

## ⚠️ Wichtige Hinweise

1. **Verwenden Sie immer das `_bak_2025-10-17_17-03-00` Verzeichnis**
2. **Nie manuell ins quarantinierte Verzeichnis wechseln**
3. **Bei Updates: `EXPECTED_ROOT_SUFFIX` in `ci/autorun_suite.py` anpassen**
4. **Logs nie als Befehle ins Terminal pasten** (wird automatisch verhindert durch Guardrails)

## 🔧 Wartung

Falls Sie das Repo-Verzeichnis umbenennen:
1. Neuen Suffix in `ci/autorun_suite.py` setzen:
```python
EXPECTED_ROOT_SUFFIX = "_neuer_suffix"
```
2. Pfad in `run_suite.cmd` anpassen:
```cmd
cd /d "H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_neuer_suffix"
```

---
**Erstellt**: 2025-10-17  
**Letztes Update**: 2025-10-17  
**Status**: ✅ Produktiv
