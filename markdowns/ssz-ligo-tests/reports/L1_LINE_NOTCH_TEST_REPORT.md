# L1 Line / Notch Test Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 07:11:55

## Configuration
- Trigger GPS: 1411261107.984
- Window: 4.0s
- Band: 20.0-210.0 Hz
- Peak threshold: +6.0 dB over local median
- Notch width: +/-2.0 Hz per peak

## Bandpower Summary

| Det | Window | BP full | BP notched | In-line % | N peaks | Structure |
|-----|--------|---------|------------|-----------|---------|-----------|
| H1 | TRIGGER | 1.468e-43 | 6.488e-44 | 55.8% | 2 | LINE_DOMINATED |
| L1 | TRIGGER | 2.712e-43 | 1.201e-43 | 55.7% | 4 | LINE_DOMINATED |
| L1 | OFF_m500 | 3.083e-43 | 1.422e-43 | 53.9% | 3 | LINE_DOMINATED |

## Peak List

| Det | Window | Freq (Hz) | Height (dB) | Classification |
|-----|--------|-----------|-------------|----------------|
| H1 | TRIGGER | 20.00 | +8.8 | UNKNOWN |
| H1 | TRIGGER | 177.00 | +6.4 | UNKNOWN |
| L1 | TRIGGER | 20.00 | +7.4 | UNKNOWN |
| L1 | TRIGGER | 60.00 | +17.0 | KNOWN_LINE:mains_60@60.0Hz |
| L1 | TRIGGER | 120.00 | +6.8 | KNOWN_LINE:mains_120@120.0Hz |
| L1 | TRIGGER | 180.00 | +6.9 | KNOWN_LINE:mains_180@180.0Hz |
| L1 | OFF_m500 | 20.00 | +7.4 | UNKNOWN |
| L1 | OFF_m500 | 60.00 | +13.5 | KNOWN_LINE:mains_60@60.0Hz |
| L1 | OFF_m500 | 180.00 | +6.3 | KNOWN_LINE:mains_180@180.0Hz |

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
