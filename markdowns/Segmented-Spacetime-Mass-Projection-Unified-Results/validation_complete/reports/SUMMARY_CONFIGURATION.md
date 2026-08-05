# Summary-Pipeline Konfiguration

## 📋 Übersicht

Die Summary-Pipeline ist jetzt als **regulärer Suite-Step** integriert und wird über `ci/suite_config.yaml` gesteuert.

## ⚙️ Konfiguration

### In `ci/suite_config.yaml`

```yaml
steps:
  - name: autofetch
    enabled: true
  - name: ssz_pipeline
    enabled: true
  - name: ssz_terminal_all
    enabled: true
  - name: nightly_bundle_replay
    enabled: true
  - name: tests
    enabled: true
  - name: visualize
    enabled: true
  - name: summary        # ← NEU
    enabled: true        # ← Aktiviert/Deaktiviert Summary

# Optional: Ring temperature analysis
rings_csv: null          # Path to CSV or null to disable
# rings_csv: "data/example_rings.csv"  # Uncomment to enable
rings_v0: 10.0           # Baseline velocity [km/s]
```

## 🚀 Verwendung

### 1. Summary aktiviert (Standard)
```yaml
- name: summary
  enabled: true
```

**Ergebnis**:
- ✅ `output-summary.md` wird generiert
- ✅ `output-summary.html` wird generiert
- ✅ Plots werden erstellt (falls matplotlib)

### 2. Summary deaktiviert
```yaml
- name: summary
  enabled: false
```

**Ergebnis**:
- ❌ Keine Summary-Reports

### 3. Mit Ring-Analyse
```yaml
- name: summary
  enabled: true

rings_csv: "data/example_rings.csv"
rings_v0: 10.0
```

**Ergebnis**:
- ✅ Summary mit Ring-Sektion ganz oben
- ✅ Ring-Artefakte in `reports/<run_id>/ring_temp2v/`

## 📊 Output-Artefakte

Nach jedem Suite-Lauf (falls summary enabled):

```
reports/<run_id>/
├── output-summary.md       ← Markdown-Report
├── output-summary.html     ← HTML-Report
├── _summary_assets/        ← Plots (falls matplotlib)
│   ├── dz_seg_hist.png
│   ├── dz_gr_hist.png
│   └── ...
└── ring_temp2v/            ← Ring-Analyse (falls rings_csv)
    ├── ring_results.csv
    └── ring_summary.json
```

## 🎯 Vorteile der neuen Integration

### Vorher (Inline nach allen Steps)
- ❌ Hart-kodiert, immer aktiv
- ❌ Keine Kontrolle über Ausführung
- ❌ Nicht in Step-Liste sichtbar

### Nachher (Als regulärer Step)
- ✅ In `suite_config.yaml` steuerbar
- ✅ In Suite-Manifest sichtbar
- ✅ Kann enabled/disabled werden
- ✅ Konsistent mit anderen Steps
- ✅ Flexible Ring-Konfiguration

## 📝 Finale Ausgabe

```
Suite complete in 128.286s -> OK: 7, Fail: 0
Markdown Report: reports/<run_id>/output-summary.md
HTML Report    : reports/<run_id>/output-summary.html
Plot Assets    : reports/<run_id>/_summary_assets
```

## 🔧 Step-Funktion

```python
def step_summary(run_id: str, cfg: Dict[str, Any], logger: logging.Logger):
    """
    Generate markdown and HTML summary reports.
    
    Args:
        run_id: Suite run identifier
        cfg: Suite configuration (includes rings_csv, rings_v0)
        logger: Logging instance
        
    Returns:
        Dict with artifacts:
        - markdown: Path to output-summary.md
        - html: Path to output-summary.html
        - assets: Path to _summary_assets/
    """
```

## 🆘 Troubleshooting

### "Unknown step 'summary' in configuration"
→ `ci/autorun_suite.py` ist nicht aktuell, neu laden

### Summary läuft nicht
→ Prüfen Sie `suite_config.yaml`: `enabled: true`

### Ring-Analyse fehlt
→ Setzen Sie `rings_csv: "data/example_rings.csv"` in `suite_config.yaml`

### pandas/numpy Fehler
→ `pip install pandas numpy` oder setzen Sie `rings_csv: null`

---

**Erstellt**: 2025-10-17  
**Version**: 2.0 - Flexible Step-Integration  
**Status**: ✅ PRODUKTIONSBEREIT
