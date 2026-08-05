# GW250207 Artifact Gate — Cross-Event Comparison

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 07:58:49

## Events
- GW240925 GPS: 1411261107.984
- GW250207 GPS: 1422964625.26

## Configuration
- Band: 20.0-210.0 Hz  Window: 4.0s
- Stationarity: +-500.0s in 4s steps
- Known lines notched: [60.0, 120.0, 180.0, 16.0, 32.0, 48.0, 35.9, 36.7]

## Comparison Table

| Metric | GW240925 | GW250207 |
|--------|----------|----------|
| L1/H1 BP ratio | 1.5639 | N/A |
| L1 stationarity quantile (%) | 74.5000 | N/A |
| H1 stationarity quantile (%) | 10.3000 | N/A |
| L1 line fraction | 0.0465 | N/A |
| H1/L1 coherence | 0.0561 | N/A |
| Cross-phase stability R | 0.9115 | N/A |
| Mean cross-phase (deg) | -167.0200 | N/A |

## Interpretation
- L1/H1 ratio < 1.5 and L1-Q < 90%: cleaner event
- L1/H1 ratio > 2.0 or L1-Q > 95%: L1 excess, gate FAIL

## GW250207 Strain Data
- Required: O4b 4kHz HDF5, 4096s block at GPS 1422964096
- Download: run `scripts/download_gw250207_strain.py`
- GWOSC: https://gwosc.org/events/GW250207_115645/

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
