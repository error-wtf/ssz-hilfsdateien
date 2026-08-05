# Twist Branch Synthetic Comparison Report

Generated: 2026-05-18 22:29:28  
Status: DERIVED_V0_CONCEPTUAL  
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO  
No LIGO data used. No posterior parameters used. Synthetic only.

## Setup

| Parameter | Value |
|-----------|-------|
| Waveform | Synthetic Gaussian-chirp, 20–210 Hz |
| M_total (synthetic, not posterior) | 37 M_sun |
| r_s | 109292.27 m |
| Xi at r_ISCO | 0.1667 |
| SSZ scale V0 (D^2 at ISCO) | 0.734694 |
| F+/Fx H1 | 0.52/0.38 |
| F+/Fx L1 | 0.31/0.62 |
| Synthetic data | GR (no SSZ injected) |

Note: antenna patterns and mass are NOT from GW240925 posterior.
They are fixed round numbers for the synthetic distinguishability test only.

## Model Comparison (lnL relative to GR)

| Model | delta_lnL vs GR | Residual H1 | Residual L1 |
|-------|----------------|-------------|-------------|
| GR (reference) | 0.000 | 0.0000 | 0.0000 |
| scale-only | -7.0158 | 0.2653 | 0.2653 |

Scale-only reduces lnL by 7.02 relative to GR.
This is the cost of SSZ amplitude suppression with no twist.

## Constant Theta Scan

| theta [rad] | dlnL vs GR | dlnL vs scale | H1/L1 ratio Δ | res H1 | res L1 | Detectable vs scale |
|------------|------------|--------------|--------------|--------|--------|---------------------|
| 0.001 | -6.993 | 0.023 | -0.0003 | 0.2650 | 0.2648 | UNDETECTABLE |
| 0.010 | -6.797 | 0.219 | -0.0034 | 0.2618 | 0.2600 | UNDETECTABLE |
| 0.050 | -6.089 | 0.927 | -0.0178 | 0.2497 | 0.2431 | UNDETECTABLE |
| 0.100 | -5.573 | 1.443 | -0.0371 | 0.2387 | 0.2328 | UNDETECTABLE |

## Physics Proxy Theta Forms

| Form | theta [rad] | dlnL vs scale | Detectable |
|------|------------|--------------|-----------|
| xi_proxy | 0.1667 | 1.533 | UNDETECTABLE |
| rsg_proxy | 0.0556 | 1.004 | UNDETECTABLE |

## H1/L1 Distinguishability

The key observable is the **H1/L1 amplitude ratio change** under twist.
Because H1 and L1 have different antenna patterns (F+/Fx), a polarisation
rotation produces a *detector-specific* change in strain, unlike a scalar
scale that affects both detectors identically.

H1/L1 ratio (GR):    1.2630

Under twist, this ratio changes:

| theta [rad] | H1/L1 ratio | Delta |
|------------|------------|-------|
| 0 (GR) | 1.2630 | 0 |
| 0.001 | 1.2627 | -0.0003 |
| 0.010 | 1.2596 | -0.0034 |
| 0.050 | 1.2452 | -0.0178 |
| 0.100 | 1.2259 | -0.0371 |

The H1/L1 ratio changes because the rotation mixes h+ and hx differently
into each detector's F+/Fx projection. This is the distinctive signature
of a twist compared to a scalar scale factor.

## Detectability Threshold

Threshold for |delta_lnL vs scale| >= 8 (DETECTABLE): **>0.1 rad (not reached in scan)**

Interpretation:
- theta < 0.001 rad: twist indistinguishable from scale-only
- theta ~ 0.01–0.1 rad: marginal to detectable vs scale-only
- The H1/L1 ratio change is the cleanest discriminator

## What Would Constitute Interesting Evidence

```
NOT a claim — conceptual threshold only:

If:  scale-only fits poorly (dlnL_scale << 0)
AND: twist model improves match with theta > threshold
AND: H1/L1 ratio change matches observed H1/L1 residual difference
THEN: twist branch warrants further investigation
NEVER: this constitutes an SSZ support claim
```

## Anti-Circularity Check

- [x] No posterior f, m, chi used
- [x] No LIGO strain data used
- [x] No SSZ claim made
- [x] Synthetic data = GR (conservative, no SSZ injected)
- [x] Theta values fixed by sensitivity scan, not fitted to data
- [x] Status locked: DERIVED_V0_CONCEPTUAL

## Gate Status

```
TWIST_BRANCH_STATUS:            DERIVED_V0_CONCEPTUAL
THETA_DERIVED_FROM_SPIN_CONN:   NO (placeholder forms only)
SYNTHETIC_TEST:                 COMPLETE
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```
