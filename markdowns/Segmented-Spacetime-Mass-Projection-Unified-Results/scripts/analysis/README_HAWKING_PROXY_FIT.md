# Hawking Proxy Fit - Quick Start Guide

**Standalone BIC-based spectrum analysis tool**

Simplified alternative to `test_hawking_spectrum_continuum.py` for quick spectrum fits.

---

## 🚀 Quick Start

### **Step 1: Get spectrum data**
```bash
# Download M87 spectrum from NED
python scripts/data_acquisition/fetch_m87_spectrum.py \
    --out m87_spectrum.csv
```

### **Step 2: Run fit**
```bash
python scripts/analysis/hawking_proxy_fit.py \
    --spectrum m87_spectrum.csv \
    --SSZ data/config/ssz_config_m87_TEMPLATE.json \
    --out reports/hawking_fit_report.md \
    --plot reports/hawking_fit_plot.png
```

### **Step 3: View results**
- Report: `reports/hawking_fit_report.md`
- Plot: `reports/hawking_fit_plot.png`

---

## 📋 Full Usage

```bash
python scripts/analysis/hawking_proxy_fit.py \
    --spectrum <SPECTRUM_CSV> \
    --SSZ <SSZ_CONFIG_JSON> \
    --C <TEMP_FACTOR> \
    --out <REPORT_MD> \
    --plot <PLOT_PNG>
```

### **Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| `--spectrum` | `m87_spectrum.csv` | Input spectrum (freq_Hz, flux_Jy, sigma_Jy) |
| `--SSZ` | `ssz_config.json` | SSZ config with κ_seg |
| `--C` | `1e30` | Temperature seed factor: T = C × \|κ_seg\| |
| `--out` | `hawking_fit_report.md` | Output report (Markdown) |
| `--plot` | `hawking_fit_plot.png` | Output plot (PNG) |

---

## 🎯 What it does

### **1. Loads data:**
- Spectrum CSV (from NED or ALMA)
- SSZ config JSON (κ_seg from Segmented Spacetime)

### **2. Fits two models:**

**Model 1: Thermal (Planck-like)**
```
I_ν = A · (2hν³/c²) / (exp(hν/kT) - 1)
```
Initial guess: T_seed = C × |κ_seg|

**Model 2: Non-thermal (Power-law)**
```
F_ν = A · (ν/ν₀)^α
```
Typical for synchrotron, inverse Compton, etc.

### **3. Compares via BIC:**
```
ΔBIC = BIC_powerlaw - BIC_thermal

If ΔBIC > 10:  Strong evidence for thermal
If ΔBIC > 2:   Positive evidence for thermal
If ΔBIC < -10: Strong evidence for power-law
If ΔBIC < -2:  Positive evidence for power-law
Else:          No strong preference
```

### **4. Generates:**
- Markdown report with fit parameters & interpretation
- Log-log plot showing data + both fits

---

## 📊 Example Output

### **Report (hawking_fit_report.md):**
```markdown
# Hawking Proxy Fit Report

## SSZ Configuration
- κ_seg (abs): 1.872e+03 m⁻¹
- T_seed = C × |κ_seg|, C = 1.000e+30 → 1.872e+33 K

## Data
- Spectrum file: `m87_spectrum.csv`
- Data points: 150
- Frequency range: 2.300e+11 - 5.000e+18 Hz

## Best-fit Parameters
**Thermal (Planck-like):**
- T = 1.234e+32 K
- A = 5.678e-02
- BIC = 145.3

**Power-law:**
- A = 0.950
- α = -0.73
- BIC = 165.8

## Model Comparison
- ΔBIC = BIC_powerlaw - BIC_thermal = 20.5

### Interpretation: ✅ **Strong evidence for thermal model**
ΔBIC > 10 indicates the thermal (Planck-like) spectrum is strongly preferred.
```

### **Plot:**
- Log-log axes
- Data points with error bars (black)
- Thermal fit (red solid line)
- Power-law fit (blue dashed line)
- BIC values in legend
- ΔBIC in title

---

## 🔧 SSZ Config Format

**Example:** `ssz_config_m87.json`
```json
{
  "source": "M87*",
  "M_solar": 6.5e9,
  "r_emit_m": 1.2e13,
  "kappa_seg_per_m": 1.872e3,
  "T_seg_K": 7.593e-18
}
```

**Required field:**
- `kappa_seg_per_m`: Surface gravity proxy (m⁻¹)

**Optional fields:**
- `source`, `M_solar`, `r_emit_m`, `T_seg_K`: Metadata

