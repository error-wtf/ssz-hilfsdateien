# SSZ-LIGO Phase Transport Principle

**Version:** 1.0  
**Date:** 2026-05-18  
**Branch:** PHASE_TRANSPORT_BRANCH  
**Status:** DERIVED_V0_CONCEPTUAL  
**Builds on:**
  - DETECTOR_SIDE_ANHOLONOMY_RESULT.md (local arm correction = negligible)
  - SSZ_GEOMETRIC_ALGEBRA_INTERFEROMETER_MODEL.md (retarded path integral)
  - SSZ_TWIST_ANHOLONOMY_BRANCH.md (polarization rotation)
**READY_FOR_REAL_LIGO_CLAIM: NO**

---

## 1. The Co-Scaling Argument: Why Local Scale Is Not Directly Observable

When a uniform (or slowly varying) scale factor acts on a region of space,
it scales **everything simultaneously**: the arm length, the mirrors, the
laser wavelength, the ruler used to measure the arm.

Formally: if the SSZ metric factor s(r) varies slowly over the arm length L
(which it does — see DETECTOR_SIDE_ANHOLONOMY_RESULT.md, Δh/h ~ 1e-9),
then the arm, the laser, and the local standard of length all scale by the
same factor s. The simple ratio L_arm / λ_laser is unchanged to first order
in Xi_local.

```
s * L_arm         L_arm
-----------  =  ---------   [unchanged under co-scaling]
s * λ_laser      λ_laser
```

This is the same reason a person made of rubber living in a uniformly
expanding rubber room cannot detect the expansion using a rubber ruler.

**Consequence:** Any SSZ effect that is purely a local co-scaling of the
detector frame is **gauge-equivalent to nothing**. It leaves no observable
imprint in Michelson fringe counts.

This is not a failure of SSZ. It is a fundamental property of how
interferometers work: they are **differential phase instruments**, not
absolute length instruments.

---

## 2. What LIGO Actually Measures

The LIGO output is one number at each time t:

```
ΔΦ(t) = Φ_x(t) - Φ_y(t)
```

where Φ_x and Φ_y are the **accumulated photon phases** along the two arms:

```
Φ_x(t) = ∫_{γ_x} ω_photon^SSZ(x, t)   dl
Φ_y(t) = ∫_{γ_y} ω_photon^SSZ(x, t)   dl
```

This is a **curve integral of the second kind**: the photon phase field
ω_photon is integrated along the specific spacetime path γ_i.

The photons are the probe. They are not mechanically deflected — their
phase accumulation / null direction / polarisation frame is **parallel-
transported** along the lightlike geodesic. If the geometry changes during
transit, the photon integrates that change along the path.

The effective GW strain is:

```
h(t) ~ (λ / 2π L) · ΔΦ(t)
```

---

## 3. Why Only the Phase Difference Is Observable

Consider two cases:

**Case A: Uniform global scaling (s = constant everywhere)**

```
ω_x^SSZ = s · ω_x^GR    along γ_x
ω_y^SSZ = s · ω_y^GR    along γ_y

ΔΦ^SSZ = s · Φ_x^GR - s · Φ_y^GR = s · ΔΦ^GR
```

This is a global rescaling of the observable by s. It is in principle
observable, but only if an external reference exists. If the laser
wavelength λ also scales by s (co-scaling), then h = λ/(2πL) ΔΦ is
unchanged.

**Key point:** A local, co-scaling SSZ factor is not detectable with
the Michelson fringe alone. Only a **differential** or **path-dependent**
phase accumulation is directly observable.

**Case B: Non-uniform or anholonomic scaling (s varies along γ)**

```
ω_x^SSZ = s(x, t) · ω_x^GR    (different at each point of γ_x)
ω_y^SSZ = s(y, t) · ω_y^GR    (different at each point of γ_y)
```

Now:

```
ΔΦ^SSZ = ∫_{γ_x} s(x,t) ω_x^GR dl  -  ∫_{γ_y} s(y,t) ω_y^GR dl
        ≠  s_global · ΔΦ^GR
```

This is what a gravitational wave produces: the metric perturbation h(t)
varies over the light-travel time. The arm-by-arm accumulation differs.

This is also what SSZ source-frame modifications produce: the phase
accumulated during propagation from the strong-field source region
differs from GR, and this difference survives the arrival at the detector.

---

## 4. The Phase Transport Operator

For the scaling-only case:

```
U_i(t) = exp( i Φ_i(t) )  ∈ U(1)
```

The observable is:

```
U_y†(t) U_x(t) = exp( i ΔΦ(t) )
```

This is the **relative U(1) holonomy** between the two arms.

**If the geometry also twists** (SSZ spin-connection contribution θ_SSZ),
the photon frame is additionally rotated. The transport operator becomes
an element of U(1) × SO(2):

```
U_i(t) = exp(i Φ_i(t)) · R(θ_i(t))
```

where R(θ) is the GA rotor in the (e_x, e_y) plane (see
SSZ_GEOMETRIC_ALGEBRA_INTERFEROMETER_MODEL.md, section 3).

The relative transport is:

```
U_rel(t) = U_y†(t) · U_x(t) = exp(i ΔΦ) · R(Δθ)
```

