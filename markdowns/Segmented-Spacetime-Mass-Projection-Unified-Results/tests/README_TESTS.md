# SSZ Suite - Test System Documentation

**Last Updated:** 2025-10-20  
**Complete Test System Overhaul + Production Analysis Scripts**

---

## Overview

The SSZ Suite contains **69+ tests total**:
- **35 Physics Tests** - Detailed output with physical interpretations
- **23 Technical Tests** - Silent mode (run in background)
- **11 Multi-Ring Validation Tests** - Real astronomical datasets
- **7 Smoke Tests** - Quick health checks (NEW: includes rapidity validation!)
- **3 Production Analysis Scripts** - NEW: Rapidity-based tools

---

## Test Directory Structure

```
/
├── test_*.py                    # Root-level physics tests (6)
├── tests/
│   ├── test_segwave_core.py    # Physics: 16 tests
│   ├── test_segwave_cli.py     # Technical: 16 tests (silent)
│   ├── test_print_all_md.py    # Technical: 6 tests (silent)
│   ├── test_utf8_encoding.py   # Technical: 1 test (silent)
│   └── cosmos/
│       └── test_multi_body_sigma.py  # Physics: 1 test
├── scripts/tests/
│   ├── test_ssz_kernel.py      # Physics: 4 tests
│   ├── test_ssz_invariants.py  # Physics: 6 tests
│   ├── test_segmenter.py       # Physics: 2 tests
│   ├── test_cosmo_multibody.py # Physics: 3 tests
│   ├── test_cosmo_fields.py    # Technical (silent)
│   ├── test_data_fetch.py      # Technical (silent)
│   ├── test_gaia_required_columns.py  # Technical (silent)
│   └── test_plot_ssz_maps.py   # Technical (silent)
└── reports/                     # Generated test outputs
    ├── RUN_SUMMARY.md
    └── summary-output.md
```

---

## 1. ROOT-LEVEL PHYSICS TESTS (6 tests)

**Location:** `/` (repository root)

### test_ppn_exact.py
**Purpose:** PPN Parameters β, γ exactness test  
**Output:** Detailed with physical interpretation  
**Run:** `python test_ppn_exact.py`

**Example Output:**
```
================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
β = 1.000000000000 (perfect)
γ = 1.000000000000 (perfect)

Physical Interpretation:
  • β=1 → No preferred frame (GR-like)
  • γ=1 → Standard curvature response
  • Both match GR in weak field limit
================================================================================
PASSED
```

### test_vfall_duality.py
**Purpose:** Dual velocity invariant v_esc × v_fall = c²  
**Output:** Detailed table with γ values  
**Run:** `python test_vfall_duality.py`

### test_energy_conditions.py
**Purpose:** Energy conditions WEC/DEC/SEC  
**Output:** Table with ρ, p_r, p_t and condition checks  
**Run:** `python test_energy_conditions.py`

### test_c1_segments.py
**Purpose:** C1 continuity at segment joins  
**Output:** Cubic Hermite blend verification  
**Run:** `python test_c1_segments.py`

### test_c2_segments_strict.py
**Purpose:** C2 strict continuity  
**Output:** Quintic Hermite with analytic derivatives  
**Run:** `python test_c2_segments_strict.py`

### test_c2_curvature_proxy.py
**Purpose:** C2 + curvature proxy smoothness  
**Output:** Curvature proxy ≈ 10⁻¹⁵  
**Run:** `python test_c2_curvature_proxy.py`

---

## 2. TESTS/ DIRECTORY

### tests/test_segwave_core.py (16 PHYSICS TESTS)

**Test Classes:**

#### TestQFactor (3 tests)
- `test_temperature_only_basic` - Basic q_k calculation
- `test_temperature_with_beta` - β parameter effect
- `test_temperature_and_density` - Combined T and n effect

#### TestVelocityProfile (5 tests)
- `test_single_shell` - Initial condition
- `test_two_shells_alpha_one` - Two-shell propagation
- `test_deterministic_chain` - 5-ring chain evolution
- `test_alpha_zero_constant_velocity` - Classical limit α=0
- `test_with_density` - Temperature + density combined

#### TestFrequencyTrack (2 tests)
- `test_single_gamma` - Single γ redshift
- `test_frequency_decreases_with_gamma` - γ sequence evolution

#### TestResiduals (3 tests)
- `test_perfect_match` - MAE/RMSE = 0
- `test_systematic_bias` - Constant bias detection
- `test_mixed_residuals` - Over/under prediction

#### TestCumulativeGamma (3 tests)
- `test_constant_q` - Exponential growth
- `test_all_ones` - Isothermal medium
- `test_increasing_sequence` - Heating trend

**Run:** `pytest tests/test_segwave_core.py -s -v`

---

### tests/test_segwave_cli.py (16 TECHNICAL TESTS - SILENT)

**Purpose:** CLI argument validation and execution  
**Mode:** Silent (only shows PASSED)  
**Run:** `pytest tests/test_segwave_cli.py -s -v`

