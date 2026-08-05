# QNM Ringdown Injection Sensitivity Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 21:49:33

## Purpose

Tests whether a QNM_FREQ_3PCT branch frequency shift would be distinguishable
from GR ringdown at GW240925 noise level.
This is a SENSITIVITY test only. No real ringdown signal is claimed.

## Anti-Circularity

- No posterior f_220, M_f, chi_f used
- f_220_GR computed from M_total (fixed physical prior, no posterior)
- PSD from H1 off-source Welch only
- Synthetic injection — not real ringdown strain

## Parameters

| Parameter | Value |
|-----------|-------|
| M_total | 20.4 Msun |
| f_220_GR (Schwarzschild, chi=0) | 152.6 Hz |
| tau_220_GR | 4.2 ms |
| Injected ringdown SNR | 55.97 |
| Est. ringdown SNR (analytic) | 13.50 |

## Frequency Resolution

- Analytic: delta_f/f ~ 1/(rho * 2*pi*f*tau) = 0.01%
- For 3% shift to be detectable: need rho > 3336.4

## Epsilon Scan Results

| epsilon | f_220_SSZ (Hz) | delta_f% | delta_lnL | Detectability |
|---------|---------------|----------|-----------|---------------|
| 0.0000 | 152.632 | 0.00% | 0.0000e+00 | UNDETECTABLE |
| 0.0100 | 154.158 | 1.00% | -8.0198e-02 | UNDETECTABLE |
| 0.0200 | 155.684 | 2.00% | -3.2181e-01 | UNDETECTABLE |
| 0.0300 | 157.211 | 3.00% | -7.2579e-01 | UNDETECTABLE |
| 0.0500 | 160.263 | 5.00% | -2.0207e+00 | MARGINAL |
| 0.1000 | 167.895 | 10.00% | -8.0195e+00 | DETECTABLE |
| 0.2000 | 183.158 | 20.00% | -3.0025e+01 | DETECTABLE |
| 0.3081 | 199.651 | 30.81% | -6.2764e+01 | DETECTABLE |
| 0.3100 | 199.948 | 31.00% | -6.3389e+01 | DETECTABLE |
| 0.3900 | 212.158 | 39.00% | -8.9080e+01 | DETECTABLE |

## 3% Branch Assessment

```
epsilon_220 = 0.03  (QNM_FREQ_3PCT_BRANCH, SSZ Book V51 Ch.30)
delta_lnL = -7.258e-01
detectability = UNDETECTABLE
analytic_freq_resolution = 0.01%
3pct_above_resolution = YES
ringdown_SNR_needed_for_3pct = 3336.4
actual_ringdown_SNR_est = 13.50
```

## Interpretation

- The injected ringdown SNR is low (~13.5)
- At this SNR, frequency resolution is ~0.0%
- A 3% shift is above the frequency resolution threshold
- This means: **even if SSZ predicts a 3% shift, GW240925 ringdown SNR
  may not be sufficient to distinguish it from GR**
- A stacking analysis across multiple events would be needed

## Final Gate

```
QNM_FREQ_3PCT_SENSITIVITY_RUN:     COMPLETE
QNM_3PCT_DETECTABLE_AT_GW240925:   UNDETECTABLE
RINGDOWN_STRAIN_OBSERVABLE_BUILT:  YES (synthetic injection only)
READY_FOR_REAL_RINGDOWN_TEST:      NO — insufficient SNR or MARGINAL
READY_FOR_REAL_LIGO_SSZ_CLAIM:     NO
SSZ_SUPPORT_CLAIM_MADE:            NO
SSZ_FALSIFICATION_CLAIM_MADE:      NO
```
