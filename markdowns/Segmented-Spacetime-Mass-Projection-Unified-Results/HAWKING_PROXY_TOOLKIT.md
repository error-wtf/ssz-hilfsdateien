# Hawking Proxy Toolkit (for SSZ) - Complete Guide

**End-to-end pipeline: Data → Analysis → Results**

Complete toolkit for testing thermal (Hawking-like) vs non-thermal spectra using SSZ-derived parameters.

---

## 🚀 Quick Start (3 Steps)

### **Installation:**
```bash
pip install astroquery astropy numpy pandas scipy matplotlib
```

### **Step 1: Fetch Spectrum (M87; 30–1000 GHz)**
```bash
python scripts/data_acquisition/fetch_m87_spectrum.py \
    --name "M87" \
    --minGHz 30 \
    --maxGHz 1000 \
    --out m87_spectrum.csv
```

### **Step 2: Parse SSZ Horizon Report to JSON**
```bash
python scripts/data_acquisition/parse_ssz_horizon.py \
    --report reports/hawking_proxy_fit.md \
    --out ssz_config.json
```

### **Step 3: Fit & Compare**
```bash
python scripts/analysis/hawking_proxy_fit.py \
    --spectrum m87_spectrum.csv \
    --SSZ ssz_config.json \
    --C 1e30 \
    --out hawking_fit_report.md
```

**Output:**
- `hawking_fit_report.md` - Markdown report with ΔBIC
- `hawking_fit_plot.png` - Log-log spectrum + fits

---

## 📦 Toolkit Components

### **1. Data Acquisition:**

**fetch_m87_spectrum.py**
- Downloads real continuum spectra from NED (NASA/IPAC)
- Supports: M87, Sgr A*, Cyg X-1, NGC 1275, etc.
- Output: CSV with freq_Hz, flux_Jy, sigma_Jy

**parse_ssz_horizon.py**
- Extracts r_φ, A_H, κ_seg from SSZ reports
- Input: Markdown report from test_horizon_hawking_predictions.py
- Output: JSON config for fits

### **2. Analysis:**

**hawking_proxy_fit.py**
- Fits thermal (Planck) vs non-thermal (power-law) models
- Uses SSZ κ_seg for temperature seed: T_seed = C × |κ_seg|
- BIC-based model selection
- Auto-generates plots + reports

### **3. Testing:**

**test_hawking_spectrum_continuum.py**
- Full test framework (part of test suite)
- Multi-source support
- Additional models (broken power-law)
- Integration with validation pipeline

---

## 🛠️ Detailed Usage

### **Script 1: fetch_m87_spectrum.py**

**Purpose:** Download continuum spectrum from NED

**Parameters:**
```bash
--name      Source name (default: M87)
--minGHz    Min frequency in GHz (default: 30)
--maxGHz    Max frequency in GHz (default: 1000)
--out       Output CSV file (default: m87_spectrum.csv)
--M_solar   Black hole mass in M☉ (default: 6.5e9)
--r_emit_m  Emission radius in m (default: 1.2e13)
```

**Examples:**
```bash
# M87 (supermassive BH)
python fetch_m87_spectrum.py --name "M87"

# Sgr A* (Galactic Center)
python fetch_m87_spectrum.py --name "Sgr A*" --M_solar 4.15e6

# Wide frequency range
python fetch_m87_spectrum.py --minGHz 0.1 --maxGHz 100000
```

**Output CSV format:**
```csv
source,frequency_Hz,flux_density_Jy,flux_error_Jy,M_solar,r_emit_m,instrument
M87,2.30e+11,0.95,0.05,6.5e9,1.2e13,VLA
M87,3.45e+11,1.02,0.06,6.5e9,1.2e13,ALMA
...
```

---

### **Script 2: parse_ssz_horizon.py**

**Purpose:** Extract SSZ parameters from horizon report

**Parameters:**
```bash
--report    Input SSZ report (Markdown)
--out       Output JSON config (default: ssz_config.json)
```

