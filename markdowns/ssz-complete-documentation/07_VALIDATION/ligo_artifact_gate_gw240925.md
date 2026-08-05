# LIGO Artifact Gate — GW240925 L1 Anomaly

**Date:** 2026-05-19 | **Event:** GW240925 (GPS 1411261107.984, GWOSC O4b)
**Cross-ref:** `ssz-ligo-tests/reports/L1_ARTIFACT_GATE_FINAL_STATUS.md`
**Claim:** NO

## Final Gate

```
GAUSSIANITY_ARTIFACT_GATE:    FAIL_L1_NON_GAUSSIAN
L1_EXCESS_CLASS:              TRIGGER_SPECIFIC_LOW_FREQ_SUBBAND
L1_ANOMALY_BAND:              20-40 Hz (ex_k=+44.9 trigger, +1.1 off-source)
L1_STATUS:                    DQ_FLAGGED_DIAGNOSTIC_ONLY
H1_STATUS:                    USABLE_EXPLORATORY
H1_L1_COHERENCE_STATUS:       BLOCKED_BY_L1_DQ
ARTIFACT_SCORE:               10/24  RISK=MEDIUM
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```

## Diagnostic Chain

### Sub-band Gaussianity (key finding)

| Band | L1 trigger ex_k | L1 off-500s ex_k | H1 trigger ex_k | Flag |
|------|-----------------|------------------|-----------------|------|
| **20-40 Hz** | **+44.9** | **+1.1** | +3.7 | **ANOMAL** |
| 40-80 Hz | -0.5 | -0.6 | +0.3 | clean |
| 80-120 Hz | +3.3 | +0.9 | +2.4 | mild |
| 120-160 Hz | +5.7 | +1.4 | +1.3 | mild |
| 160-210 Hz | +2.3 | +0.8 | +0.7 | mild |

The 20-40 Hz excess (Δex_k = +43.7) is trigger-specific in L1. H1 is clean.

### DQ Bit Provenance

- L1 CBC_CAT2/CAT3: CLEAN (no CBC veto)
- Offline Omicron / iDQ / hveto: NOT AVAILABLE in public GWOSC release
- Conclusion: public DQ products insufficient to classify the L1 excess

### Line/Notch Test

- L1 spectral lines: 60, 120, 180 Hz (US mains harmonics) + 26, 36, 41, 53 Hz
- H1 trigger peaks (22, 28, 40 Hz): **zero overlap** with L1
- After notching 10 strongest peaks: L1/H1 ratio rises from 1.56 → 3.08
- Lines explain ~55% of in-band power; diffuse broadband floor remains

### Stationarity

- L1 trigger at 85th percentile of ±1000 s windows
- No temporal trend (slope ≈ 0)
- Verdict: MILD_OUTLIER_80

### STFT Omicron-Lite

- 21.6% hot TF tiles trigger vs 20.8% off-source
- No trigger-specific burst structure — INCONCLUSIVE

## What Cannot Be Said

- "L1 anomaly is a confirmed glitch" — requires Omicron/iDQ/offline DQ
- "L1 anomaly is a signal" — no positive evidence
- "SSZ falsified" — L1 excluded from claim chain; H1 unaffected
- "SSZ supported" — no differential H1/L1 test possible while L1 DQ unresolved
