# Calibration/PSD Sensitivity Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18 21:30:09

## Purpose
Check whether the SSZ V1 inspiral effect is distinguishable from
calibration and PSD estimation uncertainty.
No physics claim is made. READY_FOR_REAL_CLAIM: NO

## Nominal Result
| Model | lnL | delta_lnL |
|-------|-----|-----------|
| GR control 0PN | -3.2372e+07 | — |
| SSZ V1 0PN | -3.2372e+07 | 6.3404e-06 |

## Amplitude Calibration Scan (±3%, ±5%)
| amp_error | delta_lnL | diff_vs_nominal |
|-----------|-----------|-----------------|
| +0.000 | 6.340444e-06 | 0.000000e+00 |
| +0.030 | 6.381422e-06 | 4.097819e-08 |
| -0.030 | 6.299466e-06 | -4.097819e-08 |
| +0.050 | 6.411225e-06 | 7.078052e-08 |
| -0.050 | 6.273389e-06 | -6.705523e-08 |

## Phase Calibration Scan (±0.01 rad, ±0.05 rad)
| phase_error | delta_lnL | diff_vs_nominal |
|-------------|-----------|-----------------|
| +0.000 | 6.340444e-06 | 0.000000e+00 |
| +0.010 | 6.329268e-06 | -1.117587e-08 |
| -0.010 | 6.351620e-06 | 1.117587e-08 |
| +0.050 | 6.284565e-06 | -5.587935e-08 |
| -0.050 | 6.396323e-06 | 5.587935e-08 |

## PSD Welch Variant Scan
| nperseg | delta_lnL | diff_vs_nominal |
|---------|-----------|-----------------|
| nperseg=2048 | 2.175570e-06 | -4.164875e-06 |
| nperseg=4096 | 6.340444e-06 | 0.000000e+00 |
| nperseg=8192 | 2.875924e-05 | 2.241880e-05 |

## Sensitivity Assessment
- SSZ effect |delta_lnL|: 6.3404e-06
- Max calibration spread: 7.0781e-08
- SSZ_EFFECT_ABOVE_CALIBRATION: YES — SSZ effect exceeds calibration spread

## Final Gate
```
SSZ_EFFECT_ABOVE_CALIBRATION:  YES — SSZ effect exceeds calibration spread
CALIBRATION_SCAN:              COMPLETE
PSD_VARIANT_SCAN:              COMPLETE
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```
