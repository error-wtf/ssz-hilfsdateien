# Summary-All-Tests Tool

## 📁 Speicherorte

### Script
```
H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00\summary-all-tests.py
```

### Standard-Ausgabe
```
H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00\output-summary.md
```

## 🚀 Verwendung

### ⭐ Automatisch (nach jedem Suite-Lauf)
Das Script wird **automatisch am Ende jeder Suite-Ausführung** aufgerufen:
```powershell
run_suite
# → output-summary.md wird automatisch generiert
```

### Manuell (neueste Run-ID)
```powershell
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python -X utf8 summary-all-tests.py
```

### Mit spezifischer Run-ID
```powershell
python -X utf8 summary-all-tests.py --run-id 2025-10-17_gaia_ssz_real
```

### Mit benutzerdefinierter Ausgabe
```powershell
python -X utf8 summary-all-tests.py --out mein-report.md
```

### Alle Optionen
```powershell
python -X utf8 summary-all-tests.py --root . --run-id <run-id> --out <output-file.md>
```
Note: Replace `<output-file.md>` with your desired filename (e.g., `report.md`)

## 📊 Was wird aggregiert?

### 1. Suite-Status (`ci/suite_manifest.json`)
- Run-ID, Start/Ende, Gesamtstatus
- Liste aller ausgeführten Schritte mit Dauer

### 2. PyTest-Ergebnisse
- **Repository gesamt**: `testergebnisse/<run-id>/repo_pytest_full.xml`
- **Scripts/Tests**: `reports/<run-id>/pytest_results.xml`
- Anzahl Tests, Failures, Errors, Skipped, Dauer

### 3. SSZ/GAIA Reports (`agent_out/reports/`)
- **Bound Energy**: `bound_energy.txt`
- **Redshift-Auswertung**:
  - Medians: `redshift_medians.json`
  - Paired Stats: `redshift_paired_stats.json`
- **Mass Validation**: `mass_validation.csv` (mit Vorschau)

### 4. Debug-Dateien (`out/`)
- **Enhanced Debug**: `_enhanced_debug.csv` (Kennzahlen)
- **Explain Debug**: `_explain_debug.csv` (Vorschau)

## 📝 Ausgabeformat

Die generierte Markdown-Datei enthält:
- ✅ Strukturierte Tabellen (PyTest-Stats)
- ✅ CSV-Vorschauen mit Zeilenzahl
- ✅ JSON-Zusammenfassungen (Redshift, Paired Stats)
- ✅ Fehlerbehandlung (fehlende Dateien → Hinweis statt Crash)
- ✅ UTF-8 sicher (keine Encoding-Fehler)

## 🛡️ Robustheit

Das Script ist robust gegen:
- ❌ Fehlende Dateien → Hinweis im Markdown
- ❌ Korrupte CSVs/JSONs/XMLs → Fehler-Hinweis
- ❌ Encoding-Probleme → UTF-8 mit `errors="replace"`
- ❌ Große Dateien → Automatische Kürzung (max. 8000 Zeichen)

## 💡 Tipps

### Nach Suite-Ausführung
```powershell
# 1. Suite laufen lassen
run_suite

# 2. Zusammenfassung generieren
python -X utf8 summary-all-tests.py

# 3. Markdown öffnen
notepad output-summary.md
# oder
code output-summary.md
```

### Mehrere Runs vergleichen
```powershell
# Run 1
python -X utf8 summary-all-tests.py --run-id run1 --out summary-run1.md

# Run 2
python -X utf8 summary-all-tests.py --run-id run2 --out summary-run2.md
```

### Integration in CI/Autorun ✅ BEREITS INTEGRIERT
Das Script ist **bereits automatisch eingebunden** in `ci/autorun_suite.py` (Zeile ~833):
```python
# Wird automatisch nach jedem Suite-Lauf ausgeführt
summary_proc = subprocess.run(
    [sys.executable, "-X", "utf8", str(summary_script), "--run-id", run_id],
    capture_output=True,
    text=True,
    encoding="utf-8",
    errors="replace",
    env=_utf8_env(os.environ),
)
```
**Kein manueller Eingriff nötig** - einfach `run_suite` ausführen!

## 📦 Erweiterungen

Um weitere Artefakte hinzuzufügen:

1. **Pfad definieren** (in `main()`):
```python
my_artifact = root / "my_folder" / "my_file.csv"
```

2. **Summarize-Funktion** erstellen:
```python
def summarize_my_artifact(p: Path) -> str:
    info = try_csv_head_counts(p, max_rows=5)
    if not info:
        return "_my_file.csv nicht gefunden._\n"
    return f"Zeilen: {info['rows_total']}\n"
```

3. **In Ausgabe einfügen** (in `main()`):
```python
lines.append("## Mein Artefakt")
lines.append(summarize_my_artifact(my_artifact))
```

## ⚙️ Technische Details

- **Python**: 3.10+
- **Encoding**: UTF-8 erzwungen (Windows-safe)
- **Dependencies**: Nur Standard-Library (json, csv, xml, pathlib)
- **Performance**: Schnell (streamt große CSVs)
- **Sicherheit**: Keine Code-Ausführung, nur Lesen

## 🆘 Troubleshooting

### "Run-ID nicht gefunden"
→ Überprüfen Sie `reports/` Ordner oder geben Sie `--run-id` explizit an

### Encoding-Fehler
→ Verwenden Sie `-X utf8` Flag: `python -X utf8 summary-all-tests.py`

### Leere Ausgabe
→ Prüfen Sie, ob die Artefakt-Pfade korrekt sind (logs in der Konsole)

---

**Erstellt**: 2025-10-17  
**Lizenz**: MIT  
**Wartung**: Auto-generiert, leicht erweiterbar
