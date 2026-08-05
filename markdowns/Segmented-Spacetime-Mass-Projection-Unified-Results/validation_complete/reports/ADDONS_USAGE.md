# SSZ Pipeline Add-ons - Aktivierung

Die Pipeline unterstützt **optionale Add-ons** die automatisch am Ende ausgeführt werden können.

---

## 🎯 Verfügbare Add-ons

### 1. **Segment-Redshift** (`SSZ_SEGMENT_REDSHIFT`)

Berechnet gravitationelle Rotverschiebung basierend auf Segment-Dichte-Integration.

**Output:**
- `reports/segment_redshift.csv`
- `reports/segment_redshift.md`
- `reports/figures/fig_shared_segment_redshift_profile.png`

### 2. **Extended Metrics** (`SSZ_EXTENDED_METRICS`)

Erweiterte Ring-Metriken und Plots für G79 und Cygnus X.

**Output:**
- `reports/data/{object}_ring_metrics.csv`
- `reports/stats/{object}_fit_summary.csv`
- `reports/figures/{object}/fig_*.png/svg`

---

## 🚀 Aktivierung in der Pipeline

### **Windows (PowerShell):**

```powershell
# Segment-Redshift aktivieren:
$env:SSZ_SEGMENT_REDSHIFT="1"
python run_all_ssz_terminal.py

# Extended Metrics aktivieren:
$env:SSZ_EXTENDED_METRICS="1"
python run_all_ssz_terminal.py

# BEIDE aktivieren:
$env:SSZ_SEGMENT_REDSHIFT="1"
$env:SSZ_EXTENDED_METRICS="1"
python run_all_ssz_terminal.py
```

### **Linux/WSL (Bash):**

```bash
# Segment-Redshift aktivieren:
export SSZ_SEGMENT_REDSHIFT=1
python3 run_all_ssz_terminal.py

# Extended Metrics aktivieren:
export SSZ_EXTENDED_METRICS=1
python3 run_all_ssz_terminal.py

# BEIDE aktivieren:
export SSZ_SEGMENT_REDSHIFT=1
export SSZ_EXTENDED_METRICS=1
python3 run_all_ssz_terminal.py
```

---

## 📊 Pipeline-Flow mit Add-ons

```
run_all_ssz_terminal.py
├── [Phase 1-7] Normal Pipeline
│   ├── Tests
│   ├── SSZ Analysis
│   ├── G79/Cygnus X Examples
│   └── Summary
│
├── [ADDON] Extended Metrics (wenn SSZ_EXTENDED_METRICS=1)
│   ├── Ring-Daten laden (G79, Cygnus X)
│   ├── Metriken berechnen
│   ├── CSV exportieren
│   └── Plots erstellen
│
├── [ADDON] Segment-Redshift (wenn SSZ_SEGMENT_REDSHIFT=1)
│   ├── Pipeline-Daten laden (ring_chain.csv)
│   ├── Φ_seg integrieren
│   ├── ν_∞ berechnen
│   └── Report + Plot erstellen
│
└── [FINAL] Plot-Übersicht
    └── Liste ALLE generierten Plots
```

---

## ⚙️ Standard-Parameter

### **Segment-Redshift:**

| Parameter | Wert | Anpassen via |
|-----------|------|--------------|
| `--proxy` | `N` | Direkt in `run_all_ssz_terminal.py` Zeile 1154 |
| `--nu-em` | `1.0e18` Hz | Zeile 1155 |
| `--r-em` | `2.0` r_s | Zeile 1156 |
| `--r-out` | `50.0` r_s | Zeile 1157 |
| `--seg-plot` | aktiviert | Zeile 1158 |

**Oder:** Add-on manuell ausführen mit eigenen Parametern:
```bash
python scripts/addons/segment_redshift_addon.py \
  --segment-redshift \
  --proxy rho-pr \
  --nu-em 5.0e14 \
  --r-em 3.0 \
  --r-out 100.0 \
  --seg-plot
```

### **Extended Metrics:**

Verwendet automatisch G79 und Cygnus X Ring-Daten aus `data/observations/`.

---

## 🛡️ Sicherheit

**Add-ons sind:**
- ✅ **Optional:** Nur mit Environment-Variable aktiv
- ✅ **Non-invasive:** Keine Änderung an Pipeline-Outputs
- ✅ **Fail-safe:** Bei Fehler wird gewarnt, aber Pipeline läuft weiter
- ✅ **Eigener Namespace:** Keine Konflikte mit bestehenden Files

**Falls Add-on fehlschlägt:**
```
[SSZ ADDON] WARNING: Segment-Redshift failed: <error>
```
→ Pipeline läuft normal weiter!

---

## 📖 Beispiele

### **Nur Pipeline (Default):**
```bash
python run_all_ssz_terminal.py
# Add-ons NICHT ausgeführt
```

### **Pipeline + Segment-Redshift:**
```bash
# Windows:
$env:SSZ_SEGMENT_REDSHIFT="1"
python run_all_ssz_terminal.py

# Linux:
SSZ_SEGMENT_REDSHIFT=1 python3 run_all_ssz_terminal.py
```

### **Pipeline + Alle Add-ons:**
```bash
# Windows:
$env:SSZ_SEGMENT_REDSHIFT="1"
$env:SSZ_EXTENDED_METRICS="1"
python run_all_ssz_terminal.py

# Linux:
SSZ_SEGMENT_REDSHIFT=1 SSZ_EXTENDED_METRICS=1 python3 run_all_ssz_terminal.py
```

---

## 🔍 Output-Locations

```
reports/
├── segment_redshift.csv         # Segment-Redshift
├── segment_redshift.md          # Segment-Redshift
├── data/
│   ├── G79_ring_metrics.csv     # Extended Metrics
│   └── CygnusX_ring_metrics.csv # Extended Metrics
├── stats/
│   ├── G79_fit_summary.csv      # Extended Metrics
│   └── CygnusX_fit_summary.csv  # Extended Metrics
└── figures/
    ├── fig_shared_segment_redshift_profile.png  # Segment-Redshift
    ├── G79/                     # Extended Metrics
    │   ├── fig_G79_ringchain_v_vs_k.png
    │   ├── fig_G79_gamma_log_vs_k.png
    │   └── ...
    └── CygnusX/                 # Extended Metrics
        └── ...
```

---

## 🧪 Tests

```bash
# Test Segment-Redshift (isoliert):
python scripts/addons/segment_redshift_addon.py --segment-redshift

# Test Extended Metrics (isoliert):
$env:SSZ_EXTENDED_METRICS="1"
python -c "from run_all_ssz_terminal import _finalize_extended_outputs; _finalize_extended_outputs()"

# Test in Pipeline:
$env:SSZ_SEGMENT_REDSHIFT="1"
$env:SSZ_EXTENDED_METRICS="1"
python run_all_ssz_terminal.py
```

---

## ❓ FAQ

**Q: Werden Add-ons standardmäßig ausgeführt?**
A: Nein! Nur mit Environment-Variable `SSZ_*=1`.

**Q: Kann ich Add-ons separat ausführen?**
A: Ja! Siehe `scripts/addons/README.md`.

**Q: Was wenn ein Add-on fehlt?**
A: Warning wird angezeigt, Pipeline läuft normal weiter.

**Q: Kann ich eigene Add-ons erstellen?**
A: Ja! Einfach nach dem Pattern in `scripts/addons/` erstellen.

---

## 📝 Lizenz

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
