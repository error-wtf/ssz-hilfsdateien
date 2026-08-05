# Complete Formula Compendium

**Status:** CANONICAL — Single Source of Truth

---

## B.1 Fundamental Equations

### Segment Density Ξ(r)

**g1 / weak-form branch** (asymptotically weak; operative outer branch above the blend):
```
Ξ_weak(r) = r_s / (2r)
```

**Inner exponential / decay form** (operative g2 branch in `segcalc`, r_s/r < 1.8):
```
Ξ_strong(r) = 1 - exp(-φ × r_s / r)
```

**Local saturation form** (metric-pure/paper-local comparison; not global weak-field asymptotic):
```
Ξ_sat(r) = min(1 - exp(-φ × r_s / r), Ξ_max)
```

**Blend Zone** (1.8 ≤ r/r_s ≤ 2.2):
```
Ξ_blend(r) = H₅(t),  t = (r/r_s - 1.8) / 0.4
```

### Time Dilation D(r)
```
D_SSZ(r) = 1 / (1 + Ξ(r))
```
Limits: D(r→∞) = 1, D(r_s) = 0.555

### Gravitational Redshift
```
z_SSZ(r) = 1/D(r) - 1 = Ξ(r)
```

### Schwarzschild Radius
```
r_s = 2GM / c²
```

### Scaling Factor
```
s(r) = 1 + Ξ(r) = 1 / D(r)
```

---

## B.2 Regime Definitions

| Regime | r/r_s | Operative Xi branch | Physical meaning |
|--------|-------|---------------------|------------------|
| very_close | < 1.8 | inner exponential / g2 | near-horizon |
| blended | 1.8–2.2 | Hermite C² | transition |
| photon_sphere | 2.2–3.0 | g1 formula | photon orbit zone |
| strong | 3.0–10.0 | g1 formula | compact-object strong field |
| weak | > 10.0 | Ξ_weak | Solar System / GPS |

### Hermite C² Interpolation
```
t = (r/r_s - 1.8) / 0.4
H₅(t) = (1-t)³(1+3t+6t²)Ξ_strong(1.8r_s) + t³(1+3(1-t)+6(1-t)²)Ξ_weak(2.2r_s) + derivative terms
```

### Irreversible Coherence-Collapse
```
g₁ → g₂: Unidirectional (not reversible)
```

---

## B.3 Kinematics

### Dual Velocities
```
v_esc(r) = c · √(r_s / r)
v_fall(r) = c · √(r / r_s) = c² / v_esc

INVARIANT: v_esc × v_fall = c²  (for all r)
```

### Lorentz Indeterminacy at v=0
```
GR:  γ_GR(v=0) = 1  (trivial)
SSZ: γ_SSZ(v) = exp(Ξ · v²/c²),  γ_SSZ(v=0) = 1 (regular, with gravitational encoding)
```

### Kinematic Closure
```
v_esc(r) × v_fall(r) = c²   (independent of M!)
```

---

## B.4 Electromagnetism

### Radial Scaling Gauge
```
s(r) = 1 + Ξ(r) = 1/D(r)
E'(r) = s(r) · E(r)
B'(r) = s(r) · B(r)
```

### Maxwell Wave Equation with Scaling
```
∇ · (s² E) = 0
∇ × (s² B) = μ₀ε₀ s² ∂E/∂t
```

### Segment-Based Group Velocity
```
v_group = L_seg · f / N
```

### Additive Light-Travel Time
```
Δt_total = Δt_flat + Δt_grav
Δt_grav = ∫ (s(r) - 1) dr/c = ∫ Ξ(r) dr/c
```

---

## B.5 PPN Formulas

**CRITICAL:** Lensing and Shapiro use PPN (γ=1), NOT Ξ-based formulas!

### Lensing Deflection
```
α_lens = (1 + γ) · r_s / b = 2 · r_s / b
```
Eddington 1919: α = 1.75 arcsec (confirmed)

