# H1/L1 Abs-Correlation Replication Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Generated:** 2026-05-19
**Event:** GW240925 (GPS 1411261107.984)
**Status:** COHERENT_WITH_SIGN_FLIP — NO CLAIM

---

## Sign Convention: Why Negative Correlation Is Not a Failure

```text
corr = +0.99  ->  strongly co-directed
corr = -0.99  ->  strongly counter-directed (same pattern, mirrored)
|corr| = 0.99 ->  strongly coupled
```

For the H1/L1 detector pair, opposite arm orientations, antenna projection,
and sign conventions can cause the same GW signal to appear with opposite
sign at the two sites. A large negative correlation at the correct time delay
is therefore a valid coherence result, not a failure.

**Rule:** Always use `argmax(|C(tau)|)` for peak detection, not `argmax(C(tau))`.

---

## Summary

When sign convention is handled correctly, the trigger window shows a strong
anti-correlated match at dt=0 ms:

```text
corr(dt=0 ms) = -0.991
abs(corr)     =  0.991
```

The previous dt=-10 ms result and PERSISTENT_SYSTEMATIC classification were
xcorr implementation artifacts from using argmax(corr) instead of argmax(|corr|).

---

## Classification

```text
H1_L1_REPLICATION_STATUS:        COHERENT_WITH_SIGN_FLIP
BEST_DELAY:                       0 ms
BEST_ABS_CORR:                    0.991
SIGN_RELATION:                    OPPOSITE_SIGN
PREVIOUS_DT_MINUS_10MS_RESULT:    CLASSIFICATION_ARTIFACT
L1_ONLY_STRUCTURE:                NO, not globally
L1_20_40_STATUS:                  DQ/artifact context still required — see below
READY_FOR_REAL_LIGO_SSZ_CLAIM:    NO
SSZ_SUPPORT_CLAIM_MADE:           NO
SSZ_FALSIFICATION_CLAIM_MADE:     NO
```

---

## What This Means

**The H1/L1 anti-correlation at dt=0 ms IS a valid coherence signal.**

When the sign convention between detectors is accounted for, abs(corr) = 0.991
at zero delay is an extremely strong match. This is not bad correlation —
it is expected behavior for the H1/L1 detector pair.

**What this does NOT mean:**

```text
- L1 is fully clean
- The 20-40 Hz L1 anomaly is resolved
- SSZ is confirmed
- SSZ is falsified
- This event is free of DQ concerns
```

---

## Critical Gate: Trigger vs. Off-Source |corr|

The decisive professional check is:

```text
Is |corr| at the trigger window significantly stronger than in off-source windows?
```

Current full-band values:

```text
Window     |corr|   interpretation
TRIGGER    0.991    strong coupling
OFF_m500   0.9999   strong coupling (off-source)
```

**Assessment:** Trigger and off-source abs-correlation are comparable.
This indicates a stationary coupling mode rather than an event-specific signal.

Possible causes:

```text
- Persistent environmental common mode (Schumann resonances)
- Shared noise floor between H1 and L1
- Detector orientation: structural anti-correlation that is always present
```

Conclusion: Full-band coherence with abs(corr)=0.991 is confirmed, but it is
persistent — not exclusive to the trigger. The event-specific contribution
must be isolated via subband analysis (especially 20-40 Hz) and longer
off-source baselines.

---

## Remaining Open Gate: L1 20-40 Hz

The L1 20-40 Hz non-Gaussian structure (kurtosis +44.9 at trigger) remains separately
unresolved. Full-band coherence does not automatically imply that the 20-40 Hz subband
contributes coherently.

**Required next gate:** Subband abs-correlation test.
See: reports/H1_L1_SUBBAND_REPLICATION_REPORT.md

---

## Anti-Circularity

```text
No PE/QNM posteriors used.
No Kerr/SSZ model parameters used.
Peak detection: argmax(|C(tau)|) — sign-convention-safe.
```
