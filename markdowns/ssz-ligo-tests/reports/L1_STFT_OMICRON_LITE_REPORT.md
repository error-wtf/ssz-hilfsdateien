# L1 STFT Omicron-Lite Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 07:12:18

## Configuration
- STFT nperseg: 512 (125 ms)
- Overlap: 75%
- Hot tile threshold: +8.0 dB over off-source median
- Band: 20.0-210.0 Hz

## Results

| Det | Window | BP mean | Hot% | MaxCluster | TF Class |
|-----|--------|---------|------|------------|----------|
| H1 | TRIGGER | 2.049e-39 | 2.4% | 1 | SCATTERED_EXCESS |
| H1 | OFF_m500 | 3.553e-39 | 9.6% | 2 | SCATTERED_EXCESS |
| L1 | TRIGGER | 5.423e-39 | 21.6% | 2 | SCATTERED_EXCESS |
| L1 | OFF_m500 | 7.517e-39 | 20.8% | 18 | SINGLE_BURST_CANDIDATE |

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
