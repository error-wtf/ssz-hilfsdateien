# L1 Anomaly Diagnostic Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18 21:52:53

## Purpose
Diagnose why L1 MF-SNR=647 and xcorr>1 appeared in the H1/L1 pipeline.
No SSZ claim is made.

## H1 / L1 Strain Window Statistics

| Window | H1 RMS | L1 RMS | L1/H1 | Notes |
|--------|--------|--------|-------|-------|
| on | 2.727e-18 | 4.236e-18 | 1.55 | OK |
| pre | 5.060e-18 | 3.288e-18 | 0.65 | OK |
| post | 3.682e-18 | 3.206e-18 | 0.87 | OK |
| off | 4.092e-18 | 3.370e-18 | 0.82 | OK |

## H1 Anomalies
- Status: MINOR_ANOMALY
- Anomalies: ['POSSIBLE_CLIPPING']
- MF-SNR GR: 44.20

## L1 Anomalies
- Status: NOISE_ANOMALY
- Anomalies: ['POSSIBLE_CLIPPING', 'MF_SNR_GR_ANOMALOUS (647)']
- MF-SNR GR: 646.94
- RMS ratio on/off: 1.26

## Root Cause Analysis

**L1 MF-SNR anomaly:**
- MF-SNR depends on off-source PSD as noise estimator
- If off-source window (-500s) is quiet but trigger window is loud,
  the PSD underestimates the true noise → inflated SNR
- L1 trigger window RMS / off-source RMS ratio reveals this
- This is a noise non-stationarity issue, NOT an SSZ effect

**xcorr > 1 root cause:**
- Previous pipeline used: xcorr = correlate(a/std(a), b/std(b)) / n
- std-normalisation does NOT guarantee output in [-1,1]
  for non-stationary or impulsive signals
- Correct formula: xcorr = dot(a,b) / sqrt(dot(a,a)*dot(b,b))
  (Cauchy-Schwarz, guaranteed in [-1,1])

## Corrected Cross-Correlation

- Method: Cauchy-Schwarz normalisation
- xcorr_corrected = 0.368039
- lag = -3252 samples
- XCORR_STATUS: CORRELATED_NEEDS_INVESTIGATION

## Final Gate
```
H1_STATUS:                      MINOR_ANOMALY
L1_STATUS:                      NOISE_ANOMALY
XCORR_STATUS:                   CORRELATED_NEEDS_INVESTIGATION
COHERENCE_TEST_VALID:           PENDING (depends on L1_STATUS)
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```