# Detector-Side Anholonomy Result

**Version:** 1.0  
**Date:** 2026-05-18  
**Branch:** GA_INTERFEROMETER_BRANCH  
**Derived from:** geometric_algebra_interferometer.py + synthetic tests  
**Status:** RESULT_LOCKED  
**READY_FOR_REAL_LIGO_CLAIM: NO**

---

## Result Summary

The GA interferometer forward model (synthetic, no LIGO data) shows:

| Quantity | Value | Significance |
|----------|-------|-------------|
| GR phase-integral recovery | corr = 0.9999 | Model is correct |
| Near-detector SSZ arm correction | Δh/h ~ 1e-9 or smaller | **NEGLIGIBLE** |
| Retarded correction at 100 Hz | ~0.003 (0.3%) | Also negligible |
| LIGO sensitivity floor | ~1e-23 to 1e-24 | ~10^14 times larger |

**The direct near-detector SSZ arm correction is negligible relative to
LIGO sensitivity. It is not a viable observable.**

---

## Why This Is Not a Setback

This result is physically correct and expected.

The SSZ correction at the detector arm is:

```
Δh/h ~ [s(r_det)/D(r_det) - 1]
      ~ Xi(r_det)
      ~ r_s / (2 * r_det)
```

For a LIGO detector at Earth (r_det ~ 1 AU from any compact object):

```
r_s (stellar mass BH, 30 Msun) ~ 90 m
r_det ~ 1.5e11 m

Xi(r_det) ~ 90 / (2 * 1.5e11) ~ 3e-10
```

This is **seven orders of magnitude below LIGO sensitivity**.

The LIGO arm is not inside a strong SSZ field. It is in flat Minkowski
space to extraordinary precision. No SSZ local arm correction is
expected or observed.

---

## What This Implies for the Theory

The Sagnac/phase-integral analogy (Carmen's idea) is **correct but
localised at the wrong place** when applied to the detector arm.

The Sagnac effect at LIGO:

```
Wrong picture:
  LIGO arm is twisted/scaled by local SSZ geometry.
  → Local Xi at Earth ~ 3e-10 → unobservable.

Correct picture:
  The GW itself carries the SSZ geometry imprinted at the source.
  LIGO projects the arriving polarization/phase structure onto two arms.
  The observable is in the wave, not in the arm.
```

The Michelson interferometer is the **measurement device**.
The SSZ signal is in the **incoming wave**.

---

## The Correct SSZ-LIGO Search Path

```
source strong-field region (r ~ r_ISCO, Xi ~ 0.1–0.8)
    ↓
SSZ phase accounting during inspiral/merger
(RSG scale, δΨ_SSZ, polarization rotation θ_SSZ)
    ↓
propagation to Earth (Xi_propagation negligible in weak field)
    ↓
arriving GW: h_+(t), h_×(t) with SSZ-imprinted structure
    ↓
LIGO Michelson: projects h+/hx onto arms via F+, F×
    ↓
residual strain: h(t) - h_GR(t) = SSZ observable
```

This is the structure already implemented in the V0/V1 pipeline
(`derived_phase.py`, `derived_amplitude.py`, `ssz_twist.py`).

The GA interferometer model **confirms** that the detector projection
step is correctly modelled and that no additional local arm correction
is needed.

---

## What the GA Model Does Contribute

Although the near-detector correction is negligible, the GA framework
contributes the following:

1. **GR recovery verification** — confirmed at corr > 0.999, validating
   the pipeline structure.

2. **Retarded integral** — correct light-travel-time averaging is
   implemented. For LIGO band (20–210 Hz): correction < 1%, negligible.
   (For LISA at 1 mHz, this would be essential.)

3. **Twist projection geometry** — the SO(2) arm-rotation model correctly
   captures how h+/hx mixing enters the detector response. This is the
   geometrically correct description of the F+/F× projection under SSZ
   twist. **This part remains useful in the source-frame branch.**

4. **Null result for local arm correction** — a cleanly derived null
   result is a real result. It eliminates a class of models.

---

## Locked Conclusions

```
RESULT_1: GR phase-integral recovery confirmed (corr > 0.999).
RESULT_2: Near-detector SSZ arm correction is NEGLIGIBLE (Δh/h ~ 1e-9).
RESULT_3: Direct LIGO arm twist is NOT the main SSZ observable.
RESULT_4: SSZ LIGO signal must reside in the source/propagation frame.
RESULT_5: Detector projection (F+/F×, polarization mixing) is correct.
```

---

## Next Branch

**SOURCE_PROPAGATION_TWIST_BRANCH**

The SSZ observable is in the source frame:

```
h_+(f)^SSZ = S(f) * [cos θ · h_+^GR(f) - sin θ · h_×^GR(f)]
h_×(f)^SSZ = S(f) * [sin θ · h_+^GR(f) + cos θ · h_×^GR(f)]
```

where:
- `S(f)` = SSZ amplitude scaling from source strong-field (already in V0)
- `θ(f)` = SSZ polarization rotation from spin connection holonomy
  (not yet derived — currently placeholder in `ssz_twist.py`)

**The detector then simply measures F+ h+(t) + F× h×(t)**,
with no additional local arm correction needed.

This is cleaner, better motivated, and consistent with the null result
for local detector-arm SSZ.

---

## Anti-Circularity Statement

- No LIGO strain data used in this derivation
- No posterior parameters used
- No SSZ support or falsification claimed
- This is a synthetic forward-model null result for the detector side

---

## Gate Status

```
DETECTOR_SIDE_SSZ_ARM_CORRECTION:  NEGLIGIBLE — RESULT LOCKED
GR_RECOVERY_SYNTHETIC:             CONFIRMED
LOCAL_ARM_TWIST_BRANCH:            CLOSED (null result, not a failure)
SOURCE_PROPAGATION_TWIST_BRANCH:   OPEN — NEXT PRIORITY
READY_FOR_REAL_LIGO_SSZ_CLAIM:     NO
SSZ_SUPPORT_CLAIM_MADE:            NO
SSZ_FALSIFICATION_CLAIM_MADE:      NO
```
