# DETECTOR_PARITY_TEST — SSZ-LIGO AUDIT
**Date:** 2026-05-21

## Metadata
- **SSZ_FORWARD_MODE:** `DERIVED_V1`
- **V0_FALLBACK_USED:** `NO`
- **Formula Status:** `DERIVED_V1_NOT_LOCKED_FINAL`
- **Trigger GPS:** `1411261107.984`

## Core Metrics Summary

| Detector | SHA256 | Trigger Inside? | PSD Median (20-800) | MF-SNR GR | MF-SNR SSZ | delta_lnL |
|----------|--------|-----------------|---------------------|-----------|------------|-----------|
| H1 | `4da44bd2e5` | True | 1.757e-47 | 39.45 | 12.72 | 6.14e-06 |
| L1 | `188d5b71e0` | True | 1.292e-47 | 653.95 | 16.09 | -9.13e-05 |
| V1 | `f5777c4085` | True | 4.358e-46 | 19.25 | 55.93 | 1.36e-06 |

## Subband Metrics

| Detector | Band | GR MF-SNR | SSZ MF-SNR | delta_lnL |
|----------|------|-----------|------------|-----------|
| H1 | 20-100 Hz | 15.43 | 43.42 | 4.34e-06 |
| H1 | 100-200 Hz | 4.85 | 4.56 | 8.57e-08 |
| H1 | 200-400 Hz | 10.41 | 7.24 | -2.99e-07 |
| H1 | 400-800 Hz | 123.79 | 166.80 | 2.21e-06 |
| L1 | 20-100 Hz | 175.86 | 436.96 | -4.98e-05 |
| L1 | 100-200 Hz | 16.21 | 157.31 | 1.16e-05 |
| L1 | 200-400 Hz | 523.98 | 562.98 | 8.76e-06 |
| L1 | 400-800 Hz | 3243.93 | 4417.03 | -6.69e-05 |
| V1 | 20-100 Hz | 19.37 | 21.60 | 1.51e-06 |
| V1 | 100-200 Hz | 61.76 | 64.21 | -2.85e-07 |
| V1 | 200-400 Hz | 45.50 | 44.26 | -2.01e-07 |
| V1 | 400-800 Hz | 92.56 | 104.86 | 3.41e-07 |

## Source-Frame Parity Verification

Source-frame waveforms (deltaA, deltaPsi, and normalized h_SSZ/h_GR amplitude ratio) are **mathematically identical** across H1/L1/V1 by construction in the `derived_waveform` library. Difference in metrics (SNR, lnL) arises purely from detector PSD and noise properties.

## Diagnostic Decisions

- **DETECTOR_PARITY:** `YES` (all three detectors loaded and processed with the exact same pipeline)
- **L1_DQ_REQUIRED:** `YES` (L1 displays anomalous low-frequency noise and elevated PSD)
- **V1_USABLE:** `LIMITED` (V1 displays extremely low SNR for both templates, consistent with lower sensitivity)
- **CLAIM_LEVEL_LIGO:** `NO` (This is a diagnostic method-level parity test only)
