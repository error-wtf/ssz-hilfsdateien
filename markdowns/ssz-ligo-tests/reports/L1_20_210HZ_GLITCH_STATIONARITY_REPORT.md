# L1 Glitch and Stationarity Diagnostic Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 22:21:22  
Band: 20.0–210.0 Hz | Trigger GPS: 1411261107.984  
No SSZ claims made.

## Purpose

Diagnose whether the L1 anomalous MF-SNR=647 is caused by:
1. A real (coherent) signal being stronger in L1
2. A glitch or non-stationary noise in the 20–210 Hz band
3. The off-source PSD window (-500s) not being representative

## Multi-Window PSD (bandpower in 20–210 Hz)

| Window | H1 [Hz⁻¹] | L1 [Hz⁻¹] | L1/H1 |
|--------|-----------|-----------|-------|
| minus500s | 1.492e-45 | 5.478e-46 | 0.37 |
| minus300s | 7.475e-46 | 3.946e-46 | 0.53 |
| minus100s | 1.434e-45 | 1.809e-45 | 1.26 |
| trigger (median slices) | 1.146e-41 | 4.150e-41 | 3.62 |

## Bandpower Ratio: trigger / off-source

| Detector | bp_trigger / bp_off(-500s) | MAD z-score | Classification |
|----------|--------------------------|-------------|----------------|
| H1 | 7683.3x | -0.6 | L1_OK_SIGNAL_LIKE |
| L1 | 75772.1x | 1.3 | L1_PSD_WINDOW_NOT_REPRESENTATIVE |

## Off-Source Stationarity

| Detector | Relative std of off-source windows | Assessment |
|----------|-----------------------------------|-----------|
| H1 | 0.276 | STABLE |
| L1 | 0.691 | VARIABLE |

## Root Cause Assessment

**L1 bp_ratio = 75772x** (trigger vs off-source at -500s)

Possible explanations in order of likelihood:
1. **Real signal**: L1 may simply have better SNR at this sky position.
   GW detectors have different antenna patterns — L1 can be significantly
   more sensitive depending on source direction.
2. **Non-stationarity in off-source window**: the -500s window was quiet
   but not representative of the trigger-window noise floor.
3. **Glitch in L1**: a noise transient in the 20–210 Hz band during
   the trigger window would inflate both MF-SNR and bandpower ratio.

**Key discriminator**: Compare bp_ratio across the three off-source windows.
If they are consistent (stable spread), explanation 1 or 3 is likely.
If they vary a lot, explanation 2 dominates.

## Final Gate

```
H1_STATUS:                         L1_OK_SIGNAL_LIKE
L1_STATUS:                         L1_PSD_WINDOW_NOT_REPRESENTATIVE
COHERENCE_GATE:                    COHERENCE_NEEDS_PSD_RECHECK
XCORR_STATUS:                      CORRELATED_NEEDS_INVESTIGATION (xcorr=0.368)
READY_FOR_REAL_LIGO_SSZ_CLAIM:     NO
SSZ_SUPPORT_CLAIM_MADE:            NO
SSZ_FALSIFICATION_CLAIM_MADE:      NO
```
