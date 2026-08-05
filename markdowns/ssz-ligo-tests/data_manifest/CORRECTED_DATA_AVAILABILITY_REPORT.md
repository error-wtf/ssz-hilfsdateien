# Corrected Data Availability Report

**Generated:** 2026-05-14  
**Task:** Final corrected assessment after complete recursive scan  

---

## Executive Summary

After complete recursive scan of `E:\clone\ligo-gw240925-gw250207-release\18600070`, the **corrected** data availability status is:

| Category | Status |
|----------|--------|
| **Primary posterior samples (Top-Level Metafiles)** | ✅ **Available and usable** |
| **Strain data** | ✅ **Available and usable** |
| **Ringdown products** | ✅ **Available and usable** |
| **QNM/FTI products** | ❌ **Blocked - 0-byte symlink placeholders** |
| **TIGER products** | ❌ **Blocked - 0-byte symlink placeholders** |

**Neither "everything broken" nor "everything OK" - but the primary data for QNM R_f analysis IS available.**

---

## Product-by-Product Truth Table

| Product | Location | File Count | Real Size | Status | Usable |
|---------|----------|------------|-----------|--------|--------|
| **GW240925_combinedPHM** | Root level | 1 | 190.8 MB | ✅ Real HDF5 | **YES** |
| **GW250207_combinedPHM** | Root level | 1 | 292.5 MB | ✅ Real HDF5 | **YES** |
| **GW240925-C00-Strain** | `GW240925-C00-Strain/` | 6 | 51-486 MB each | ✅ Real HDF5 | **YES** |
| **ringdown** | `ringdown/` | 1 | 1.2 MB | ✅ Real HDF5 | **YES** |
| **qnmrf** | `qnmrf/` | 2 | ~MB each | ✅ Real HDF5 | **YES** |
| **pca** | `pca/` | 8 | 25-106 MB each | ✅ Real HDF5 | **YES** |
| **pseobnr** | `pseobnr/` | 6 | 16-40 MB each | ✅ Real HDF5 | **YES** |
| **fti** | `fti/fti/` | 50 | **0 B each** | ❌ Broken symlinks | **NO** |
| **tiger** | `tiger/tiger/` | 72 | **0 B each** | ❌ Broken symlinks | **NO** |
| **calibration** | `calibration/` | 3 | Small | ✅ Real files | Partial |
| **residuals** | `residuals/` | 12 | Mixed | ⚠️ Check individually | Partial |
| **skymaps** | `skymaps/` | 37 | PNG/FITS | ✅ Real files | Non-HDF5 |

---

## Real File Counts and Sizes

### Usable HDF5 Files (Verified with h5py)

| File Path | Size | Objects | QNM-Related |
|-----------|------|---------|-------------|
| `GW240925_combinedPHM_envcalC01_metafile.hdf5` | 190.8 MB | 1,898 | Yes |
| `GW250207_combinedPHM_cal_metafile.hdf5` | 292.5 MB | 3,105 | Yes |
| `pca/*.hdf5` (8 files) | 25-106 MB each | Varies | Partial |
| `pseobnr/*.hdf5` (6 files) | 16-40 MB each | 379-469 each | Yes |
| `qnmrf/*.hdf5` (2 files) | ~MB each | Varies | Yes |
| `ringdown/*.hdf5` (1 file) | 1.2 MB | 10 | Yes |
| `GW240925-C00-Strain/*.hdf5` (6 files) | 51-486 MB | 26 each | Strain data |

**Total usable HDF5 data: ~1.5 GB**

### 0-Byte/Broken Files

| Location | Count | Size | Issue |
|----------|-------|------|-------|
| `fti/fti/*/` | 50 | 0 B each | Broken symlinks to `/home/tgr.o4/...` |
| `tiger/tiger/*/` | 72 | 0 B each | Broken symlinks to `/home/tgr.o4/...` |
| **Total blocked** | **122** | **0 B** | **Windows extraction artifact** |

---

## What Is Usable

### Primary Data (Essential for R_f)
✅ **GW240925_combinedPHM_envcalC01_metafile.hdf5**
- Contains: Posterior samples for GW240925
- Size: 190.8 MB
- Groups: C01:IMRPhenomXPHM-SpinTaylor, C01:IMRPhenomXPNR, C01:Mixed, C01:SEOBNRv5PHM
- Fields expected: final_mass, final_spin, mass_1, mass_2, calibration, etc.

✅ **GW250207_combinedPHM_cal_metafile.hdf5**
- Contains: Posterior samples for GW250207  
- Size: 292.5 MB
- Groups: C00:IMRPhenomXAS, C00:IMRPhenomXPHM-SpinTaylor, C00:IMRPhenomXPNR, C00:Mixed, C00:NRSur7dq4, C00:SEOBNRv5PHM
- Fields expected: final_mass, final_spin, calibration, etc.

