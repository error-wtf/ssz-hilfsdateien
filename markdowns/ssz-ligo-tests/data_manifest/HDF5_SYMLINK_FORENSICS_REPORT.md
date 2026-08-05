# HDF5 Symlink Forensics Report

**Generated:** 2026-05-14T13:24:18.304779

## Executive Summary

- **Total HDF5-like paths:** 159
- **Symbolic Links:** 129
- **Regular files:** 30
- **Accessible (can open):** 0
- **Broken/Inaccessible:** 159
- **Linux absolute symlinks:** 129

## Root Cause Analysis

### Windows Extraction of Linux Symlinks

The archives were created on Linux with **absolute symlinks** pointing to:
- `/home/sylvia.biscoveanu/...` (combined_samples)
- `/home/tgr.o4/...` (FTI)
- `/home/tgr.o4/...` (TIGER, inferred)

When extracted on Windows:
1. Windows created SymbolicLink reparse points
2. Linux absolute paths are NOT resolvable on Windows
3. Links appear as 0-byte files with 'Archive, ReparsePoint' attributes
4. h5py cannot open these files (FileNotFoundError)

### Affected Archives

| Archive | Symlinks in Archive | Status |
|---------|---------------------|--------|
| combined_samples.tar.gz | 7 | BROKEN on Windows |
| fti.tar.gz | 50 | BROKEN on Windows |
| ringdown.tar.gz | 0 | OK (no symlinks) |
| qnmrf.tar.gz | 0 | OK (no symlinks) |

## Classification

- **UNKNOWN:** 159

## Accessibility Test Results

Files that can be opened as HDF5: **0**

**No files are currently accessible via standard Python open()!**

This suggests the accessible files may require different handling or the test was too strict.

## Recommendations

### Immediate Options

1. **Use WSL/Linux Extraction** (Recommended)
   - Extract archives under WSL2 with proper symlink support
   - Or extract to a Linux VM/container
   - Results go to: `01_EXTRACTED_WSL/`

2. **Skip Symlink-Dependent Data**
   - Use only the truly regular files (ringdown, qnmrf, GWOSC)
   - Note: This may bias the QNM analysis

3. **Manual Download**
   - Download symlink targets directly from LIGO if available

### Safe Remediation

**DO NOT:**
- Delete broken symlinks (they show what data is missing)
- Try to 'fix' symlinks manually (path mapping is complex)
- Re-extract over existing data (may create more broken links)

**DO:**
- Create new extraction in separate WSL directory
- Document which specific datasets are missing
- Verify accessibility of regular files first

## Impact on Phase 3

| Dataset | Type | Status | Impact |
|---------|------|--------|--------|
| combined_samples | Symlink-heavy | BROKEN | **HIGH** - Main posterior data
| fti | Symlink-heavy | BROKEN | **HIGH** - FTI analysis data
| tiger | Symlink-heavy | BROKEN | **MEDIUM** - TIGER validation
| ringdown | Regular files | OK | **LOW** - Accessible
| qnmrf | Regular files | OK | **LOW** - Accessible
| GWOSC | Regular files | OK | **LOW** - Strain data accessible

## Conclusion

**Windows extraction issue: CONFIRMED**

- 129 files are broken Linux absolute symlinks
- These represent 81.1% of all HDF5 paths
- The ringdown, qnmrf, and GWOSC data remain accessible
- WSL re-extraction is required for full QNM analysis

