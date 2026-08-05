# Robust Multi-Window PSD Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 22:58:06  
Event: GW240925 (trigger GPS 1411261107.984)  
No LIGO claim. No posterior. No SSZ support/falsification.

## Motivation

Previous diagnostics showed L1 bp_trigger/bp_off ~ 75000× using a single
-500s off-source window. This suggests the -500s window is too quiet to
be representative. We re-estimate the PSD using 5 windows
centred at offsets [-500.0, -300.0, -100.0, 100.0, 300.0] s from trigger, each 64.0s long.
The robust PSD is the **median** across available windows.

## H1 Results

| Quantity | Value |
|---------|-------|

| PSD status | PSD_WINDOWS_CONSISTENT |
| n windows used | 4 |
| PSD_robust band median | 2.8434e-47 1/Hz |
| PSD_single (minus500) band median | 2.8164e-47 1/Hz |
| robust/single ratio | 1.010 |
| MF-SNR GR (robust PSD) | 40.20 |
| MF-SNR SSZ (robust PSD) | 9.89 |
| lnL_GR | -3.2918e+07 |
| lnL_SSZ | -3.2918e+07 |
| delta_lnL | 5.2378e-06 |
| bp_trigger | 2.2276e-39 |
| bp_noise_estimate | 5.4024e-45 |
| bp_trigger/bp_noise | 412343.0 |
| SNR_STATUS | OK |


## L1 Results

| Quantity | Value |
|---------|-------|

| PSD status | PSD_WINDOWS_CONSISTENT |
| n windows used | 5 |
| PSD_robust band median | 1.9212e-47 1/Hz |
| PSD_single (minus500) band median | 1.9598e-47 1/Hz |
| robust/single ratio | 0.980 |
| MF-SNR GR (robust PSD) | 423.69 |
| MF-SNR SSZ (robust PSD) | 179.44 |
| lnL_GR | -1.5718e+10 |
| lnL_SSZ | -1.5718e+10 |
| delta_lnL | -3.4332e-05 |
| bp_trigger | 9.4356e-38 |
| bp_noise_estimate | 3.6502e-45 |
| bp_trigger/bp_noise | 25849264.9 |
| SNR_STATUS | ANOMALOUS_HIGH_SNR |


## H1/L1 Coherence (Robust PSD)

| Quantity | Value |
|---------|-------|
| H1/L1 MF-SNR ratio | 0.095 |
| H1 PSD consistency | PSD_WINDOWS_CONSISTENT |
| L1 PSD consistency | PSD_WINDOWS_CONSISTENT |
| COHERENCE_STATUS | COHERENCE_PARTIAL_SNR_ANOMALY |

## Interpretation

The key question: does the robust multi-window PSD give a stable,
representative noise floor, and do H1/L1 SNRs become consistent?

- If `PSD_WINDOWS_CONSISTENT`: the noise floor is stable across time;
  single-window anomaly was real, robust PSD is trusted.
- If `PSD_WINDOW_NOT_REPRESENTATIVE`: the noise floor varies significantly,
  meaning the previous single-window SNR/lnL values were not reliable.
  Further data quality work is needed before SSZ interpretation.

## Gate Status

```
PSD_ROBUST_RECHECK:             COHERENCE_PARTIAL_SNR_ANOMALY
H1_PSD_STATUS:                  PSD_WINDOWS_CONSISTENT
L1_PSD_STATUS:                  PSD_WINDOWS_CONSISTENT
H1_SNR_STATUS:                  OK
L1_SNR_STATUS:                  ANOMALOUS_HIGH_SNR
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```
