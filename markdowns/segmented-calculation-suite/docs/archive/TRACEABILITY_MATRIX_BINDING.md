# TRACEABILITY MATRIX (BINDING)

**Generated:** 2025-01-16  
**Status:** BINDING - No validation without this mapping  
**Source:** ssz-qubits repo (74 tests), ssz-metric-pure (12+ tests)

---

## Method → Test → Export Mapping

| method_id | source_file:line | test_ids | tolerance | export_field |
|-----------|------------------|----------|-----------|--------------|
| schwarzschild_radius | ssz_qubits.py:98-114 | test_earth_schwarzschild_radius, test_sun_schwarzschild_radius | 8.8e-3<r_s<8.9e-3, 2.9e3<r_s<3.0e3 | r_s_m |
| xi_segment_density | ssz_qubits.py:117-178 | test_xi_at_earth_surface, test_xi_decreases_with_radius | 6e-10<xi<8e-10, rtol=1e-10 | Xi |
| xi_gradient | ssz_qubits.py:181-221 | (implicit in xi tests) | - | dXi_dr |
| ssz_time_dilation | ssz_qubits.py:224-246 | test_time_dilation_matches_gr, test_pound_rebka, test_gps | rtol=0.01, rtol=1e-6 | D_ssz |

---

## Test → Source Reference

| test_id | source_file | class:method | lines | assertion |
|---------|-------------|--------------|-------|-----------|
| test_earth_schwarzschild_radius | test_ssz_physics.py | TestSchwarzschildRadius:test_earth_schwarzschild_radius | 49-67 | `assert 8.8e-3 < r_s < 8.9e-3` |
| test_sun_schwarzschild_radius | test_ssz_physics.py | TestSchwarzschildRadius:test_sun_schwarzschild_radius | 69-81 | `assert 2.9e3 < r_s < 3.0e3` |
| test_xi_at_earth_surface | test_ssz_physics.py | TestSegmentDensityWeakField:test_xi_at_earth_surface | 99-116 | `assert 6e-10 < xi < 8e-10` |
| test_xi_decreases_with_radius | test_ssz_physics.py | TestSegmentDensityWeakField:test_xi_decreases_with_radius | 118-140 | `assert np.isclose(ratio, 2.0, rtol=1e-10)` |
| test_time_dilation_matches_gr | test_validation.py | TestGRWeakFieldComparison:test_time_dilation_matches_gr_weak_field | 38-77 | `assert abs(d_ssz - d_gr_exact) < xi**2 * 10` |
| test_gravitational_redshift | test_validation.py | TestGRWeakFieldComparison:test_gravitational_redshift_formula | 79-114 | `assert np.isclose(z_ssz, z_gr, rtol=0.01)` |
| test_pound_rebka | test_validation.py | TestGRWeakFieldComparison:test_pound_rebka_experiment | 116-152 | `assert np.isclose(z_ssz, z_theoretical, rtol=1e-6)` |
| test_gps_timing | test_validation.py | TestGPSValidation:test_gps_satellite_time_dilation | 162-203 | `assert np.isclose(dt_per_day, known_gr_effect, rtol=0.01)` |
| test_gps_position_error | test_validation.py | TestGPSValidation:test_gps_position_error_without_correction | 205-235 | `assert 10 < position_error_per_day_km < 15` |

---

## Tolerance Summary (FROM SOURCE)

| tolerance_type | value | used_by | source_line |
|----------------|-------|---------|-------------|
| rtol=1e-10 | Mathematical identities | r_s, Xi ratio | test_ssz_physics.py:62,135 |
| rtol=0.01 | Physical measurements | redshift, GPS | test_validation.py:109,197 |
| rtol=1e-6 | Precision experiments | Pound-Rebka | test_validation.py:146 |
| range bounds | Hard limits | r_s, Xi, position error | Various |

---

## Coverage Status

| Suite | Total Tests | Mapped | Coverage |
|-------|-------------|--------|----------|
| test_ssz_physics.py | 17 | 4 | 24% |
| test_validation.py | 17 | 5 | 29% |
| test_edge_cases.py | 25 | 0 | 0% |
| **TOTAL** | **59** | **9** | **15%** |

**VERDICT: Current implementation covers only 15% of original tests**

---

## Required Actions for Full Parity

1. **Import ALL 59 tests** from ssz-qubits/tests/
2. **Use EXACT tolerances** from source assertions
3. **Add source references** to every test output
4. **Fix regime inconsistency** (90-110 blend vs hard 100)
5. **Report honest coverage** (not fake 100%)

---

## Regime Specification Traceability

| Spec | Source | Value |
|------|--------|-------|
| Weak threshold | E_transition.md:20 | r/r_s > 110 |
| Strong threshold | E_transition.md:21 | r/r_s < 90 |
| Blend function | E_transition.md:39 | 6t⁵ - 15t⁴ + 10t³ |
| **Implementation** | ssz_qubits.py:166 | r/r_s > 100 (NO BLEND!) |

**INCONSISTENCY:** Documentation says 90-110 with blend, code does hard switch at 100.

---

## Constants Traceability

| Constant | Value | Source |
|----------|-------|--------|
| C | 299792458.0 m/s | ssz_qubits.py:29 |
| G | 6.67430e-11 m³/(kg·s²) | ssz_qubits.py:30 |
| PHI | 1.6180339887498948 | ssz_qubits.py:36 |
| M_EARTH | 5.972e24 kg | ssz_qubits.py:32 |
| R_EARTH | 6.371e6 m | ssz_qubits.py:33 |

---

**This matrix is BINDING. No "100% pass" claims without full coverage.**
