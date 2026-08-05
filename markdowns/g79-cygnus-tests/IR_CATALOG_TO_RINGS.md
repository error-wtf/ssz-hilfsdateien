# IR Catalog → Ring Profile Workflow

**Date:** 2025-11-05  
**Status:** ✅ Scripts ready, data downloaded

---

## 📊 Available Data

### AKARI FIS (Far-Infrared Survey)
- **File:** `data/telescope/akari_fis_test.csv`
- **Sources:** 24 objects around G79
- **Bands:** 65, 90, 140, 160 μm
- **Columns:** `flux65`, `flux90`, `flux140`, `flux160` (Jy)

### WISE AllWISE (Mid-Infrared)
- **File:** `data/telescope/allwise_p3as_psd_test.csv`
- **Sources:** 1371 objects around G79
- **Bands:** W1 (3.4 μm), W2 (4.6 μm), W3 (12 μm), W4 (22 μm)
- **Columns:** `w1mpro`, `w2mpro`, `w3mpro`, `w4mpro` (magnitudes)

---

## 🚀 Quick Start

### Option 1: Process ALL catalogs (recommended)
```bash
python scripts/process_ir_catalogs.py
```

**Output:**
- `data/telescope/akari_fis_rings.csv` - AKARI 4-band ring profile
- `data/telescope/allwise_rings.csv` - WISE 4-band ring profile

### Option 2: Process individual catalog
```bash
# AKARI
python scripts/catalog_to_rings.py \
  data/telescope/akari_fis_test.csv \
  --bands flux65,flux90,flux140,flux160 \
  --output data/telescope/akari_fis_rings.csv

# WISE
python scripts/catalog_to_rings.py \
  data/telescope/allwise_p3as_psd_test.csv \
  --bands w1mpro,w2mpro,w3mpro,w4mpro \
  --output data/telescope/allwise_rings.csv
```

---

## 📁 Script Overview

### 1. `catalog_to_rings.py` - Core converter
**Purpose:** Convert catalog point sources to radial ring profiles

**Method:**
1. Load catalog CSV
2. Calculate radius from G79 center (RA 20:31:41, Dec +40:21:07)
3. Bin sources into rings (0-2 pc, 0.2 pc spacing = 10 rings)
4. Average flux in each ring
5. Save ring profile CSV

**Arguments:**
- `catalog_file` - Input CSV with RA, Dec, flux columns
- `--bands` - Comma-separated flux column names
- `--ra-col` - RA column name (default: `ra`)
- `--dec-col` - Dec column name (default: `dec`)
- `--output` - Output CSV file (default: auto-generated)

### 2. `process_ir_catalogs.py` - Batch processor
**Purpose:** Process AKARI + WISE catalogs in one run

**Runs:**
- AKARI FIS: 4 bands (65, 90, 140, 160 μm)
- WISE: 4 bands (W1, W2, W3, W4)

---

## 📊 Output Format

Ring profile CSV with columns:
- `ring` - Ring index (0 = innermost)
- `r_min_pc` - Inner radius [pc]
- `r_max_pc` - Outer radius [pc]  
- `radius_pc` - Ring center [pc]
- `n_sources` - Number of catalog sources in ring
- For each band:
  - `{band}_mean` - Mean flux
  - `{band}_median` - Median flux
  - `{band}_std` - Standard deviation
  - `{band}_err` - Standard error
  - `{band}_n` - Number of valid measurements

**Example (AKARI):**
```csv
ring,r_min_pc,r_max_pc,radius_pc,n_sources,flux65_mean,flux65_median,flux65_std,...
0,0.0,0.2,0.1,5,120.5,115.2,12.3,...
1,0.2,0.4,0.3,8,98.2,95.1,8.7,...
...
```

---

## 🔄 Workflow Integration

### Current pipeline:
```
1. Query IRSA catalogs        → test_irsa_catalogs.py
2. Save catalog CSVs          → data/telescope/*.csv
3. Convert to ring profiles   → catalog_to_rings.py
4. Fit γ_seg(r)              → fit_gamma_seg_profile.py
5. Compare to theory          → (integration needed)
```

### Next steps after ring extraction:
1. **Validate rings:** Check CSV files look reasonable
2. **Convert units:** WISE magnitudes → flux if needed
3. **Fit profiles:** Run `fit_gamma_seg_profile.py`
4. **Compare:** AKARI vs WISE consistency?
5. **Theory test:** Match γ_seg predictions?

---

## 🎯 Scientific Goal

**Test SSZ Prediction:**
Radial density profile should follow:
```
γ_seg(r) ∝ exp(-r/r_seg)  (segmented spacetime decay)
```

**IR data advantages:**
- Dust emission traces matter density
- Multiple wavelengths → temperature
- Catalog sources → easy radial binning
- Complements NH3/CO line data

---

## 🔬 Technical Notes

### Coordinate transformation
```python
# G79 center
G79_CENTER = SkyCoord("20h31m41s +40d21m07s", frame="icrs")
G79_DISTANCE = 1.7  # kpc

# Calculate radius for each source
coords = SkyCoord(ra=df['ra'], dec=df['dec'], frame='icrs')
r_ang = coords.separation(G79_CENTER)
r_pc = (r_ang.to(u.rad) * (G79_DISTANCE * u.kpc)).to(u.pc).value
```

### Ring binning
```python
# Ring edges: 0.0, 0.2, 0.4, ..., 2.0 pc
R_EDGES_PC = np.arange(0.0, 2.0 + 0.2, 0.2)

# Bin sources
for r_min, r_max in zip(R_EDGES_PC[:-1], R_EDGES_PC[1:]):
    mask = (r_pc >= r_min) & (r_pc < r_max)
    flux_ring = df.loc[mask, 'flux'].mean()
```

### Error propagation
```python
# Standard error of the mean
flux_err = flux_std / sqrt(n_sources)
```

---

## ⚠️ Known Limitations

1. **WISE magnitudes:** Currently saved as magnitudes, not flux
   - Need conversion: `F_ν = F_0 × 10^(-mag/2.5)`
   - WISE zero points: W1=309.54 Jy, W2=171.79 Jy, W3=31.67 Jy, W4=8.36 Jy

2. **Point source assumption:** Assumes sources are unresolved
   - May miss extended emission
   - Complements FITS image analysis

3. **Sparse sampling:** AKARI has only 24 sources
   - Some rings may be empty
   - WISE has better coverage (1371 sources)

---

## 📚 Related Files

**Data extraction:**
- `scripts/test_irsa_catalogs.py` - Test catalog queries
- `data/telescope/*.csv` - Downloaded catalogs

**Ring extraction (FITS images):**
- `scripts/extract_akari_rings.py` - For 2D FITS images
- `scripts/fits_to_ring_profile.py` - Generic FITS → rings

**Analysis:**
- `scripts/fit_gamma_seg_profile.py` - Fit exponential profiles
- `scripts/analyze_nh3_velocities.py` - NH3 analysis
- `scripts/extract_co_velocity_rings.py` - CO analysis

---

## 🎉 Success Criteria

✅ AKARI catalog → ring profile  
✅ WISE catalog → ring profile  
⏳ Validate ring consistency  
⏳ Convert WISE mag → flux  
⏳ Fit γ_seg(r) to both datasets  
⏳ Compare AKARI vs WISE  
⏳ Test against SSZ predictions  

---

© 2025 Carmen N. Wrede, Lino P. Casu  
Method: Catalog point source binning  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
