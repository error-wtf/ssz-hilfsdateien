# GW250207 Artifact Gate Comparison

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 08:27:50

## Events
- GW240925 GPS: 1411261107.984
- GW250207 GPS: 1422964625.26

## Pipeline Configuration
- Band: 20.0-210.0 Hz  Window: 4.0s
- Stationarity: +-500.0s  Known lines: [60.0, 120.0, 180.0, 16.0, 32.0, 48.0, 35.9, 36.7]
- Sub-bands: ['20-40', '40-80', '80-120', '120-160', '160-210']
- Phase-rand N=100

## Comparison Table

| Metric | GW240925 | GW250207 | Flag |
|--------|----------|----------|------|
| L1/H1 BP ratio | 1.564 | N/A |  |
| L1 stationarity Q % | 74.500 | N/A |  |
| H1 stationarity Q % | 10.300 | N/A |  |
| L1 line fraction | 0.046 | N/A |  |
| H1/L1 coherence | 0.056 | N/A |  |
| Cross-phase R | 0.911 | N/A |  |
| L1 20-40Hz ex_k | 44.857 | N/A |  |
| L1 40-80Hz ex_k | -0.515 | N/A |  |
| L1 80-120Hz ex_k | 3.266 | N/A |  |
| L1 120-160Hz ex_k | 5.663 | N/A |  |
| L1 160-210Hz ex_k | 0.198 | N/A |  |
| H1 20-40Hz ex_k | 3.673 | N/A |  |
| L1 phase-rand kurtosis Q% | 60.000 | N/A |  |

## Classification: GW250207_STATUS = MISSING_DATA

> GW250207 strain files not available. Run scripts/download_gw250207_strain.py first. Cannot classify.

### Reasons
- GW250207 strain files not available

## Key Finding: 20-40 Hz Sub-band
The 20-40 Hz excess kurtosis in L1 at the GW240925 trigger is +44.9.
This band is most sensitive to seismic coupling, suspension noise,
and control-system artefacts in LIGO.
GW250207 comparison: see table above

## Gate Verdicts
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO

## Next Steps
- If SAME_L1_LOW_FREQ_PATTERN: request Omicron/iDQ for both events
- If CLEANER_THAN_GW240925: run full SSZ pipeline on GW250207
- If MISSING_DATA: run scripts/download_gw250207_strain.py