**Test Classes:**
- TestCLIBasic (3 tests) - Help, args, invalid paths
- TestCLIExecution (4 tests) - Fixed/fit alpha, frequency, exponents
- TestCLIValidation (2 tests) - Negative values, mutex args
- TestBundledDatasets (7 tests) - Dataset existence, loading

---

### tests/test_print_all_md.py (6 TECHNICAL TESTS - SILENT)

**Purpose:** Markdown printing functionality  
**Mode:** Silent  
**Run:** `pytest tests/test_print_all_md.py -s -v`

---

### tests/cosmos/test_multi_body_sigma.py (1 PHYSICS TEST)

**Purpose:** Two-body σ field superposition  
**Output:** Detailed with field linearity check  
**Run:** `pytest tests/cosmos/test_multi_body_sigma.py -s -v`

---

## 3. SCRIPTS/TESTS/ DIRECTORY

### scripts/tests/test_ssz_kernel.py (4 PHYSICS TESTS)

**Tests:**
- `test_gamma_bounds_and_monotonic` - γ ∈ [0.02, 1.0], monotonic
- `test_redshift_mapping` - z = (1/γ) - 1
- `test_rotation_modifier` - v_mod ∝ γ^(-p)
- `test_lensing_proxy_positive` - κ > 0 everywhere

**Run:** `pytest scripts/tests/test_ssz_kernel.py -s -v`

---

### scripts/tests/test_ssz_invariants.py (6 PHYSICS TESTS)

**Tests:**
- `test_segment_growth_is_monotonic` - Growth statistics
- `test_natural_boundary_positive` - φ-based scales
- `test_segment_density_positive` - Positive density
- `test_manifest_exists` - Manifest file check
- `test_spiral_index_bounds` - Spiral index validation
- `test_solar_segments_non_empty` - Solar segment presence

**Run:** `pytest scripts/tests/test_ssz_invariants.py -s -v`

**Updated:** 2025-10-18 (added 3 new tests)

---

### scripts/tests/test_segmenter.py (2 PHYSICS TESTS)

**Tests:**
- `test_segments_cover_all_points` - Complete spacetime coverage
- `test_segment_counts_grow` - Resolution scaling

**Run:** `pytest scripts/tests/test_segmenter.py -s -v`

**Fixed:** 2025-10-18 (removed invalid `create_segments` import)

---

### scripts/tests/test_cosmo_multibody.py (3 PHYSICS TESTS)

**Tests:**
- `test_sigma_additive_mass` - Multi-body σ superposition
- `test_tau_monotonic_with_alpha` - Time dilation τ(α)
- `test_refractive_index_baseline` - Causality n ≥ 1

**Run:** `pytest scripts/tests/test_cosmo_multibody.py -s -v`

---

### scripts/tests/ TECHNICAL TESTS (SILENT)

**Files:**
- `test_cosmo_fields.py` - Field presence checks
- `test_data_fetch.py` - GAIA/SDSS/Planck fetch tests
- `test_gaia_required_columns.py` - Column validation
- `test_plot_ssz_maps.py` - Plotting functions
- `test_utf8_encoding.py` - UTF-8 handling

---

## Running Tests

### Individual Test Files:

```bash
# Root-level physics tests:
python test_ppn_exact.py
python test_vfall_duality.py
python test_energy_conditions.py

# Pytest physics tests:
pytest tests/test_segwave_core.py -s -v
pytest scripts/tests/test_ssz_kernel.py -s -v
```

### All Tests (Complete Suite):

```bash
python run_full_suite.py
```

**Generates:**
- `reports/RUN_SUMMARY.md` - Compact overview
- `reports/summary-output.md` - Complete detailed log (~100-500 KB)

### Pytest Only:

```bash
# All pytest tests:
pytest tests/ scripts/tests/ -s -v --tb=short

# Physics tests only:
pytest tests/test_segwave_core.py scripts/tests/test_ssz_kernel.py -s -v
```

---

## Test Output Format

### Physics Tests (Verbose):

```
================================================================================
TEST TITLE: Physical Phenomenon
================================================================================
Configuration:
  Parameter = Value
  ...

Results/Calculation:
  Value = Number
  ...

Physical Interpretation:
  • Point 1: Explanation
  • Point 2: Explanation
  • Point 3: Explanation

================================================================================
PASSED
================================================================================
```

### Technical Tests (Silent):

```
tests/test_segwave_cli.py::test_help_flag PASSED
tests/test_segwave_cli.py::test_invalid_csv_path PASSED
```

---

## Critical Pytest Flag

**ALWAYS use `-s` flag!**

```bash
# ✅ CORRECT:
pytest tests/ -s -v --tb=short

# ❌ WRONG (causes crash):
pytest tests/ -v --tb=short --disable-warnings
```

**Reason:** `--disable-warnings` causes `ValueError: I/O operation on closed file`

---

## Test Summary

### By Type:

| Type | Count | Mode |
|------|-------|------|
| Physics Tests | 35 | Verbose |
| Technical Tests | 23 | Silent |
| **TOTAL** | **58** | Mixed |