**How to get κ_seg:**
From SSZ analysis (e.g., `test_horizon_hawking_predictions.py`) or simplified:
```python
κ_seg ≈ c² / (4 × r_φ)
```

---

## 🆚 Comparison with test_hawking_spectrum_continuum.py

| Feature | `hawking_proxy_fit.py` | `test_hawking_spectrum_continuum.py` |
|---------|------------------------|--------------------------------------|
| **Purpose** | Quick standalone analysis | Full test framework |
| **Input** | Spectrum + SSZ config | Spectrum (auto-detects) |
| **Models** | Planck + Power-law | Planck + Power-law + Broken PL |
| **Output** | Report + Plot | Test results + Report |
| **Integration** | Standalone tool | Part of test suite |
| **Speed** | ⚡ Fast | 🐢 Slower (more checks) |
| **Best for** | Quick fits, exploration | Validation, multiple sources |

---

## 📈 Use Cases

### **1. Quick analysis after NED download:**
```bash
python scripts/data_acquisition/fetch_m87_spectrum.py
python scripts/analysis/hawking_proxy_fit.py
# → Instant fit + plot!
```

### **2. Compare different κ_seg values:**
```bash
# Low κ_seg
python hawking_proxy_fit.py --C 1e28 --out report_low.md

# High κ_seg
python hawking_proxy_fit.py --C 1e32 --out report_high.md
```

### **3. Multiple sources:**
```bash
for src in M87 "Sgr A*" "Cyg X-1"; do
    python fetch_m87_spectrum.py --name "$src" --out "${src}.csv"
    python hawking_proxy_fit.py --spectrum "${src}.csv" --out "${src}_fit.md"
done
```

### **4. Publication-quality plots:**
```bash
python hawking_proxy_fit.py --plot high_res_fit.png
# Edit script: increase dpi, adjust colors, add annotations
```

---

## ⚠️ Known Limitations

### **1. Simplified fits:**
- Uses scipy.curve_fit (may fail for complex spectra)
- No broken power-law (available in full test)
- No multi-component models

### **2. Temperature seed:**
- T_seed = C × |κ_seg| is heuristic
- May need manual adjustment of C factor
- Real T_seg ~ 1e-34 K often too small for direct use

### **3. Data quality:**
- No automatic outlier rejection
- Assumes Gaussian errors
- No RFI/flare flagging

### **Workarounds:**
- For complex fits → use `test_hawking_spectrum_continuum.py`
- For multi-component → add models to script
- For data cleaning → preprocess CSV manually

---

## 🎯 Troubleshooting

### **Error: "Spectrum file not found"**
```bash
# Generate spectrum first:
python scripts/data_acquisition/fetch_m87_spectrum.py
```

### **Error: "SSZ config not found"**
```bash
# Use template:
cp data/config/ssz_config_m87_TEMPLATE.json ssz_config.json
# Or: Script will use default κ_seg = 1e-13
```

### **Fit fails (RuntimeError)**
```bash
# Adjust C factor:
python hawking_proxy_fit.py --C 1e28  # Lower temperature seed
python hawking_proxy_fit.py --C 1e32  # Higher temperature seed
```

### **ΔBIC ~ 0 (no preference)**
```bash
# Normal! Means:
# - Not enough frequency coverage
# - Data quality issues
# - Source genuinely hybrid thermal+non-thermal
# → Try getting better data (ALMA, Chandra)
```

---

## 📚 Scientific Background

### **Why BIC?**
Bayesian Information Criterion penalizes model complexity:
```
BIC = χ² + k·ln(n)
```
- Simpler model (fewer parameters k) preferred if fits equally well
- Both our models have k=2 → fair comparison!

### **Why Planck for Hawking?**
Hawking radiation is thermal with temperature:
```
T_H = ℏκ / (2πk_Bc)
```
where κ is surface gravity. In SSZ:
```
κ_seg ≈ c² / (4r_φ)
T_seg ≈ ℏκ_seg / (2πk_Bc)
```
If emission is thermal with T ≈ T_seg → evidence for Hawking-like process!

### **Why Power-law as alternative?**
Most AGN/XRB spectra are non-thermal (synchrotron, Comptonization).
If ΔBIC > 0 → thermal fits better than standard non-thermal processes!

---

## 📝 Citation

If you use this tool in a publication, please cite:
```
Casu, L. & Wrede, C. (2025). Segmented Spacetime Mass Projection.
https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
```

---

**© 2025 Carmen Wrede, Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Version:** 1.0.0  
**Last Updated:** 2025-10-19  
**Status:** ✅ READY TO USE
