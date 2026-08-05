# Validation Lab Report

## Summary
- **Total Tests:** 9
- **Passed:** 9
- **Failed:** 0

## Test Results

| Test | Status | Residual | DOF | Notes |
|------|--------|----------|-----|-------|
| UT1_phase_identity | PASS | 0.00e+00 | - |  |
| UT2_shear_identity | PASS | 0.00e+00 | - |  |
| UT3_forward_equivalence | PASS | 2.22e-16 | - |  |
| ST1_minimal_recovery | PASS | 1.00e-01 | 3 | theta_E err=0.0177, true={'theta_E': 1.0... |
| ST2_multi_source | PASS | 8.00e-02 | 9 | constraints=16, params=7 |
| ST3_noise_scaling | PASS | 0.00e+00 | - | residuals=['0.1000', '0.6667', '0.6724'] |
| CM1_alg_vs_scan | PASS | 1.00e-01 | - | phi_a=0.785, phi_b=0.000, res_a=0.1000, ... |
| RB1_dof_forbidden | PASS | 0.00e+00 | - | FORBIDDEN: 10 params > 8 constraints. Ne... |
| RB2_degeneracy | PASS | 0.00e+00 | - | ['DEGENERACY: 18 scan points within 10% ... |

## Diagnostics Legend
- **DOF Margin:** constraints - params (positive = overdetermined)
- **Residual:** max lens equation residual
- **Condition:** matrix condition number (high = ill-conditioned)