**What it extracts:**
- `r_phi_m`: Photon sphere radius (m)
- `A_H_m2`: Horizon area (m²)
- `kappa_seg_per_m`: Surface gravity proxy (m⁻¹)

**Example:**
```bash
python parse_ssz_horizon.py \
    --report reports/hawking_proxy_fit.md \
    --out ssz_config.json
```

**Output JSON format:**
```json
{
  "r_phi_m": 2.88e13,
  "A_H_m2": 1.04e27,
  "kappa_seg_per_m": 1872.0,
  "source": "M87*",
  "M_solar": 6.5e9,
  "extracted_from": "reports/hawking_proxy_fit.md",
  "extraction_time": "2025-10-19T06:51:00"
}
```

---

### **Script 3: hawking_proxy_fit.py**

**Purpose:** Fit thermal vs non-thermal models

**Parameters:**
```bash
--spectrum  Input spectrum CSV (required)
--SSZ       SSZ config JSON (required)
--C         Temperature factor: T = C × |κ_seg| (default: 1e30)
--out       Output report MD (default: hawking_fit_report.md)
--plot      Output plot PNG (default: hawking_fit_plot.png)
```

**What it does:**

1. **Loads data:**
   - Spectrum (freq, flux, error)
   - SSZ config (κ_seg)

2. **Fits two models:**
   - **M1 (Thermal):** Planck spectrum with T_seed = C × |κ_seg|
   - **M2 (Non-thermal):** Power-law F_ν = A·ν^α

3. **Compares via BIC:**
   - ΔBIC = BIC_powerlaw - BIC_thermal
   - ΔBIC > 10 → Strong evidence for thermal
   - ΔBIC > 2 → Positive evidence for thermal

4. **Generates:**
   - Markdown report with fit parameters
   - PNG plot (log-log, data + fits)

**Example:**
```bash
python hawking_proxy_fit.py \
    --spectrum m87_spectrum.csv \
    --SSZ ssz_config.json \
    --C 1e30
```

---

## 📊 Complete Workflow Example

### **Scenario: M87 Spectrum Analysis**

```bash
# ============================================================================
# STEP 1: Fetch M87 spectrum from NED
# ============================================================================
python scripts/data_acquisition/fetch_m87_spectrum.py \
    --name "M87" \
    --minGHz 1 \
    --maxGHz 10000 \
    --out m87_spectrum.csv

# Expected output:
# ✅ Success!
#    Wrote 150 data points to m87_spectrum.csv
#    Frequency range: 1.0e+09 - 1.0e+13 Hz
#    Flux range: 0.1 - 100 Jy


# ============================================================================
# STEP 2: Generate SSZ horizon report (if not already done)
# ============================================================================
python scripts/tests/test_horizon_hawking_predictions.py

# This generates: reports/hawking_proxy_fit.md
# Contains: r_φ, A_H, κ_seg for all sources


# ============================================================================
# STEP 3: Parse SSZ report to JSON
# ============================================================================
python scripts/data_acquisition/parse_ssz_horizon.py \
    --report reports/hawking_proxy_fit.md \
    --out ssz_config.json

# Expected output:
# ✅ Configuration extracted:
#    r_phi_m: 2.880e+13
#    A_H_m2: 1.040e+27
#    kappa_seg_per_m: 1.872e+03


# ============================================================================
# STEP 4: Fit spectrum
# ============================================================================
python scripts/analysis/hawking_proxy_fit.py \
    --spectrum m87_spectrum.csv \
    --SSZ ssz_config.json \
    --C 1e30 \
    --out hawking_fit_report.md \
    --plot hawking_fit_plot.png

# Expected output:
# Fitting thermal (Planck) model...
#   T_fit = 1.234e+32 K
#   BIC = 145.3
# Fitting power-law model...
#   α_fit = -0.73
#   BIC = 165.8
# 
# ΔBIC = BIC_powerlaw - BIC_thermal = 20.5
# ✅ Strong evidence for thermal model (ΔBIC > 10)
# 
# ✅ Analysis complete!
#    Report: hawking_fit_report.md
#    Plot: hawking_fit_plot.png


# ============================================================================
# STEP 5: View results
# ============================================================================
# Open hawking_fit_report.md in browser/editor
# Open hawking_fit_plot.png to see spectrum + fits
```

