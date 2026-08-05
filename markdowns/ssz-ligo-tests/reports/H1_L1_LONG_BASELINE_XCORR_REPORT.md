# H1/L1 Long-Baseline Cross-Correlation Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

**Generated: 2026-05-19 16:00:04.350307**

## Executive Summary

| Metric | Value |
|--------|-------|
| Total delay-scan rows | 2208 |
| Bands analyzed | 6 |
| Windows | TRIGGER, OFF_m500 |
| Best abs(corr) TRIGGER | 0.999869 |
| Best abs(corr) OFF_m500 | 0.999955 |

## Trigger vs Off-Source by Band

| band    |   trig_abs_corr |   percentile |
|:--------|----------------:|-------------:|
| 120-160 |        0.999869 |            0 |
| 160-210 |        0.999445 |            0 |
| 20-210  |        0.995873 |            0 |
| 20-40   |        0.999817 |          100 |
| 40-80   |        0.99965  |            0 |
| 80-120  |        0.999618 |            0 |

## Classification

**H1_L1_XCORR_TRIGGER_STATUS:**
- 20-40 Hz: TRIGGER_SPECIFIC (percentile=100)
- 40-80 Hz: BELOW_OFFSOURCE (percentile=0)
- 80-120 Hz: BELOW_OFFSOURCE (percentile=0)
- 120-160 Hz: BELOW_OFFSOURCE (percentile=0)
- 160-210 Hz: BELOW_OFFSOURCE (percentile=0)
- 20-210 Hz total: BELOW_OFFSOURCE (percentile=0)

**READY_FOR_REAL_LIGO_SSZ_CLAIM:** NO
**Reason:** Only 20-40 Hz shows trigger-specific coherence; other bands show higher off-source correlation. Total band non-trigger-specific.

## Gate Status

`
[X] Long-baseline xcorr computed
[X] Quantiles calculated
[X] Trigger-specificity evaluated
[ ] Extended off-source baseline (-1000s to +1000s, 50+ windows) - PARTIAL (only 1 off-source window available)
[ ] Phase coherence analysis
[ ] Time-shift null test
`

## Files Generated
- data_manifest/h1_l1_long_baseline_xcorr.csv
- data_manifest/h1_l1_xcorr_quantiles.csv
- reports/H1_L1_LONG_BASELINE_XCORR_REPORT.md (this file)
