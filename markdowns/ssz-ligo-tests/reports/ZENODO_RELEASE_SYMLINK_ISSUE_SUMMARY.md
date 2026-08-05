# Zenodo Release Symlink Issue Summary

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Date:** 2026-05-14  
**Task ID:** LIGO_PHASE_3C_SYMLINK_TARGET_RESOLUTION_AUDIT  
**Status:** RELEASE_PACKAGING_ISSUE_SUSPECTED  

---

## Problem Summary

The Zenodo release for GW240925 and GW250207 (Event ID: 18600070) contains HDF5 products distributed as **absolute Linux symbolic links** pointing to local paths under `/home/...`.

The symlink targets do **not appear to be included** in the public release archive, making these products inaccessible from a clean extraction environment.

This is a **packaging/release issue**, not a problem with the underlying scientific data.

---

## Affected Archives

| Archive | HDF5 Symlinks | Regular HDF5s | Status |
|---------|---------------|---------------|--------|
| `combined_samples.tar.gz` | 7 | 1 | Partial |
| `fti.tar.gz` | 50 | 0 | **Blocked** |
| `tiger.tar.gz` | 72 | 0 | **Blocked** |
| `ringdown.tar.gz` | 0 | 1 | OK |
| `qnmrf.tar.gz` | 0 | 2 | OK |
| `pca.tar.gz` | 0 | 8 | OK |
| `pseobnr.tar.gz` | 0 | 6 | OK |
| `GW240925-C00-Strain.tar` | 0 | 6 | OK |

**Total HDF5-like paths found:** 159  
**Symlinks found:** 129  
**Missing symlink targets:** 50  
**Ambiguous/circular references:** 72  

---

## Symlink Target Examples

### FTI Archive (fti.tar.gz)
```
Source: fti/S250207bg_no_cal/fti_dchi0.h5
Target: /home/tgr.o4/GW240925_GW250207/FTI/asimov/results/S250207bg_no_cal/fti_dchi0/posterior_samples.h5
```

### Combined Samples (combined_samples.tar.gz)
```
Source: combined_samples/S240925n/combinedPHM_envcalC00_metafile.hdf5
Target: /home/sylvia.biscoveanu/gw240925_and_gw250207/data/combined_samples/S240925n/combinedPHM_envcalC00_metafile.hdf5
```

### Tiger Archive (tiger.tar.gz) - Circular Links
```
Source: tiger/GW250207_no_cal/tiger_GW250207_dchi_0.h5
Target: /home/tgr.o4/GW240925_GW250207/TIGER/GW250207_no_cal/dchi_0//samples/tiger_GW250207_dchi_0.h5

Note: The basename (tiger_GW250207_dchi_0.h5) exists in the archive,
but both _cal and _no_cal versions point to targets that resolve to
each other, creating ambiguity.
```

---

## Why WSL Extraction Does Not Fix This

WSL (Windows Subsystem for Linux) can resolve Linux symlinks, BUT:

1. The targets (`/home/tgr.o4/...`, `/home/sylvia.biscoveanu/...`) do **not exist** in a default WSL installation
2. The targets are **not included** in the Zenodo release archive
3. Re-extracting under WSL will produce the same broken links because the target files are simply not present

This is fundamentally a **missing data issue**, not an extraction environment issue.

---

## Products: Usable vs Blocked

### Usable Products (Regular HDF5 Files)

These products contain actual HDF5 data files and can be accessed:

- **pca.tar.gz**: 8 regular HDF5s
- **pseobnr.tar.gz**: 6 regular HDF5s  
- **GW240925-C00-Strain.tar**: 6 regular HDF5s (strain data)
- **combined_samples.tar.gz**: 1 regular HDF5 (partial)
- **ringdown.tar.gz**: 1 regular HDF5
- **qnmrf.tar.gz**: 2 regular HDF5s

### Blocked Products (Symlink-Only, Missing Targets)

These products are distributed exclusively as symlinks without their targets:

- **fti.tar.gz**: 50 symlinks → targets missing
- **tiger.tar.gz**: 72 symlinks → targets missing (or circular references)

---

## Scientific Impact

