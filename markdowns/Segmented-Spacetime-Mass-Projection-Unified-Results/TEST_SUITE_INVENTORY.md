# SSZ TEST SUITE INVENTORY

**Generated:** Phase 3 of Contract Enforcement  
**Source:** pytest discovery + file scan  
**Repository:** Segmented-Spacetime-Mass-Projection-Unified-Results

---

## 1. PYTEST COLLECTED TESTS (54 Total)

### tests/cosmos/
| Test | Function |
|------|----------|
| test_multi_body_sigma.py | `test_two_body_sigma_superposition` |

### tests/
| Test File | Functions |
|-----------|-----------|
| test_print_all_md.py | `test_print_all_md_basic`, `test_print_all_md_depth_order`, `test_print_all_md_exclude_dirs`, `test_print_all_md_size_limit`, `test_print_all_md_no_files`, `test_print_all_md_custom_includes` |
| test_ring_datasets.py | 10 parameterized tests for G79 and CygnusX datasets |
| test_segwave_cli.py | 16 tests across TestCLIBasic, TestCLIExecution, TestCLIValidation, TestBundledDatasets |
| test_segwave_core.py | 20 tests across TestQFactor, TestVelocityProfile, TestFrequencyTrack, TestResiduals, TestCumulativeGamma |
| test_ssz_real_data_comprehensive.py | Comprehensive SSZ validation tests |

---

## 2. ALL TEST FILES (47 Files)

### Root Level Tests
| File | Description |
|------|-------------|
| test_c1_segments.py | C¹ continuity tests |
| test_c2_curvature_proxy.py | C² curvature proxy tests |
| test_c2_segments_strict.py | Strict C² segments tests |
| test_clone_and_verify.py | Clone/verify pipeline |
| test_energies_minimal.py | Minimal energy validation |
| test_energy_1000.py | 1000-object energy tests |
| test_energy_conditions.py | WEC/DEC/SEC tests |
| test_grid_convergence.py | Numerical grid convergence |
| test_output_script.py | Output script tests |
| test_phi_impact.py | φ-geometry impact tests |
| test_ppn_exact.py | PPN exactness tests |
| test_solutions_100_percent.py | 100% solution tests |
| test_theory_predictions_cross_platform.py | Cross-platform theory tests |
| test_utf8_encoding.py | UTF-8 encoding tests |
| test_vfall_duality.py | v_fall duality invariant tests |

### scripts/tests/
| File | Description |
|------|-------------|
| test_cosmo_fields.py | Cosmological fields tests |
| test_cosmo_multibody.py | Multi-body cosmology tests |
| test_data_fetch.py | Data fetching tests |
| test_data_validation.py | Data validation tests |
| test_gaia_required_columns.py | GAIA column requirements |
| test_hawking_spectrum_continuum.py | Hawking spectrum tests |
| test_horizon_hawking_predictions.py | Horizon/Hawking predictions |
| test_plot_ssz_maps.py | SSZ map plotting tests |
| test_segmenter.py | Segmenter tests |
| test_ssz_invariants.py | SSZ invariant tests |
| test_ssz_kernel.py | SSZ kernel tests |
| test_utf8_encoding.py | UTF-8 tests (duplicate) |

### Named *_test.py Scripts
| File | Description |
|------|-------------|
| calculation_test.py | Calculation tests |
| final_test.py | Final validation script |
| investigate_paired_test.py | Paired test investigation |
| lino_qed_test.py | QED-related tests |
| perfect_paired_test.py | Perfect paired analysis |
| phi_bic_test.py | BIC comparison with φ |
| phi_test.py | φ-correction tests |
| segspace_enhanced_test.py | Enhanced segspace tests |
| segspace_final_test.py | Final segspace tests |
| stratified_paired_test.py | Stratified paired tests |

---

## 3. TEST SUITES FROM full-output.md (25 Suites)

