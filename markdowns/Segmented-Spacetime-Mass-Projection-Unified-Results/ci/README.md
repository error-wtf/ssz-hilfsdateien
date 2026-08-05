# CI Suite - Continuous Integration für SSZ Projection

## Übersicht

Die CI-Suite führt automatisierte Tests und Analysen für das Segmented Spacetime Zipper (SSZ) Projekt durch.

## Schnellstart

### ⚠️ WICHTIG: PowerShell Crash-Problem

**Führen Sie Python-Skripte NICHT direkt in PowerShell aus!**

Die PowerShell Extension in VS Code/Windsurf kann abstürzen, wenn Python-Code im Output erscheint.

### ✅ Empfohlene Ausführung

**Option 1: Batch-Datei (Windows)**
```cmd
.\ci\run_suite_safe.bat
```

**Option 2: PowerShell Wrapper**
```powershell
.\ci\run_safe.ps1 -ScriptPath "ci\autorun_suite.py"
```

**Option 3: Separates CMD Terminal**
```cmd
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python ci\autorun_suite.py --config ci\suite_config.yaml
```

**Option 4: WSL/Linux**
```bash
python ci/autorun_suite.py --config ci/suite_config.yaml
```

## Konfiguration

Die Suite wird über `suite_config.yaml` konfiguriert:

```yaml
run_id: 2025-10-17_gaia_ssz_real
time_window_days: 7
prefer_parquet: true
outputs_root: experiments/2025-10-17_gaia_ssz_real/suite
logs_root: data/logs
mode: full

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
  - name: ring_temperature_analysis
    enabled: true
  - name: summary
    enabled: true
  - name: final_reports
    enabled: true
```

## Suite-Schritte

### 1. autofetch
- Lädt aktuelle GAIA-Daten herunter
- Parquet-Format bevorzugt
- Logs: `data/logs/autofetch_*.log`

### 2. ssz_pipeline
- Führt SSZ-Berechnungen durch
- Validiert Massenrekonstruktion
- Output: Segment-Dichte-Felder

### 3. ssz_terminal_all
- Umfassende Terminalgeschwindigkeits-Analyse
- Berechnet v_fall, v_esc, Rotverschiebung
- Prüft Dualitätsinvariante: v_esc × v_fall = c²

### 4. nightly_bundle_replay
- Verarbeitet gespeicherte Nightly-Bundles
- Replay-Modus für reproduzierbare Tests

### 5. tests
- Unit-Tests für alle Module
- Kovarianztests (Lino Casu Framework)
- PPN-Parameter-Validierung
- Energie-Bedingungen (WEC, DEC, SEC)

### 6. visualize
- 3D-Visualisierungen
- Segment-Dichte-Plots
- Vergleichsgrafiken (GR vs SSZ)

### 7. ring_temperature_analysis
- Analyse von Temperaturringen in Nebeln
- Konversion Temperatur → Geschwindigkeit
- Integration mit Cygnus X Diamond Ring Daten

### 8. summary
- Erstellt Zusammenfassungen aller Ergebnisse
- JSON- und Markdown-Output
- Statistische Auswertung

### 9. final_reports
- Generiert finale PDF/HTML-Berichte
- Konsolidiert alle Analysen
- Export für Papers und Präsentationen

## Command-Line Optionen

```bash
python ci/autorun_suite.py [OPTIONS]

Optionen:
  --config PATH          Pfad zur Konfigurationsdatei (Standard: ci/suite_config.yaml)
  --run-id ID           Override für run_id
  --mode {full,fast}    Ausführungsmodus (full: alle Tests, fast: nur wichtigste)
  --steps STEP1,STEP2   Nur bestimmte Schritte ausführen
  --skip STEP1,STEP2    Bestimmte Schritte überspringen
  --verbose             Detaillierte Ausgabe
  --dry-run             Nur Ablaufplan anzeigen, nicht ausführen
```

### Beispiele

**Nur Autofetch und Tests:**
```bash
python ci/autorun_suite.py --steps autofetch,tests
```

**Alles außer Visualisierung:**
```bash
python ci/autorun_suite.py --skip visualize
```

**Fast-Mode für Quick-Checks:**
```bash
python ci/autorun_suite.py --mode fast
```

## Output-Struktur

```
experiments/2025-10-17_gaia_ssz_real/
├── suite/
│   ├── autofetch/
│   │   ├── gaia_data.parquet
│   │   └── manifest.json
│   ├── ssz_pipeline/
│   │   ├── segments.csv
│   │   └── validation_results.json
│   ├── tests/
│   │   ├── junit.xml
│   │   └── coverage_report.html
│   └── final_reports/
│       ├── consolidated_report.pdf
│       └── summary.md
└── logs/
    ├── suite_run.log
    └── step_errors.log
```

## Troubleshooting

### PowerShell Extension Crash
→ Siehe `POWERSHELL_CRASH_FIX.md` für detaillierte Lösung

### UTF-8 Encoding Fehler
```bash
# Windows
set PYTHONUTF8=1
python ci/autorun_suite.py

# Linux/Mac
export PYTHONUTF8=1
python ci/autorun_suite.py
```

### Missing Dependencies
```bash
pip install -r requirements.txt
```

### GAIA Download Fehler
- Prüfen Sie Internetverbindung
- VizieR könnte temporär nicht verfügbar sein
- Retry nach 5-10 Minuten

### Disk Space
Die Suite kann mehrere GB an Daten generieren. Stellen Sie sicher, dass genug Speicherplatz verfügbar ist.

## CI/CD Integration

### GitHub Actions

```yaml
name: SSZ CI Suite
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run CI Suite
        run: python ci/autorun_suite.py --mode fast
```

### GitLab CI

```yaml
SSZ-suite:
  image: python:3.11
  script:
    - pip install -r requirements.txt
    - python ci/autorun_suite.py --mode fast
  artifacts:
    paths:
      - experiments/
      - data/logs/
```

## Entwicklung

### Neuen Step hinzufügen

1. Funktion in `autorun_suite.py` erstellen:
```python
def run_my_step(ctx: RunContext) -> StepResult:
    # Implementation
    pass
```

2. In `STEP_HANDLERS` registrieren:
```python
STEP_HANDLERS = {
    "my_step": run_my_step,
    # ...
}
```

3. In `suite_config.yaml` aktivieren:
```yaml
steps:
  - name: my_step
    enabled: true
```

### Tests erweitern

Fügen Sie Tests in `tests/` hinzu und sie werden automatisch von der Suite erkannt.

## Support

Bei Fragen oder Problemen:
1. Lesen Sie `POWERSHELL_CRASH_FIX.md`
2. Prüfen Sie Logs in `data/logs/`
3. Erstellen Sie ein Issue im Repository

## Lizenz

Anti-Capitalist Software License (v 1.4)
