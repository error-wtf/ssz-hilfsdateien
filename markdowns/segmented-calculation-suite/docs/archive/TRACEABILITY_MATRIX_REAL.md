# REAL TRACEABILITY MATRIX

**Purpose:** Map EVERY test to EXACT original source with EXACT tolerances  
**Date:** 2025-01-16  
**Status:** BINDING - No test without source mapping

---

## Test → Original Source Mapping

### Physics Tests

| test_id | original_file | class:method | line | tolerance | source_assertion |
|---------|---------------|--------------|------|-----------|------------------|
| test_earth_r_s | ssz-qubits/tests/test_ssz_physics.py | TestSchwarzschildRadius:test_earth_schwarzschild_radius | 49-67 | `8.8e-3 < r_s < 8.9e-3` AND `rtol=1e-10` | `assert 8.8e-3 < r_s < 8.9e-3` |
| test_sun_r_s | ssz-qubits/tests/test_ssz_physics.py | TestSchwarzschildRadius:test_sun_schwarzschild_radius | 69-81 | `2.9e3 < r_s < 3.0e3` | `assert 2.9e3 < r_s < 3.0e3` |
| test_xi_earth_surface | ssz-qubits/tests/test_ssz_physics.py | TestSegmentDensityWeakField:test_xi_at_earth_surface | 99-116 | `6e-10 < xi < 8e-10` | `assert 6e-10 < xi < 8e-10` |
| test_xi_1_over_r | ssz-qubits/tests/test_ssz_physics.py | TestSegmentDensityWeakField:test_xi_decreases_with_radius | 118-140 | `rtol=1e-10` for ratio=2.0 | `assert np.isclose(ratio, 2.0, rtol=1e-10)` |

### Validation Tests

| test_id | original_file | class:method | line | tolerance | source_assertion |
|---------|---------------|--------------|------|-----------|------------------|
| test_ssz_vs_gr_weak | ssz-qubits/tests/test_validation.py | TestGRWeakFieldComparison:test_time_dilation_matches_gr_weak_field | 38-77 | `< xi**2 * 10` | `assert abs(d_ssz - d_gr_exact) < xi**2 * 10` |
| test_grav_redshift | ssz-qubits/tests/test_validation.py | TestGRWeakFieldComparison:test_gravitational_redshift_formula | 79-114 | `rtol=0.01` (1%) | `assert np.isclose(z_ssz, z_gr, rtol=0.01)` |
| test_pound_rebka | ssz-qubits/tests/test_validation.py | TestGRWeakFieldComparison:test_pound_rebka_experiment | 116-152 | `rtol=1e-6` | `assert np.isclose(z_ssz, z_theoretical, rtol=1e-6)` |
| test_gps_timing | ssz-qubits/tests/test_validation.py | TestGPSValidation:test_gps_satellite_time_dilation | 162-203 | `rtol=0.01` (1%) | `assert np.isclose(dt_per_day, known_gr_effect, rtol=0.01)` |
| test_gps_position_error | ssz-qubits/tests/test_validation.py | TestGPSValidation:test_gps_position_error_without_correction | 205-235 | `10 < error_km < 15` | `assert 10 < position_error_per_day_km < 15` |

### Constants (from ssz-qubits/ssz_qubits.py)

| constant | value | source_line | tolerance |
|----------|-------|-------------|-----------|
| PHI | `(1 + np.sqrt(5)) / 2` | line 45 | EXACT (mathematical) |
| C | `299792458.0` | line 42 | EXACT (defined) |
| G | `6.67430e-11` | line 43 | EXACT (CODATA 2018) |

---

## Xi_max Clarification

### ISSUE IDENTIFIED

**Problem:** My implementation uses `xi_max=0.802` as a parameter, but original code does NOT have xi_max as a parameter.

**Original Strong Field Formula (ssz-qubits/ssz_qubits.py line 156-160):**
```python
def xi_segment_density(r, M, regime='auto'):
    ...
    if regime == 'strong':
        return 1.0 - np.exp(-PHI * r_s / r)
```

**At horizon (r = r_s):**
```
Xi(r_s) = 1 - exp(-PHI) = 1 - exp(-1.618...) = 1 - 0.198 = 0.802
```

**This is a COMPUTED VALUE, not a parameter!**

### FIX REQUIRED

Remove `xi_max` as a configurable parameter. It should be computed from the formula.

---

## Tolerance Violations in My Implementation

| my_test | my_tolerance | original_tolerance | violation |
|---------|--------------|-------------------|-----------|
| test_golden_ratio | `1e-15` | EXACT | OK |
| test_schwarzschild_sun | `0.5 m` | `2.9e3 < r_s < 3.0e3` (100m range) | **TOO LOOSE** |
| test_gps_timing | `5 μs` (~11%) | `rtol=0.01` (1%) | **TOO LOOSE** |
| test_pound_rebka | `0.1e-15` (~4%) | `rtol=1e-6` (0.0001%) | **TOO LOOSE** |

---

## FAKE Tests (No Original Source)

These tests in my harness have NO corresponding original test:

| my_test | status | action |
|---------|--------|--------|
| test_ns_psr_j0740 | NO SOURCE | Must find original or remove |
| test_ns_psr_j0348 | NO SOURCE | Must find original or remove |
| test_ns_psr_j0030 | NO SOURCE | Must find original or remove |
| test_power_law_fit | PARTIAL | Unified-Results has this |
| test_dual_velocity_invariance | PARTIAL | Unified-Results has this |

---

## Required Fixes

1. **Remove xi_max parameter** - compute from formula
2. **Tighten GPS tolerance** from 5μs to 1% rtol
3. **Tighten Pound-Rebka tolerance** from 0.1e-15 to rtol=1e-6
4. **Add source traceability** to every test output
5. **Remove or source NS tests** - find original or mark as "extension"

---

## Coverage Comparison

| Suite | Original Tests | My Tests | Coverage |
|-------|----------------|----------|----------|
| ssz-qubits/tests/test_ssz_physics.py | 17 | 5 | 29% |
| ssz-qubits/tests/test_validation.py | 17 | 4 | 24% |
| ssz-qubits/tests/test_edge_cases.py | 25 | 4 | 16% |
| Unified-Results/scripts/tests/ | 31+ | 0 | 0% |
| **TOTAL** | **90+** | **13** | **14%** |

**VERDICT: My "100% pass" is fake - I only implemented 14% of original tests**

---

## Path Forward

1. Import ALL tests from original repos
2. Use EXACT tolerances from original assertions
3. Add traceability header to each test output
4. Remove self-invented tests or mark clearly as "extension"
5. Report honest coverage: "13/90 original tests (14%)"
