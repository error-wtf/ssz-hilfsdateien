# Verbose Tests Progress

## Status: 23/65 Tests erweitert (35%)

---

## ✅ FERTIG (23 Tests mit detaillierten Outputs)

### **Root-Level Tests (6/7)**
1. ✅ test_ppn_exact.py - PPN β=γ=1
2. ✅ test_vfall_duality.py - Dual velocity
3. ✅ test_energy_conditions.py - WEC/DEC/SEC
4. ✅ test_c1_segments.py - C1 continuity
5. ✅ test_c2_segments_strict.py - C2 strict
6. ✅ test_c2_curvature_proxy.py - Curvature proxy
7. ⚠️ test_utf8_encoding.py - SKIP (nur technisch)

### **tests/test_segwave_core.py (15/20)**
1. ✅ test_temperature_only_basic - Q-Factor β=1
2. ✅ test_temperature_with_beta - Q-Factor β=2
3. ✅ test_temperature_and_density - Q-Factor T+n
4. ✅ test_single_shell - Initial condition
5. ✅ test_two_shells_alpha_one - SSZ propagation
6. ✅ test_deterministic_chain - 5-ring chain
7. ✅ test_alpha_zero_constant_velocity - Classical limit
8. ⚠️ test_with_density - SKIP (einfach)
9. ⚠️ test_mismatched_lengths_raises - SKIP (error test)
10. ✅ test_single_gamma - Frequency redshift
11. ✅ test_frequency_decreases_with_gamma - Frequency evolution
12. ⚠️ test_invalid_gamma_raises - SKIP (error test)
13. ✅ test_perfect_match - Perfect residuals
14. ✅ test_systematic_bias - Systematic bias
15. ⚠️ test_mixed_residuals - SKIP (redundant)
16. ✅ test_constant_q - Cumulative γ constant
17. ✅ test_all_ones - Cumulative γ = 1
18. ✅ test_increasing_sequence - Cumulative γ increasing

### **tests/cosmos/test_multi_body_sigma.py (1/1)**
1. ✅ test_two_body_sigma_superposition - Multi-body

### **scripts/tests/test_cosmo_multibody.py (3/3)**
1. ✅ test_sigma_additive_mass - Sun+Jupiter
2. ✅ test_tau_monotonic_with_alpha - Time dilation
3. ✅ test_refractive_index_baseline - Causality

### **scripts/tests/test_cosmo_kernel.py (4/4)**
1. ✅ test_gamma_bounds_and_monotonic - SSZ kernel
2. ✅ test_redshift_mapping - Cosmology
3. ✅ test_rotation_modifier - Flat curves
4. ✅ test_lensing_proxy_positive - Lensing

---

## ⏳ IN ARBEIT (42 Tests)

### **tests/test_segwave_cli.py (0/16)** ← NÄCHSTE
- ⏳ test_help_flag
- ⏳ test_missing_required_args
- ⏳ test_invalid_csv_path
- ⏳ test_fixed_alpha_execution
- ⏳ test_fit_alpha_execution
- ⏳ test_frequency_tracking
- ⏳ test_custom_exponents
- ⏳ test_negative_v0
- ⏳ test_mutually_exclusive_alpha
- ⏳ test_g79_dataset_exists
- ⏳ test_cygx_dataset_exists
- ⏳ test_sources_json_exists
- ⏳ test_sources_config_yaml_exists
- ⏳ test_load_sources_config_function
- ⏳ test_g79_cli_smoke_run
- ⏳ test_cygx_cli_smoke_run

### **tests/test_print_all_md.py (0/6)**
- ⏳ test_print_all_md_basic
- ⏳ test_print_all_md_depth_order
- ⏳ test_print_all_md_exclude_dirs
- ⏳ test_print_all_md_size_limit
- ⏳ test_print_all_md_no_files
- ⏳ test_print_all_md_custom_includes

### **scripts/tests/test_ssz_kernel.py (0/4)**
- ⏳ 4 kernel tests (brauchen Details)

### **scripts/tests/test_ssz_invariants.py (0/6)**
- ⏳ test_segment_growth_is_monotonic
- ⏳ test_natural_boundary_positive
- ⏳ test_manifest_exists
- ⏳ test_spiral_index_bounds
- ⏳ test_solar_segments_non_empty
- ⏳ test_segment_density_positive

### **scripts/tests/test_segmenter.py (0/2)**
- ⏳ test_segments_cover_all_points
- ⏳ test_segment_counts_grow

---

## 📊 Zusammenfassung

- ✅ **Fertig**: 23 Tests (35%)
- ⏳ **Zu erledigen**: 42 Tests (65%)
- ⚠️ **Übersprungen**: 5 Tests (Error/Technical)

**GESAMT: 70 Tests** (65 physikalische + 5 technische)

---

**Nächster Schritt: test_segwave_cli.py (16 Tests)**

© 2025 Carmen Wrede, Lino Casu
Anti-Capitalist Software License (v 1.4)
