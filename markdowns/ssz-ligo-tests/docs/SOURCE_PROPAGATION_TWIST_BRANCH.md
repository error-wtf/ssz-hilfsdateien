# SOURCE_PROPAGATION_TWIST_BRANCH

**Version:** 1.0  
**Date:** 2026-05-18  
**Status:** DERIVED_V0_CONCEPTUAL  
**Depends on:**
  - DETECTOR_SIDE_ANHOLONOMY_RESULT.md (local arm = CLOSED_NEGLIGIBLE)
  - SSZ_LIGO_PHASE_TRANSPORT_PRINCIPLE.md (co-scaling argument)
  - SSZ_GEOMETRIC_ALGEBRA_INTERFEROMETER_MODEL.md

**LOCAL_ARM_TWIST_STATUS: CLOSED_NEGLIGIBLE**  
**READY_FOR_REAL_LIGO_SSZ_CLAIM: NO**

---

## 1. Why the Detector Is Not the Source of SSZ Effects

The detector-side null result is now locked
(DETECTOR_SIDE_ANHOLONOMY_RESULT.md):

```
Xi(r_Earth) ~ r_s / (2 r_det) ~ 3e-10
delta_h/h ~ 1e-9 or smaller
LOCAL_ARM_SSZ_CORRECTION: CLOSED
```

The LIGO interferometer arms are in essentially flat spacetime. No SSZ
distortion of the arm geometry is measurable with current sensitivity.

**Consequence:** The detector is a projection device, not the seat of
SSZ effects. It projects the incoming GW polarisations via antenna
patterns (F+, Fx). Whatever SSZ imprints exist must arrive with the wave.

The correct picture is:

```
SOURCE STRONG FIELD          PROPAGATION           DETECTOR
(r ~ r_ISCO, Xi ~ 0.1-0.8)  (r >> r_s, Xi ~ 0)   (Xi ~ 3e-10)
  SSZ scale S(f)       →     wave carries          → F+ h+^SSZ + Fx hx^SSZ
  SSZ twist theta(f)   →     SSZ signature         → strain h(t)
  polarization mixing  →     to Earth              → measured
```

---

## 2. The Forward Model

The source-propagation SSZ modification acts on the GR polarisation
amplitudes in the source frame before projection:

```
[h+^SSZ(f)]   =  S(f) * R(theta(f)) * [h+^GR(f)]
[hx^SSZ(f)]                             [hx^GR(f)]
```

where:

```
S(f)      = SSZ amplitude scale factor (real, positive)
            from SSZ V0 pipeline: A_SSZ(f) exp(i delta_Psi(f))
            (for constant-theta model: S = scalar)

R(theta)  = [[cos theta,  -sin theta],
             [sin theta,   cos theta]]   in SO(2)

theta(f)  = SSZ polarisation twist angle [rad]
            = phi(f) in source/propagation strong-field geometry
```

The detector output is:

```
h_det(f) = F+ * h+^SSZ(f) + Fx * hx^SSZ(f)
```

This is the **only** form where SSZ can appear as a LIGO observable,
given the local arm null result.

---

## 3. Physical Meaning of Each Term

### S(f): Amplitude Scale

SSZ modifies the metric near the source (r ~ r_ISCO, Xi ~ 0.1-0.8).
The outgoing wave amplitude is suppressed or enhanced by the local
Riemann scalar geometry factor. In the SSZ V0 pipeline this is:

```
S(f) = |A_SSZ(f)| / |A_GR(f)|
```

This is the source-frame modification already implemented.

### theta(f): Polarisation Twist

If the SSZ geometry near the source is not spherically symmetric in the
orbital plane (e.g., the spin-connection has an azimuthal component),
the outgoing wave's polarisation frame is rotated relative to the GR
prediction. The rotation is:

```
h+^SSZ = cos(theta) h+^GR - sin(theta) hx^GR
hx^SSZ = sin(theta) h+^GR + cos(theta) hx^GR
```

This is **not** a precession of the binary orbit (already in h+^GR, hx^GR).
It is an additional frame rotation of the polarisation basis due to the
SSZ spin connection in the strong-field region.

### Physical regime for theta

For a BBH merger with M_total ~ 20 Msun:

```
r_s ~ 2 GM/c^2 ~ 29 km * (M/10 Msun)
r_ISCO ~ 3 r_s ~ 87 km
Xi(r_ISCO) ~ 1 - exp(-phi * r_ISCO / r_s)
           ~ 1 - exp(-3*phi) ~ 0.99  [strong field]
Xi weak:  r_s / (2 r_ISCO) = 1/6 ~ 0.17  [weak-field estimate]
```

The twist angle is expected to be of order Xi(r_char), where r_char
is the dominant emission radius. For a rough proxy:

```
theta ~ Xi(r_ISCO) ~ 0.1 -- 0.8 rad  [order of magnitude only]
```

**This is a sensitivity estimate, not a derived value.**

### Frequency dependence

In the simplest V0 model: theta = const (frequency-independent).
More general: theta(f) is set by the emission radius r(f) via the
chirp kinematics (r decreases as f increases toward merger):

```
f_GW = (1/pi) * sqrt(G M_tot / r^3)  [Kepler]
r(f) = (G M_tot / pi^2 f^2)^{1/3}
theta(f) ~ Xi(r(f)) * phi_geom
```

This gives a frequency-dependent twist that increases toward merger.

---

## 4. Why H1 and L1 See It Differently

The key observable feature of source-frame twist:

```
h_det^H1 = F+^H1 * h+^SSZ + Fx^H1 * hx^SSZ
h_det^L1 = F+^L1 * h+^SSZ + Fx^L1 * hx^SSZ
```

Under scale-only (theta=0):

```
h_det^H1 / h_det^L1 = (F+^H1 h+^GR + Fx^H1 hx^GR)
                    / (F+^L1 h+^GR + Fx^L1 hx^GR) * S  [same S, same ratio]
```

Under scale+twist (theta != 0):

```
h+^SSZ = S*(cos theta * h+^GR - sin theta * hx^GR)
hx^SSZ = S*(sin theta * h+^GR + cos theta * hx^GR)

h_det^H1 / h_det^L1  [now depends on F+/Fx ratio AND theta]
```

Different (F+^H1, Fx^H1) vs (F+^L1, Fx^L1) means the two detectors
see **different amplitudes** of the twist. This is the primary
observable signature of source-frame SSZ twist:
the H1/L1 amplitude ratio shifts under twist in a way that
**cannot be mimicked by a scale-only model**.

---

## 5. What Is Not Claimed

```
NOT CLAIMED:
  - Twist was detected in GW240925 or any event
  - theta(f) has been derived from SSZ first principles
  - S(f) from SSZ V0 accurately models the real source
  - Antenna patterns used in scripts are from PE posterior

CLAIMED (conceptual only):
  - If SSZ twist exists in the source frame, it maps to a
    differential H1/L1 response shift via (F+, Fx) mixing
  - This is testable in principle with real LIGO data
  - The detector-arm correction is closed as negligible
```

---

## 6. Branch Architecture

```
source_propagation_twist.py:
  theta_constant(freqs, theta0)            constant theta proxy
  theta_xi_proxy(freqs, M, rs, alpha)      Xi-based theta(f)
  theta_rsg_proxy(freqs, M, rs, alpha)     RSG-proxy theta(f)
  rotate_polarizations(hp, hx, theta)      SO(2) rotation
  apply_source_scale_twist(hp, hx, S, th)  full forward model
  detector_projection(hp, hx, Fp, Fx)      antenna projection
  compare_scale_only_vs_scale_twist(...)   diagnostic scan
```

---

## 7. Gate Status

```
SOURCE_PROPAGATION_TWIST_STATUS:  DERIVED_V0_CONCEPTUAL
LOCAL_ARM_TWIST_STATUS:           CLOSED_NEGLIGIBLE
THETA_DERIVED_FROM_FIRST_PRINCIPLES: NO (proxies only)
SCALE_S_FROM_SSZ_FIRST_PRINCIPLES:   V0 only
GR_RECOVERY:                      IMPLEMENTED
POWER_CONSERVATION_UNDER_TWIST:   VERIFIED (tests)
H1_L1_DIFFERENTIAL_RESPONSE:      IMPLEMENTED
READY_FOR_REAL_LIGO_SSZ_CLAIM:    NO
SSZ_SUPPORT_CLAIM_MADE:           NO
SSZ_FALSIFICATION_CLAIM_MADE:     NO
```
