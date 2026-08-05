# SSZ Twist / Anholonomy Branch

**Version:** 1.0  
**Date:** 2026-05-18  
**Branch ID:** TWIST_POLARIZATION_PHASE_BRANCH  
**Formula status:** DERIVED_V0_CONCEPTUAL  
**READY_FOR_REAL_LIGO_CLAIM: NO**  
**Anti-circularity: NO posterior used, NO SSZ claim made**

---

## 1. Motivation: Scale Is Not Enough

The current V0/V1 pipeline models SSZ as:

```
h_SSZ(f) = h_GR(f) · (1 + δA_SSZ(f)) · exp(i · δΨ_SSZ(f))
```

This captures two effects:
- **Amplitude scaling**: D(r)² modifies the emitted power
- **Phase shift**: modified inspiral dynamics shift the orbital phase

But this representation is incomplete if SSZ also **rotates the local frame**.

In GR the TT metric perturbation mixes two independent polarisation channels:

```
h_ij = h_+ · e_ij^+  +  h_× · e_ij^×
```

If SSZ modifies not only the radial scale factor s(r) but also the **orientation
of null directions** (as suggested by the RSG and anholonomy picture), then
the two polarisation components can mix. The + and × channels are no longer
independently preserved under SSZ transport.

This produces a **twist** — a rotation in polarisation space — that is
invisible to any purely scalar amplitude/phase model.

---

## 2. Mathematical Structure

### 2.1 Scale-Only Model (Current V0/V1)

```
[h_+^SSZ]   =  (1 + δA) · e^{iδΨ} · I₂  ·  [h_+^GR]
[h_×^SSZ]                                    [h_×^GR]
```

where I₂ is the 2×2 identity. The two polarisations are scaled and phase-shifted
identically. **No mixing between + and ×.**

### 2.2 Scale + Twist Model (This Branch)

```
[h_+^SSZ]   =  S(r,f) · R(θ_SSZ(r,f))  ·  [h_+^GR]
[h_×^SSZ]                                    [h_×^GR]
```

where:

```
S(r,f) = (1 + δA_SSZ) · e^{iδΨ_SSZ}     (scale + phase, as before)

R(θ) = | cos θ   -sin θ |                (polarisation rotation matrix)
        | sin θ    cos θ |
```

and θ_SSZ(r,f) is the SSZ-induced twist angle, which is the new unknown.

### 2.3 Detector Response

Each detector I measures:

```
h_I(f) = F_I^+(θ_I, φ_I, ψ_I) · h_+^SSZ(f)
        + F_I^×(θ_I, φ_I, ψ_I) · h_×^SSZ(f)
```

where F^+, F^× are the standard antenna patterns (sky position and
polarisation angle). In the scale-only model, this reduces to the
standard GR expression scaled by (1+δA)·exp(iδΨ). In the twist model,
the SSZ polarisation rotation appears as an **effective shift in the
polarisation angle ψ → ψ + θ_SSZ**, which changes the F^+/F^× mixing.

### 2.4 Observable Consequence

The twist produces an **effective polarisation angle offset** that changes
the H1/L1 amplitude ratio relative to GR:

```
h_I^SSZ / h_I^GR = (F_I^+ cos θ - F_I^× sin θ) / F_I^+ · (h_+/h)
                 + (F_I^+ sin θ + F_I^× cos θ) / F_I^× · (h_×/h)
```

For θ ≠ 0, the H1 and L1 strains are modified differently because their
antenna patterns differ. This could partly explain why H1 and L1 show
different residuals / anomalies in the current pipeline.

---

## 3. Where θ_SSZ Would Come From

### 3.1 Null-Geodesic Rotation

In a spacetime with non-trivial curvature, parallel transport of a null
vector along a path rotates the polarisation vector by the gravitational
Faraday rotation angle:

```
θ_GR(path) = -1/2 · ∮ Ric_μν k^μ k^ν ds    (vanishes in GR vacuum)
```

In GR vacuum (R_μν = 0) the rotation is zero. But SSZ modifies the
effective curvature through the RSG terms — so θ_SSZ may be non-zero.

### 3.2 RSG Holonomy Argument

From the Sagnac analogy (see SSZ_LIGO_SAGNAC_ANALOGY_PHASE_TRANSPORT.md):
the transport operator along a closed path is:

```
U(γ) = P exp(-∮_γ ω_μ^{ab} dx^μ)  ∈ SO(3,1)
```

In GR, this is the identity for a round-trip along a LIGO arm (flat local
geometry). In SSZ, the modified connection ω^{ab,SSZ} may produce a
non-trivial holonomy — specifically a rotation in the (x,y) polarisation
plane, which is a rotation in the SO(2) subgroup of SO(3,1).

