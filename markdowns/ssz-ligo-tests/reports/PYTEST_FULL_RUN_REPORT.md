# PYTEST FULL RUN REPORT

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18 14:51:02.185132

## Command
```
pytest -ra -v --tb=short tests
```

## Exit Code
1

## Counts
- Passed:  123
- Failed:  52
- Errors:  0
- Skipped: 0
- XFailed: 1

## Status
FAIL_EXIT_1

## Full Output
```
============================= test session starts =============================
platform win32 -- Python 3.12.10, pytest-8.4.2, pluggy-1.6.0 -- C:\Users\linoc\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\python.exe
cachedir: .pytest_cache
rootdir: E:\clone\ssz-ligo-tests
configfile: pyproject.toml
plugins: anyio-4.12.1, dash-2.18.2, Faker-40.4.0, cov-4.1.0, timeout-2.4.0, zarr-3.1.6
collecting ... collected 176 items

tests/integration/test_forward_model.py::TestForwardModelInitialization::test_initially_unlocked FAILED [  0%]
tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_epsilon_220 FAILED [  1%]
tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_eta_220 FAILED [  1%]
tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_kappa_phase FAILED [  2%]
tests/integration/test_forward_model.py::TestRingdownShift::test_unshifted_when_epsilon_zero FAILED [  2%]
tests/integration/test_forward_model.py::TestRingdownShift::test_shifted_when_epsilon_nonzero FAILED [  3%]
tests/integration/test_forward_model.py::TestRingdownShift::test_raises_when_epsilon_not_locked FAILED [  3%]
tests/integration/test_forward_model.py::TestRingdownShift::test_tau_shift_raises_when_eta_not_locked FAILED [  4%]
tests/integration/test_forward_model.py::TestPhaseDeformation::test_raises_when_kappa_not_locked FAILED [  5%]
tests/integration/test_forward_model.py::TestPhaseDeformation::test_zero_at_high_frequencies FAILED [  5%]
tests/integration/test_forward_model.py::TestAmplitudeDeformation::test_raises_when_kappa_not_locked FAILED [  6%]
tests/integration/test_forward_model.py::TestDetectorResponse::test_antenna_response FAILED [  6%]
tests/integration/test_forward_model.py::TestDetectorResponse::test_residual FAILED [  7%]
tests/integration/test_forward_model.py::TestLikelihood::test_likelihood_decreases_with_mismatch FAILED [  7%]
tests/integration/test_forward_model.py::TestLikelihood::test_inner_product_symmetry FAILED [  8%]
tests/integration/test_forward_model.py::TestAntiCircularity::test_model_rejects_unlocked_parameters FAILED [  9%]
tests/integration/test_inspiral_phase_forward_model.py::TestGWPower::test_ssz_less_than_gr PASSED [  9%]
tests/integration/test_inspiral_phase_forward_model.py::TestGWPower::test_correction_factor_reasonable PASSED [ 10%]
tests/integration/test_inspiral_phase_forward_model.py::TestRdot::test_rdot_negative PASSED [ 10%]
tests/integration/test_inspiral_phase_forward_model.py::TestRdot::test_ssz_slower_than_gr PASSED [ 11%]
tests/integration/test_inspiral_phase_forward_model.py::TestOrbitalFrequency::test_decreases_with_radius PASSED [ 11%]
tests/integration/test_inspiral_phase_forward_model.py::TestOrbitalFrequency::test_proportional_to_sqrt_mass PASSED [ 12%]
tests/integration/test_inspiral_phase_forward_model.py::TestDphiDr::test_finite_everywhere PASSED [ 13%]
tests/integration/test_inspiral_phase_forward_model.py::TestDphiDr::test_ssz_vs_gr_different PASSED [ 13%]
tests/integration/test_inspiral_phase_forward_model.py::TestAccumulatedPhase::test_negative_inspiral FAILED [ 14%]
tests/integration/test_inspiral_phase_forward_model.py::TestAccumulatedPhase::test_many_radians PASSED [ 14%]
tests/integration/test_inspiral_phase_forward_model.py::TestDeltaPhase::test_ssz_gr_phase_difference_finite PASSED [ 15%]
tests/integration/test_inspiral_phase_forward_model.py::TestDeltaPhase::test_small_mass_gives_small_phase_diff PASSED [ 15%]
tests/integration/test_inspiral_phase_forward_model.py::TestISCO::test_isco_at_6m PASSED [ 16%]
tests/integration/test_strong_to_weak_transition.py::TestStrongToWeakTransition::test_xi_smooth_across_transition PASSED [ 17%]
tests/integration/test_strong_to_weak_transition.py::TestStrongToWeakTransition::test_blend_weight_transitions PASSED [ 17%]
tests/integration/test_strong_to_weak_transition.py::TestStrongToWeakTransition::test_pure_strong_at_horizon PASSED [ 18%]
tests/integration/test_strong_to_weak_transition.py::TestStrongToWeakTransition::test_pure_weak_far_out PASSED [ 18%]
tests/integration/test_strong_to_weak_transition.py::TestPhaseAccountingTransition::test_factor_continuous PASSED [ 19%]
tests/integration/test_strong_to_weak_transition.py::TestRSGCoordinate::test_rsg_increases_monotonically PASSED [ 19%]
tests/integration/test_strong_to_weak_transition.py::TestPhysicalRegimes::test_strong_field_dominates_near_horizon PASSED [ 20%]
tests/integration/test_strong_to_weak_transition.py::TestPhysicalRegimes::test_weak_field_far_out PASSED [ 21%]
tests/test_00_environment.py::test_import_ssz_ligo FAILED                [ 21%]
tests/test_00_environment.py::test_constants_available PASSED            [ 22%]
tests/test_00_environment.py::test_core_functions_available PASSED       [ 22%]
tests/test_00_environment.py::test_equation_registry_available PASSED    [ 23%]
tests/test_01_source_inventory.py::test_source_root_exists[book-full-06-papers-E:\\clone\\book-full\\06_PAPERS] PASSED [ 23%]
tests/test_01_source_inventory.py::test_source_root_exists[book-full-v7-E:\\clone\\book-full\\05_OUTPUT\\V7_BUILD\\06_final_v7] PASSED [ 24%]
tests/test_01_source_inventory.py::test_source_root_exists[ssz-qubit-papers-E:\\clone\\SSZ_QUBIT_PAPERS] PASSED [ 25%]
tests/test_01_source_inventory.py::test_source_root_exists[ssz-complete-doc-E:\\clone\\ssz-complete-documentation] PASSED [ 25%]
tests/test_01_source_inventory.py::test_source_root_exists[ssz-all-tests-E:\\clone\\ssz-all-tests] PASSED [ 26%]
tests/test_01_source_inventory.py::test_source_root_exists[segmented-mass-projection-E:\\clone\\Segmented-Spacetime-Mass-Projection-Unified-Results] PASSED [ 26%]
tests/test_01_source_inventory.py::test_source_root_exists[ssz-metric-pure-E:\\clone\\ssz-metric-pure] PASSED [ 27%]
tests/test_01_source_inventory.py::test_source_root_exists[segmented-calc-suite-E:\\clone\\segmented-calculation-suite] PASSED [ 27%]
tests/test_01_source_inventory.py::test_source_root_has_content[book-full-06-papers-E:\\clone\\book-full\\06_PAPERS] PASSED [ 28%]
tests/test_01_source_inventory.py::test_source_root_has_content[book-full-v7-E:\\clone\\book-full\\05_OUTPUT\\V7_BUILD\\06_final_v7] PASSED [ 28%]
tests/test_01_source_inventory.py::test_source_root_has_content[ssz-qubit-papers-E:\\clone\\SSZ_QUBIT_PAPERS] PASSED [ 29%]
tests/test_01_source_inventory.py::test_source_root_has_content[ssz-complete-doc-E:\\clone\\ssz-complete-documentation] PASSED [ 30%]
tests/test_01_source_inventory.py::test_source_root_has_content[ssz-all-tests-E:\\clone\\ssz-all-tests] PASSED [ 30%]
tests/test_01_source_inventory.py::test_source_root_has_content[segmented-mass-projection-E:\\clone\\Segmented-Spacetime-Mass-Projection-Unified-Results] PASSED [ 31%]
tests/test_01_source_inventory.py::test_source_root_has_content[ssz-metric-pure-E:\\clone\\ssz-metric-pure] PASSED [ 31%]
tests/test_01_source_inventory.py::test_source_root_has_content[segmented-calc-suite-E:\\clone\\segmented-calculation-suite] PASSED [ 32%]
tests/test_01_source_inventory.py::test_critical_ssz_book_exists PASSED  [ 32%]
tests/test_01_source_inventory.py::test_critical_pdf_exists PASSED       [ 33%]
tests/test_01_source_inventory.py::test_ssz_metric_pure_is_canonical PASSED [ 34%]
tests/test_02_equation_registry.py::TestLockedCoreEquations::test_phi_matches_book PASSED [ 34%]
tests/test_02_equation_registry.py::TestLockedCoreEquations::test_xi_max_matches_book PASSED [ 35%]
tests/test_02_equation_registry.py::TestLockedCoreEquations::test_d_min_matches_book PASSED [ 35%]
tests/test_02_equation_registry.py::TestLockedCoreEquations::test_all_core_equations_locked PASSED [ 36%]
tests/test_02_equation_registry.py::TestMissingForwardEquations::test_epsilon_220_ambiguous PASSED [ 36%]
tests/test_02_equation_registry.py::TestMissingForwardEquations::test_delta_psi_missing PASSED [ 37%]
tests/test_02_equation_registry.py::TestMissingForwardEquations::test_delta_amp_missing PASSED [ 38%]
tests/test_02_equation_registry.py::TestMissingForwardEquations::test_eta_220_missing PASSED [ 38%]
tests/test_02_equation_registry.py::TestMissingForwardEquations::test_h_ssz_waveform_missing PASSED [ 39%]
tests/test_02_equation_registry.py::TestReadinessCheck::test_not_ready_for_numerical_test PASSED [ 39%]
tests/test_02_equation_registry.py::TestReadinessCheck::test_readiness_reason_lists_missing PASSED [ 40%]
tests/test_03_ssz_core.py::TestSchwarzschildRadius::test_sun_schwarzschild_radius PASSED [ 40%]
tests/test_03_ssz_core.py::TestSchwarzschildRadius::test_30_solar_masses PASSED [ 41%]
tests/test_03_ssz_core.py::TestXiWeak::test_at_10_rs PASSED              [ 42%]
tests/test_03_ssz_core.py::TestXiWeak::test_at_100_rs PASSED             [ 42%]
tests/test_03_ssz_core.py::TestXiWeak::test_asymptotic_to_zero PASSED    [ 43%]
tests/test_03_ssz_core.py::TestXiStrong::test_at_horizon PASSED          [ 43%]
tests/test_03_ssz_core.py::TestXiStrong::test_finite_at_horizon PASSED   [ 44%]
tests/test_03_ssz_core.py::TestXiStrong::test_saturates_at_xi_max PASSED [ 44%]
tests/test_03_ssz_core.py::TestDSSZ::test_at_horizon PASSED              [ 45%]
tests/test_03_ssz_core.py::TestDSSZ::test_finite_at_horizon PASSED       [ 46%]
tests/test_03_ssz_core.py::TestDSSZ::test_approaches_1_at_infinity PASSED [ 46%]
tests/test_03_ssz_core.py::TestDGR::test_zero_at_horizon PASSED          [ 47%]
tests/test_03_ssz_core.py::TestDGR::test_ssz_vs_gr_difference PASSED     [ 47%]
tests/test_03_ssz_core.py::TestRegimeDetection::test_weak_regime PASSED  [ 48%]
tests/test_03_ssz_core.py::TestRegimeDetection::test_strong_regime PASSED [ 48%]
tests/test_03_ssz_core.py::TestRegimeDetection::test_blend_regime PASSED [ 49%]
tests/test_03_ssz_core.py::TestGetXi::test_uses_weak_far_out PASSED      [ 50%]
tests/test_03_ssz_core.py::TestGetXi::test_uses_strong_near_horizon FAILED [ 50%]
tests/test_04_forward_model_placeholders.py::TestPhaseDeformationBlocked::test_delta_psi_raises_not_implemented PASSED [ 51%]
tests/test_04_forward_model_placeholders.py::TestAmplitudeDeformationBlocked::test_delta_amp_raises_not_implemented PASSED [ 51%]
tests/test_04_forward_model_placeholders.py::TestRingdownFrequencyShiftBlocked::test_raises_when_epsilon_none FAILED [ 52%]
tests/test_04_forward_model_placeholders.py::TestRingdownFrequencyShiftBlocked::test_ambiguity_mentioned PASSED [ 52%]
tests/test_04_forward_model_placeholders.py::TestRingdownFrequencyShiftBlocked::test_works_when_epsilon_locked FAILED [ 53%]
tests/test_04_forward_model_placeholders.py::TestRingdownTauShiftBlocked::test_raises_when_eta_none FAILED [ 53%]
tests/test_04_forward_model_placeholders.py::TestRingdownTauShiftBlocked::test_works_when_eta_locked FAILED [ 54%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_posterior_fields_flagged_invalid[H1_only/f] PASSED [ 55%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_posterior_fields_flagged_invalid[H1_only/m] PASSED [ 55%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_posterior_fields_flagged_invalid[H1_only/chi] PASSED [ 56%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_posterior_fields_flagged_invalid[H1_only/m1] PASSED [ 56%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_posterior_fields_flagged_invalid[H1_only/m2] PASSED [ 57%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_f_from_posterior_invalid PASSED [ 57%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_m_from_posterior_invalid PASSED [ 58%]
tests/test_08_anti_circularity.py::TestPosteriorFieldsForbidden::test_chi_from_posterior_invalid PASSED [ 59%]
tests/test_08_anti_circularity.py::TestStrainAllowed::test_strain_fields_valid[H1/strain_data] PASSED [ 59%]
tests/test_08_anti_circularity.py::TestStrainAllowed::test_strain_fields_valid[H1/residual] PASSED [ 60%]
tests/test_08_anti_circularity.py::TestStrainAllowed::test_strain_fields_valid[H1/power_spectrum] FAILED [ 60%]
tests/test_08_anti_circularity.py::TestKerrNotSSZReference::test_same_source_circular PASSED [ 61%]
tests/test_08_anti_circularity.py::TestKerrNotSSZReference::test_strain_independent PASSED [ 61%]
tests/test_08_anti_circularity.py::TestSelfConsistencyRisk::test_r_f_circular PASSED [ 62%]
tests/unit/test_radial_scaling_core.py::TestSScale::test_at_horizon PASSED [ 63%]
tests/unit/test_radial_scaling_core.py::TestSScale::test_in_weak_field PASSED [ 63%]
tests/unit/test_radial_scaling_core.py::TestBlendFunction::test_pure_strong PASSED [ 64%]
tests/unit/test_radial_scaling_core.py::TestBlendFunction::test_pure_weak PASSED [ 64%]
tests/unit/test_radial_scaling_core.py::TestBlendFunction::test_blend_zone PASSED [ 65%]
tests/unit/test_radial_scaling_core.py::TestDRhoDr::test_at_horizon FAILED [ 65%]
tests/unit/test_radial_scaling_core.py::TestDRhoDr::test_decreases_outward FAILED [ 66%]
tests/unit/test_radial_scaling_core.py::TestPhaseAccountingFactor::test_ssz_vs_gr_at_horizon PASSED [ 67%]
tests/unit/test_radial_scaling_core.py::TestRhoRSG::test_zero_at_horizon PASSED [ 67%]
tests/unit/test_radial_scaling_core.py::TestRhoRSG::test_positive_outward PASSED [ 68%]
tests/unit/test_radial_scaling_core.py::TestXiBlended::test_smooth_transition PASSED [ 68%]
tests/unit/test_ssz_core.py::TestSSZConstants::test_phi_value PASSED     [ 69%]
tests/unit/test_ssz_core.py::TestSSZConstants::test_xi_max_value PASSED  [ 69%]
tests/unit/test_ssz_core.py::TestSSZConstants::test_d_min_value PASSED   [ 70%]
tests/unit/test_ssz_core.py::TestSSZConstants::test_n0_value PASSED      [ 71%]
tests/unit/test_ssz_core.py::TestXiWeak::test_formula_at_large_r PASSED  [ 71%]
tests/unit/test_ssz_core.py::TestXiWeak::test_asymptotic_behavior PASSED [ 72%]
tests/unit/test_ssz_core.py::TestXiWeak::test_matches_gr_at_weak_field PASSED [ 72%]
tests/unit/test_ssz_core.py::TestXiStrong::test_saturation_at_horizon PASSED [ 73%]
tests/unit/test_ssz_core.py::TestXiStrong::test_finite_value_at_horizon PASSED [ 73%]
tests/unit/test_ssz_core.py::TestXiStrong::test_increases_with_depth FAILED [ 74%]
tests/unit/test_ssz_core.py::TestXiStrong::test_saturates_at_xi_max PASSED [ 75%]
tests/unit/test_ssz_core.py::TestDSSZ::test_at_horizon FAILED            [ 75%]
tests/unit/test_ssz_core.py::TestDSSZ::test_finite_at_horizon FAILED     [ 76%]
tests/unit/test_ssz_core.py::TestDSSZ::test_approaches_1_at_infinity FAILED [ 76%]
tests/unit/test_ssz_core.py::TestDSSZ::test_monotonic_in_xi FAILED       [ 77%]
tests/unit/test_ssz_core.py::TestDGR::test_zero_at_horizon FAILED        [ 77%]
tests/unit/test_ssz_core.py::TestDGR::test_approaches_1_at_infinity FAILED [ 78%]
tests/unit/test_ssz_core.py::TestDGR::test_ssz_vs_gr_at_horizon FAILED   [ 78%]
tests/unit/test_ssz_core.py::TestRegimeDetection::test_strong_regime_at_horizon FAILED [ 79%]
tests/unit/test_ssz_core.py::TestRegimeDetection::test_weak_regime_far_out PASSED [ 80%]
tests/unit/test_ssz_core.py::TestSSZScaling::test_finite_at_horizon FAILED [ 80%]
tests/validation/test_against_book.py::TestAgainstSSZBook::test_phi_matches_book PASSED [ 81%]
tests/validation/test_against_book.py::TestAgainstSSZBook::test_xi_max_matches_book PASSED [ 81%]
tests/validation/test_against_book.py::TestAgainstSSZBook::test_d_min_matches_book PASSED [ 82%]
tests/validation/test_against_book.py::TestAgainstSSZBook::test_xi_at_horizon_from_book PASSED [ 82%]
tests/validation/test_against_book.py::TestAgainstSSZBook::test_d_at_horizon_from_book FAILED [ 83%]
tests/validation/test_against_book.py::TestAgainstSSZBook::test_gr_d_zero_at_horizon FAILED [ 84%]
tests/validation/test_against_book.py::TestKeySSZPredictions::test_d_min_universal FAILED [ 84%]
tests/validation/test_against_book.py::TestKeySSZPredictions::test_weak_field_gr_agreement FAILED [ 85%]
tests/validation/test_against_book.py::TestKeySSZPredictions::test_strong_field_divergence FAILED [ 85%]
tests/validation/test_against_book.py::TestKeySSZPredictions::test_finite_vs_infinite_redshift PASSED [ 86%]
tests/validation/test_against_book.py::TestRingdownAmbiguity::test_d_min_squared_vs_3_percent XFAIL [ 86%]
tests/validation/test_against_book.py::TestGuardrails::test_regime_detection_critical PASSED [ 87%]
tests/validation/test_anti_circularity.py::TestAntiCircularityRules::test_posterior_fields_not_direct_observables PASSED [ 88%]
tests/validation/test_anti_circularity.py::TestAntiCircularityRules::test_kerr_is_not_ssz_reference PASSED [ 88%]
tests/validation/test_anti_circularity.py::TestAntiCircularityRules::test_same_fit_parameters_not_independent PASSED [ 89%]
tests/validation/test_anti_circularity.py::TestAntiCircularityRules::test_strain_is_real_observable PASSED [ 89%]
tests/validation/test_anti_circularity.py::TestAntiCircularityRules::test_residual_is_valid_test PASSED [ 90%]
tests/validation/test_anti_circularity.py::TestModelLockRequirement::test_ssz_parameters_must_be_locked FAILED [ 90%]
tests/validation/test_anti_circularity.py::TestModelLockRequirement::test_no_post_hoc_adjustment FAILED [ 91%]
tests/validation/test_anti_circularity.py::TestForbiddenObservables::test_forbidden_list_comprehensive PASSED [ 92%]
tests/validation/test_anti_circularity.py::TestForbiddenObservables::test_allowed_are_strain_based PASSED [ 92%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_status_is_conflicting FAILED [ 93%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_conflicting_sources_defined FAILED [ 93%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_source_a_is_3_percent FAILED [ 94%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_source_b_is_31_percent FAILED [ 94%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_source_c_is_39_percent FAILED [ 95%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_factor_10_difference FAILED [ 96%]
tests/validation/test_ringdown_conflict_detection.py::TestCheckRingdownUsable::test_returns_not_usable PASSED [ 96%]
tests/validation/test_ringdown_conflict_detection.py::TestCheckRingdownUsable::test_reason_mentions_conflict FAILED [ 97%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownFunctionRaises::test_ssz_ringdown_frequency_shift_raises PASSED [ 97%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownFunctionRaises::test_error_includes_conflict_report PASSED [ 98%]
tests/validation/test_ringdown_conflict_detection.py::TestRingdownFunctionRaises::test_epsilon_220_from_corpus_raises FAILED [ 98%]
tests/validation/test_ringdown_conflict_detection.py::TestConflictReport::test_report_includes_all_sources PASSED [ 99%]
tests/validation/test_ringdown_conflict_detection.py::TestConflictReport::test_report_asks_resolution_questions FAILED [100%]

================================== FAILURES ===================================
___________ TestForwardModelInitialization.test_initially_unlocked ____________
tests\integration\test_forward_model.py:17: in test_initially_unlocked
    assert model.epsilon_220 is None
           ^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'epsilon_220'
__________ TestForwardModelInitialization.test_can_lock_epsilon_220 ___________
tests\integration\test_forward_model.py:25: in test_can_lock_epsilon_220
    model.lock_epsilon_220(0.03, "SSZ_BOOK_DE_CLEAN.md Ch.30")
    ^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
____________ TestForwardModelInitialization.test_can_lock_eta_220 _____________
tests\integration\test_forward_model.py:31: in test_can_lock_eta_220
    model.lock_eta_220(0.05, "SSZ_BOOK_DE_CLEAN.md Ch.30")
    ^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'lock_eta_220'
__________ TestForwardModelInitialization.test_can_lock_kappa_phase ___________
tests\integration\test_forward_model.py:37: in test_can_lock_kappa_phase
    model.lock_kappa_phase(1.0, "placeholder")
    ^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'lock_kappa_phase'
_____________ TestRingdownShift.test_unshifted_when_epsilon_zero ______________
tests\integration\test_forward_model.py:47: in test_unshifted_when_epsilon_zero
    model.lock_epsilon_220(0.0, "test")
    ^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
_____________ TestRingdownShift.test_shifted_when_epsilon_nonzero _____________
tests\integration\test_forward_model.py:55: in test_shifted_when_epsilon_nonzero
    model.lock_epsilon_220(0.03, "test")
    ^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
____________ TestRingdownShift.test_raises_when_epsilon_not_locked ____________
tests\integration\test_forward_model.py:64: in test_raises_when_epsilon_not_locked
    model.ssz_ringdown_frequency_shift(250.0)
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_frequency_shift'
_________ TestRingdownShift.test_tau_shift_raises_when_eta_not_locked _________
tests\integration\test_forward_model.py:70: in test_tau_shift_raises_when_eta_not_locked
    model.ssz_ringdown_tau_shift(0.01)
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_tau_shift'
___________ TestPhaseDeformation.test_raises_when_kappa_not_locked ____________
tests\integration\test_forward_model.py:84: in test_raises_when_kappa_not_locked
    model.ssz_phase_deformation(freqs, M, rs)
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'ssz_phase_deformation'
_____________ TestPhaseDeformation.test_zero_at_high_frequencies ______________
tests\integration\test_forward_model.py:89: in test_zero_at_high_frequencies
    model.lock_kappa_phase(1.0, "test")
    ^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'lock_kappa_phase'
_________ TestAmplitudeDeformation.test_raises_when_kappa_not_locked __________
tests\integration\test_forward_model.py:114: in test_raises_when_kappa_not_locked
    model.ssz_amplitude_deformation(freqs, M, rs)
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'ssz_amplitude_deformation'
_________________ TestDetectorResponse.test_antenna_response __________________
tests\integration\test_forward_model.py:128: in test_antenna_response
    h_I = model.detector_response(h_plus, h_cross, F_plus, F_cross)
          ^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'detector_response'
_____________________ TestDetectorResponse.test_residual ______________________
tests\integration\test_forward_model.py:137: in test_residual
    r = model.residual(data, model_vec)
        ^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'residual'
___________ TestLikelihood.test_likelihood_decreases_with_mismatch ____________
tests\integration\test_forward_model.py:156: in test_likelihood_decreases_with_mismatch
    ll_match = model.log_likelihood(data, model_match, psd, freqs)
               ^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'log_likelihood'
_________________ TestLikelihood.test_inner_product_symmetry __________________
tests\integration\test_forward_model.py:173: in test_inner_product_symmetry
    ip_ab = model.noise_weighted_inner_product(a, b, psd, freqs)
            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'noise_weighted_inner_product'
_________ TestAntiCircularity.test_model_rejects_unlocked_parameters __________
tests\integration\test_forward_model.py:188: in test_model_rejects_unlocked_parameters
    model.ssz_ringdown_frequency_shift(250.0)
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_frequency_shift'
_________________ TestAccumulatedPhase.test_negative_inspiral _________________
tests\integration\test_inspiral_phase_forward_model.py:134: in test_negative_inspiral
    assert phi < 0  # Phase accumulates inward
    ^^^^^^^^^^^^^^
E   assert 60535.41268891149 < 0
____________________________ test_import_ssz_ligo _____________________________
tests\test_00_environment.py:8: in test_import_ssz_ligo
    assert slt.__version__ == "0.1.0"
E   AssertionError: assert '0.2.0' == '0.1.0'
E     
E     - 0.1.0
E     ?   ^
E     + 0.2.0
E     ?   ^
___________________ TestGetXi.test_uses_strong_near_horizon ___________________
tests\test_03_ssz_core.py:142: in test_uses_strong_near_horizon
    assert np.isclose(xi, expected)
E   assert np.False_
E    +  where np.False_ = <function isclose at 0x0000025F7CB024F0>(np.float64(0.6547062749508291), np.float64(0.8017118471377938))
E    +    where <function isclose at 0x0000025F7CB024F0> = np.isclose
_______ TestRingdownFrequencyShiftBlocked.test_raises_when_epsilon_none _______
tests\test_04_forward_model_placeholders.py:48: in test_raises_when_epsilon_none
    assert "not locked" in str(exc_info.value).lower()
E   assert 'not locked' in "ringdown blocked: partial_exploratory\n\n# ssz ringdown source status report\n\n**status:** partial_exploratory\n\n## authoritative source\n\n**v51 pdf / book ch.30:**\n- value: ~3%\n- context: fundamental mode qnm shift, below single-event detector precision\n- status: exploratory_only\n\n## important note\n\nthe ~3% shift is below current single-event detector precision.\ntestable via stacking or next-gen detectors (et/ce).\n\n## discarded/outdated sources\n\n- 39% photon-sphere value: not for ligo\n- 31% d_min\xb2 interpretation: possibly different regime\n\n\n\nto use this function, you must:\n1. resolve which source is authoritative\n2. explicitly provide epsilon_220 with documented source\n3. or use 'source' parameter with resolved choice"
E    +  where "ringdown blocked: partial_exploratory\n\n# ssz ringdown source status report\n\n**status:** partial_exploratory\n\n## authoritative source\n\n**v51 pdf / book ch.30:**\n- value: ~3%\n- context: fundamental mode qnm shift, below single-event detector precision\n- status: exploratory_only\n\n## important note\n\nthe ~3% shift is below current single-event detector precision.\ntestable via stacking or next-gen detectors (et/ce).\n\n## discarded/outdated sources\n\n- 39% photon-sphere value: not for ligo\n- 31% d_min\xb2 interpretation: possibly different regime\n\n\n\nto use this function, you must:\n1. resolve which source is authoritative\n2. explicitly provide epsilon_220 with documented source\n3. or use 'source' parameter with resolved choice" = <built-in method lower of str object at 0x0000025F20FF6E50>()
E    +    where <built-in method lower of str object at 0x0000025F20FF6E50> = "RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice".lower
E    +      where "RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice" = str(ValueError("RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice"))
E    +        where ValueError("RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice") = <ExceptionInfo ValueError("RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLOR...ritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice") tblen=2>.value
______ TestRingdownFrequencyShiftBlocked.test_works_when_epsilon_locked _______
tests\test_04_forward_model_placeholders.py:61: in test_works_when_epsilon_locked
    f_ssz = ssz_ringdown_frequency_shift(250.0, epsilon_220=0.03)
            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
src\ssz_ligo_tests\ssz_ringdown.py:112: in ssz_ringdown_frequency_shift
    raise ValueError(
E   ValueError: RINGDOWN BLOCKED: PARTIAL_EXPLORATORY
E   
E   # SSZ Ringdown Source Status Report
E   
E   **Status:** PARTIAL_EXPLORATORY
E   
E   ## Authoritative Source
E   
E   **V51 PDF / Book Ch.30:**
E   - Value: ~3%
E   - Context: Fundamental mode QNM shift, below single-event detector precision
E   - Status: EXPLORATORY_ONLY
E   
E   ## Important Note
E   
E   The ~3% shift is BELOW current single-event detector precision.
E   Testable via stacking or next-gen detectors (ET/CE).
E   
E   ## Discarded/Outdated Sources
E   
E   - 39% photon-sphere value: NOT FOR LIGO
E   - 31% D_min² interpretation: Possibly different regime
E   
E   
E   
E   To use this function, you must:
E   1. Resolve which source is authoritative
E   2. Explicitly provide epsilon_220 with documented source
E   3. Or use 'source' parameter with resolved choice
____________ TestRingdownTauShiftBlocked.test_raises_when_eta_none ____________
tests\test_04_forward_model_placeholders.py:73: in test_raises_when_eta_none
    assert "not locked" in str(exc_info.value).lower()
E   AssertionError: assert 'not locked' in 'ringdown blocked: eta_220 formula not found in ssz corpus. see ssz_forward_model_equation_gaps.md: missing_forward_equation.'
E    +  where 'ringdown blocked: eta_220 formula not found in ssz corpus. see ssz_forward_model_equation_gaps.md: missing_forward_equation.' = <built-in method lower of str object at 0x0000025F1CA961E0>()
E    +    where <built-in method lower of str object at 0x0000025F1CA961E0> = 'RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.'.lower
E    +      where 'RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.' = str(ValueError('RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.'))
E    +        where ValueError('RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.') = <ExceptionInfo ValueError('RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.') tblen=2>.value
___________ TestRingdownTauShiftBlocked.test_works_when_eta_locked ____________
tests\test_04_forward_model_placeholders.py:77: in test_works_when_eta_locked
    tau_ssz = ssz_ringdown_tau_shift(0.01, eta_220=0.05)
              ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
src\ssz_ligo_tests\ssz_ringdown.py:128: in ssz_ringdown_tau_shift
    raise ValueError(
E   ValueError: RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.
________ TestStrainAllowed.test_strain_fields_valid[H1/power_spectrum] ________
tests\test_08_anti_circularity.py:45: in test_strain_fields_valid
    assert status == CircularityStatus.VALID_INDEPENDENT
E   AssertionError: assert <CircularityStatus.UNKNOWN: 'UNKNOWN'> == <CircularityStatus.VALID_INDEPENDENT: 'VALID_INDEPENDENT'>
E    +  where <CircularityStatus.VALID_INDEPENDENT: 'VALID_INDEPENDENT'> = CircularityStatus.VALID_INDEPENDENT
_________________________ TestDRhoDr.test_at_horizon __________________________
tests\unit\test_radial_scaling_core.py:55: in test_at_horizon
    assert np.isclose(drho, expected, rtol=0.01)
E   assert np.False_
E    +  where np.False_ = <function isclose at 0x0000025F7CB024F0>(np.float64(0.3652230444261071), np.float64(0.3080557585001735), rtol=0.01)
E    +    where <function isclose at 0x0000025F7CB024F0> = np.isclose
______________________ TestDRhoDr.test_decreases_outward ______________________
tests\unit\test_radial_scaling_core.py:61: in test_decreases_outward
    assert drho_inner > drho_outer
E   assert np.float64(0.45863690626118414) > 0.8264462809917354
___________________ TestXiStrong.test_increases_with_depth ____________________
tests\unit\test_ssz_core.py:90: in test_increases_with_depth
    assert np.all(np.diff(xi_values) > 0)  # Increasing
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   assert np.False_
E    +  where np.False_ = <function all at 0x0000025F7CAF6230>(array([0., 0., 0., 0., 0.]) > 0)
E    +    where <function all at 0x0000025F7CAF6230> = np.all
E    +    and   array([0., 0., 0., 0., 0.]) = <function diff at 0x0000025F7CD2C0F0>(array([0.80171185, 0.80171185, 0.80171185, 0.80171185, 0.80171185,\n       0.80171185]))
E    +      where <function diff at 0x0000025F7CD2C0F0> = np.diff
__________________________ TestDSSZ.test_at_horizon ___________________________
tests\unit\test_ssz_core.py:107: in test_at_horizon
    d = D_ssz(xi)
        ^^^^^
E   NameError: name 'D_ssz' is not defined
_______________________ TestDSSZ.test_finite_at_horizon _______________________
tests\unit\test_ssz_core.py:113: in test_finite_at_horizon
    d = D_ssz(xi)
        ^^^^^
E   NameError: name 'D_ssz' is not defined
___________________ TestDSSZ.test_approaches_1_at_infinity ____________________
tests\unit\test_ssz_core.py:120: in test_approaches_1_at_infinity
    d = D_ssz(xi)
        ^^^^^
E   NameError: name 'D_ssz' is not defined
________________________ TestDSSZ.test_monotonic_in_xi ________________________
tests\unit\test_ssz_core.py:126: in test_monotonic_in_xi
    d_values = D_ssz(xi_values)
               ^^^^^
E   NameError: name 'D_ssz' is not defined
________________________ TestDGR.test_zero_at_horizon _________________________
tests\unit\test_ssz_core.py:137: in test_zero_at_horizon
    d = D_gr(r, rs)
        ^^^^
E   NameError: name 'D_gr' is not defined
____________________ TestDGR.test_approaches_1_at_infinity ____________________
tests\unit\test_ssz_core.py:144: in test_approaches_1_at_infinity
    d = D_gr(r, rs)
        ^^^^
E   NameError: name 'D_gr' is not defined
______________________ TestDGR.test_ssz_vs_gr_at_horizon ______________________
tests\unit\test_ssz_core.py:151: in test_ssz_vs_gr_at_horizon
    d_ssz = D_ssz(XI_MAX)
            ^^^^^
E   NameError: name 'D_ssz' is not defined
______________ TestRegimeDetection.test_strong_regime_at_horizon ______________
tests\unit\test_ssz_core.py:167: in test_strong_regime_at_horizon
    assert np.isclose(xi, XI_MAX, rtol=0.1)
E   assert np.False_
E    +  where np.False_ = <function isclose at 0x0000025F7CB024F0>(np.float64(0.6547062749508291), np.float64(0.8017118471377938), rtol=0.1)
E    +    where <function isclose at 0x0000025F7CB024F0> = np.isclose
____________________ TestSSZScaling.test_finite_at_horizon ____________________
tests\unit\test_ssz_core.py:185: in test_finite_at_horizon
    d_values = ssz_scaling(r_values, rs)
               ^^^^^^^^^^^^^^^^^^^^^^^^^
E   TypeError: d_ssz() takes 1 positional argument but 2 were given
_______________ TestAgainstSSZBook.test_d_at_horizon_from_book ________________
tests\validation\test_against_book.py:39: in test_d_at_horizon_from_book
    d = D_ssz(xi_horizon)
        ^^^^^
E   NameError: name 'D_ssz' is not defined
________________ TestAgainstSSZBook.test_gr_d_zero_at_horizon _________________
tests\validation\test_against_book.py:45: in test_gr_d_zero_at_horizon
    d_gr = D_gr(rs, rs)
           ^^^^
E   NameError: name 'D_gr' is not defined
_________________ TestKeySSZPredictions.test_d_min_universal __________________
tests\validation\test_against_book.py:59: in test_d_min_universal
    d = D_ssz(xi)
        ^^^^^
E   NameError: name 'D_ssz' is not defined
_____________ TestKeySSZPredictions.test_weak_field_gr_agreement ______________
tests\validation\test_against_book.py:68: in test_weak_field_gr_agreement
    d_ssz = D_ssz(xi)
            ^^^^^
E   NameError: name 'D_ssz' is not defined
_____________ TestKeySSZPredictions.test_strong_field_divergence ______________
tests\validation\test_against_book.py:80: in test_strong_field_divergence
    d_ssz = D_ssz(xi)
            ^^^^^
E   NameError: name 'D_ssz' is not defined
_________ TestModelLockRequirement.test_ssz_parameters_must_be_locked _________
tests\validation\test_anti_circularity.py:101: in test_ssz_parameters_must_be_locked
    model.ssz_ringdown_frequency_shift(250.0)
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_frequency_shift'
____________ TestModelLockRequirement.test_no_post_hoc_adjustment _____________
tests\validation\test_anti_circularity.py:116: in test_no_post_hoc_adjustment
    model.lock_epsilon_220(0.03, "SSZ_BOOK_DE_CLEAN.md Ch.30")
    ^^^^^^^^^^^^^^^^^^^^^^
E   AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
________________ TestRingdownStatus.test_status_is_conflicting ________________
tests\validation\test_ringdown_conflict_detection.py:20: in test_status_is_conflicting
    assert RINGDOWN_MODEL_STATUS == "CONFLICTING_SSZ_SOURCES"
E   AssertionError: assert 'PARTIAL_EXPLORATORY' == 'CONFLICTING_SSZ_SOURCES'
E     
E     - CONFLICTING_SSZ_SOURCES
E     + PARTIAL_EXPLORATORY
_____________ TestRingdownStatus.test_conflicting_sources_defined _____________
tests\validation\test_ringdown_conflict_detection.py:24: in test_conflicting_sources_defined
    assert "source_a_3_percent" in CONFLICTING_SOURCES
E   assert 'source_a_3_percent' in {'v51_pdf_3_percent': {'value': 0.03, 'origin': 'SSZ_BOOK_DE_CLEAN.md Ch.30 / V51 PDF', 'formula': 'approximately 3%', 'context': 'Fundamental mode QNM shift, below single-event detector precision', 'status': 'EXPLORATORY_ONLY'}, 'legacy_d_min_squared': {'value': np.float64(0.3080557585001735), 'origin': "Older interpretation 'proportional to D_min\xb2'", 'formula': '\u03b5 \u221d D_min\xb2 \u2248 0.31', 'context': 'Possibly outdated or different physical regime', 'status': 'SUPERSEDED_OR_DIFFERENT_REGIME'}, 'discarded_photon_sphere_39': {'value': 0.39, 'origin': 'qnm_spectrum.md at photon sphere (DISCARDED)', 'formula': 'f_SSZ/f_GR \u2248 1.39', 'context': 'NOT FOR LIGO - different physical scenario', 'status': 'DISCARDED_FOR_LIGO'}}
________________ TestRingdownStatus.test_source_a_is_3_percent ________________
tests\validation\test_ringdown_conflict_detection.py:30: in test_source_a_is_3_percent
    source = CONFLICTING_SOURCES["source_a_3_percent"]
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   KeyError: 'source_a_3_percent'
_______________ TestRingdownStatus.test_source_b_is_31_percent ________________
tests\validation\test_ringdown_conflict_detection.py:35: in test_source_b_is_31_percent
    source = CONFLICTING_SOURCES["source_b_31_percent"]
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   KeyError: 'source_b_31_percent'
_______________ TestRingdownStatus.test_source_c_is_39_percent ________________
tests\validation\test_ringdown_conflict_detection.py:41: in test_source_c_is_39_percent
    source = CONFLICTING_SOURCES["source_c_39_percent"]
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   KeyError: 'source_c_39_percent'
________________ TestRingdownStatus.test_factor_10_difference _________________
tests\validation\test_ringdown_conflict_detection.py:46: in test_factor_10_difference
    val_a = CONFLICTING_SOURCES["source_a_3_percent"]["value"]
            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
E   KeyError: 'source_a_3_percent'
____________ TestCheckRingdownUsable.test_reason_mentions_conflict ____________
tests\validation\test_ringdown_conflict_detection.py:63: in test_reason_mentions_conflict
    assert "CONFLICTING" in reason or "BLOCKED" in reason
E   AssertionError: assert ('CONFLICTING' in 'PARTIAL_EXPLORATORY: epsilon_220 ~0.03 (3%) is EXPLORATORY. V51 PDF indicates this is below current single-event precision. Exact derivation/locking needed before numerical claims.' or 'BLOCKED' in 'PARTIAL_EXPLORATORY: epsilon_220 ~0.03 (3%) is EXPLORATORY. V51 PDF indicates this is below current single-event precision. Exact derivation/locking needed before numerical claims.')
_______ TestRingdownFunctionRaises.test_epsilon_220_from_corpus_raises ________
tests\validation\test_ringdown_conflict_detection.py:90: in test_epsilon_220_from_corpus_raises
    assert "CONFLICTING" in str(exc_info.value)
E   AssertionError: assert 'CONFLICTING' in 'Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.'
E    +  where 'Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.' = str(NotImplementedError('Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.'))
E    +    where NotImplementedError('Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.') = <ExceptionInfo NotImplementedError('Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.') tblen=2>.value
__________ TestConflictReport.test_report_asks_resolution_questions ___________
tests\validation\test_ringdown_conflict_detection.py:108: in test_report_asks_resolution_questions
    assert "Which source" in report
E   AssertionError: assert 'Which source' in '# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n'
=========================== short test summary info ===========================
XFAIL tests/validation/test_against_book.py::TestRingdownAmbiguity::test_d_min_squared_vs_3_percent - \u03b5_220 ambiguity: 31% vs 3% must be resolved
FAILED tests/integration/test_forward_model.py::TestForwardModelInitialization::test_initially_unlocked - AttributeError: 'SSZForwardModel' object has no attribute 'epsilon_220'
FAILED tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_epsilon_220 - AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
FAILED tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_eta_220 - AttributeError: 'SSZForwardModel' object has no attribute 'lock_eta_220'
FAILED tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_kappa_phase - AttributeError: 'SSZForwardModel' object has no attribute 'lock_kappa_phase'
FAILED tests/integration/test_forward_model.py::TestRingdownShift::test_unshifted_when_epsilon_zero - AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
FAILED tests/integration/test_forward_model.py::TestRingdownShift::test_shifted_when_epsilon_nonzero - AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
FAILED tests/integration/test_forward_model.py::TestRingdownShift::test_raises_when_epsilon_not_locked - AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_frequency_shift'
FAILED tests/integration/test_forward_model.py::TestRingdownShift::test_tau_shift_raises_when_eta_not_locked - AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_tau_shift'
FAILED tests/integration/test_forward_model.py::TestPhaseDeformation::test_raises_when_kappa_not_locked - AttributeError: 'SSZForwardModel' object has no attribute 'ssz_phase_deformation'
FAILED tests/integration/test_forward_model.py::TestPhaseDeformation::test_zero_at_high_frequencies - AttributeError: 'SSZForwardModel' object has no attribute 'lock_kappa_phase'
FAILED tests/integration/test_forward_model.py::TestAmplitudeDeformation::test_raises_when_kappa_not_locked - AttributeError: 'SSZForwardModel' object has no attribute 'ssz_amplitude_deformation'
FAILED tests/integration/test_forward_model.py::TestDetectorResponse::test_antenna_response - AttributeError: 'SSZForwardModel' object has no attribute 'detector_response'
FAILED tests/integration/test_forward_model.py::TestDetectorResponse::test_residual - AttributeError: 'SSZForwardModel' object has no attribute 'residual'
FAILED tests/integration/test_forward_model.py::TestLikelihood::test_likelihood_decreases_with_mismatch - AttributeError: 'SSZForwardModel' object has no attribute 'log_likelihood'
FAILED tests/integration/test_forward_model.py::TestLikelihood::test_inner_product_symmetry - AttributeError: 'SSZForwardModel' object has no attribute 'noise_weighted_inner_product'
FAILED tests/integration/test_forward_model.py::TestAntiCircularity::test_model_rejects_unlocked_parameters - AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_frequency_shift'
FAILED tests/integration/test_inspiral_phase_forward_model.py::TestAccumulatedPhase::test_negative_inspiral - assert 60535.41268891149 < 0
FAILED tests/test_00_environment.py::test_import_ssz_ligo - AssertionError: assert '0.2.0' == '0.1.0'
  
  - 0.1.0
  ?   ^
  + 0.2.0
  ?   ^
FAILED tests/test_03_ssz_core.py::TestGetXi::test_uses_strong_near_horizon - assert np.False_
 +  where np.False_ = <function isclose at 0x0000025F7CB024F0>(np.float64(0.6547062749508291), np.float64(0.8017118471377938))
 +    where <function isclose at 0x0000025F7CB024F0> = np.isclose
FAILED tests/test_04_forward_model_placeholders.py::TestRingdownFrequencyShiftBlocked::test_raises_when_epsilon_none - assert 'not locked' in "ringdown blocked: partial_exploratory\n\n# ssz ringdown source status report\n\n**status:** partial_exploratory\n\n## authoritative source\n\n**v51 pdf / book ch.30:**\n- value: ~3%\n- context: fundamental mode qnm shift, below single-event detector precision\n- status: exploratory_only\n\n## important note\n\nthe ~3% shift is below current single-event detector precision.\ntestable via stacking or next-gen detectors (et/ce).\n\n## discarded/outdated sources\n\n- 39% photon-sphere value: not for ligo\n- 31% d_min\xb2 interpretation: possibly different regime\n\n\n\nto use this function, you must:\n1. resolve which source is authoritative\n2. explicitly provide epsilon_220 with documented source\n3. or use 'source' parameter with resolved choice"
 +  where "ringdown blocked: partial_exploratory\n\n# ssz ringdown source status report\n\n**status:** partial_exploratory\n\n## authoritative source\n\n**v51 pdf / book ch.30:**\n- value: ~3%\n- context: fundamental mode qnm shift, below single-event detector precision\n- status: exploratory_only\n\n## important note\n\nthe ~3% shift is below current single-event detector precision.\ntestable via stacking or next-gen detectors (et/ce).\n\n## discarded/outdated sources\n\n- 39% photon-sphere value: not for ligo\n- 31% d_min\xb2 interpretation: possibly different regime\n\n\n\nto use this function, you must:\n1. resolve which source is authoritative\n2. explicitly provide epsilon_220 with documented source\n3. or use 'source' parameter with resolved choice" = <built-in method lower of str object at 0x0000025F20FF6E50>()
 +    where <built-in method lower of str object at 0x0000025F20FF6E50> = "RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice".lower
 +      where "RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice" = str(ValueError("RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice"))
 +        where ValueError("RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n\n\nTo use this function, you must:\n1. Resolve which source is authoritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice") = <ExceptionInfo ValueError("RINGDOWN BLOCKED: PARTIAL_EXPLORATORY\n\n# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLOR...ritative\n2. Explicitly provide epsilon_220 with documented source\n3. Or use 'source' parameter with resolved choice") tblen=2>.value
FAILED tests/test_04_forward_model_placeholders.py::TestRingdownFrequencyShiftBlocked::test_works_when_epsilon_locked - ValueError: RINGDOWN BLOCKED: PARTIAL_EXPLORATORY

# SSZ Ringdown Source Status Report

**Status:** PARTIAL_EXPLORATORY

## Authoritative Source

**V51 PDF / Book Ch.30:**
- Value: ~3%
- Context: Fundamental mode QNM shift, below single-event detector precision
- Status: EXPLORATORY_ONLY

## Important Note

The ~3% shift is BELOW current single-event detector precision.
Testable via stacking or next-gen detectors (ET/CE).

## Discarded/Outdated Sources

- 39% photon-sphere value: NOT FOR LIGO
- 31% D_min² interpretation: Possibly different regime



To use this function, you must:
1. Resolve which source is authoritative
2. Explicitly provide epsilon_220 with documented source
3. Or use 'source' parameter with resolved choice
FAILED tests/test_04_forward_model_placeholders.py::TestRingdownTauShiftBlocked::test_raises_when_eta_none - AssertionError: assert 'not locked' in 'ringdown blocked: eta_220 formula not found in ssz corpus. see ssz_forward_model_equation_gaps.md: missing_forward_equation.'
 +  where 'ringdown blocked: eta_220 formula not found in ssz corpus. see ssz_forward_model_equation_gaps.md: missing_forward_equation.' = <built-in method lower of str object at 0x0000025F1CA961E0>()
 +    where <built-in method lower of str object at 0x0000025F1CA961E0> = 'RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.'.lower
 +      where 'RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.' = str(ValueError('RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.'))
 +        where ValueError('RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.') = <ExceptionInfo ValueError('RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.') tblen=2>.value
FAILED tests/test_04_forward_model_placeholders.py::TestRingdownTauShiftBlocked::test_works_when_eta_locked - ValueError: RINGDOWN BLOCKED: eta_220 formula not found in SSZ corpus. See SSZ_FORWARD_MODEL_EQUATION_GAPS.md: MISSING_FORWARD_EQUATION.
FAILED tests/test_08_anti_circularity.py::TestStrainAllowed::test_strain_fields_valid[H1/power_spectrum] - AssertionError: assert <CircularityStatus.UNKNOWN: 'UNKNOWN'> == <CircularityStatus.VALID_INDEPENDENT: 'VALID_INDEPENDENT'>
 +  where <CircularityStatus.VALID_INDEPENDENT: 'VALID_INDEPENDENT'> = CircularityStatus.VALID_INDEPENDENT
FAILED tests/unit/test_radial_scaling_core.py::TestDRhoDr::test_at_horizon - assert np.False_
 +  where np.False_ = <function isclose at 0x0000025F7CB024F0>(np.float64(0.3652230444261071), np.float64(0.3080557585001735), rtol=0.01)
 +    where <function isclose at 0x0000025F7CB024F0> = np.isclose
FAILED tests/unit/test_radial_scaling_core.py::TestDRhoDr::test_decreases_outward - assert np.float64(0.45863690626118414) > 0.8264462809917354
FAILED tests/unit/test_ssz_core.py::TestXiStrong::test_increases_with_depth - assert np.False_
 +  where np.False_ = <function all at 0x0000025F7CAF6230>(array([0., 0., 0., 0., 0.]) > 0)
 +    where <function all at 0x0000025F7CAF6230> = np.all
 +    and   array([0., 0., 0., 0., 0.]) = <function diff at 0x0000025F7CD2C0F0>(array([0.80171185, 0.80171185, 0.80171185, 0.80171185, 0.80171185,\n       0.80171185]))
 +      where <function diff at 0x0000025F7CD2C0F0> = np.diff
FAILED tests/unit/test_ssz_core.py::TestDSSZ::test_at_horizon - NameError: name 'D_ssz' is not defined
FAILED tests/unit/test_ssz_core.py::TestDSSZ::test_finite_at_horizon - NameError: name 'D_ssz' is not defined
FAILED tests/unit/test_ssz_core.py::TestDSSZ::test_approaches_1_at_infinity - NameError: name 'D_ssz' is not defined
FAILED tests/unit/test_ssz_core.py::TestDSSZ::test_monotonic_in_xi - NameError: name 'D_ssz' is not defined
FAILED tests/unit/test_ssz_core.py::TestDGR::test_zero_at_horizon - NameError: name 'D_gr' is not defined
FAILED tests/unit/test_ssz_core.py::TestDGR::test_approaches_1_at_infinity - NameError: name 'D_gr' is not defined
FAILED tests/unit/test_ssz_core.py::TestDGR::test_ssz_vs_gr_at_horizon - NameError: name 'D_ssz' is not defined
FAILED tests/unit/test_ssz_core.py::TestRegimeDetection::test_strong_regime_at_horizon - assert np.False_
 +  where np.False_ = <function isclose at 0x0000025F7CB024F0>(np.float64(0.6547062749508291), np.float64(0.8017118471377938), rtol=0.1)
 +    where <function isclose at 0x0000025F7CB024F0> = np.isclose
FAILED tests/unit/test_ssz_core.py::TestSSZScaling::test_finite_at_horizon - TypeError: d_ssz() takes 1 positional argument but 2 were given
FAILED tests/validation/test_against_book.py::TestAgainstSSZBook::test_d_at_horizon_from_book - NameError: name 'D_ssz' is not defined
FAILED tests/validation/test_against_book.py::TestAgainstSSZBook::test_gr_d_zero_at_horizon - NameError: name 'D_gr' is not defined
FAILED tests/validation/test_against_book.py::TestKeySSZPredictions::test_d_min_universal - NameError: name 'D_ssz' is not defined
FAILED tests/validation/test_against_book.py::TestKeySSZPredictions::test_weak_field_gr_agreement - NameError: name 'D_ssz' is not defined
FAILED tests/validation/test_against_book.py::TestKeySSZPredictions::test_strong_field_divergence - NameError: name 'D_ssz' is not defined
FAILED tests/validation/test_anti_circularity.py::TestModelLockRequirement::test_ssz_parameters_must_be_locked - AttributeError: 'SSZForwardModel' object has no attribute 'ssz_ringdown_frequency_shift'
FAILED tests/validation/test_anti_circularity.py::TestModelLockRequirement::test_no_post_hoc_adjustment - AttributeError: 'SSZForwardModel' object has no attribute 'lock_epsilon_220'
FAILED tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_status_is_conflicting - AssertionError: assert 'PARTIAL_EXPLORATORY' == 'CONFLICTING_SSZ_SOURCES'
  
  - CONFLICTING_SSZ_SOURCES
  + PARTIAL_EXPLORATORY
FAILED tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_conflicting_sources_defined - assert 'source_a_3_percent' in {'v51_pdf_3_percent': {'value': 0.03, 'origin': 'SSZ_BOOK_DE_CLEAN.md Ch.30 / V51 PDF', 'formula': 'approximately 3%', 'context': 'Fundamental mode QNM shift, below single-event detector precision', 'status': 'EXPLORATORY_ONLY'}, 'legacy_d_min_squared': {'value': np.float64(0.3080557585001735), 'origin': "Older interpretation 'proportional to D_min\xb2'", 'formula': '\u03b5 \u221d D_min\xb2 \u2248 0.31', 'context': 'Possibly outdated or different physical regime', 'status': 'SUPERSEDED_OR_DIFFERENT_REGIME'}, 'discarded_photon_sphere_39': {'value': 0.39, 'origin': 'qnm_spectrum.md at photon sphere (DISCARDED)', 'formula': 'f_SSZ/f_GR \u2248 1.39', 'context': 'NOT FOR LIGO - different physical scenario', 'status': 'DISCARDED_FOR_LIGO'}}
FAILED tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_source_a_is_3_percent - KeyError: 'source_a_3_percent'
FAILED tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_source_b_is_31_percent - KeyError: 'source_b_31_percent'
FAILED tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_source_c_is_39_percent - KeyError: 'source_c_39_percent'
FAILED tests/validation/test_ringdown_conflict_detection.py::TestRingdownStatus::test_factor_10_difference - KeyError: 'source_a_3_percent'
FAILED tests/validation/test_ringdown_conflict_detection.py::TestCheckRingdownUsable::test_reason_mentions_conflict - AssertionError: assert ('CONFLICTING' in 'PARTIAL_EXPLORATORY: epsilon_220 ~0.03 (3%) is EXPLORATORY. V51 PDF indicates this is below current single-event precision. Exact derivation/locking needed before numerical claims.' or 'BLOCKED' in 'PARTIAL_EXPLORATORY: epsilon_220 ~0.03 (3%) is EXPLORATORY. V51 PDF indicates this is below current single-event precision. Exact derivation/locking needed before numerical claims.')
FAILED tests/validation/test_ringdown_conflict_detection.py::TestRingdownFunctionRaises::test_epsilon_220_from_corpus_raises - AssertionError: assert 'CONFLICTING' in 'Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.'
 +  where 'Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.' = str(NotImplementedError('Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.'))
 +    where NotImplementedError('Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.') = <ExceptionInfo NotImplementedError('Cannot retrieve epsilon_220: PARTIAL_EXPLORATORY\n\nConflicting values:\n  - Source A (Book text): ~3%\n  - Source B (D_min\xb2): ~31%\n  - Source C (Photon sphere): ~39%\n\nResolution required from SSZ authors.') tblen=2>.value
FAILED tests/validation/test_ringdown_conflict_detection.py::TestConflictReport::test_report_asks_resolution_questions - AssertionError: assert 'Which source' in '# SSZ Ringdown Source Status Report\n\n**Status:** PARTIAL_EXPLORATORY\n\n## Authoritative Source\n\n**V51 PDF / Book Ch.30:**\n- Value: ~3%\n- Context: Fundamental mode QNM shift, below single-event detector precision\n- Status: EXPLORATORY_ONLY\n\n## Important Note\n\nThe ~3% shift is BELOW current single-event detector precision.\nTestable via stacking or next-gen detectors (ET/CE).\n\n## Discarded/Outdated Sources\n\n- 39% photon-sphere value: NOT FOR LIGO\n- 31% D_min\xb2 interpretation: Possibly different regime\n\n'
================== 52 failed, 123 passed, 1 xfailed in 9.40s ==================

```
