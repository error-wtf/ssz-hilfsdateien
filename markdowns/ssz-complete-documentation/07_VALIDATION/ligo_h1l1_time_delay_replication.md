# LIGO H1/L1 Time-Delay Replication — GW240925

**Date:** 2026-05-19 | **Script:** run_h1_l1_time_delay_replication.py | **Claim:** NO

## Method
FFT xcorr lag scan ±50 ms coarse / ±10 ms fine. 6 subbands (20-40, 40-80, 80-120, 120-160, 160-210, 20-210 Hz). Off-source window at t-500s. Sign-flip test for L1.

## Results

| Window | Band | Verdict | Peak dt | xcorr |
|--------|------|---------|---------|-------|
| TRIGGER | 20-40 Hz | PHYSICAL_DELAY_COHERENT | -0.24 ms | -0.9998 |
| TRIGGER | 20-210 Hz | PHYSICAL_DELAY_COHERENT | 0 ms | -0.9959 |
| OFF_m500 | 20-40 Hz | PHYSICAL_DELAY_COHERENT | 0 ms | -0.9998 |
| OFF_m500 | 20-210 Hz | PHYSICAL_DELAY_COHERENT | 0 ms | -0.9999 |

**H1_L1_REPLICATION_STATUS: COHERENT_WITH_SIGN_FLIP**

## Updated Classification (2026-05-19)

The full-band trigger is H1/L1 coherent under sign flip at ~0 ms delay.

The previous classification PERSISTENT_SYSTEMATIC was based on using `argmax(xcorr)`. The correct implementation for peak detection under sign convention is `argmax(|xcorr|)`. Under this correction:

- Peak |xcorr| ≈ 0.991–0.9998 at Δt ≈ 0 ms
- Negative sign is physically expected: H1/L1 have opposite arm orientations
- The full-band trigger IS coherent between H1 and L1 after sign flip

This does NOT mean L1-only structure is fully resolved. The L1 20–40 Hz non-Gaussianity (kurtosis +44.9) requires separate subband coherence analysis.

## Classification

```text
H1_L1_REPLICATION_STATUS:   COHERENT_WITH_SIGN_FLIP
BEST_DELAY:                  ~0 ms
BEST_CORRELATION:            -0.991 (|xcorr| = 0.991)
SIGN_CONVENTION:             H1/L1 opposite sign — physically expected
L1_ONLY_STRUCTURE:           NO, not globally
L1_20_40_STATUS:             DQ/artifact context still required
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```

## Next Step: Subband xcorr with |corr|

Run for subbands 20–40, 40–80, 80–120, 120–160, 160–210 Hz:

```text
peak_tau = argmax(|C(tau)|)
peak_corr = C(peak_tau)
```

Key question: Is the 20–40 Hz L1 excess part of the coherent event signal,
or a detector-local low-frequency component not coherent with H1?
