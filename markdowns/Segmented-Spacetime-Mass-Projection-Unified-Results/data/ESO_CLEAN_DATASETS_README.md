# ESO Clean Datasets - Ready for Immediate Use

## 📦 Included Datasets (Public Release)

### 1. `real_data_emission_lines_clean.csv` (47 observations)
**The 97.9% Validation Dataset**

- **Size:** 12.3 KB
- **Observations:** 47 ESO spectroscopic measurements
- **Success Rate:** 97.9% (46/47 wins vs. GR×SR, p<0.0001)
- **Sources:** ESO Archive (GRAVITY, XSHOOTER instruments)
- **Coverage:** Sgr A*, M87, other compact objects
- **Quality:** Professional-grade spectroscopy (λ/Δλ > 10,000)

**Perfect for:**
- Quick validation testing (`python perfect_paired_test.py`)
- Colab notebooks (no fetch required)
- Full pipeline runs
- Reproducing published 97.9% results

### 2. `real_data_emission_lines_best.csv` (26 observations)
**Sgr A* Optimal Subset**

- **Size:** 7.3 KB
- **Observations:** 26 Sgr A* measurements (best quality)
- **Success Rate:** Even higher than full dataset
- **Sources:** ESO GRAVITY (S-stars + hot spot)
- **Focus:** Photon sphere regime (r ≈ 2-3 r_s)

**Perfect for:**
- Photon sphere validation
- φ/2 boundary tests
- Highest precision demonstrations

---

## 🚀 Quick Start

### Option 1: Instant Test (10 seconds)
```bash
python perfect_paired_test.py --output out/clean_results.csv
# Expected: "SEG wins: 46/47 (97.9%), p-value: 0.0000"
```

### Option 2: Colab Notebook
The datasets are automatically available in Colab notebooks - no fetch needed!

### Option 3: Custom Analysis
```python
import pandas as pd

# Load the 97.9% validation dataset
df = pd.read_csv('data/real_data_emission_lines_clean.csv')

# Or the Sgr A* optimal subset
df_best = pd.read_csv('data/real_data_emission_lines_best.csv')

# Your analysis here...
```

---

## 📊 Data Format

**Columns provided:**
- `case`: Observation identifier
- `category`: Source type (S-stars, emission lines, etc.)
- `M_solar`: Mass in solar masses
- `r_emit_m`: Emission radius in meters
- `v_los_mps`: Line-of-sight velocity (m/s)
- `v_tot_mps`: Total velocity (m/s)
- `lambda_emit_nm`: Rest wavelength (nm)
- `lambda_obs_nm`: Observed wavelength (nm)
- `z`: Observed redshift
- `z_geom_hint`: Geometric hint for SEG model
- `source`: Data provenance (ESO instrument + publication)

**Data Quality:**
- ✅ Sub-percent wavelength accuracy
- ✅ Complete kinematic parameters
- ✅ Pure emission-line spectroscopy
- ✅ Direct local gravitational redshift measurements
- ✅ Gold standard for precision gravitational tests

---

## 🔬 Want More ESO Data?

These 47 observations are curated from ESO Archive for immediate use.

**For additional ESO observations (100+):**

1. **Complete Data Acquisition Guide:**
   - See [`DATA_ACQUISITION_COMPLETE_GUIDE.md`](../docs/DATA_ACQUISITION_COMPLETE_GUIDE.md) - **All methods** (ESO, NED, SIMBAD, GAIA)
   - [`PAIRED_TEST_ANALYSIS_COMPLETE.md`](../PAIRED_TEST_ANALYSIS_COMPLETE.md) - Section "ESO Data Acquisition"
   - Complete 11-step workflow with ADQL queries, FITS handling, data cleaning

2. **Requirements:**
   - ESO user account (free registration)
   - TAP/ADQL expertise
   - FITS file processing knowledge
   - 8-14 hours first-time investment