where Δθ = θ_x - θ_y is the **differential frame twist** accumulated
along the two arms.

For a + polarised GW with SSZ twist:

```
h_eff(t) = (λ / 2π L) · [ΔΦ_GR + ΔΦ_SSZ]
polarisation mixing: h+ ↔ h× via Δθ
```

---

## 5. Path-Ordered Transport for Strong Twist

If the twist θ(x,t) is not small or not slowly varying, the full
**path-ordered transport** applies:

```
R(γ) = P exp( -∫_γ Ω_SSZ )
```

where Ω_SSZ is the SSZ spin connection form along the arm.

For the two arms:

```
R_x = P exp( -∫_{γ_x} Ω_SSZ )
R_y = P exp( -∫_{γ_y} Ω_SSZ )
```

The observable relative holonomy is:

```
R_rel = R_y^{-1} · R_x   ∈ SO(2)  [for 2D arm plane]
```

This is the anholonomy of the two-arm Michelson loop. For Ω_SSZ = 0
(GR alone): R_rel = identity. For Ω_SSZ ≠ 0 (SSZ twist present):
R_rel = R(Δθ_SSZ) ≠ identity.

**This is the most general form of the SSZ-LIGO observable.**

For the current pipeline:
- Ω_SSZ is not yet derived from the SSZ spin connection (placeholder forms)
- The V0/V1 observable is the limiting case: R_rel = 1, ΔΦ_SSZ = δΨ_SSZ
- The twist branch adds: R_rel = R(θ_SSZ) with constant θ_SSZ (sensitivity test)

---

## 6. GR Recovery in This Framework

In GR (no SSZ, no twist):

```
Φ_x^GR(t) = ∫_0^L (ω_L/c) · (1 + h_xx(t - ℓ/c) / 2) dℓ
           ≈ (ω_L L / c) · (1 + <h_xx>_ret / 2)

Φ_y^GR(t) = (ω_L L / c) · (1 + <h_yy>_ret / 2)

ΔΦ^GR(t) = (ω_L L / c) · (<h_xx> - <h_yy>)_ret / 2
```

For + polarisation: h_xx = +h(t), h_yy = -h(t):

```
ΔΦ^GR(t) = (ω_L L / c) · <h(t)>_ret
h_eff = ΔΦ^GR · λ/(2πL) = λ/(2π c/ω_L) · <h(t)>_ret
      = <h(t)>_ret   [modulo the λ/(2πL) normalization]
```

This is confirmed by the GA interferometer tests (corr > 0.999).

---

## 7. The Three Layers of the SSZ-LIGO Problem

| Layer | Location | Status |
|-------|----------|--------|
| **Source frame** | r ~ r_ISCO, Xi ~ 0.1–0.8 | V0/V1 implemented |
| **Propagation** | r >> r_s, Xi ~ 0 | negligible (weak field) |
| **Detector** | Earth, Xi ~ 3e-10 | NULL RESULT (locked) |

**The SSZ signal enters only in Layer 1 (source frame).**

The detector is merely the measurement device for the source-imprinted
phase/polarisation structure. The Michelson response correctly extracts
the relative phase — no local arm correction is needed or expected.

---

## 8. Formal Summary: What Is and Is Not Observable

```
NOT OBSERVABLE in Michelson alone:
  - Absolute arm length L
  - Absolute photon phase Φ_x or Φ_y
  - Global co-scaling s(r_det) [because optics co-scales]

OBSERVABLE in Michelson:
  - Relative phase: ΔΦ = Φ_x - Φ_y
  - Relative transport: U_rel = U_y† U_x
  - Relative holonomy: R_rel = R_y^{-1} R_x [if twist present]
  - Path-dependent phase accumulation [retarded integral]
```

---

## 9. Consequence for the SSZ-LIGO Pipeline

The V0/V1 SSZ pipeline already implements the correct structure:

```
h_SSZ(f) = A_SSZ(f) · exp(i δΨ_SSZ(f)) · h_GR(f)
```

This is precisely the source-frame contribution to ΔΦ_SSZ, expressed
in the frequency domain. The detector projection (F+, F×) applies on top.

The twist branch adds:

```
[h+]^SSZ     [cos θ  -sin θ] [h+]^GR
[hx]     = S [sin θ   cos θ] [hx]
```

which is the relative holonomy R_rel acting on the polarisation state.

**No local arm correction is needed. The GA interferometer null result
confirms this.**

---

## 10. Gate Status

```
PHASE_TRANSPORT_BRANCH:          DERIVED_V0_CONCEPTUAL
CO_SCALING_ARGUMENT:             STATED AND DOCUMENTED
GR_RECOVERY:                     CONFIRMED (synthetic)
DETECTOR_ARM_CORRECTION:         NULL — NOT NEEDED
SOURCE_FRAME_PIPELINE:           V0/V1 IMPLEMENTS CORRECT STRUCTURE
SPIN_CONNECTION_DERIVATION:      NOT YET DONE (Ω_SSZ placeholder)
READY_FOR_REAL_LIGO_SSZ_CLAIM:   NO
SSZ_SUPPORT_CLAIM_MADE:          NO
SSZ_FALSIFICATION_CLAIM_MADE:    NO
```
