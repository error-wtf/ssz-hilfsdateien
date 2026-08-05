# LIGO Release Inventory

**Generated:** 2026-05-14T00:52:25.118104

## Executive Summary

- Total files inventoried: 1

### Files by Category

- archive: 1

### Files by Event

- unknown: 1

## Key Files for Calibration Robustness


## Key Files for C00 vs C01 Comparison


## Key Files for GR-Test/Ringdown/QNM


## Unknown or Ambiguous Files


## DO NOT INTERPRET YET

This inventory is **evidence handling only**. No scientific conclusions have been drawn.

**What this inventory does NOT tell us:**
- Whether C00 or C01 calibration is "correct"
- Whether GR deviations exist in the data
- Whether calibration artifacts mimic physics
- Whether ringdown/QNM parameters are robust

**Required before interpretation:**
1. Nested archives (tar.gz) must be extracted and inventoried
2. HDF5 files must be inspected for structure (not just listed)
3. Notebooks must be run to verify reproducibility
4. Calibration envelopes must be loaded and plotted
5. Posterior samples must be loaded and compared

**Phase 2 required:** Nested archive extraction and detailed file inspection.

## Recommended Phase 2

Next phase should:

1. Extract nested tar.gz archives into separate folders:
   - calibration.tar.gz → 01_EXTRACTED/nested/calibration/
   - ringdown.tar.gz → 01_EXTRACTED/nested/ringdown/
   - etc.

2. Load and inspect one HDF5 posterior file to verify structure

3. Run one notebook to verify Python environment works

4. Identify which files are:
   - Raw strain (C00 vs C01 vs envcal)
   - Posterior samples (C00 vs C01)
   - Ringdown posteriors
   - GR-test results

5. Create mapping: File → Comparison type (C00/C01, calibration envelope, GR test)

6. Document data volumes and compute requirements

**Do NOT run:**
- Full parameter estimation
- GR deviation tests
- Calibration robustness analysis
- Plotting of "SSZ vs GR" comparisons

**Do NOT claim:**
- "This proves/disproves SSZ"
- "Calibration explains all deviations"
- "Ringdown shows GR violation"
