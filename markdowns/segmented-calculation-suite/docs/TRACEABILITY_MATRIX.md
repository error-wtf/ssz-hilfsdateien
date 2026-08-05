# TRACEABILITY_MATRIX: Method ↔ Source ↔ Tests ↔ Plots ↔ Exports

**Generated:** 2025-01-16  
**Purpose:** Full traceability from original source to implementation

---

## Core Methods

| method_id | source_file:function | tests | plots | export_fields |
|-----------|---------------------|-------|-------|---------------|
| `schwarzschild_radius` | ssz-qubits/ssz_qubits.py:schwarzschild_radius | test_schwarzschild_sun, test_schwarzschild_earth | (component) | r_s_m, r_s_km |
| `xi_weak` | ssz-qubits/ssz_qubits.py:xi_segment_density(regime='weak') | test_xi_weak_field, test_weak_regime_boundary | xi_profile, regime_zones | Xi |
| `xi_strong` | ssz-metric-pure/src/ssz_core/segment_density.py:Xi | test_xi_strong_field, test_xi_at_horizon | xi_profile, regime_zones | Xi |
| `xi_blended` | segcalc/methods/xi.py:xi_blended | test_blend_regime, test_blend_continuity | regime_zones | Xi |
| `xi_auto` | ssz-qubits/ssz_qubits.py:xi_segment_density(regime='auto') | test_weak_regime_boundary, test_strong_regime_boundary | xi_profile | Xi, regime |
| `D_ssz` | ssz-metric-pure/src/ssz_core/segment_density.py:D_SSZ | test_D_ssz_finite_at_horizon, test_singularity_free | dilation_profile, gr_vs_ssz | D_ssz |
| `D_gr` | ssz-metric-pure/src/ssz_core/segment_density.py:D_GR | test_D_gr_singular_at_horizon | dilation_profile, gr_vs_ssz | D_gr |
| `find_intersection` | ssz-metric-pure/src/ssz_core/segment_density.py:find_intersection | test_universal_intersection | universal_intersection | r_star_over_rs |

---

## Redshift Methods

| method_id | source_file:function | tests | plots | export_fields |
|-----------|---------------------|-------|-------|---------------|
| `z_gravitational` | segcalc/methods/redshift.py:z_gravitational | test_pound_rebka | redshift_breakdown | z_gr |
| `z_doppler` | segcalc/methods/redshift.py:z_special_rel | (implicit) | redshift_breakdown | z_sr |
| `z_ssz_total` | Unified-Results/ssz_unified_suite.py | test_ns_psr_* | comparison_scatter, residuals | z_ssz_total |
| `delta_M` | Unified-Results/ssz_unified_suite.py:delta_M | (implicit in z_ssz) | - | delta_M_pct |
| `r_phi` | Unified-Results/ssz_unified_suite.py:r_phi | - | - | r_phi_m |

---

## Unified Suite Methods

| method_id | source_file:function | tests | plots | export_fields |
|-----------|---------------------|-------|-------|---------------|
| `sigma` | Unified-Results/ssz_unified_suite.py:sigma | test_sigma_formula | sigma_profile | sigma |
| `tau` | Unified-Results/ssz_unified_suite.py:tau | test_tau_formula | tau_profile | tau |
| `n_index` | Unified-Results/ssz_unified_suite.py:n_index | test_refractive_index | n_profile | n_index |
| `dual_velocity` | Unified-Results/ssz_unified_suite.py:dual_velocity | test_dual_velocity_invariance | dual_velocity_plot | v_esc, v_fall |
| `euler_spiral` | Unified-Results/ssz_unified_suite.py:euler_spiral | test_euler_spiral | euler_spiral_plot | spiral_coords |

---

## PPN Methods

| method_id | source_file:function | tests | plots | export_fields |
|-----------|---------------------|-------|-------|---------------|
| `ppn_lensing` | segcalc/methods/ppn.py:light_deflection | test_light_deflection | lensing_plot | alpha_rad |
| `ppn_shapiro` | segcalc/methods/ppn.py:shapiro_delay | test_shapiro_delay | shapiro_plot | dt_shapiro |
| `ppn_perihelion` | segcalc/methods/ppn.py:perihelion_precession | test_perihelion_precession | - | precession_arcsec |

---

## Empirical Methods

| method_id | source_file:function | tests | plots | export_fields |
|-----------|---------------------|-------|-------|---------------|
| `power_law_prediction` | segcalc/methods/power_law.py:power_law_prediction | test_power_law_fit, test_power_law_coefficient | power_law | E_norm_predicted |
| `compactness` | segcalc/methods/power_law.py:compactness | - | - | compactness |

---

## Tensor Methods (Advanced)

