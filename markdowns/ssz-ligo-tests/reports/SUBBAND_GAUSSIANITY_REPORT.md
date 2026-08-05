# Sub-band Gaussianity Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 07:44:36

## Configuration
- Trigger GPS: 1411261107.984
- Window: 4.0s
- Sub-bands: ['20-40', '40-80', '80-120', '120-160', '160-210']
- Whitening: off-source PSD (64.0s at -500.0s)
- Filter order: 8 (Butterworth, sosfiltfilt)

## L1 Trigger — Sub-band Summary

| Band | Excess Kurt | Skew | |z|>4 | L1/H1 | Class |
|------|-------------|------|-------|-------|-------|
| 20-40 | +44.857 | -2.032 | 232 | N/A | STRONGLY_NON_GAUSSIAN |
| 40-80 | -0.515 | +0.000 | 0 | N/A | BORDERLINE |
| 80-120 | +3.266 | -0.000 | 77 | N/A | STRONGLY_NON_GAUSSIAN |
| 120-160 | +5.663 | -0.000 | 69 | N/A | STRONGLY_NON_GAUSSIAN |
| 160-210 | +0.198 | +0.000 | 15 | N/A | GAUSSIAN |

## H1 Trigger — Sub-band Summary

| Band | Excess Kurt | Skew | |z|>4 | Class |
|------|-------------|------|-------|-------|
| 20-40 | +3.673 | -0.323 | 94 | STRONGLY_NON_GAUSSIAN |
| 40-80 | +0.340 | +0.007 | 0 | BORDERLINE |
| 80-120 | +2.386 | +0.001 | 59 | STRONGLY_NON_GAUSSIAN |
| 120-160 | +1.252 | +0.001 | 35 | STRONGLY_NON_GAUSSIAN |
| 160-210 | +0.405 | +0.000 | 16 | GAUSSIAN |

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