| Suite | Duration | Status |
|-------|----------|--------|
| PPN Exact Tests | 0.3s | PASS |
| Dual Velocity Tests | 0.7s | PASS |
| Energy Conditions Tests | 0.3s | PASS |
| C1 Segments Tests | 0.2s | PASS |
| C2 Segments Strict Tests | 0.3s | PASS |
| C2 Curvature Proxy Tests | 0.2s | PASS |
| SegWave Core Math Tests | 5.9s | PASS |
| Energy Formulas Minimal Test | 0.5s | PASS |
| Perfect Energy Formulas Demo | 1.3s | PASS |
| Multi-Ring Validation Tests | 5.3s | PASS |
| SSZ Kernel Tests | 5.3s | PASS |
| SSZ Invariants Tests | 5.7s | PASS |
| Segmenter Tests | 5.4s | PASS |
| Cosmo Fields Tests | 5.6s | PASS |
| Cosmo Multibody Tests | 6.5s | PASS |
| Data Validation Tests | 5.5s | PASS |
| Cosmos Multi-Body Sigma Tests | 6.7s | PASS |
| SSZ Complete Analysis | 115.8s | PASS |
| Rapidity Equilibrium Analysis | 1.5s | PASS |
| Perfect Paired Test | 2.8s | PASS |
| SSZ Theory Predictions | 2.7s | PASS |
| G79 Analysis | 2.4s | PASS |
| Cygnus X Analysis | 2.5s | PASS |
| Paper Export Tools | 5.5s | PASS |
| Final Validation | 0.1s | PASS |

**Total:** 25/25 PASS (100%)  
**Total Time:** 189.0s

---

## 4. CRITICAL TESTS TO NEVER DELETE

### Physics Invariants
- `test_vfall_duality.py` - Dual velocity v_esc × v_fall = c²
- `test_ppn_exact.py` - PPN β=γ=1
- `test_energy_conditions.py` - WEC/DEC/SEC

### SSZ Core
- `test_ssz_invariants.py` - Segment invariants
- `test_ssz_kernel.py` - Kernel tests
- `test_c1_segments.py` - C¹ continuity
- `test_c2_segments_strict.py` - C² continuity

### Regime Validation
- `test_phi_impact.py` - φ-geometry impact
- `test_ssz_real_data_comprehensive.py` - Real data validation

---

## 5. PYTEST CONFIGURATION

From `pyproject.toml`:
```toml
testpaths = ["tests", "scripts/tests"]
```

---

## 6. HOW TO RUN TESTS

### Full Suite
```bash
cd E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results
python -m pytest
```

### Specific Test File
```bash
python -m pytest tests/test_segwave_core.py -v
```

### Category
```bash
python -m pytest scripts/tests/test_ssz_kernel.py -v
```

### Full Pipeline (as in full-output.md)
```bash
python run_all_tests.py
```

---

## 7. TEST COVERAGE BY PHYSICS DOMAIN

| Domain | Test Files | Count |
|--------|------------|-------|
| PPN/Weak Field | test_ppn_exact.py | 1 |
| Dual Velocity | test_vfall_duality.py | 1 |
| Energy Conditions | test_energy_conditions.py | 1 |
| Metric Continuity | test_c1_segments.py, test_c2_*.py | 3 |
| φ-Geometry | test_phi_impact.py, phi_test.py | 2 |
| SegWave/Ring | test_segwave_*.py, test_ring_*.py | 4 |
| Cosmology | test_cosmo_*.py | 2 |
| Data Validation | test_data_*.py | 2 |
| SSZ Kernel | test_ssz_*.py | 3 |
| Hawking/Horizon | test_horizon_*.py, test_hawking_*.py | 2 |

---

## 8. CONTRACT BINDING

All tests in this inventory are **protected by the Implementation Contract**.

Any changes to physics logic MUST:
1. Not break existing tests
2. Be justified by documentary evidence from full-output.md
3. Maintain all invariants

---

*Test Suite Inventory - Phase 3 Complete*
