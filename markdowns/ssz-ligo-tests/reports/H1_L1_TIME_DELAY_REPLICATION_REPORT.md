# H1/L1 Time-Delay Replication Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 10:35:43

## Configuration
- Trigger GPS: 1411261107.984
- Window: 4.0s
- Coarse scan: +/-50.0ms step=1.0ms
- Fine scan: +/-10.0ms step=0.244ms
- Physical range: |dt| <= 10.012ms
- Sign-flip test: +L1 and -L1

## Subbands
| Band | f_lo | f_hi |
|------|------|------|
| 20-40 | 20.0 | 40.0 |
| 40-80 | 40.0 | 80.0 |
| 80-120 | 80.0 | 120.0 |
| 120-160 | 120.0 | 160.0 |
| 160-210 | 160.0 | 210.0 |
| 20-210 | 20.0 | 210.0 |

## Final Classification
| Key | Value |
|-----|-------|
| H1_L1_REPLICATION_STATUS TRIGGER (20-210 Hz) | COHERENT_WITH_SIGN_FLIP |
| H1_L1_REPLICATION_STATUS TRIGGER (20-40 Hz) | COHERENT_WITH_SIGN_FLIP |
| H1_L1_REPLICATION_STATUS OFF_m500 (20-210 Hz) | COHERENT_WITH_SIGN_FLIP |
| H1_L1_REPLICATION_STATUS OFF_m500 (20-40 Hz) | COHERENT_WITH_SIGN_FLIP |
| BEST_DELAY | 0 ms |
| BEST_ABS_CORR | 0.991 |
| SIGN_RELATION | OPPOSITE_SIGN (physically expected) |
| PREVIOUS_DT_MINUS_10MS_RESULT | CLASSIFICATION_ARTIFACT |
| TRIGGER_SPECIFIC | PENDING — subband abs-corr run required |
| L1_20_40_STATUS | DQ_CONTEXT_REQUIRED — subband coherence pending |

## Subband Verdicts
| Band | TRIGGER | OFF_m500 |
|------|---------|----------|
| 20-40 Hz | PHYSICAL_DELAY_COHERENT | PHYSICAL_DELAY_COHERENT |
| 40-80 Hz | PHYSICAL_DELAY_COHERENT | PHYSICAL_DELAY_COHERENT |
| 80-120 Hz | PHYSICAL_DELAY_COHERENT | PHYSICAL_DELAY_COHERENT |
| 120-160 Hz | PHYSICAL_DELAY_COHERENT | PHYSICAL_DELAY_COHERENT |
| 160-210 Hz | PHYSICAL_DELAY_COHERENT | PHYSICAL_DELAY_COHERENT |
| 20-210 Hz | PHYSICAL_DELAY_COHERENT | PHYSICAL_DELAY_COHERENT |

## NOTE: Sign Convention

Peak detection uses argmax(|C(tau)|), not argmax(C(tau)).
H1/L1 have opposite arm orientations — negative correlation at correct delay
is physically expected, not a failure of coherence.

corr(dt=0 ms) = -0.991  -->  abs(corr) = 0.991 (strong match)

The previous classification PERSISTENT_SYSTEMATIC was a classification artifact
from using argmax(corr). Under argmax(|corr|) the full-band coherence is confirmed.

Trigger-specificity of individual subbands (especially 20-40 Hz) requires
the subband abs-correlation run. See reports/H1_L1_SUBBAND_REPLICATION_REPORT.md

**This result does not yet support a GW signal claim or SSZ claim.**
Subband coherence and DQ/Omicron/iDQ context are still required for 20-40 Hz.

## Interpretation Key
- PHYSICAL_DELAY_COHERENT: peak |xcorr| at |dt|<=10ms,
  SNR>5 vs unphysical range noise floor
- L1_ONLY_STRUCTURE: no physical peak, SNR<2
- UNPHYSICAL_DELAY_PREFERRED: peak outside physical range
- INCONCLUSIVE: ambiguous evidence
- SYSTEMATIC_SATURATION: xcorr saturated at scan boundary

## Anti-Circularity
- No PE/QNM posteriors used
- No Kerr/SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
