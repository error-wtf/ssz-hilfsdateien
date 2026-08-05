# Core Postulates of SSZ

**Status:** CANONICAL

---

## Postulate 1: Segment Density Field

There exists a dimensionless, non-negative scalar field **Ξ(r)** (segment density) that characterizes the degree of spacetime segmentation at radial coordinate r from a gravitating mass.

- Ξ is determined by mass M and radius r (not freely tunable)
- Ξ ≥ 0 everywhere
- Ξ → 0 as r → ∞ (flat spacetime limit)
- Ξ is bounded: Ξ ≤ Ξ_max = 1 - e^(-φ) ≈ 0.80171

---

## Postulate 2: Modified Time Dilation

The SSZ time-dilation factor is:
```
D_SSZ(r) = 1 / (1 + Ξ(r))
```

This replaces the GR expression D_GR(r) = √(1 - r_s/r) in the strong field while converging to it in the weak field.

Consequences:
- D(r→∞) = 1 (no dilation far from mass)
- D(r_s) = 0.55503 (finite, not zero!)
- D is monotonically increasing with r
- No singularity at any finite r

---

## Postulate 3: Two-Regime Structure

### g1 — Weak Field (r/r_s > 2.2)
```
Ξ_weak(r) = r_s / (2r)
```
Recovers GR to arbitrary precision. PPN parameters β = γ = 1 (exact).

### g2 — Strong Field (r_s/r < 1.8)
```
Ξ_strong(r) = 1 - exp(-φ · r_s / r)
```
Saturates at Ξ_max. Finite time dilation at all radii.

### Transition (1.8 ≤ r/r_s ≤ 2.2)
Hermite C² interpolation ensures continuous Ξ, dΞ/dr, d²Ξ/dr².

---

## Postulate 4: φ-Geometry Constraint

The golden ratio φ = (1+√5)/2 = 1.618... enters as a **structural constant**, not a free parameter:

- Ξ_strong uses φ as exponential scale
- Coupling radius: r_φ = (φ/2) · r_s · [1 + β · Δ(M)]
- φ/2 = 0.80902 appears as coupling factor
- The ratio φ constrains regime transitions and scaling behavior

This is treated as a constraint that reduces arbitrariness, not numerology.

---

## Postulate 5: Observable → Method Assignment

Not all observables use the same formula. SSZ mandates:

| Observable Type | Method | Formula |
|----------------|--------|---------|
| Timelike (clocks, redshift) | Ξ-based | D = 1/(1+Ξ) |
| Null (light: lensing, Shapiro) | PPN (1+γ) | result = Ξ_only × (1+γ) |
| Orbit (precession) | PPN (β,γ) | Standard PPN machinery |

**This is the Prime Directive: Never use a single method for all observables.**

---

## Postulate 6: No Free Parameters

SSZ has exactly **zero** tunable fitting parameters:
- φ is a mathematical constant
- β, γ are PPN parameters (both = 1)
- Formula-domain boundaries are fixed by the canonical 1.8/2.2 blend rule; `r*` values are derived `D_SSZ = D_GR` comparisons for declared Xi forms
- Mass-dependent correction Δ(M) follows from φ-geometry

If SSZ predictions are wrong, SSZ is wrong — there is no knob to turn.

---

## Postulate 7: Irreversible Coherence-Collapse

The transition from g1 to g2 is **unidirectional**:
```
g₁ → g₂: Irreversible (not reversible)
```

Once spacetime segmentation reaches the strong-field regime, it does not spontaneously return to the weak-field state. This is a thermodynamic-style arrow, not a dynamical instability.

---

## Postulate 8: Anti-Circularity

SSZ formulas must never be calibrated against the data they are used to predict. Every prediction follows from:
```
Mass M → r_s → Ξ(r) → D(r) → Observable
```
The chain is one-directional. Reverse inference (observable → Ξ → M) is used only for consistency checks, never for calibration.

---

## Summary Table

| # | Postulate | Expression |
|---|-----------|------------|
| 1 | Segment density | Ξ(r) ≥ 0, bounded |
| 2 | Time dilation | D = 1/(1+Ξ) |
| 3 | Two regimes | g1: weak, g2: strong |
| 4 | φ-constraint | φ as structural constant |
| 5 | Method assignment | Observable → Class → Method |
| 6 | No free parameters | Zero tunable knobs |
| 7 | Irreversible g1→g2 | Coherence-collapse law |
| 8 | Anti-circularity | No data → formula feedback |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