### QNM R_f Test Status
- **Status:** BLOCKED
- **Reason:** Core posterior samples (FTI, TIGER, most of combined_samples) are not accessible
- **R_f computed:** NO
- **SSZ/GR claims made:** NO
- **Circularity status:** UNKNOWN (insufficient data for independence verification)

### What Can Be Done with Available Data
The usable products (pca, pseobnr, ringdown, qnmrf, strain) can be analyzed, but they do not contain the primary posterior samples needed for the pre-registered QNM frequency ratio test.

---

## Evidence Files Generated

The following forensic audit files were generated during Phase 3B and 3C:

1. **`HDF5_SYMLINK_FORENSICS.csv`** (02_INVENTORY/)
   - Classification of all 159 HDF5-like paths
   - Link types, attributes, accessibility status

2. **`ARCHIVE_MEMBER_INDEX.csv`** (02_INVENTORY/)
   - Complete index of all archive members
   - Member types, sizes, symlink targets

3. **`HDF5_SYMLINK_TARGET_RESOLUTION.csv`** (02_INVENTORY/)
   - Resolution status for all 129 symlinks
   - Classification: RESOLVED / MISSING / AMBIGUOUS

4. **`HDF5_SYMLINK_TARGET_RESOLUTION_REPORT.md`** (02_INVENTORY/)
   - Full forensic analysis report

5. **`PHASE_3B_SYMLINK_FORENSICS_LOG.md`** (06_WINDSURF_LOGS/)
   - Execution log for Phase 3B

6. **`PHASE_3C_SYMLINK_TARGET_RESOLUTION_LOG.md`** (06_WINDSURF_LOGS/)
   - Execution log for Phase 3C

---

## Draft Message to LIGO/Zenodo

```
Dear LIGO/Virgo/KAGRA data release team,

Thank you again for providing the Zenodo release for GW240925 and GW250207.

During a clean local extraction and inventory of the release, we found that 
several HDF5 products appear to be distributed as symbolic links pointing to 
absolute Linux paths under /home/....

Examples include targets under paths such as:

  /home/tgr.o4/GW240925_GW250207/...
  /home/sylvia.biscoveanu/...

In our extraction audit, the issue mainly affects the FTI and TIGER products. 
The symlink targets do not appear to be included in the public release archive, 
so these files cannot be opened from a clean extraction environment. 
Re-extraction under WSL/Linux would not resolve absolute /home/... links unless 
those target files are also provided.

Summary of our audit:

  - Total HDF5-like paths found: 159
  - Symlinks found: 129
  - Missing symlink targets: 50
  - Affected products include FTI and TIGER
  - Some products such as ringdown, qnmrf, pca, pseobnr, and 
    GW240925-C00-Strain appear to contain regular files

Could you please check whether the release archive accidentally preserved 
local absolute symlinks instead of including the target HDF5 files themselves?

We can provide our generated audit files if helpful:

  - HDF5_SYMLINK_FORENSICS_REPORT.md
  - HDF5_SYMLINK_TARGET_RESOLUTION_REPORT.md
  - ARCHIVE_MEMBER_INDEX.csv
  - HDF5_SYMLINK_TARGET_RESOLUTION.csv

Best regards,
Lino Casu
```

---

## Final Status Summary

| Item | Status |
|------|--------|
| **Release packaging issue** | SUSPECTED |
| **Local extraction** | Successful for regular files |
| **Symlink resolution** | IMPOSSIBLE (targets not in release) |
| **WSL extraction** | Will not fix absolute /home links |
| **QNM R_f test** | BLOCKED (missing critical data) |
| **SSZ hypothesis test** | NOT RUN |
| **R_f computed** | NO |
| **Circularity assessed** | UNKNOWN (insufficient data) |

---

## Recommended Next Steps

1. **Report issue to LIGO/Zenodo** using the draft message above
2. **Await response** regarding missing target files
3. **Do not attempt workarounds** that modify raw data or symlinks
4. **Preserve all audit files** as evidence of the issue
5. **Once complete data is available**, re-run Phase 3 HDF5 inspection
6. **Only then proceed** with QNM R_f test and SSZ hypothesis evaluation

---

*This document was generated as part of the SSZ LIGO data pipeline forensic audit.*  
*All findings are based on actual filesystem inspection and archive analysis.*
