# Scripts/Tests Directory - SSZ Suite

**Location:** `scripts/tests/`  
**Last Updated:** 2025-10-18

---

## Overview

This directory contains **12 physics tests** + **several technical tests** for the SSZ Suite.

---

## Physics Tests (Verbose Output)

### test_ssz_kernel.py (4 tests)

**Purpose:** SSZ kernel validation (γ, redshift, rotation, lensing)

**Tests:**
1. `test_gamma_bounds_and_monotonic`
   - γ ∈ [0.02, 1.0]
   - Monotonic decrease with radius
   
2. `test_redshift_mapping`
   - z = (1/γ) - 1
   - Observable redshift from field
   
3. `test_rotation_modifier`
   - v_mod ∝ γ^(-p)
   - Explains flat rotation curves
   
4. `test_lensing_proxy_positive`
   - κ > 0 everywhere
   - Positive mass lenses light

**Run:**
```bash
pytest scripts/tests/test_ssz_kernel.py -s -v
```

---

### test_ssz_invariants.py (6 tests)

**Purpose:** SSZ physical invariants and constraints

**Tests:**
1. `test_segment_growth_is_monotonic`
   - Growth statistics
   - Density increases outward
   
2. `test_natural_boundary_positive`
   - Boundary radius statistics
   - φ-based natural scales
   
3. `test_segment_density_positive`
   - Density statistics
   - Positive density ensures physical segments
   
4. `test_manifest_exists`
   - Manifest file presence check
   
5. `test_spiral_index_bounds`
   - Spiral index validation
   
6. `test_solar_segments_non_empty`
   - Solar segment presence

**Run:**
```bash
pytest scripts/tests/test_ssz_invariants.py -s -v
```

**Updated:** 2025-10-18 (added 3 new tests)

---

### test_segmenter.py (2 tests)

**Purpose:** Spacetime segmentation validation

**Tests:**
1. `test_segments_cover_all_points`
   - Complete spacetime coverage
   - No gaps in segmentation
   - Each point in exactly one segment
   
2. `test_segment_counts_grow`
   - Resolution scaling
   - Segment count grows with ring index
   - Algorithm handles varying densities

**Run:**
```bash
pytest scripts/tests/test_segmenter.py -s -v
```

**Fixed:** 2025-10-18
- Removed invalid `create_segments` import
- Now uses correct `assign_segments_xy` API

---

### test_cosmo_multibody.py (3 tests)

**Purpose:** Multi-body cosmological field validation

**Tests:**
1. `test_sigma_additive_mass`
   - σ field superposition
   - Sun + Jupiter mass validation
   
2. `test_tau_monotonic_with_alpha`
   - Time dilation τ(α) dependence
   - Monotonic behavior verification
   
3. `test_refractive_index_baseline`
   - Causality n ≥ 1
   - Refractive index validation

**Run:**
```bash
pytest scripts/tests/test_cosmo_multibody.py -s -v
```

---

## Technical Tests (Silent)

### test_cosmo_fields.py
**Purpose:** Field presence checks  
**Mode:** Silent

### test_data_fetch.py
**Purpose:** GAIA/SDSS/Planck fetch smoke tests  
**Mode:** Silent

### test_gaia_required_columns.py
**Purpose:** Column validation and harmonization  
**Mode:** Silent

### test_plot_ssz_maps.py
**Purpose:** Plotting function tests  
**Mode:** Silent

---

## Example Output

### Physics Test (Verbose):

```bash
$ pytest scripts/tests/test_ssz_kernel.py::test_gamma_bounds_and_monotonic -s -v

================================================================================
GAMMA SEGMENT FIELD TEST
================================================================================
Sample points: 100
Radial range: [1.0, 1000.0] r_s

γ Statistics:
  Min: 0.020000
  Max: 1.000000
  Range: 0.980000

Monotonicity Check:
  All Δγ ≤ 0: True

Physical Interpretation:
  • γ bounded in [0.02, 1.0] (stable field)
  • Monotonic decrease ensures physical consistency
  • Field strength grows with proximity to source
================================================================================
PASSED
```

### Technical Test (Silent):

```bash
$ pytest scripts/tests/test_cosmo_fields.py -s -v

scripts/tests/test_cosmo_fields.py::test_cosmo_fields_added PASSED
```

---

## Running All Scripts/Tests

### All Physics Tests:
```bash
pytest scripts/tests/test_ssz_kernel.py \
       scripts/tests/test_ssz_invariants.py \
       scripts/tests/test_segmenter.py \
       scripts/tests/test_cosmo_multibody.py \
       -s -v
```

### All Tests (including technical):
```bash
pytest scripts/tests/ -s -v
```

---

## Test Statistics

| File | Physics Tests | Technical Tests |
|------|--------------|-----------------|
| test_ssz_kernel.py | 4 | 0 |
| test_ssz_invariants.py | 6 | 0 |
| test_segmenter.py | 2 | 0 |
| test_cosmo_multibody.py | 3 | 0 |
| test_cosmo_fields.py | 0 | 1 |
| test_data_fetch.py | 0 | 3 |
| test_gaia_required_columns.py | 0 | 3 |
| test_plot_ssz_maps.py | 0 | 2 |
| **TOTAL** | **15** | **9** |

---

## Recent Updates (2025-10-18)

### Added/Fixed:
- ✅ All physics tests now verbose with interpretations
- ✅ Fixed test_segmenter.py import bug
- ✅ Added 3 new tests to test_ssz_invariants.py
- ✅ Technical tests made silent
- ✅ Complete documentation

### Test Format Standard:
All physics tests now follow:
```python
print("\n" + "="*80)
print("TEST TITLE")
print("="*80)
print("Configuration: ...")
print("\nResults: ...")
print("\nPhysical Interpretation:")
print("  • Point 1")
print("  • Point 2")
print("="*80)
```

---

## Integration with Full Suite

These tests are run as part of `run_full_suite.py` in **PHASE 3**:

```bash
python run_full_suite.py
```

**Output:**
```
====================================================================================================
PHASE 3: SCRIPTS/TESTS
====================================================================================================

[RUNNING] SSZ Kernel Tests
  Command: python -m pytest scripts/tests/test_ssz_kernel.py -s -v --tb=short

================================================================================
GAMMA SEGMENT FIELD TEST
================================================================================
...
PASSED

[OK] SSZ Kernel Tests (took 4.9s)
```

---

## Contact

**Authors:** Carmen Wrede, Lino Casu  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4  
**Copyright:** © 2025
