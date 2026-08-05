# SSZ Interferometer — Anholonomy Formulation

**Version:** 1.0  
**Date:** 2026-05-18  
**Status:** THEORETICAL_FRAMEWORK — not yet numerically implemented  
**READY_FOR_REAL_LIGO_SSZ_CLAIM: NO**

---

## 1. Why LIGO Is Not a Telescope Observable

A telescope measures:
```
Source emits photons → photons propagate → detector records frequency / spectrum
```
The relevant SSZ observable is then a gravitational redshift or frequency ratio
acting on the photon energy. This is a **timelike or null geodesic** problem
at the source location.

LIGO measures something fundamentally different:
```
Gravitational wave deforms local spacetime
→ two laser beams travel two different arms
→ each arm accumulates a different optical phase
→ the phase difference at the beamsplitter is the signal
```

LIGO measures a **local phase difference** — the result of transporting
an optical phase along two different paths and comparing the result.
This is an **anholonomy** (path-holonomy) problem, not a redshift problem.

**Consequence for SSZ:**
The relevant SSZ quantity for LIGO is not "what happens at the source black hole"
but "how does SSZ modify the phase transport along the two interferometer arms?"

---

## 2. Interferometer as a Path-Phase-Difference Device

Let the two interferometer arms be paths γ_x and γ_y in spacetime.
Laser light travels each arm and returns. The accumulated optical phase along arm x is:

```
Φ_x = ∫_{γ_x} k_μ dx^μ
```

where k_μ is the photon 4-wavevector. The interferometer output is:

```
ΔΦ = Φ_x - Φ_y
```

In GR, a passing gravitational wave perturbs the metric:

```
g_μν = η_μν + h_μν(t)
```

which changes the proper length of each arm differently, producing:

```
ΔΦ_GR = (2π/λ) · ΔL_eff = (2π/λ) · L · h(t)
```

where h(t) is the strain. The strain is therefore a proxy for the differential
phase accumulated along the two arms.

**For SSZ:** the same logic applies, but the metric is modified by Ξ(r):

```
ds²_SSZ = -D(r)² c² dt² + s(r)² dr² + r² dΩ²
```

The photon 4-wavevector k_μ satisfies the null condition g^{μν} k_μ k_ν = 0
in the SSZ metric. This modifies the accumulated phase relative to GR.

---

## 3. SSZ-RSG as Phase Accounting

The Radial Scaling Gauge (RSG) is the SSZ rule for how coordinate lengths
relate to physical lengths:

```
ds_phys = s(r) · dr_coord    (radial direction)
ds_phys = D(r) · c · dt      (time direction)
```

For a photon travelling radially along arm x with coordinate length L_arm:

```
Φ_x^SSZ = ∫_0^{L_arm} k_r^SSZ(r) dr
```

where the SSZ radial wavevector component is modified relative to GR:

```
k_r^SSZ = k_r^GR · s(r) / D(r)
```

(from null condition in SSZ metric).

The differential phase between the two arms, after the gravitational wave
has passed, contains both the GW strain and an SSZ correction:

```
ΔΦ_SSZ = ΔΦ_GR + δΦ_SSZ
```

where δΦ_SSZ encodes the RSG modification to the photon transport.

In the far-field / weak-field limit (r >> r_s, Ξ → r_s/2r → 0):
```
s(r) / D(r) → 1 + r_s/r + O((r_s/r)²)
```
so the correction is small and perturbative — consistent with the PPN limit.

---

## 4. Required Mathematical Objects

### 4.1 Tetrad (Vierbein)

The local orthonormal frame (tetrad) e^a_μ satisfies:

```
g_μν = η_ab · e^a_μ · e^b_ν
```

For SSZ Schwarzschild:

```
e^0_t = D(r)       (time component)
e^1_r = s(r)       (radial component)
e^2_θ = r          (angular)
e^3_φ = r·sin(θ)   (angular)
```

