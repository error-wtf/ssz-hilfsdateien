# LIGO H1/L1 Mini-Pipeline: Test Plan

**Version:** 1.0 | **Date:** 2026-05-19
**Authors:** Carmen N. Wrede, Lino P. Casu
**Status:** ACTIVE — Phase 0-2 complete, Phase 3-10 pending

---

## Objective

Determine whether the **L1 excess in the 20-210 Hz band** is a local detector/noise
artifact, or whether a physically interesting residual remains after all diagnostic checks.

Not the objective:

> "Prove SSZ."

The objective is:

> "Cleanly exclude artifacts, noise, phase errors, and local L1 disturbances
> before any physical interpretation is considered."

---

## Phase 0 — Dataset Documentation

Record for every run:

```text
EVENT_NAME:
GPS_TRIGGER_TIME:
H1_FILE:
L1_FILE:
SAMPLE_RATE:
WINDOW_LENGTH:
FREQUENCY_BAND:       20-210 Hz
WHITENING_METHOD:
PSD_WINDOW:
BANDPASS_METHOD:
CODE_VERSION:
```

**Gate 0:** No claim without these fields fully populated.

---

## Phase 1 — Baseline: Identical H1/L1 Processing

Verify:

```text
same sample rate?
same window length?
same bandpass?
same whitening?
same PSD method?
same normalization?
H1/L1 not swapped?
strain / ASD / PSD / whitened not confused?
```

**PASS:** H1 and L1 are processed identically.
**FAIL:** Do not interpret result.

---

## Phase 2 — Bandpower Test

Compute for windows Trigger, Off -100s, Off -300s, Off -500s, Off +100s, Off +300s:

```text
Bandpower H1  20-210 Hz
Bandpower L1  20-210 Hz
Ratio L1/H1
```

**Decision:**

- L1 elevated only at trigger → potentially interesting
- L1 elevated off-source too → local L1 noise likely

---

## Phase 3 — Gaussianity Test

For H1 and L1, trigger and off-source:

```text
mean / std / skewness / kurtosis / excess kurtosis
count |z| > 3 / > 4 / > 5
QQ-plot / histogram
```

**Gate 3:**

```text
If L1_trigger approximates L1_off-source:
    L1 is stationary non-Gaussian.
    No event-related claim permitted.
```

Current GW240925 result: L1 excess kurtosis +44.9 trigger vs +1.1 off-source.
Status: L1 DIAGNOSTIC-ONLY — gate blocked.

---

## Phase 4 — Frequency Resolution

Resolve the spectrum. Do not treat 20-210 Hz as one block.

Produce: PSD H1 trigger / PSD L1 trigger / PSD H1 off-source / PSD L1 off-source / peak list.

Check for peaks at 20-40, 50, 60, 100, 120, 150, 180, 200 Hz.

Also check: Are peaks harmonic? f_n approximately n * f0?

**Decision:**

- Peaks at 50/100/150/200 Hz → European mains suspect
- Peaks at 60/120/180 Hz → US mains suspect
- Broad hump → general low-frequency detector noise
- Decaying peak → resonance/oscillator

---

## Phase 5 — Harmonic Oscillator Test

If peaks found, test: f_n approximately n * f0

Time domain check: x(t) = A * exp(-gamma*t) * cos(omega*t + phi)

**Gate 5:**

```text
If L1 shows a stable harmonic pattern:
    Detector/resonance artifact is more likely.
    Do not interpret as astrophysical signal.
```

---

## Phase 6 — H1/L1 Time-Delay Check

Scan tau = -10 ms to +10 ms.

**CRITICAL:** Use `peak_tau = argmax(|C(tau)|)`, not `argmax(C(tau))`.
H1/L1 may be negatively correlated due to opposite arm orientations — a negative
peak at the correct delay is a valid coherence result.

Cross-correlation: C(tau) = sum_t H1(t) * L1(t + tau)

**PASS:** Clear |xcorr| peak at physically allowed |tau| <= ~10 ms.
**FAIL:** No stable |xcorr| peak, or peak explained by L1 spectral excess alone.

Current GW240925 result (updated): Full-band trigger is COHERENT_WITH_SIGN_FLIP.
|xcorr| ≈ 0.991–0.9998 at Δt ≈ 0 ms. Negative sign is physically expected.

Phase 6 full-band: PASS (sign flip accounted for).

Remaining question for Phase 6b — Subband xcorr:

```text
For each subband (20-40, 40-80, 80-120, 120-160, 160-210 Hz):
    peak_tau  = argmax(|C(tau)|)
    peak_corr = C(peak_tau)
```

Key question: Is the 20-40 Hz L1 excess part of the coherent signal,
or a detector-local component not coherent with H1?

---

## Phase 7 — Phase and Coherence

Compute: coherence gamma_sq(f) / phase difference Delta_phi(f) / cross-spectrum H1* L1

**Decision:**

- L1 high power, no H1 coherence → L1-local artifact
- H1/L1 coherent with correct time delay → potentially interesting

---

## Phase 8 — Sonification

Produce:

```text
L1_trigger_30s_20-210Hz.wav
H1_trigger_30s_20-210Hz.wav
stereo_H1_L1_trigger_30s.wav
L1_off_minus300s_30s.wav
stereo_L1_trigger_vs_offsource.wav
optional: x4 / x8 speedup
```

If L1 sounds the same at trigger and off-source: the excess is not an event signal.

---

## Phase 9 — Matched Filtering / Standard-Model Comparison

Only after Phases 1-8 do not block. Check:

```text
Does H1/L1 match the official GW waveform?
Time delay / phase / amplitude ratio / antenna pattern match?
```

If excess is explained by standard GR waveform: no new physics claim.
Otherwise: document residual.

---

## Phase 10 — SSZ Test: Last Step Only

Only now ask whether SSZ makes a concrete prediction for:

```text
- why 20-210 Hz?
- why L1 stronger?
- which phase?
- which time delay?
- which amplitude scale?
- why not H1 equally strong?
```

Without a concrete prior prediction:

```text
SSZ_CLAIM = NO
```

With a concrete prior prediction AND all gates passed:

```text
SSZ_CANDIDATE = POSSIBLE
```

Still not "proven".

---

## Hard PASS/FAIL Gate

```text
READY_FOR_REAL_LIGO_SSZ_CLAIM = YES
only if ALL of:

[PASS] identical processing verified
[PASS] off-source does not explain L1 excess
[PASS] Gaussianity check does not block
[PASS] no harmonic detector pattern found
[PASS] H1/L1 correlate with physical time delay
[PASS] phase / coherence consistent
[PASS] standard GR does not fully explain residual
[PASS] SSZ delivered concrete prior prediction
```

If any check fails:

```text
READY_FOR_REAL_LIGO_SSZ_CLAIM = NO
DATA_QUALITY_FINDING = YES   (if anomaly is documented and reproducible)
```

---

## Current Status — GW240925 (2026-05-19)

| Phase | Status | Note |
|-------|--------|------|
| 0 — Dataset documentation | PASS | Complete |
| 1 — Identical processing | PASS | Verified |
| 2 — Bandpower test | PASS | L1 excess found, persistent off-source |
| 3 — Gaussianity | BLOCKED | L1 kurtosis +44.9 trigger = off-source pattern |
| 4 — Frequency resolution | PENDING | — |
| 5 — Harmonic oscillator | PENDING | — |
| 6 — Time delay (full-band) | PASS | COHERENT_WITH_SIGN_FLIP, abs(xcorr)=0.991, Dt~0 ms |
| 6b — Subband xcorr | PENDING | 20-40 Hz: is it coherent or L1-local? |
| 7 — Phase / coherence | PENDING | — |
| 8 — Sonification | PENDING | — |
| 9 — Matched filtering | PENDING | — |
| 10 — SSZ test | PENDING | Gate 3 not passed; Gate 6 full-band passed |

**Overall:**

```text
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
DATA_QUALITY_FINDING:          YES (L1 20-40 Hz excess, kurtosis +44.9, persistent)
NEXT STEP:                     Phase 6b — Subband xcorr with |corr| to determine
                               whether 20-40 Hz L1 excess is H1-coherent or L1-local
```

---

## Result Statement for Lino

> We have not released an SSZ claim. The full-band trigger is H1/L1 coherent under
> sign flip at ~0 ms delay (|xcorr| ≈ 0.991). The previous PERSISTENT_SYSTEMATIC
> classification was an xcorr implementation artifact from using argmax(xcorr) instead
> of argmax(|xcorr|). The full-band coherence result does not resolve the L1 20-40 Hz
> non-Gaussianity: that band requires subband coherence analysis to determine whether
> the excess is part of the coherent event signal or a detector-local component.
> No SSZ claim.

---

*Authors: Carmen N. Wrede, Lino P. Casu*
*License: Anticapitalist License 1.4*
