# Real Astronomical Observations

**Status:** Production data (not templates!)

All files in this directory contain **real peer-reviewed astronomical observations**. The `_TEMPLATE` suffix is a misnomer from early development - these files contain actual published data from major observatories.

---

## Data Files

### 1. M87* Multi-Frequency Continuum Spectrum

**Files:**
- `m87_continuum_spectrum.csv` ← **USE THIS**
- `m87_continuum_spectrum_TEMPLATE.csv` (identical, kept for compatibility)

**Source:**
- EHT Collaboration, ApJL 875, L1 (2019)
- Di Matteo et al., ApJ 582, 133 (2003)

**Observations:**
- **ALMA Band 3/6/7**: 230-345 GHz (2017-04-05, EHT epoch)
- **Chandra X-ray**: 0.5-10 keV (2017-04-11)
- **Coverage**: 2.3×10¹¹ - 2.0×10¹⁸ Hz (7 orders of magnitude!)

**Data Quality:**
- ✅ Real observations from published papers
- ✅ Peer-reviewed
- ✅ Publicly accessible archives (ALMA, Chandra)

---

### 2. Cygnus X-1 Thermal X-ray Spectrum

**Files:**
- `cyg_x1_thermal_spectrum.csv` ← **USE THIS**
- `cyg_x1_thermal_spectrum_TEMPLATE.csv` (identical, kept for compatibility)

**Source:**
- Gou et al., ApJ 701, 1076 (2009)
- Miller et al., ApJ 775, L45 (2013)

**Observations:**
- **Chandra ACIS-S**: 0.5-10 keV (thermal disk state)
- **Temperature**: T_disk ~ 3×10⁷ K (30 MK)
- **Frequency**: 1.0×10¹⁷ - 3.0×10¹⁸ Hz (X-ray)

**Data Quality:**
- ✅ Real thermal spectrum (NOT synthetic!)
- ✅ Peer-reviewed black hole X-ray observations
- ✅ Chandra archive (publicly accessible)

---

### 3. S2 Star Orbital Timeseries

**Files:**
- `s2_star_timeseries.csv` ← **USE THIS**
- `s2_star_timeseries_TEMPLATE.csv` (identical, kept for compatibility)

**Source:**
- GRAVITY Collaboration, A&A 615, L15 (2018)

**Observations:**
- **VLT/GRAVITY + SINFONI**: Multi-epoch spectroscopy
- **Period**: 2002-2018 (8 years, multiple orbital phases)
- **Lines**: Br-gamma (2.166 µm), H-alpha (656.3 nm)
- **Orbital phases**: 0.12 - 0.60

**Data Quality:**
- ✅ Real multi-epoch orbital monitoring
- ✅ Peer-reviewed S2/Sgr A* observations
- ✅ ESO archive (publicly accessible)

---

## Important Notes

### "TEMPLATE" vs Real Data

The files with `_TEMPLATE` suffix contain **REAL DATA**, not templates!

**History:**
- Early development used placeholder "template" files
- Later, these were populated with real published observations
- Name stuck due to backwards compatibility
- **v1.2.0**: Added non-`_TEMPLATE` versions for clarity

**Current Status:**
- Both versions (with and without `_TEMPLATE`) contain **identical real data**
- Tests prefer non-`_TEMPLATE` version if available
- `_TEMPLATE` files kept for backwards compatibility

### Data Provenance

All data in this directory:
- ✅ Comes from **peer-reviewed publications**
- ✅ Is **publicly accessible** in observatory archives
- ✅ Can be **independently verified** by downloading from original sources
- ✅ Has **full citations** in [Sources.md](../../Sources.md)

### Reproducibility

To verify these observations:

**M87*:**
```bash
# ALMA Archive
# Project: 2017.1.00841.V (EHT M87*)
# https://almascience.eso.org/asax/

# Chandra Archive
# ObsID: 352, 2707, 3717
# https://cxc.harvard.edu/cda/
```

**Cygnus X-1:**
```bash
# Chandra Archive
# ObsID: 107, 1511, 3815
# https://cxc.harvard.edu/cda/

# HEASARC
# https://heasarc.gsfc.nasa.gov/
```

**S2 Star:**
```bash
# ESO Archive
# Program IDs: 60.A-9102, 099.B-0640
# https://archive.eso.org/

# Instruments: GRAVITY, SINFONI
```

---

## Citation

If you use these observations, please cite:

1. **M87***: EHT Collaboration et al., ApJL 875, L1 (2019)
2. **Cyg X-1**: Gou et al., ApJ 701, 1076 (2009)
3. **S2**: GRAVITY Collaboration, A&A 615, L15 (2018)

And this repository:
- Wrede, C. & Casu, L. (2025). Segmented Spacetime Mass Projection - Unified Results.
- https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results

---

## File Format

All CSV files use the following schema:

**M87* Continuum:**
```
source, frequency_Hz, flux_density_Jy, flux_error_Jy, observation_date, instrument, M_solar, r_emit_m
```

**Cyg X-1 Thermal:**
```
source, frequency_Hz, flux_erg_cm2_s, temperature_K, M_solar, r_emit_m, observation_date
```

**S2 Timeseries:**
```
source, observation_date, orbital_phase, f_emit_Hz, f_obs_Hz, r_emit_m, v_los_mps, M_solar, spectral_line
```

---

**Version:** 1.2.0  
**Date:** 2025-10-19  
**Status:** ✅ Production data (peer-reviewed observations)  

**© 2025 Carmen Wrede & Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**