### By Location:

| Location | Physics | Technical | Total |
|----------|---------|-----------|-------|
| Root-level | 6 | 0 | 6 |
| tests/ | 17 | 23 | 40 |
| scripts/tests/ | 12 | 0 | 12 |
| **TOTAL** | **35** | **23** | **58** |

---

## Recent Updates (2025-10-18)

### 1. All Physics Tests Now Verbose
- Added detailed output to all 35 physics tests
- Standardized format with physical interpretations

### 2. Technical Tests Made Silent
- UTF-8, CLI, MD Print tests now run in background
- Only show PASSED (no verbose output)

### 3. Pytest Fix Applied
- Changed from `--disable-warnings` to `-s` flag
- Prevents I/O operation crash

### 4. Bug Fixes
- Fixed `test_segmenter.py` import error
- Fixed summary "Failed: 3" bug
- Added cache clearing instructions

### 5. New Documentation
- Complete test listings
- Verification status
- Logging system docs

---

## Papers & Data

### Papers (both formats included):
```
papers/
├── *.md   # Markdown versions (GitHub viewing)
└── *.pdf  # PDF versions (offline reading, printing)
```

### Data Files:
```
data/
├── real_data_full.csv          # ~50 MB (in release)
├── gaia/
│   ├── gaia_sample_small.csv   # ~1 MB (in release)
│   ├── gaia_cone_g79.csv       # ~500 KB (in release)
│   └── gaia_cone_cygx.csv      # ~500 KB (in release)
└── planck/
    └── COM_PowerSpect_CMB-TT-full_R3.01.txt  # ~2 GB (auto-fetched)
```

---

## Troubleshooting

### Problem: Pytest crashes with I/O error
**Solution:** Use `-s` flag instead of `--disable-warnings`

### Problem: Tests show only "PASSED" (no details)
**Solution:** Clear Python cache:
```bash
python -c "import pathlib, shutil; [shutil.rmtree(p, ignore_errors=True) for p in pathlib.Path('.').rglob('__pycache__')]"
```

### Problem: Import errors
**Solution:** Ensure virtual environment is activated:
```bash
# Windows:
.\.venv\Scripts\Activate.ps1

# Linux:
source .venv/bin/activate
```

---

## Production-Ready Analysis Scripts (NEW - Oct 2025)

**Beyond testing - production tools for analysis:**

### 1. Rapidity-Based Equilibrium Analysis
**Script:** [`perfect_equilibrium_analysis.py`](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/perfect_equilibrium_analysis.py) (428 lines)  
**Purpose:** Eliminates 0/0 singularities at equilibrium points

```bash
python perfect_equilibrium_analysis.py
```

**Features:**
- Rapidity formulation: χ = arctanh(v/c)
- Angular bisector for natural origin
- Expected improvement: 0% → 35-50% at r < 2 r_s
- Complete validation tests included

**Documentation:** [RAPIDITY_IMPLEMENTATION.md](../RAPIDITY_IMPLEMENTATION.md)

### 2. Standalone Interactive Analysis
**Script:** [`perfect_seg_analysis.py`](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/perfect_seg_analysis.py) (480 lines)  
**Purpose:** User-friendly tool for custom datasets

```bash
# Interactive mode
python perfect_seg_analysis.py --interactive

# CSV batch
python perfect_seg_analysis.py --csv data.csv --output results.csv
```

**Features:**
- 3 usage modes (Interactive/Single/CSV)
- Flexible column detection
- Regime classification
- Rapidity-based (NO 0/0!)

**Documentation:** [PERFECT_SEG_ANALYSIS_GUIDE.md](../PERFECT_SEG_ANALYSIS_GUIDE.md)

### 3. Perfect Paired Test Framework
**Script:** [`perfect_paired_test.py`](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/perfect_paired_test.py) (470 lines)  
**Purpose:** Complete paired test with ALL findings

```bash
python perfect_paired_test.py --csv data/real_data_full.csv --output results.csv
```

**Features:**
- φ-geometry fundamental (not fitting!)
- Rapidity formulation (NO 0/0!)
- Regime stratification
- Complete statistics

**Documentation:** [PERFECT_PAIRED_TEST_GUIDE.md](../PERFECT_PAIRED_TEST_GUIDE.md)

### 4. Smoke Tests (Quick Health Checks)
**Script:** `smoke_test_all.py`  
**Purpose:** Fast validation of critical components

```bash
python smoke_test_all.py
```

**Tests (7 total):**
1. Critical imports
2. φ calculation
3. Data files
4. Output directories
5. Matplotlib
6. Precision
7. **Rapidity equilibrium (NEW!)**

**Runtime:** ~5 seconds  
**Test 7:** Validates rapidity functions, v=0 handling, bisector

---

## Contact & License

**Authors:** Carmen Wrede, Lino Casu  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4  
**Copyright:** © 2025

---

**All 69+ tests verified and documented!** ✅  
**3 production analysis scripts ready for deployment!** 🚀