### Shapiro Delay
```
Δt_Shapiro = (1 + γ) · (r_s / c) · ln(4 r₁ r₂ / d²) = 2 · (r_s / c) · ln(4 r₁ r₂ / d²)
```
Cassini 2003: γ = 1.000021 ± 0.000023

**WARNING:** Distinguish one-way vs round-trip (factor 2 is separate from PPN)!

### Perihelion Precession
```
Δω = 6πGM / [a(1-e²)c²]
```
SSZ = GR (standard PPN with β=γ=1). Mercury: 42.98"/century.

### PPN Parameters
```
β = 1 (exact in SSZ)
γ = 1 (exact in SSZ)
```

---

## B.6 Structural Constants

| Constant | Value | Role |
|----------|-------|------|
| φ | 1.618033988749895 | Fundamental segmentation constant |
| π | 3.141592653589793 | Division constant |
| α | 1/137.036 | Fine-structure (SSZ: geometric origin) |
| φ/2 | 0.80902 | Coupling factor |

---

## B.7 Special Values & Invariants

### At Schwarzschild Radius
```
Ξ(r_s) = 1 - exp(-φ) = 0.80171
D_SSZ(r_s) = 1/(1 + 0.80171) = 0.55503
z_SSZ(r_s) = 0.80171
```
**FINITE** (not 0 or ∞ like GR!)

### D-Intersection Comparisons
```
r*/r_s = 1.594811   for Xi_A(x)=1-exp(-phi/x)
D_SSZ(r*) = D_GR(r*) = 0.610710

r*/r_s = 1.386562   for Xi_B(x)=1-exp(-phi*x)
D_SSZ(r*) = D_GR(r*) = 0.528007
```
Both are mass-independent. Always state which Xi form is being used.

### Natural Boundary
```
r_φ = (φ/2) · r_s · [1 + β · Δ(M)]
```

### Mass-Dependent Correction
```
Δ(M) = A · exp(-α / M^B)
A = 98.01, α = 2.7177 × 10⁴, B = 1.96
```
From φ-geometry, NOT data fitting.

### Fundamental Constants

| Constant | Symbol | Value | Unit |
|----------|--------|-------|------|
| Speed of light | c | 299,792,458.0 | m/s |
| Gravitational const. | G | 6.67430 × 10⁻¹¹ | m³/(kg·s²) |
| Planck constant | ℏ | 1.054571817 × 10⁻³⁴ | J·s |
| Solar mass | M☉ | 1.98892 × 10³⁰ | kg |

---

## B.8 Energy Conditions

```
For r ≥ 5 r_s:
  ρ_eff ≥ 0                      (WEC: Weak Energy Condition)
  ρ_eff + p_r ≥ 0                (DEC: Dominant Energy Condition)
  ρ_eff + p_r + 2p_⊥ ≥ 0        (SEC: Strong Energy Condition)

Radial equation of state: p_r = -ρ_eff · c²
```

---

## Cross-Reference: Formula → Chapter → Test

| Formula | Paper | Primary Test |
|---------|-------|--------------|
| Ξ_weak | 01, 03 | test_ppn_exact.py |
| Ξ_strong | 04, 16 | test_xi_strong.py |
| D_SSZ | 03 | test_dilation_finite.py |
| z_SSZ | 21 | test_redshift.py |
| v_esc × v_fall | 02 | test_vfall_duality.py |
| γ_SSZ(v=0) | 19 | test_lorentz_limit.py |
| s(r) | 01 | test_radial_scaling.py |
| α_lens (PPN) | 01, 10 | test_lensing_deflection.py |
| Δt_Shapiro | 01 | test_shapiro_delay.py |
| Δω (perihelion) | PPN | test_perihelion.py |
| Δ(M) | 18 | test_phi_correction.py |
| Energy Cond. | 04 | test_energy_conditions.py |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
