# H1/L1 Cross-Coherence and Phase Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 07:18:22

## Configuration
- Trigger GPS: 1411261107.984
- Window: 4.0s  NPERSEG: 1024
- Sub-bands: ['full', '20-60', '60-120', '120-210']

## Results

| Tag | Band | Mean Coh | Phase R | Mean Phase | Coh Class | Phase Class |
|-----|------|----------|---------|------------|-----------|-------------|
| TRIGGER | full | 0.0561 | 0.9115 | -167.0° | INCOHERENT | STABLE_PHASE |
| TRIGGER | 20-60 | 0.0618 | 0.9956 | -154.6° | INCOHERENT | STABLE_PHASE |
| TRIGGER | 60-120 | 0.0631 | 0.9891 | -166.0° | INCOHERENT | STABLE_PHASE |
| TRIGGER | 120-210 | 0.0490 | 0.8438 | -174.8° | INCOHERENT | STABLE_PHASE |
| OFF_m500 | full | 0.0818 | 0.9914 | -10.7° | INCOHERENT | STABLE_PHASE |
| OFF_m500 | 20-60 | 0.1068 | 0.9991 | -18.6° | WEAKLY_COHERENT | STABLE_PHASE |
| OFF_m500 | 60-120 | 0.0896 | 0.9984 | -11.1° | INCOHERENT | STABLE_PHASE |
| OFF_m500 | 120-210 | 0.0643 | 0.9904 | -6.7° | INCOHERENT | STABLE_PHASE |
| OFF_m300 | full | 0.1205 | 0.9869 | +170.2° | WEAKLY_COHERENT | STABLE_PHASE |
| OFF_m300 | 20-60 | 0.1608 | 0.9982 | +162.5° | WEAKLY_COHERENT | STABLE_PHASE |
| OFF_m300 | 60-120 | 0.1377 | 0.9992 | +170.3° | WEAKLY_COHERENT | STABLE_PHASE |
| OFF_m300 | 120-210 | 0.0897 | 0.9804 | +173.8° | INCOHERENT | STABLE_PHASE |

## Interpretation
- mean_coh > 0.2: COHERENT — potential shared signal
- phase_R > 0.5: STABLE_PHASE — consistent cross-phase
- INCOHERENT + RANDOM_PHASE -> detector-side noise

## Anti-Circularity
- No SSZ parameters used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
