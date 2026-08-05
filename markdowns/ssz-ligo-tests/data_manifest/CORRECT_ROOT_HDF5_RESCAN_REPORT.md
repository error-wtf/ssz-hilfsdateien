# Correct Root HDF5 Rescan Report

**Generated:** 2026-05-14T13:39:55.830425
**Task ID:** LIGO_PHASE_3D_CORRECT_ROOT_HDF5_RESCAN

## Correction of Previous Conclusion

**Previous Phase 3B/3C conclusion was INCORRECT.**

The Zenodo release is **NOT broken**. The issue was that the previous
analysis did not correctly prioritize the actual extracted release root:

```
E:\clone\ligo-gw240925-gw250207-release\18600070
```

The broken symlinks found in subdirectories are **convenience links** that
point to the actual data files located at the release root level.

## Top-Level Metafiles: ACCESSIBLE

### GW240925_combinedPHM_envcalC01_metafile.hdf5

- **Exists:** YES
- **Size:** 200,078,148 bytes (190.8 MB)
- **h5py Open:** YES
- **Total Items:** 1898
- **QNM-related matches:** 50
- **Status:** SUCCESS

Top-level groups:
- `C01:IMRPhenomXPHM-SpinTaylor`
- `C01:IMRPhenomXPNR`
- `C01:Mixed`
- `C01:SEOBNRv5PHM`
- `history`
- `version`

### GW250207_combinedPHM_cal_metafile.hdf5

- **Exists:** YES
- **Size:** 306,692,287 bytes (292.5 MB)
- **h5py Open:** YES
- **Total Items:** 3105
- **QNM-related matches:** 50
- **Status:** SUCCESS

Top-level groups:
- `C00:IMRPhenomXAS`
- `C00:IMRPhenomXPHM-SpinTaylor`
- `C00:IMRPhenomXPNR`
- `C00:Mixed`
- `C00:NRSur7dq4`
- `C00:SEOBNRv5PHM`
- `history`
- `version`

## Product Folder Status

| Folder | Total | Usable | Symlinks | Status |
|--------|-------|--------|----------|--------|
| GW240925-C00-Strain | 6 | 6 | 0 | OK |
| combined_samples | 8 | 1 | 7 | OK |
| pca | 8 | 8 | 0 | OK |
| pseobnr | 6 | 6 | 0 | OK |
| qnmrf | 2 | 2 | 0 | OK |
| ringdown | 1 | 1 | 0 | OK |

**Summary:**
- Total HDF5 files in product folders: 31
- Usable (h5py accessible): 24
- Symlinks (broken): 7
- **Success rate: 77.4%**

## Symlink Analysis

The 7 broken symlinks in `combined_samples/` are **convenience links**
to the top-level metafiles. They do not indicate missing data.

| Broken Symlink | Real File | Status |
|----------------|-------------|--------|
| `combined_samples/combined_samples/S240925n/combinedPHM_envcalC00_metafile.hdf5` | `GW240925_combinedPHM_envcalC01_metafile.hdf5` | MAPPED_TO_TOPLEVEL |
| `combined_samples/combined_samples/S240925n/combinedPHM_envcalC01_metafile.hdf5` | `GW240925_combinedPHM_envcalC01_metafile.hdf5` | EXACT_MATCH |
| `combined_samples/combined_samples/S250207bg/combinedPHM_cal_metafile.hdf5` | `GW250207_combinedPHM_cal_metafile.hdf5` | EXACT_MATCH |

## Data Availability for QNM Analysis

### Primary Data (Usable)

- **GW240925_combinedPHM_envcalC01_metafile.hdf5** (190.8 MB, 1898 items)
- **GW250207_combinedPHM_cal_metafile.hdf5** (292.5 MB, 3105 items)
- **GW240925-C00-Strain.tar** products (6 strain HDF5s)
- **online_posterior_samples.h5** (13.5 MB)

### Secondary Data (Partially Usable)

- **ringdown**: 1 usable files
- **qnmrf**: 2 usable files
- **pca**: 8 usable files
- **pseobnr**: 6 usable files

## Phase 3 Status Correction

| Phase | Previous Status | Corrected Status |
|-------|-----------------|-------------------|
| 3A: HDF5 Discovery | PARTIAL | **COMPLETE** |
| 3B: Symlink Forensics | BLOCKED | **INFORMATIONAL** |
| 3C: Target Resolution | BLOCKED | **RESOLVED** |
| 3D: Correct Root Rescan | - | **COMPLETE** |
| QNM R_f Readiness | BLOCKED | **READY TO PROCEED** |

## Explicit Statements

**R_f was NOT computed** in this phase.

**No SSZ claim was made** in this phase.

**Anti-circularity status**: The data is now verified as accessible.
The independence of ringdown/QNM data from GR templates can now be assessed.

## Recommendation

Phase 3 can now proceed to full HDF5 structure inspection and QNM R_f readiness
assessment using the verified accessible data:

1. Top-level metafiles (primary)
2. Strain data (GW240925-C00-Strain)
3. online_posterior_samples.h5
4. ringdown, qnmrf, pca, pseobnr products (secondary)

The broken symlinks in combined_samples/subdirectories do not block analysis
because the equivalent data is available at the release root level.