The tetrad encodes how SSZ deforms the local frames relative to GR.

### 4.2 Connection (Spin Connection / Christoffel)

The SSZ-modified Christoffel symbols Γ^λ_μν differ from GR by terms
involving ∂_r Ξ(r) = ∂_r D / D² (from the metric functions).

The relevant component for radial photon propagation:

```
Γ^r_rr^SSZ = (D'/D - s'/s)    [prime = d/dr]
```

This modifies the parallel transport of the photon wavevector along the arm.

### 4.3 Transport Operator

The path-ordered transport operator along path γ is:

```
U(γ) = P exp(- ∫_γ Γ_μ dx^μ)
```

In GR, the gravitational wave contributes a small perturbation to U.
In SSZ, U is additionally modified by the D(r) and s(r) profiles.

For a LIGO arm at distance r from the Earth's surface (weak field, r >> r_s):
the SSZ correction to U is perturbative and proportional to Ξ(r_Earth) ~ 10^{-9},
which is below any observable threshold for the detector itself.

**The relevant SSZ effect for LIGO comes from the source, not the detector.**

### 4.4 U(1) Laser Phase

The optical phase of the laser light is a U(1) variable:

```
φ_laser ∈ U(1) = [0, 2π)
```

The interferometer measures:

```
ΔΦ = φ_x - φ_y  (mod 2π)
```

This is the holonomy of the U(1) connection along the closed path
γ_x ∪ γ_y^{-1}.

### 4.5 Holonomy / Anholonomy

For a closed path γ = γ_x ∪ γ_y^{-1}:

```
Hol(γ) = P exp(- ∮_γ ω_μ dx^μ)
```

where ω_μ is the combined gauge + gravitational connection.

If Hol(γ) ≠ identity, the transport is **anholonomic** — the phase
accumulated going one way differs from going back the other.
This anholonomy is exactly what LIGO detects as strain.

---

## 5. Derivation Sketch: ΔΦ_SSZ → h_SSZ

**Step 1:** Write the SSZ metric perturbation from a passing GW as:

```
g_μν^SSZ = g_μν^SSZ_background + δg_μν^GW
```

where g_μν^SSZ_background is the SSZ static metric and δg_μν^GW is the
transverse-traceless GW perturbation (same as GR to leading order).

**Step 2:** Compute the null geodesic in g_μν^SSZ for a photon along arm x:

```
k^μ_SSZ satisfies: g_μν^SSZ k^μ k^ν = 0
```

The solution modifies the phase velocity of light along the arm:

```
c_eff(r) = c · D(r) / s(r)
```

**Step 3:** Compute the round-trip optical phase for each arm:

```
Φ_x^SSZ = (4π L_x / λ) · ∫_0^1 [1 + δg_xx/2 + δΞ(r)] ds
```

where δΞ is the SSZ correction beyond GR.

**Step 4:** The interferometer output is:

```
ΔΦ_SSZ = Φ_x^SSZ - Φ_y^SSZ
        = ΔΦ_GR + ΔΦ_Ξ
```

**Step 5:** Map to strain:

```
h_SSZ(t) = ΔΦ_SSZ · λ / (4π L)
          = h_GR(t) + δh_Ξ(t)
```

In the frequency domain (stationary phase approximation):

```
h_SSZ(f) = h_GR(f) · (1 + δA_SSZ(f)) · exp(i · δΨ_SSZ(f))
```

This recovers the form used in the current V0/V1 pipeline —
but now with a clear derivation path from the interferometer physics.

---

## 6. Equations Already in SSZ Corpus

