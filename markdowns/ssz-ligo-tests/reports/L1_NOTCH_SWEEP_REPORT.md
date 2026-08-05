# L1 Notch Sweep Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 07:30:11

## Configuration
- Trigger GPS: 1411261107.984
- Window: 4.0s  Band: 20.0-210.0Hz
- Notch width: +/-1.5Hz per peak
- N notch steps: [0, 1, 3, 5, 10, 20]

## L1/H1 Ratio Sweep

| N notched | H1 BP | L1 BP | L1/H1 ratio | L1 remaining |
|-----------|-------|-------|-------------|--------------|
| 0 | 1.468e-43 | 2.712e-43 | 1.848 | 100.0% |
| 1 | 1.466e-43 | 2.625e-43 | 1.790 | 96.8% |
| 3 | 5.255e-44 | 2.621e-43 | 4.989 | 96.7% |
| 5 | 5.228e-44 | 9.386e-44 | 1.795 | 34.6% |
| 10 | 1.842e-44 | 5.671e-44 | 3.078 | 20.9% |
| 20 | 1.676e-44 | 5.384e-44 | 3.213 | 19.9% |

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
