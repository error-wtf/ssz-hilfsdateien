# Segment Density Ξ(r)

**Status:** CANONICAL

---

## Definition

The segment density Ξ (Xi) is the central quantity in SSZ. It is a dimensionless, non-negative scalar field that measures the degree of spacetime segmentation at radial coordinate r from a gravitating mass M.

```
Ξ(r) ≥ 0    for all r
Ξ(r) → 0    as r → ∞
Ξ(r_s) = 1 - e^(-φ) ≈ 0.801712
```

For exterior horizon comparisons (`r >= r_s`) the key finite value is `Xi(r_s)=0.801712`. Some local/inner extrapolations approach 1 as `r -> 0`; do not confuse that extrapolation with the exterior horizon value.

---

## Weak-Field Formula (g1)

**Validity:** outer g1 branch; formula domain r/r_s > 2.2 (observationally indistinguishable from GR already for r/r_s > 10)

```
Ξ_weak(r) = r_s / (2r)
```

where r_s = 2GM/c² is the Schwarzschild radius.

**Properties:**
- Recovers GR time dilation to arbitrary precision
- Monotonically decreasing with r
- At Earth surface: Ξ ≈ 7 × 10⁻¹⁰
- At Sun surface: Ξ ≈ 2 × 10⁻⁶
- At GPS orbit: Ξ ≈ 7 × 10⁻¹⁰

---

## Inner Exponential Formula (g2 / decay form)

**Validity:** r_s/r < 1.8

```
Ξ_strong(r) = 1 - exp(-φ · r_s / r)
```

where φ = (1+√5)/2 = 1.618033988749895 is the golden ratio.

**Properties:**
- Gives the finite horizon value Ξ(r_s)=1-exp(-φ)
- Approaches 1 in the formal r→0 extrapolation (no divergence)
- Monotonically decreasing with r
- At Schwarzschild radius: Ξ(r_s) = 1 - e^(-φ) = 0.80171
- Continuous and smooth

---

## Blend Zone (Hermite C² Interpolation)

**Validity:** 1.8 ≤ r/r_s ≤ 2.2

```
t = (r/r_s - 1.8) / 0.4
Ξ_blend(r) = H₅(t)
```

The Hermite quintic interpolation H₅(t) ensures:
- Ξ is continuous at both boundaries
- dΞ/dr is continuous (C¹)
- d²Ξ/dr² is continuous (C²)

```
H₅(t) = (1-t)³(1+3t+6t²)·Ξ_strong(1.8·r_s) + t³(1+3(1-t)+6(1-t)²)·Ξ_weak(2.2·r_s)
         + derivative matching terms
```

This is not a free choice — it is the unique C² interpolant matching both function values and first two derivatives.

---

## Regime Boundaries Summary

| Regime | r/r_s | Operative Xi branch | Description |
|--------|-------|---------------------|-------------|
| very_close | < 1.8 | g2 / inner exponential | Near/at horizon |
| blended | 1.8–2.2 | H₅(t) | Smooth transition |
| photon_sphere | 2.2–3.0 | g1 branch | SSZ optimal physical zone |
| strong | 3.0–10.0 | g1 branch | Measurable deviations |
| weak | > 10.0 | Ξ_weak | GR-identical to tested precision |

---

## Key Values

| Location | r/r_s | Ξ_weak | Ξ_strong | Used |
|----------|-------|--------|----------|------|
| Earth surface | ~7×10⁸ | 7×10⁻¹⁰ | — | weak |
| Sun surface | ~5×10⁵ | 1×10⁻⁶ | — | weak |
| S2 perihelion | ~2800 | 1.8×10⁻⁴ | — | weak |
| Neutron star | ~2–3 | 0.167–0.250 | context-dependent | photon/strong |
| D-intersection r* | 1.595 / 1.387 | context-dependent | context-dependent | specify Xi form |
| Schwarzschild | 1.0 | 0.500 | **0.802** | strong |

---

## The Intersection Points r*

The invariant comparison is `D_SSZ = D_GR`, not a generic `Xi_weak = Xi_strong` crossing. Two source contexts exist:
```
r*/r_s = 1.594811  for Xi_A(x)=1-exp(-phi/x), D*=0.610710
r*/r_s = 1.386562  for Xi_B(x)=1-exp(-phi*x), D*=0.528007
```

Both intersections are:
- **Mass-independent** (purely geometric)
- **Derived**, not fitted
- Inside the phi bracket `1 < r*/r_s < phi`

---

## DEPRECATED Formula (FORBIDDEN)

```
❌ Ξ = (r_s/r)² × exp(-r/r_φ)   — VERBOTEN
```

This old formula appears in some early drafts. It is **permanently deprecated** and must never be used in any new calculation or derivation.

---

## Cross-References

- [Time dilation D(r)](time_dilation.md) — D = 1/(1+Ξ)
- [Regime definitions](regime_definitions.md) — 5 regimes, blend zone
- [Regime vs formula domains](regime_and_formula_domain_clarification.md) — Why formula choice matters
- [Formula compendium](../03_FORMULAS/formula_compendium.md) — Complete formula list
- [Special values](../03_FORMULAS/special_values.md) — Ξ(rₛ)=0.802, D(rₛ)=0.555
- [Forbidden formulas](../03_FORMULAS/forbidden_formulas.md) — Deprecated variants
- Tests: `test_xi_calculations.py`, `test_xi_strong.py` in [segmented-calculation-suite](https://github.com/error-wtf/segmented-calculation-suite)

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