| Equation | File | Status |
|----------|------|--------|
| D(r) = 1/(1+Ξ) | ssz_core.py | LOCKED |
| s(r) = 1+Ξ | ssz_core.py | LOCKED |
| Ξ_weak = r_s/2r | ssz_core.py | LOCKED |
| Ξ_strong = 1-exp(-φ r_s / r) | ssz_core.py | LOCKED |
| rdot_SSZ = rdot_GR·D²/s⁴ | ssz_inspiral.py | LOCKED |
| δΨ_SSZ(f) | derived_phase.py | DERIVED_V1_0PN_LOCKED |
| δA_SSZ(f) = D²-1 | derived_amplitude.py | DERIVED_V0_INSPIRAL |
| h_SSZ(f) | derived_waveform.py | DERIVED_V0_PROXY |

---

## 7. Equations Still Missing

| Equation | Required for | Status |
|----------|-------------|--------|
| Γ^λ_μν^SSZ | Full SSZ connection | NOT DERIVED |
| U(γ)^SSZ | Path transport operator | NOT DERIVED |
| δh_Ξ(t) at detector arm | Near-field SSZ correction | NOT DERIVED |
| c_eff(r) along arm | Arm phase velocity | NOT DERIVED (only far-field implied) |
| Source→detector RSG propagation | Full forward model | PARTIAL (V0 proxy only) |
| Ringdown arm response | Post-merger anholonomy | NOT DERIVED |

**None of the missing equations are blocking the current inspiral pipeline.**
The current V0/V1 pipeline uses the far-field limit where SSZ corrections
to the detector arm itself are negligible (Ξ_Earth ~ 10^{-9}).

The missing equations matter for:
1. Near-source propagation corrections
2. Merger/ringdown strain model
3. Future precision tests with ET/LISA

---

## 8. Physical Interpretation of Current Pipeline

The current δΨ_SSZ(f) pipeline corresponds to:

```
SSZ modifies the inspiral dynamics at the source
→ the emitted GW carries a phase offset δΨ(f) relative to GR
→ this phase offset propagates to the detector unchanged (weak-field propagation)
→ the detector measures h_SSZ(f) = h_GR(f) · exp(i·δΨ)
```

This is the correct far-field limit. The anholonomy formulation shows
why this works: in weak fields (detector location, propagation path),
the SSZ correction to the photon transport U(γ) is negligible,
so the only SSZ effect that reaches the detector is what was
encoded in the source-frame GW amplitude and phase.

---

## 9. Connection to Lie Algebra / Group Structure

The transport operator U(γ) lives in a Lie group:

| Structure | Physical role |
|-----------|--------------|
| SO(3,1) Lorentz group | Local frame rotations along arm |
| Poincaré group | Translation + Lorentz for local observers |
| U(1) | Optical laser phase |
| Sp(2n) symplectic | Phase space transport (Hamiltonian picture) |

For LIGO, the dominant group is **U(1) × SO(3,1)**:
- U(1) for the optical phase
- SO(3,1) for the local tetrad transport along each arm

SSZ modifies the SO(3,1) part through D(r) and s(r) entering
the spin connection ω_μ^{ab}:

```
ω_μ^{ab,SSZ} = ω_μ^{ab,GR} + δω_μ^{ab}(D, s, ∂D, ∂s)
```

The anholonomy of this modified connection is what ultimately
produces δh_SSZ beyond the source-frame GW.

---

## 10. Next Derivation Steps

```
Priority 1 (blocks 3.5PN inspiral):
   Derive r(f) at 3.5PN order with SSZ corrections to rdot
   → upgrade δΨ_SSZ from 0PN to 3.5PN

Priority 2 (blocks ringdown test):
   Derive ringdown arm response in SSZ metric
   → U(γ)^SSZ for post-merger oscillating spacetime

Priority 3 (theoretical completeness):
   Derive Γ^λ_μν^SSZ explicitly
   → compute δω_μ^{ab}
   → verify near-detector correction ~ Ξ_Earth ~ 10^{-9}

Priority 4 (precision future):
   Source-to-detector RSG propagation
   → does Ξ(r) along propagation path contribute?
   → expected: negligible in cosmological weak field

READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```