**This rotation IS the twist angle θ_SSZ.**

### 3.3 V0 Placeholder Formula

Without a full derivation of ω^{ab,SSZ}, we cannot currently compute θ_SSZ.

A V0 conceptual placeholder based on dimensional analysis:

```
θ_SSZ^V0(r) ~ Ξ(r) · φ_geometry
```

where φ_geometry is a geometric phase factor of order 1 that depends
on the specific propagation path. This is CONCEPTUAL only — not derived.

For the weak field (detector location, r >> r_s):
```
θ_SSZ^V0 ~ Ξ_Earth ~ 10^{-9}  → negligible at detector
```

The dominant twist would arise from the source-side geometry, similar to
the dominant phase/amplitude SSZ effects.

---

## 4. Connection to Existing SSZ Corpus

| Concept | SSZ corpus location | Status |
|---------|-------------------|--------|
| D(r), Ξ(r), s(r) | ssz_core.py | LOCKED |
| δΨ_SSZ (inspiral phase) | derived_phase.py | LOCKED 0PN |
| δA_SSZ (amplitude) | derived_amplitude.py | LOCKED proxy |
| Spin connection ω_μ^{ab} | NOT DERIVED | MISSING |
| Holonomy in (x,y) plane | NOT DERIVED | MISSING |
| θ_SSZ(r,f) twist angle | NOT DERIVED | CONCEPTUAL |

---

## 5. Why the Current δA Anomaly May Be Partly Twist

The V0/V1 pipeline finds:

```
δA_SSZ median ~ -0.60  (60% amplitude suppression)
```

This is very large and may be physically implausible as a pure amplitude
effect. A possible reinterpretation:

```
- Part of the amplitude suppression may be a polarisation rotation
  that changes the projection of h_SSZ onto the detector
- The detector sees |F^+ · h_+ · cos θ + F^× · h_× · sin θ|
  instead of just |F^+ · h_+|
- For typical sky positions, this can reduce the effective amplitude
  by a factor that looks like a multiplicative scaling
```

This is currently speculative. It motivates the twist branch as a
**physically better-motivated model** than pure scalar amplitude scaling.

---

## 6. What Would Support or Falsify This Branch

| Signal | Interpretation |
|--------|---------------|
| H1/L1 amplitude ratio differs from GR antenna-pattern prediction | Could indicate polarisation rotation |
| Residual correlates with expected twist at given sky position | Supports twist model |
| Residual does not correlate with sky position | Falsifies geometry-dependent twist |
| Twist angle θ consistent with Ξ(r_source) | Supports SSZ origin |
| Twist angle θ >> Ξ | Inconsistent with SSZ weak-field limit |

---

## 7. Branch Registry Entry

```
Branch ID:      TWIST_POLARIZATION_PHASE_BRANCH
Formula status: DERIVED_V0_CONCEPTUAL
Observable:     h_I = F_I^+(h_+ cosθ - h_× sinθ) + F_I^×(h_+ sinθ + h_× cosθ)
Regime:         inspiral + merger (source-side)
Enters h(f):    YES — as effective polarisation angle offset
Required:       θ_SSZ(r,f) from spin connection ω^{ab,SSZ}
Anti-circularity: NO posterior ψ used, θ is SSZ-derived
Test type:      H1/L1 antenna-pattern residual analysis
Already run:    NO
Readiness:      CONCEPTUAL — θ_SSZ not yet derived
Blocker:        Γ^λ_μν^SSZ → ω^{ab,SSZ} → holonomy in SO(2)
READY_FOR_CLAIM: NO
```

---

## 8. Next Derivation Steps

```
Priority 1:
  Derive Γ^λ_μν^SSZ explicitly from SSZ metric
  → compute spin connection ω_μ^{ab,SSZ}
  → compute holonomy of ω in the x-y polarisation plane
  → this gives θ_SSZ(r) analytically

Priority 2:
  Check: does θ_SSZ vanish in Schwarzschild GR limit?
  → should: ω^{ab,GR} holonomy = 0 in vacuum (Bianchi identity)
  → SSZ correction: δω · holonomy → θ_SSZ

Priority 3:
  Compute θ_SSZ at source (r ~ r_ISCO, r ~ few r_s)
  → typical magnitude: Ξ(r_ISCO) ~ 0.1-0.8
  → twist might be O(0.1) rad — potentially observable!

Priority 4:
  Add θ_SSZ as free parameter in pipeline scan
  → same structure as epsilon_220 scan
  → vary θ from 0 to π/2, compute lnL difference
  → find threshold detectability

FORMULA_STATUS: DERIVED_V0_CONCEPTUAL
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```
