# Method → Test → Plot → Export Mapping

**Generated:** 2025-01-16  
**Version:** 1.0.0

---

## Core Methods

| Method ID | Tests | Plots | Export Fields |
|-----------|-------|-------|---------------|
| `schwarzschild_radius` | test_schwarzschild_sun, test_schwarzschild_earth | (component of all) | r_s_m, r_s_km |
| `xi_weak` | test_xi_weak_field, test_weak_regime_boundary | xi_and_dilation, regime_zones | Xi |
| `xi_strong` | test_xi_strong_field, test_xi_at_horizon | xi_and_dilation, regime_zones | Xi |
| `xi_blended` | test_blend_regime, test_blend_continuity | regime_zones | Xi |
| `xi_auto` | test_weak_regime_boundary, test_strong_regime_boundary | xi_profile | Xi, regime |
| `D_ssz` | test_D_ssz_finite_at_horizon, test_singularity_free | dilation_profile, gr_vs_ssz_comparison | D_ssz |
| `D_gr` | test_D_gr_singular_at_horizon | dilation_profile, gr_vs_ssz_comparison | D_gr |
| `find_intersection` | test_universal_intersection | universal_intersection | r_star_over_rs |

## Redshift Methods

| Method ID | Tests | Plots | Export Fields |
|-----------|-------|-------|---------------|
| `z_gravitational` | test_pound_rebka | redshift_breakdown | z_gr |
| `z_doppler` | (implicit) | redshift_breakdown | z_sr |
| `z_ssz_total` | test_ns_psr_j0740, test_ns_psr_j0348, test_ns_psr_j0030 | comparison_scatter, residuals_plot | z_ssz_total, z_ssz_grav |

## Validation Methods

| Method ID | Tests | Plots | Export Fields |
|-----------|-------|-------|---------------|
| `power_law_prediction` | test_power_law_fit, test_power_law_coefficient, test_power_law_exponent | power_law | E_norm_predicted |

## Analysis Methods

| Method ID | Tests | Plots | Export Fields |
|-----------|-------|-------|---------------|
| `delta_M` | (implicit in z_ssz) | - | delta_M_pct |
| `r_phi` | (implicit) | - | r_phi_m |

---

## Not Yet Implemented

| Method ID | Tests Needed | Plots Needed | Export Fields |
|-----------|--------------|--------------|---------------|
| `sigma` | test_sigma_formula | sigma_profile | sigma |
| `tau` | test_tau_formula | tau_profile | tau |
| `n_index` | test_refractive_index | n_profile | n_index |
| `dual_velocity` | test_dual_velocity_invariance | dual_velocity_plot | v_esc, v_fall |
| `euler_spiral` | test_euler_spiral | euler_spiral_plot | spiral_coords |
| `ppn_lensing` | test_lensing_deflection | lensing_plot | alpha_deflection |
| `ppn_shapiro` | test_shapiro_delay | shapiro_plot | dt_shapiro |
| `segment_saturation_derivative` | test_xi_derivative | xi_derivative_plot | dXi_dr |
| `metric_tensor_ssz` | test_metric_signature | metric_components | g_mu_nu |
| `einstein_tensor` | test_einstein_eqs | einstein_tensor_plot | G_mu_nu |
| `geodesic_equation` | test_geodesics | geodesic_plot | trajectory |

---

## Test → Method Dependencies

| Test Category | Required Methods |
|---------------|------------------|
| core_physics | schwarzschild_radius, xi_weak, xi_strong, D_ssz, D_gr, find_intersection |
| experimental_validation | D_ssz, xi_weak, z_gravitational |
| neutron_star_predictions | D_ssz, z_ssz_total |
| regime_classification | xi_auto, xi_blended |
| power_law | power_law_prediction |
| ssz_invariants | D_ssz, dual_velocity |
| edge_cases | schwarzschild_radius, D_ssz, xi_weak |
| qubit_applications | xi_weak, D_ssz |

---

## Plot → Method Dependencies

| Plot Category | Required Methods |
|---------------|------------------|
| core_theory | xi_weak, xi_strong, D_ssz, D_gr, find_intersection |
| experimental_validation | D_ssz, xi_weak, z_gravitational |
| empirical_analysis | power_law_prediction, z_ssz_total |
| single_object | xi_auto, D_ssz, D_gr, z_ssz_total |
| paper_plots | (various, many not implemented) |
| metric_visualization | metric_tensor_ssz, einstein_tensor |

---

## Export Field Reference

### Core Fields (always exported)
- `name` - Object identifier
- `M_Msun` - Mass in solar masses
- `R_km` - Radius in km
- `r_s_km` - Schwarzschild radius in km
- `r_over_rs` - Compactness ratio
- `regime` - weak/blended/strong

### SSZ Fields
- `Xi` - Segment density
- `D_ssz` - SSZ time dilation
- `z_ssz_grav` - SSZ gravitational redshift
- `z_ssz_total` - Total SSZ redshift

### GR Fields  
- `D_gr` - GR time dilation
- `z_gr` - GR gravitational redshift
- `z_grsr` - Combined GR×SR redshift

### Comparison Fields (when z_obs present)
- `z_obs` - Observed redshift
- `z_ssz_residual` - SSZ prediction error
- `z_grsr_residual` - GR×SR prediction error
- `ssz_closer` - Boolean: SSZ wins?

### Power Law Fields
- `E_norm_predicted` - Power law prediction
- `compactness` - r_s/R ratio

### Method Tracking
- `method_id` - Which calculation method used
- `run_id` - Unique run identifier

---

## Implementation Priority

### P1 - Core (DONE)
1. schwarzschild_radius ✅
2. xi_weak, xi_strong, xi_blended, xi_auto ✅
3. D_ssz, D_gr ✅
4. z_gravitational, z_doppler, z_ssz_total ✅
5. power_law_prediction ✅
6. find_intersection ✅

### P2 - Extended (TODO)
7. delta_M, r_phi
8. sigma, tau, n_index
9. dual_velocity
10. segment_saturation_derivative

### P3 - Advanced (TODO)
11. euler_spiral
12. ppn_lensing, ppn_shapiro
13. metric_tensor_ssz
14. einstein_tensor
15. geodesic_equation

---

*This mapping ensures full traceability from method → test → visualization → export.*
