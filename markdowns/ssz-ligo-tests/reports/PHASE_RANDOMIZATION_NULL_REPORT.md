# Phase Randomization Null Test Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 07:37:12

## Configuration
- N surrogates: 200
- Trigger GPS: 1411261107.984
- Window: 4.0s  Band: 20.0-210.0Hz
- Random seed: 42

## Interpretation
- BP_EXCEEDS_SURROGATES (>95th pctile): excess is in the ASD/PSD,
  not in phase structure. Consistent with spectral noise artifact.
- BP_CONSISTENT_WITH_SURROGATES: excess might have phase structure
  beyond what PSD alone contains.

## Results

| Det | Tag | Orig BP | Surr mean | BP quantile | BP Verdict |
|-----|-----|---------|-----------|-------------|------------|
| H1 | TRIGGER | 0.000e+00 | 0.000e+00 | 0.0% | BP_CONSISTENT_WITH_SURROGATES |
| H1 | OFF_m500 | 0.000e+00 | 0.000e+00 | 0.0% | BP_CONSISTENT_WITH_SURROGATES |
| L1 | TRIGGER | 0.000e+00 | 0.000e+00 | 0.0% | BP_CONSISTENT_WITH_SURROGATES |
| L1 | OFF_m500 | 0.000e+00 | 0.000e+00 | 42.5% | BP_CONSISTENT_WITH_SURROGATES |

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
