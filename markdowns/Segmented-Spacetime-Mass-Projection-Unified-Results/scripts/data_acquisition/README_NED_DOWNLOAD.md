# NED Spectrum Download - Quick Start Guide

**Fetch real continuum spectrum data from NED for Hawking Spectrum Test**

---

## 🚀 Quick Start

### **Installation:**
```bash
pip install astroquery
```

### **Download M87 Spectrum:**
```bash
python scripts/data_acquisition/fetch_m87_spectrum.py \
    --name "M87" \
    --minGHz 30 \
    --maxGHz 1000 \
    --out data/observations/m87_continuum_spectrum.csv
```

### **Run Hawking Spectrum Test:**
```bash
# Test will auto-detect the new data file
python scripts/tests/test_hawking_spectrum_continuum.py
```

---

## 📋 Usage Examples

### **M87 (full spectrum):**
```bash
python scripts/data_acquisition/fetch_m87_spectrum.py \
    --name "M87" \
    --minGHz 1 \
    --maxGHz 10000 \
    --M_solar 6.5e9 \
    --r_emit_m 1.2e13 \
    --out data/observations/m87_continuum_spectrum.csv
```

### **Sgr A* (Galactic Center):**
```bash
python scripts/data_acquisition/fetch_m87_spectrum.py \
    --name "Sgr A*" \
    --minGHz 1 \
    --maxGHz 1000 \
    --M_solar 4.15e6 \
    --r_emit_m 3.8e10 \
    --out data/observations/sgra_continuum_spectrum.csv
```

### **Cygnus X-1 (X-ray binary):**
```bash
python scripts/data_acquisition/fetch_m87_spectrum.py \
    --name "Cyg X-1" \
    --minGHz 0.1 \
    --maxGHz 100000 \
    --M_solar 14.8 \
    --r_emit_m 4.4e4 \
    --out data/observations/cygx1_continuum_spectrum.csv
```

---

## 🎯 Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `--name` | `M87` | Source name (NED query) |
| `--minGHz` | `30.0` | Minimum frequency (GHz) |
| `--maxGHz` | `1000.0` | Maximum frequency (GHz) |
| `--out` | `m87_spectrum.csv` | Output CSV file |
| `--M_solar` | `6.5e9` | Black hole mass (M☉) |
| `--r_emit_m` | `1.2e13` | Emission radius (m) |

---

## 📊 Output Format

**CSV Columns:**
```csv
source,frequency_Hz,flux_density_Jy,flux_error_Jy,M_solar,r_emit_m,instrument,observation_date
M87,2.300e+11,0.95,0.05,6.5e9,1.2e13,1997ApJS..110...19L,1997
M87,3.450e+11,1.02,0.06,6.5e9,1.2e13,1997ApJS..110...19L,1997
...
```

**Compatible with:**
- ✅ `test_hawking_spectrum_continuum.py`
- ✅ Standard spectrum analysis tools
- ✅ Multi-source analysis

---

## 🔍 What happens?

### **1. Query NED:**
```python
from astroquery.ned import Ned
tab = Ned.get_table('M87', table='photometry')
```

NED returns all published photometry measurements for M87.

### **2. Extract Frequencies:**
- If NED has `frequency` column → use directly
- Else: Convert wavelength (Å) → frequency (Hz)

### **3. Extract Fluxes:**
- Searches for Jy (Jansky) flux columns
- Extracts uncertainties (or assumes 10%)

### **4. Filter & Clean:**
- Frequency range: `minGHz` to `maxGHz`
- Positive fluxes only
- Remove NaN values

### **5. Save CSV:**
- Compatible format with our test framework
- Includes source metadata (M, r_emit)

---

## 🧪 Integration with Hawking Spectrum Test

### **Auto-Detection:**

`test_hawking_spectrum_continuum.py` checks:
```python
# Priority order:
1. data/observations/m87_continuum_spectrum.csv      # Real data (from NED)
2. data/observations/m87_continuum_spectrum_TEMPLATE.csv  # Template fallback
```

### **Full Workflow:**

```bash
# 1. Download real data
python scripts/data_acquisition/fetch_m87_spectrum.py

# 2. Run test (auto-detects real data)
python scripts/tests/test_hawking_spectrum_continuum.py
# Output:
# Data source: m87_continuum_spectrum.csv
# ✅ Real data loaded (not template!)
# Sources found: 1
# Frequency range: 2.300e+11 - 5.000e+18 Hz
# Data points: 150
# ...
# ΔBIC = BIC_nonth - BIC_thermal = ???
```

---

## 📈 Expected Results

### **M87 (typical):**
- **Data points:** 50-200 (depends on NED coverage)
- **Frequency range:** ~GHz (radio) to ~keV (X-ray)
- **Instruments:** VLA, ALMA, Chandra, HST, etc.

### **Quality:**
- ✅ Multi-epoch observations
- ✅ Multi-instrument cross-calibrated
- ✅ Published uncertainties
- ⚠️ May have gaps (no mm/sub-mm coverage)

---

## ⚠️ Known Limitations

### **1. NED Coverage:**
- Best for: Radio, Optical, X-ray
- Limited: mm/sub-mm (use ALMA Archive instead)
- None: γ-ray (use Fermi LAT directly)

### **2. Data Quality:**
- Heterogeneous (different instruments, epochs)
- Not simultaneous (variability possible)
- May need additional filtering

### **3. Alternatives for better data:**

**Sub-mm/mm (Horizon scale):**
- Use ALMA Archive (almascience.nrao.edu/aq/)
- EHT Public Data (eventhorizontelescope.org)

**X-ray (Accretion disk):**
- Use Chandra/XMM directly (cda.harvard.edu)
- Better spectral resolution

**Multi-wavelength SEDs:**
- EHT-MWL 2017 (VizieR: J/ApJL/875/L1)
- Coordinated campaigns

---

## 🎯 Troubleshooting

### **Error: "astroquery not installed"**
```bash
pip install astroquery
```

### **Error: "No Jy flux column detected"**
```bash
# Check available columns:
from astroquery.ned import Ned
tab = Ned.get_table('M87', table='photometry')
print(tab.colnames)
# Adapt script if needed
```

### **Error: "No data in frequency range"**
```bash
# Expand range:
python fetch_m87_spectrum.py --minGHz 0.1 --maxGHz 100000
```

### **Too few data points:**
```bash
# 1. Expand frequency range
# 2. Try different source (brighter = more coverage)
# 3. Use ALMA/Chandra for specific bands
```

---

## 📚 References

**NED (NASA/IPAC Extragalactic Database):**
- URL: https://ned.ipac.caltech.edu/
- API Docs: https://astroquery.readthedocs.io/en/latest/ned/ned.html
- Citation: Helou et al. (1991), doi:10.1086/316350

**Data Sources in NED:**
- VLA (Very Large Array)
- ALMA (Atacama Large Millimeter Array)
- Chandra X-ray Observatory
- HST (Hubble Space Telescope)
- Spitzer, Herschel, WISE, etc.

---

## ✅ Success Checklist

- [x] astroquery installed
- [x] Script runs without errors
- [x] CSV file created
- [x] Data points > 10 (preferably > 50)
- [x] Frequency range covers multiple decades
- [x] Test script auto-detects real data
- [x] ΔBIC calculation runs successfully

---

**© 2025 Carmen Wrede, Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Version:** 1.0.0  
**Last Updated:** 2025-10-19  
**Status:** ✅ READY TO USE
