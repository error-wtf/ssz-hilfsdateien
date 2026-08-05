# H1/L1 Coherence Recheck — Robust PSD

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 22:58:06  
Follows: ROBUST_MULTIWINDOW_PSD_REPORT.md

## Background

The previous H1/L1 coherence run used a single off-source PSD window (-500s).
L1 showed bp_trigger/bp_off ~ 75000×, flagged as L1_PSD_WINDOW_NOT_REPRESENTATIVE.
This recheck uses the median of 5 windows.

## Robust PSD Window Inventory

See: `data_manifest/robust_psd_windows_used.csv`

## Coherence Metrics (Robust PSD)

| Metric | H1 | L1 |
|--------|-----|-----|
| PSD_status | PSD_WINDOWS_CONSISTENT | PSD_WINDOWS_CONSISTENT |
| n_windows_used | 4 | 5 |
| robust/single ratio | 1.010 | 0.980 |
| MF-SNR GR | 40.20 | 423.69 |
| delta_lnL (SSZ-GR) | 5.2378e-06 | -3.4332e-05 |
| bp_ratio (trigger/noise) | 412343.0 | 25849264.9 |

## Status

```
COHERENCE_STATUS:               COHERENCE_PARTIAL_SNR_ANOMALY
H1_L1_SNR_RATIO_ROBUST:         0.095
NEXT_STEP:                      Further PSD/DQ work if PARTIAL or BLOCKED
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
```
