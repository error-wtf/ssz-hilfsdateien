# Time-Series Data for SSZ Theory Predictions

**Purpose:** Provide time-series and thermal spectrum data for complete validation of SSZ theory predictions.

---

## Required Data Files

### **1. S2 Star Time-Series (Information Preservation)**

**File:** `s2_star_timeseries.csv`  
**Status:** ⚠️ **TEMPLATE ONLY** - Real data needed  
**Use Case:** Jacobian reconstruction test (Test 2a)

**Template:** `s2_star_timeseries_TEMPLATE.csv`

**Required Columns:**
- `source` (str) - Source identifier (e.g., "S2")
- `observation_date` (str) - ISO date (YYYY-MM-DD) or MJD
- `orbital_phase` (float) - Orbital phase 0-1 (optional but recommended)
- `f_emit_Hz` (float) - Rest-frame frequency [Hz]
- `f_obs_Hz` (float) - Observed frequency [Hz]
- `r_emit_m` (float) - Emission radius [meters]
- `v_los_mps` (float) - Line-of-sight velocity [m/s]
- `M_solar` (float) - Central mass [solar masses]
- `spectral_line` (str) - Line identifier (e.g., "Br-gamma", "H-alpha")

**Minimum Requirements:**
- ≥5 observations per source
- ≥2 unique f_emit values (multiple spectral lines)
- Covers significant orbital range (0.1-0.9 phase)

**Data Sources:**
- ESO Archive (GRAVITY, SINFONI)
- Keck Observatory (Galactic Center observations)
- Published papers (Gillessen et al., GRAVITY Collaboration)

---

### **2. Cyg X-1 Thermal Spectrum (Hawking Radiation)**

**File:** `cyg_x1_thermal_spectrum.csv`  
**Status:** ⚠️ **TEMPLATE ONLY** - Real data needed  
**Use Case:** Hawking spectrum BIC test (Test 4a)

**Template:** `cyg_x1_thermal_spectrum_TEMPLATE.csv`

**Required Columns:**
- `source` (str) - Source identifier (e.g., "Cyg_X-1")
- `frequency_Hz` (float) - Photon frequency [Hz]
- `flux_erg_cm2_s` (float) - Energy flux [erg/cm²/s]
- `temperature_K` (float) - Thermal component temperature [K]
- `M_solar` (float) - Black hole mass [solar masses]
- `r_emit_m` (float) - Emission radius (innermost disk) [meters]
- `observation_date` (str) - Observation date (optional)

**Minimum Requirements:**
- ≥50 frequency bins
- Covers thermal peak (10¹⁶-10¹⁹ Hz for stellar BH)
- Thermal component fitted (not total spectrum)

**Data Sources:**
- HEASARC Archive (XMM-Newton, Chandra)
- Swift/BAT Catalog
- Published spectra (Remillard & McClintock, etc.)

---

## Data Validation

### **Automated Check:**
```bash
python scripts/data_loaders/load_timeseries.py data/observations/s2_star_timeseries.csv
```

**Output:**
```
TIME-SERIES DATA SUMMARY
================================================================================
Total sources loaded: 1

Source: S2
  Observations: 10
  Status: ✅ VALID
  f_emit range: 2.3395e+14 Hz (2 unique)
  f_obs range: 3.3008e+13 Hz
  r_emit range: 1.0000e+10 - 3.8072e+10 m
  
================================================================================
Total observations across all sources: 10
Sources valid for Jacobian reconstruction: 1/1
```

---

## Integration in Tests

### **Option 1: Automatic Detection**

Place files in `data/observations/`:
- `s2_star_timeseries.csv`
- `cyg_x1_thermal_spectrum.csv`

Tests will auto-detect and use them.

### **Option 2: Manual Path**

```python
python scripts/tests/test_horizon_hawking_predictions.py \
    --timeseries data/observations/s2_star_timeseries.csv \
    --thermal-spectrum data/observations/cyg_x1_thermal_spectrum.csv
```

---

## Data Acquisition Workflow

See: `DATA_ACQUISITION_PLAN.md` for detailed instructions

**Quick Start:**

### **S2 Star (ESO Archive)**
1. Visit: https://archive.eso.org
2. Search: Target="S2", Instrument="GRAVITY"
3. Download: FITS files + supplementary tables
4. Extract: Radial velocities, frequencies
5. Format: CSV as per template

### **Cyg X-1 (HEASARC)**
1. Visit: https://heasarc.gsfc.nasa.gov
2. Search: Target="Cyg X-1", Mission="XMM-Newton"
3. Download: PPS (Pipeline Products)
4. Extract: Spectrum FITS → ASCII
5. Format: CSV as per template

---

## Example: Converting Published Data

### **From Paper Tables (S2):**

**Paper:** GRAVITY Collaboration (2018), A&A 615, L15

**Table 2:** Radial Velocity Measurements

```python
import pandas as pd

# Load table from paper
paper_data = pd.read_csv('gravity_2018_table2.txt', sep='\t')

# Map to our format
df = pd.DataFrame({
    'source': 'S2',
    'observation_date': paper_data['Date'],
    'orbital_phase': paper_data['Phase'],
    'f_emit_Hz': 4.568050e+14,  # Br-gamma rest frequency
    'f_obs_Hz': paper_data['Observed_Freq'],  # Calculate from RV
    'r_emit_m': paper_data['Radius'],
    'v_los_mps': paper_data['RV'] * 1000,  # Convert km/s to m/s
    'M_solar': 4.15e6,
    'spectral_line': 'Br-gamma'
})

df.to_csv('s2_star_timeseries.csv', index=False)
```

---

## Current Status

### **Existing Data:**
- ✅ `phi_step_debug_full.csv` - 127 cross-source observations
- ✅ `_enhanced_debug.csv` - Redshift decomposition

### **Missing Data (Templates Only):**
- ⚠️ `s2_star_timeseries.csv` - Need ≥5 S2 observations
- ⚠️ `cyg_x1_thermal_spectrum.csv` - Need X-ray thermal spectrum

### **Tests Status:**
| Test | Data Available | Status |
|------|----------------|--------|
| **1. Horizon Area** | ✅ Yes | ✅ Validated |
| **2. Information** | ⚠️ Template | ⚠️ Framework ready |
| **3. Singularity** | ✅ Yes | ✅ Validated |
| **4. Hawking Proxy** | ✅ Yes | ✅ Validated |
| **1a. r_φ Cross-Verify** | ✅ Yes | ✅ Validated |
| **2a. Jacobian Recon** | ⚠️ Template | ⚠️ Needs time-series |
| **4a. Spectrum Fit** | ⚠️ Template | ⚠️ Needs thermal source |

---

## Contact & Support

**Data Questions:**
- Email: (your contact)
- GitHub Issues: https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/issues

**Archive Help:**
- ESO: archive@eso.org
- HEASARC: heasarc-vo@athena.gsfc.nasa.gov

---

**© 2025 Carmen Wrede, Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**
