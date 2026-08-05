# Unit & Normalization Audit

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 08:07:49

## Configuration
- FS=4096.0 Hz  DUR=16.0s  NPERSEG=4096  df=1.0000 Hz
- Injection: A=1.000e-21 strain  f0=100.0 Hz  window=hann
- Tolerance: 5%

## Results

| Test | Status | Error % | Ratio |
|------|--------|---------|-------|
| psd_peak_normalization | PASS | 0.024 | 1.000244 |
| bandpower_integration | PASS | 0.000 | 1.000000 |
| asd_normalization | PASS | 0.012 | 1.000122 |
| window_power_correction | PASS | 0.024 | N/A |
| onesided_vs_twosided | PASS | 0.000 | N/A |
| rfft_normalization | PASS | N/A | 1.000000 |
| real_strain_units | PASS | N/A | N/A |

## Normalization Conventions Used
- `scipy.signal.welch`: one-sided, density scaling
  `S(f) * df = power in bin`, `integral = var(x)`
- `np.fft.rfft`: `X[k] = sum(x * exp(-2pi*i*k*n/N))`
  one-sided PSD: `S(f) = 2|X(f)|^2 / (N * fs)`
- Hann window power correction: `sum(w^2)/N = 0.375`
  Applied automatically by scipy.welch in density mode.

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
