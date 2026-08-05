# H1/L1 Long-Baseline Replication Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Status:** PENDING — run `python scripts/run_h1_l1_long_baseline_replication.py` to populate.

## Purpose

Determine whether the strong H1/L1 anti-correlation (abs_corr=0.991 at dt=0 ms) is:

```text
TRIGGER_SPECIFIC:           abs_corr elevated above off-source population (Z >= 3)
CONSISTENT_WITH_OFFSOURCE:  abs_corr normal within off-source distribution
BELOW_OFFSOURCE:            abs_corr lower than off-source mean
INCONCLUSIVE:               insufficient statistics
```

## Key Interpretation Rule

A high |corr| at the trigger is only meaningful if it is statistically
stronger than comparable off-source windows processed in the same way.

## Configuration

```text
Trigger GPS:          1411261107.984
Off-source range:     +/- 1000 s
Safety exclusion:     +/- 64 s
Off-source windows:   50-100 per trigger duration
Trigger durations:    4, 8, 16, 32 s
Subbands:             20-40, 40-80, 80-120, 120-160, 160-210, 20-210 Hz
Peak detection:       argmax(|C(tau)|) -- sign-convention-safe
Physical delay range: |dt| <= 10.012 ms
```

## Results

Run not yet executed. See data_manifest/h1_l1_xcorr_quantiles.csv after run.

## Anti-Circularity

```text
No PE/QNM posteriors used.
No Kerr/SSZ parameters used.
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```