3. **Scripts:**
   
   **ESO Data (requires token):**
   - [`scripts/download_eso_fits.sh`](../scripts/download_eso_fits.sh) - Download FITS files
   - [`scripts/process_eso_fits_to_csv.py`](../scripts/process_eso_fits_to_csv.py) - Process FITS → CSV
   - [`scripts/clean_real_data_emission_lines.py`](../scripts/clean_real_data_emission_lines.py) - Clean dataset
   
   **GAIA Data (automatic):**
   - [`scripts/fetch_gaia_full.py`](../scripts/fetch_gaia_full.py) - Full GAIA catalog
   - [`scripts/gaia/fetch_gaia_adql.py`](../scripts/gaia/fetch_gaia_adql.py) - ADQL query
   - [`scripts/gaia/fetch_gaia_conesearch.py`](../scripts/gaia/fetch_gaia_conesearch.py) - Cone search
   
   **Other Data Sources (automatic):**
   - [`scripts/fetch_planck.py`](../scripts/fetch_planck.py) - Planck CMB
   - [`scripts/sdss/fetch_sdss_catalog.py`](../scripts/sdss/fetch_sdss_catalog.py) - SDSS catalog
   - [`scripts/data_acquisition/fetch_m87_spectrum.py`](../scripts/data_acquisition/fetch_m87_spectrum.py) - M87 spectrum

4. **Documentation:**
   - Complete step-by-step instructions
   - curl commands provided
   - Error handling examples
   - Validation procedures

**Trade-off:**
- **These 47 observations:** Instant use, 97.9% validation, Colab-ready
- **Full ESO fetch:** More data, but requires expertise + time investment

---

## 📚 Scientific Context

### Why These Datasets Validate SEG at 97.9%

**Professional-Grade Spectroscopy (Gold Standard):**
- Measures exactly what SEG predicts: **local gravitational redshift**
- Sub-percent precision (λ/Δλ > 10,000)
- Complete parameters (M, r, v_los, v_tot, λ, z_geom_hint)
- Direct measurements, not photometric estimates

**Comparison with Catalog Data:**
- **ESO spectroscopy (these files):** 97.9% - measures right physics with precision
- **Catalog compilations:** 51% - often different physics (cosmological redshift), lower precision
- **Quality difference:** +47 percentage points

### Key Results with These Datasets

| Metric | Value | Significance |
|--------|-------|-------------|
| **Overall Success Rate** | **97.9%** (46/47) | p < 0.0001 (highly significant) |
| **Photon Sphere Regime** | **100%** (11/11) | p = 0.0010 (PERFECT) |
| **Strong Field Regime** | **97.2%** (35/36) | p < 0.0001 (near-perfect) |
| **High Velocity Systems** | **94.4%** (17/18) | p = 0.0001 (excellent) |

**φ-Geometry Validation:**
- Without φ: 0% success (complete failure)
- With φ + these datasets: 97.9% success (near-perfect validation)
- 100% in photon sphere validates φ/2 natural boundary prediction

---

## ✅ Verification

**Check dataset integrity:**
```bash
# Count observations
wc -l data/real_data_emission_lines_clean.csv
# Expected: 48 lines (47 data + 1 header)

# Run validation test
python perfect_paired_test.py
# Expected: 97.9% success rate
```

**Dataset checksums:**
```bash
# Clean dataset (47 obs)
md5sum data/real_data_emission_lines_clean.csv

# Best dataset (26 obs)
md5sum data/real_data_emission_lines_best.csv
```

---

## 📖 Documentation References

- **[README.md](../README.md)** - Project overview with 97.9% breakthrough
- **[PAIRED_TEST_ANALYSIS_COMPLETE.md](../PAIRED_TEST_ANALYSIS_COMPLETE.md)** - Complete validation report
- **[PHI_FUNDAMENTAL_GEOMETRY.md](../PHI_FUNDAMENTAL_GEOMETRY.md)** - Why φ is fundamental
- **[STRATIFIED_PAIRED_TEST_RESULTS.md](../STRATIFIED_PAIRED_TEST_RESULTS.md)** - Regime breakdown

---

## 🎯 Summary

**These datasets enable:**
- ✅ Instant 97.9% validation testing (10 seconds)
- ✅ Colab compatibility (no complex fetch process)
- ✅ Full pipeline compatibility
- ✅ Complete reproducibility of published results
- ✅ Professional-grade data quality

**For additional data beyond these 47 observations:**
- Follow documented ESO workflow in `PAIRED_TEST_ANALYSIS_COMPLETE.md`
- Use provided automation scripts
- Expect 8-14 hour time investment for first-time setup
- ESO account + expertise required

**The "fetch horror" is optional - these 47 observations are sufficient for complete validation!**

---

**Copyright © 2025**  
Carmen Wrede & Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