| method_id | source_file:function | tests | plots | export_fields |
|-----------|---------------------|-------|-------|---------------|
| `metric_tensor_ssz` | ssz-metric-pure/src/ssz_metric_pure/metric_tensor_4d.py | test_metric_signature | metric_components | g_mu_nu |
| `einstein_tensor` | ssz-metric-pure/src/ssz_metric_pure/einstein_ricci_4d.py | test_einstein_eqs | einstein_tensor_plot | G_mu_nu |
| `geodesic_equation` | ssz-metric-pure/src/ssz_metric_pure/geodesics.py | test_geodesics | geodesic_plot | trajectory |

---

## Test → Source Mapping

| test_id | method_ids | source_test_file | tolerance |
|---------|------------|------------------|-----------|
| test_golden_ratio | PHI | ssz-qubits/tests/test_ssz_physics.py | 1e-15 |
| test_schwarzschild_sun | schwarzschild_radius | ssz-qubits/tests/test_ssz_physics.py | 0.5 m |
| test_schwarzschild_earth | schwarzschild_radius | ssz-qubits/tests/test_ssz_physics.py | 10 μm |
| test_xi_weak_field | xi_weak | ssz-qubits/tests/test_ssz_physics.py | 1e-10 |
| test_xi_strong_field | xi_strong | ssz-metric-pure/tests/ | 0.001 |
| test_xi_at_horizon | xi_strong | ssz-metric-pure/tests/ | 0.001 |
| test_D_ssz_finite_at_horizon | D_ssz | ssz-metric-pure/tests/ | 0.001 |
| test_D_gr_singular_at_horizon | D_gr | ssz-metric-pure/tests/ | - |
| test_universal_intersection | find_intersection | ssz-metric-pure/tests/ | 0.002 |
| test_gps_timing | D_ssz, xi_weak | ssz-qubits/tests/test_validation.py | 5 μs |
| test_pound_rebka | D_ssz, z_gravitational | ssz-qubits/tests/test_validation.py | 0.1e-15 |
| test_power_law_fit | power_law_prediction | Unified-Results | 0.002 R² |

---

## Plot → Method Mapping

| plot_id | required_methods | source_generator |
|---------|-----------------|------------------|
| xi_and_dilation | xi_auto, D_ssz, D_gr | segcalc/plotting/ |
| gr_vs_ssz_comparison | D_ssz, D_gr | segcalc/plotting/ |
| universal_intersection | find_intersection | segcalc/plotting/ |
| regime_zones | xi_weak, xi_strong, xi_blended | segcalc/plotting/ |
| dilation_profile | D_ssz, D_gr | app_v3.py |
| xi_profile | xi_auto | app_v3.py |
| redshift_breakdown | z_gravitational, z_doppler | app_v3.py |
| power_law | power_law_prediction | segcalc/plotting/ |
| comparison_scatter | z_ssz_total | app_v3.py |
| residuals_plot | z_ssz_total | app_v3.py |

---

## Export Field → Method Mapping

| export_field | computed_by | unit | format |
|--------------|-------------|------|--------|
| name | input | - | string |
| M_Msun | input | M☉ | float |
| R_km | input | km | float |
| r_s_km | schwarzschild_radius | km | float |
| r_over_rs | compute | - | float |
| regime | xi_auto | - | string |
| Xi | xi_auto | - | float |
| D_ssz | D_ssz | - | float |
| D_gr | D_gr | - | float |
| z_ssz_grav | z_gravitational | - | float |
| z_ssz_total | z_ssz_total | - | float |
| z_grsr | z_combined | - | float |
| z_obs | input (optional) | - | float |
| ssz_closer | compare | - | bool |
| E_norm_predicted | power_law_prediction | - | float |

---

## Implementation Status

| Category | Total | Implemented | % |
|----------|-------|-------------|---|
| Core Methods | 8 | 8 | 100% |
| Redshift Methods | 5 | 5 | 100% |
| Unified Suite Methods | 5 | 5 | 100% |
| PPN Methods | 3 | 3 | 100% |
| Empirical Methods | 2 | 2 | 100% |
| Tensor Methods | 3 | 0 | 0% |
| **TOTAL** | **26** | **23** | **88%** |

---

## Gap Analysis

### Missing Implementations
| method_id | Priority | Effort | Blocker |
|-----------|----------|--------|---------|
| metric_tensor_ssz | LOW | HIGH | Symbolic math |
| einstein_tensor | LOW | HIGH | Depends on metric |
| geodesic_equation | LOW | HIGH | ODE solver |

### Missing Tests
| test_id | method_id | Priority |
|---------|-----------|----------|
| test_sigma_formula | sigma | MEDIUM |
| test_tau_formula | tau | MEDIUM |
| test_n_index | n_index | LOW |

---

**This matrix ensures full traceability for audit and parity verification.**
