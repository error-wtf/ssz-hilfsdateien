# Summary Pipeline - Automatische Report-Generierung

## 📊 Übersicht

Die Suite generiert automatisch zwei Arten von Reports:

1. **Markdown-Report** (`output-summary.md`) - Strukturierte Textzusammenfassung
2. **HTML-Report** (`output-summary.html`) - Visueller Report mit eingebetteten Plots

## 📁 Speicherorte

### Scripts
```
ci/summary-all-tests.py     → Generiert Markdown
ci/summary_visualize.py     → Generiert HTML + Plots
```

### Generierte Reports
```
reports/<run_id>/
├── output-summary.md       → Markdown-Report
├── output-summary.html     → HTML-Report mit Plots
└── _summary_assets/        → PNG-Dateien (falls --plots)
    ├── dz_seg_hist.png
    ├── dz_gr_hist.png
    ├── dz_sr_hist.png
    ├── dz_grsr_hist.png
    └── dz_seg_vs_gr.png
```

## 🚀 Automatische Ausführung

Die Pipeline läuft **automatisch am Ende jeder Suite**:

```
run_suite
↓
[... alle Steps ...]
↓
[Step: summary_all]        → Markdown generieren
↓
[Step: summary_visualize]  → HTML + Plots generieren
↓
[Fertig]
```

### Ausgabe (Konsole)
```
Suite complete in 1234.5s -> OK: 7, Fail: 0
Markdown Report: reports/2025-10-17_run/output-summary.md
HTML Report    : reports/2025-10-17_run/output-summary.html
Plot Assets    : reports/2025-10-17_run/_summary_assets
```

## 🔧 Manuelle Ausführung

### Nur Markdown
```powershell
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python -X utf8 ci/summary-all-tests.py --run-dir . --run-id <run_id> --out reports/<run_id>/output-summary.md
```

### Markdown → HTML (ohne Plots)
```powershell
python ci/summary_visualize.py --run-dir . --md reports/<run_id>/output-summary.md --html reports/<run_id>/output-summary.html
```

### Markdown → HTML (mit Plots)
```powershell
python ci/summary_visualize.py --run-dir . --md reports/<run_id>/output-summary.md --html reports/<run_id>/output-summary.html --plots
```

## 📊 Was wird aggregiert?

### summary-all-tests.py (Markdown)
- Suite-Status & Schritte (`ci/suite_manifest.json`)
- PyTest-Ergebnisse:
  - Repository gesamt (`testergebnisse/<run_id>/repo_pytest_full.xml`)
  - Scripts/Tests (`reports/<run_id>/pytest_results.xml`)
- SSZ/GAIA Reports:
  - Bound Energy (`agent_out/reports/bound_energy.txt`)
  - Redshift-Auswertung (`redshift_medians.json`, `redshift_paired_stats.json`)
  - Mass Validation (`mass_validation.csv`)
- Debug-Dateien:
  - Enhanced Debug (`out/_enhanced_debug.csv`)
  - Explain Debug (`out/_explain_debug.csv`)

### summary_visualize.py (HTML + Plots)
Nimmt Markdown als Input und fügt hinzu:
- **PyTest-KPIs** (visuell aufbereitet)
- **CSV-Vorschauen** mit Statistiken
- **Plots** (falls `--plots` und Matplotlib verfügbar):
  - Histogramme für |Δz| (Seg, GR, SR, GR×SR)
  - Scatter-Plot: Seg vs GR
  - Base64-eingebettet (keine externen Dateien nötig)

## 🛡️ Robustheit

### UTF-8 Encoding
- Beide Scripts erzwingen UTF-8 (Windows-sicher)
- Alle subprocess-Aufrufe mit `-X utf8` Flag
- Environment: `PYTHONUTF8=1`, `PYTHONIOENCODING=utf-8`

### Fehlerbehandlung
- Fehlende Dateien → Hinweis statt Crash
- Korrupte Daten → Fehler-Meldung im Report
- Matplotlib fehlt → Plots werden übersprungen
- Script-Fehler → Warnung im Log, Suite läuft weiter

### Abhängigkeiten
- **Pflicht**: Python Standard Library (json, csv, pathlib, etc.)
- **Optional**: 
  - `markdown` (für schöneres HTML, Fallback vorhanden)
  - `matplotlib` (für Plots, sonst nur Kennzahlen)

## 🎯 Integration in ci/autorun_suite.py

```python
# Output paths (Zeile ~833)
md_out = reports_dir / "output-summary.md"
html_out = reports_dir / "output-summary.html"
assets_dir = reports_dir / "_summary_assets"

# Step 1: Markdown (Zeile ~838)
summary_script = ROOT / "ci" / "summary-all-tests.py"
subprocess.run([
    sys.executable, "-X", "utf8", str(summary_script),
    "--run-dir", str(ROOT),
    "--run-id", run_id,
    "--out", str(md_out)
], ...)

# Step 2: HTML + Plots (Zeile ~870)
viz_script = ROOT / "ci" / "summary_visualize.py"
# Check matplotlib availability
try:
    import matplotlib
    plots_flag = ["--plots"]
except:
    plots_flag = []

subprocess.run([
    sys.executable, "-X", "utf8", str(viz_script),
    "--run-dir", str(ROOT),
    "--md", str(md_out),
    "--html", str(html_out),
    *plots_flag
], ...)
```

## 📝 Erweitern

### Neues Artefakt zu Markdown hinzufügen

In `ci/summary-all-tests.py`:

```python
# 1. Pfad definieren
my_artifact = root / "my_folder" / "my_file.csv"

# 2. Summarize-Funktion
def summarize_my_artifact(p: Path) -> str:
    if not p.exists():
        return "_my_file.csv nicht gefunden._\n"
    # Daten laden und formatieren
    return "## Mein Artefakt\n...\n"

# 3. In main() einbinden
lines.append(summarize_my_artifact(my_artifact))
```

### Neuen Plot hinzufügen

In `ci/summary_visualize.py`:

```python
# In summarize_enhanced_debug() oder ähnlich
if args.plots and my_data:
    img = assets_dir / "my_plot.png"
    p = plot_scatter(x, y, "Mein Plot", img)
    if p: sec.append(img_tag(p))
```

## 🆘 Troubleshooting

### "Markdown-Report not generated"
- Prüfen: `ci/summary-all-tests.py` existiert
- Prüfen: Run-ID korrekt
- Log: `data/logs/suite_<run_id>_*.log`

### "HTML-Report not generated"
- Prüfen: `ci/summary_visualize.py` existiert
- Prüfen: Markdown wurde erfolgreich generiert
- Matplotlib fehlt → Nur Kennzahlen, keine Plots

### Encoding-Fehler
- Sollte nicht mehr vorkommen (UTF-8 erzwungen)
- Falls doch: `-X utf8` Flag prüfen

### Plots fehlen
- `matplotlib` installieren: `pip install matplotlib`
- Oder akzeptieren: Report funktioniert auch ohne Plots

## 💡 Best Practices

1. **Reports versionieren**: `reports/<run_id>/` macht Vergleiche einfach
2. **HTML teilen**: Base64-embedded → Eine Datei, keine Dependencies
3. **Plots optional**: Kennzahlen reichen oft, Plots für deep-dive
4. **Logs behalten**: `data/logs/` für Debugging

---

**Erstellt**: 2025-10-17  
**Version**: 1.0  
**Status**: ✅ Produktiv
