# Residual and Log-Likelihood Report
Generated: {NOW}

## Computation
- FFT length: {len(strain)} samples
- df: {float(fs)/len(strain):.6f} Hz
- Band: {F_LOW}–{F_HIGH} Hz

## Log-Likelihood (noise-weighted inner product)
| Model | lnL | MF-SNR | Residual RMS |
|-------|-----|--------|--------------|
| GR control (0PN) | {stats['lnL_gr']:.4e} | {stats['snr_gr']:.2f} | {stats['res_gr_rms']:.3e} |
| SSZ DERIVED_V1    | {stats['lnL_ssz']:.4e} | {stats['snr_ssz']:.2f} | {stats['res_ssz_rms']:.3e} |

**delta_lnL (SSZ - GR) = {stats['delta_lnL']:.4e}**

## Interpretation
- |delta_lnL| < 1: INDISTINGUISHABLE
- GR control is 0PN only (GR_CONTROL_TEMPLATE_LIMITED)
- SSZ uses DERIVED_V1 via derived_waveform.py (SSZ_FORWARD_DERIVED_V1)
- Neither result constitutes a physics claim

## Mandatory Statements
```
READY_FOR_REAL_SSZ_CLAIM:      NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
POSTERIOR_RF_TEST:             INVALID_FOR_SSZ
```

## Status
**PASS_NUMERICAL** — residuals and lnL computed without error
