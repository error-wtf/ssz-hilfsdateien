# HDF5 Symlink Target Resolution Report

**Generated:** 2026-05-14T13:30:21.026602
**Task ID:** LIGO_PHASE_3C_SYMLINK_TARGET_RESOLUTION_AUDIT

## Executive Summary

### Critical Finding: Zenodo Release Contains Broken Symlinks

The LIGO GW240925/GW250207 Zenodo release contains **129 HDF5 symlinks** that reference
absolute Linux paths (e.g., `/home/tgr.o4/...`, `/home/sylvia.biscoveanu/...`).

**Key Issue:** These symlinks were created for the authors' local workflow but were
archived without their targets. WSL extraction will NOT fix this because the
targets are external to the release package.

### Target Resolution Results

| Category | Count |
|----------|-------|
| RESOLVED_BASENAME_AMBIGUOUS | 72 |
| TARGET_NOT_IN_RELEASE | 50 |
| RESOLVED_BASENAME_UNIQUE | 7 |
| **Total** | **129** |

### Regular HDF5 Files Status

- Regular HDF5 files found: 30
- Accessible via h5py: **0**
- Inaccessible: 30

**WARNING:** All 'regular' files from Windows extraction are inaccessible.
This suggests the PowerShell classification misidentified reparse points.

## Dataset Completeness by Product

| Product | Regular HDF5s | Symlinks | Resolved Targets | Missing Targets | Status |
|---------|---------------|----------|------------------|-----------------|--------|
| tiger | 0 | 72 | 0 | 0 | UNCERTAIN |
| fti | 0 | 50 | 0 | 50 | BLOCKED (missing targets) |
| combined_samples | 1 | 7 | 7 | 0 | USABLE (regular files) |
| pca | 8 | 0 | 0 | 0 | USABLE (regular files) |
| pseobnr | 6 | 0 | 0 | 0 | USABLE (regular files) |
| GW240925-C00-Strain | 6 | 0 | 0 | 0 | USABLE (regular files) |
| qnmrf | 2 | 0 | 0 | 0 | USABLE (regular files) |
| ringdown | 1 | 0 | 0 | 0 | USABLE (regular files) |

## Root Cause Analysis

### The Symlink Problem

1. **Archive Creation:** Authors created symlinks pointing to local paths:
   - `/home/tgr.o4/GW240925_GW250207/TIGER/...`
   - `/home/sylvia.biscoveanu/gw240925_and_gw250207/...`

2. **Archive Contents:** Only the symlinks were archived, NOT their targets

3. **Windows Extraction:** Windows created reparse points for symlinks,
   but cannot resolve Linux absolute paths

4. **Tiger Cross-Links:** The tiger.tar.gz archive contains circular/ambiguous
   references between `_cal` and `_no_cal` versions of the same files

### Why WSL Won't Help

WSL can resolve Linux symlinks, BUT:
- The targets (`/home/tgr.o4/...`) don't exist in WSL by default
- The targets are NOT included in the Zenodo release
- Re-extracting under WSL will produce the same broken links

## Usable vs Blocked Products

### Currently Usable (Have Regular HDF5s)

- combined_samples (1 regular HDF5s)
- ringdown (1 regular HDF5s)
- qnmrf (2 regular HDF5s)
- pca (8 regular HDF5s)
- pseobnr (6 regular HDF5s)
- GW240925-C00-Strain (6 regular HDF5s)

### Blocked (Symlink-Only with Missing Targets)

- fti (50 symlinks, 50 missing targets)
- tiger (72 symlinks, target status unclear)

## Recommendations

### Immediate Actions

1. **Contact LIGO/Zenodo:** Report that the release contains broken absolute symlinks
2. **Request Complete Archive:** Ask for either:
   - Archives without symlinks (with actual data files)
   - Separate download links for the symlink target files
   - Documentation on how to obtain the missing data

### Workaround Options

1. **Use Available Data Only:**
   - pca.tar.gz (8 regular HDF5s)
   - pseobnr.tar.gz (6 regular HDF5s)
   - GW240925-C00-Strain.tar (6 regular HDF5s)
   - ringdown.tar.gz (1 regular HDF5)
   - qnmrf.tar.gz (2 regular HDF5s)

2. **Check if symlink targets exist elsewhere:**
   - Some targets may be downloadable from LIGO DCC
   - Check if posterior samples are available via GraceDB

### Do NOT

- Delete the broken symlinks (document the issue first)
- Assume WSL extraction will fix this
- Attempt to compute R_f with incomplete data
- Make SSZ/GR claims based on partial data

## Phase 3 Status

| Phase | Status |
|-------|--------|
| 3A: HDF5 Discovery | COMPLETE |
| 3B: Symlink Forensics | COMPLETE |
| 3C: Target Resolution | COMPLETE |
| 3D: QNM R_f Test | **BLOCKED** - Missing critical data |

## Conclusion

The Zenodo release for GW240925/GW250207 is **incomplete** for standalone analysis.
The core posterior samples (combined_samples, fti, tiger) are distributed as
broken symlinks without their targets. This is an archive packaging issue, not
a scientific or technical problem with the data itself.

**Next Step:** Contact LIGO/Zenodo for complete data or clarification.
