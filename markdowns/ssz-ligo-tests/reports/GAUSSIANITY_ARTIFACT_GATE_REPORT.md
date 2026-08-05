# Gaussianity Artifact Gate Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 06:57:36

## Configuration
- Trigger GPS: 1411261107.984
- Window: 4.0s
- PSD source: -500.0s x 64.0s
- Band: 20.0-210.0 Hz
- Whitening: PSD-division in frequency domain

## Statistics Table (20-210 Hz bandpassed)

| Det | Tag | Band | std | ex_kurt | |z|>4 obs/exp | |z|>5 obs/exp | AD |
|-----|-----|------|-----|---------|--------------|----------|-----|
| H1 | TRIGGER | 20.0-210.0Hz | 1.0000 | +2.605 | 36 / 1 | 15 / 0 | FAIL |
| H1 | OFF_m500 | 20.0-210.0Hz | 1.0000 | +6.375 | 91 / 1 | 24 / 0 | FAIL |
| H1 | OFF_m300 | 20.0-210.0Hz | 1.0000 | +6.334 | 91 / 1 | 28 / 0 | FAIL |
| L1 | TRIGGER | 20.0-210.0Hz | 1.0000 | +4.582 | 74 / 1 | 29 / 0 | FAIL |
| L1 | OFF_m500 | 20.0-210.0Hz | 1.0000 | +2.856 | 66 / 1 | 19 / 0 | FAIL |
| L1 | OFF_m300 | 20.0-210.0Hz | 1.0000 | +4.560 | 75 / 1 | 33 / 0 | FAIL |
| L1 | OFF_m100 | 20.0-210.0Hz | 1.0000 | +4.524 | 69 / 1 | 28 / 0 | FAIL |

## Classification
- H1_GAUSSIANITY: **STRONGLY_NON_GAUSSIAN**
- L1_GAUSSIANITY: **STRONGLY_NON_GAUSSIAN**
- L1_EXCESS_CLASS: **CHRONIC_NON_GAUSSIAN_BAND_NOISE**

## Artifact Gate
**GAUSSIANITY_ARTIFACT_GATE: FAIL_L1_NON_GAUSSIAN**

## Anti-Circularity
- No SSZ parameters used
- No posterior data (f, m, chi) used
- No QNM posterior used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