### Secondary Data (Support/Validation)
✅ **ringdown/** - 1 HDF5 file with ringdown analysis  
✅ **qnmrf/** - 2 HDF5 files with QNM reference data  
✅ **pca/** - 8 HDF5 files with PCA analysis  
✅ **pseobnr/** - 6 HDF5 files with SEOBNR comparisons  
✅ **GW240925-C00-Strain/** - 6 strain data files

---

## What Is Blocked

### FTI Products
❌ **Location:** `fti/fti/S240925n_*/` and `fti/fti/S250207bg_*/`  
❌ **Count:** 50 files  
❌ **Size:** 0 B each  
❌ **Issue:** Broken symlinks pointing to `/home/tgr.o4/GW240925_GW250207/FTI/...`  
❌ **Status:** Unusable from current Windows extraction

### TIGER Products  
❌ **Location:** `tiger/tiger/GW240925_*/` and `tiger/tiger/GW250207_*/`  
❌ **Count:** 72 files  
❌ **Size:** 0 B each  
❌ **Issue:** Broken symlinks pointing to `/home/tgr.o4/GW240925_GW250207/TIGER/...`  
❌ **Status:** Unusable from current Windows extraction

**Root cause:** These were absolute Linux symlinks in the original tar archives. Windows extraction created 0-byte placeholder files instead of resolving them.

---

## Impact on Preregistered R_f Test

### Original Plan
The preregistered R_f test included potential validation through multiple paths including FTI/TIGER products.

### Corrected Reality
**Primary R_f test CAN proceed** using:
1. Top-level combinedPHM metafiles (final_mass, final_spin posteriors)
2. ringdown products (measured QNM frequencies)
3. qnmrf products (reference QNM data)

**FTI/TIGER validation is BLOCKED** - these supplementary products are not available from current extraction.

### R_f Computation Path Forward
```
Primary measurement:
  └── GW240925/GW250207_combinedPHM metafiles
      └── final_mass, final_spin posteriors
      └── GR-predicted QNM frequency

Independent measurement:
  └── ringdown/ products
      └── Measured QNM frequencies (f_220, tau_220)

Reference data:
  └── qnmrf/ products
      └── QNM reference tables

Anti-circularity check:
  └── Verify ringdown measurement ≠ GR template used in combinedPHM
```

**FTI/TIGER were supplementary validation only.** Their absence does not block the primary R_f test.

---

## Explicit Statements

### Safety Declarations
- ✅ **R_f was NOT computed** in any previous phase
- ✅ **SSZ was NOT tested** against LIGO data
- ✅ **No GR claims were made** based on this dataset
- ✅ **No data was modified, deleted, or overwritten**
- ✅ **All original archives preserved**

### Data Integrity
- All inspections were **read-only**
- No extraction parameters were changed
- No files were repaired, symlinked, or moved
- Original broken symlinks remain as extracted

---

## Next Steps

### Immediate (Proceed)
1. **Extract final_mass, final_spin from combinedPHM metafiles**
2. **Extract QNM frequencies from ringdown products**
3. **Verify anti-circularity** (ringdown independent from GR templates)
4. **Compute R_f** only after independence confirmed

### Later (When Possible)
1. **Request FTI/TIGER clarification from LIGO** - are real files available separately?
2. **Or attempt WSL re-extraction** - may preserve symlinks differently
3. **Use FTI/TIGER for supplementary validation** once available

### NOT To Do
- ❌ Do not claim the whole release is broken (primary data is available)
- ❌ Do not claim FTI/TIGER are critical for primary R_f (they're supplementary)
- ❌ Do not attempt workarounds that modify the 0-byte files
- ❌ Do not compute R_f before anti-circularity verification

---

## Summary Table: Final Status

| Component | Availability | Role in R_f Test | Priority |
|-----------|--------------|------------------|----------|
| combinedPHM metafiles | ✅ Available | Primary data | **Critical** |
| ringdown | ✅ Available | Independent measurement | **Critical** |
| qnmrf | ✅ Available | Reference data | **High** |
| pca | ✅ Available | Cross-check | Medium |
| pseobnr | ✅ Available | Method comparison | Medium |
| Strain | ✅ Available | Event verification | Low for R_f |
| FTI | ❌ Blocked | Supplementary validation | Postponed |
| TIGER | ❌ Blocked | Supplementary validation | Postponed |

---

## Conclusion

**The primary LIGO GW240925/GW250207 data IS available and usable for the preregistered QNM R_f test.**

The FTI and TIGER products are blocked due to broken symlinks in the Windows extraction, but these were **supplementary validation paths**, not critical for the primary R_f computation.

**Next action:** Proceed with QNM field extraction from accessible top-level metafiles, ringdown, and qnmrf products only.

---

*This report corrects previous over-optimistic assessments ("everything OK") and over-pessimistic assessments ("everything broken") with the actual ground truth.*