---

## 🎯 Alternative Workflows

### **Quick Test with Template Data:**
```bash
# Use template data (no download needed)
python scripts/analysis/hawking_proxy_fit.py \
    --spectrum data/observations/m87_continuum_spectrum_TEMPLATE.csv \
    --SSZ data/config/ssz_config_m87_TEMPLATE.json
```

### **Multiple Sources:**
```bash
# Loop over sources
for src in "M87" "Sgr A*" "Cyg X-1"; do
    echo "Analyzing $src..."
    
    # Fetch spectrum
    python fetch_m87_spectrum.py --name "$src" --out "${src}.csv"
    
    # Fit (use same SSZ config or source-specific)
    python hawking_proxy_fit.py \
        --spectrum "${src}.csv" \
        --out "${src}_fit.md" \
        --plot "${src}_fit.png"
done
```

### **Parameter Exploration:**
```bash
# Try different C factors
for C in 1e28 1e29 1e30 1e31 1e32; do
    python hawking_proxy_fit.py \
        --C $C \
        --out "fit_C${C}.md" \
        --plot "fit_C${C}.png"
done
```

---

## 📈 Interpreting Results

### **ΔBIC Values:**

| ΔBIC | Interpretation |
|------|----------------|
| **> 10** | ✅ **Strong evidence for thermal** - Planck spectrum strongly preferred |
| **2 to 10** | ✅ **Positive evidence for thermal** - Planck spectrum preferred |
| **-2 to 2** | ℹ️  **Inconclusive** - Both models fit equally well |
| **-10 to -2** | ⚠️  **Positive evidence for power-law** - Non-thermal preferred |
| **< -10** | ⚠️  **Strong evidence for power-law** - Non-thermal strongly preferred |

### **Physical Interpretation:**

**If ΔBIC > 10 (thermal preferred):**
- Spectrum is consistent with Planck-like thermal emission
- Temperature T_fit ~ T_seg suggests Hawking-like process
- Evidence for thermal continuum near horizon scale

**If ΔBIC < -10 (power-law preferred):**
- Spectrum dominated by non-thermal processes
- Likely synchrotron, inverse Compton, etc.
- May indicate: (a) not probing horizon scale, or (b) non-thermal dominates

**If |ΔBIC| < 2 (inconclusive):**
- Both models fit equally well
- Possible hybrid thermal + non-thermal
- Need better data (more frequency coverage, lower uncertainties)

---

## 🔧 Troubleshooting

### **Problem: "No data in frequency range"**

**Cause:** NED has limited coverage for your frequency range

**Solution:**
```bash
# Expand range
python fetch_m87_spectrum.py --minGHz 0.1 --maxGHz 100000

# Or use different source (brighter = better coverage)
python fetch_m87_spectrum.py --name "Cyg X-1"
```

---

### **Problem: "Fit failed (RuntimeError)"**

**Cause:** Temperature seed T_seed is too high/low for data

**Solution:**
```bash
# Adjust C factor
python hawking_proxy_fit.py --C 1e28   # Lower T_seed
python hawking_proxy_fit.py --C 1e32   # Higher T_seed
```

---

### **Problem: "Parameters not extracted from report"**

**Cause:** Report format doesn't match regex patterns

**Solution:**
```bash
# Check report manually
cat reports/hawking_proxy_fit.md | grep -i "kappa\|r_phi\|A_H"

# Or create JSON manually
cat > ssz_config.json <<EOF
{
  "r_phi_m": 2.88e13,
  "A_H_m2": 1.04e27,
  "kappa_seg_per_m": 1872.0
}
EOF
```

---

### **Problem: "ΔBIC ~ 0 (no preference)"**

**Cause:** Not enough frequency coverage or data quality issues

**Solution:**
1. Get better data (ALMA for mm/sub-mm, Chandra for X-ray)
2. Accept that source may be hybrid thermal+non-thermal
3. Try narrower frequency range (zoom in on specific band)

---

## 📚 File Locations

```
Project Root/
├── scripts/
│   ├── data_acquisition/
│   │   ├── fetch_m87_spectrum.py           # NED downloader
│   │   ├── parse_ssz_horizon.py            # Report parser
│   │   └── README_NED_DOWNLOAD.md          # NED guide
│   └── analysis/
│       ├── hawking_proxy_fit.py            # Fitter
│       └── README_HAWKING_PROXY_FIT.md     # Fit guide
├── data/
│   ├── observations/
│   │   └── m87_continuum_spectrum_TEMPLATE.csv
│   └── config/
│       └── ssz_config_m87_TEMPLATE.json
├── reports/
│   ├── hawking_proxy_fit.md                # Generated by SSZ tests
│   ├── hawking_fit_report.md               # Generated by fitter
│   └── hawking_fit_plot.png                # Generated by fitter
└── HAWKING_PROXY_TOOLKIT.md                # This file
```

---

## 🎓 Scientific Background

### **Why This Toolkit?**

**Hawking Radiation Prediction:**
```
T_H = (ℏ κ) / (2π k_B c)
```
where κ is surface gravity at horizon.

**SSZ Analogue:**
```
κ_seg ≈ c² / (4 r_φ)
T_seg ≈ (ℏ κ_seg) / (2π k_B c)
```

**Test:**
If continuum spectrum is thermal with T ~ T_seg → evidence for Hawking-like emission!

**This toolkit automates:**
1. Get real spectrum (NED)
2. Get SSZ κ_seg (from tests)
3. Fit thermal vs non-thermal
4. Compare via BIC
5. → Scientific conclusion!

---

## 🎯 Next Steps

### **For Quick Test:**
```bash
# Use templates (no download)
python hawking_proxy_fit.py \
    --spectrum data/observations/m87_continuum_spectrum_TEMPLATE.csv \
    --SSZ data/config/ssz_config_m87_TEMPLATE.json
```

### **For Real Science:**
```bash
# Complete 3-step pipeline
pip install astroquery
python fetch_m87_spectrum.py
python parse_ssz_horizon.py --report <YOUR_REPORT>
python hawking_proxy_fit.py
```

### **For Publication:**
1. Get high-quality data (ALMA Archive, Chandra)
2. Run multiple sources
3. Compare ΔBIC across sources
4. Plot T_fit vs T_seg
5. → Paper-ready results!

---

## 📝 Citation

If you use this toolkit, please cite:

```
Casu, L. & Wrede, C. (2025). Segmented Spacetime Mass Projection - 
Hawking Proxy Toolkit. 
GitHub: error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
```

---

## ✅ Checklist

- [ ] Installed dependencies (`pip install astroquery ...`)
- [ ] Fetched spectrum (`fetch_m87_spectrum.py`)
- [ ] Generated SSZ report (`test_horizon_hawking_predictions.py`)
- [ ] Parsed report to JSON (`parse_ssz_horizon.py`)
- [ ] Ran fit (`hawking_proxy_fit.py`)
- [ ] Reviewed report (`hawking_fit_report.md`)
- [ ] Checked plot (`hawking_fit_plot.png`)
- [ ] Interpreted ΔBIC (thermal vs non-thermal?)

---

**© 2025 Carmen Wrede, Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Version:** 1.0.0  
**Last Updated:** 2025-10-19  
**Status:** ✅ PRODUCTION-READY

**Complete End-to-End Pipeline for Hawking Spectrum Analysis!** 🚀
