# SSZ Glossary (English)

**Status:** CANONICAL

---

## Core Concepts

| Term | Symbol | Definition |
|------|--------|------------|
| **Segment Density** | Ξ (Xi) | Dimensionless scalar field measuring spacetime segmentation at radius r. Range: 0 ≤ Ξ ≤ 0.802 |
| **Time Dilation** | D | SSZ time-dilation factor: D = 1/(1+Ξ). Ratio of proper time to coordinate time |
| **Scaling Factor** | s | Radial scaling: s = 1+Ξ = 1/D. Effective refractive index |
| **Schwarzschild Radius** | r_s | r_s = 2GM/c². Characteristic gravitational radius |
| **Golden Ratio** | φ | φ = (1+√5)/2 = 1.618... Structural constant in SSZ |
| **Intersection Point** | r* | Radius where D_SSZ = D_GR for a declared Xi form: r*/r_s = 1.594811 (decay/global) or 1.386562 (saturation/local) |

---

## Regimes

| Term | Definition |
|------|------------|
| **g1 (Weak Field)** | Regime where r/r_s > 2.2. SSZ ≡ GR. Formula: Ξ = r_s/(2r) |
| **g2 (Strong Field)** | Regime where r_s/r < 1.8. SSZ ≠ GR. Formula: Ξ = min(1-exp(-φr_s / r), Ξ_max) |
| **Blend Zone** | Transition region 1.8 ≤ r/r_s ≤ 2.2. Hermite C² interpolation |
| **Photon Sphere** | Region 2.2 ≤ r/r_s ≤ 3.0. SSZ optimal zone |
| **Coherence-Collapse** | Irreversible transition g1→g2. Not reversible |

---

## Methods

| Term | Definition |
|------|------------|
| **Ξ-proxy** | Direct use of Ξ for timelike observables (clocks, redshift) |
| **PPN** | Parameterized Post-Newtonian formalism. Used for null (light) and orbit observables |
| **PPN completion** | Multiplying Ξ-only result by (1+γ) for null observables |
| **Factor-2 rule** | Null observables need PPN (1+γ)=2, not Ξ-only |
| **Anti-circularity** | Principle: never calibrate formulas against data they predict |

---

## Key Values

| Term | Value | Meaning |
|------|-------|---------|
| **Ξ_max** | 0.802 | Maximum segment density (at horizon) |
| **D_min** | 0.555 | Minimum time dilation (at horizon) |
| **z_max** | 0.802 | Maximum redshift (at horizon) |
| **r*/r_s** | 1.594811 | Decay/global `D_SSZ = D_GR` intersection |
| **r*/r_s** | 1.386562 | Saturation/local `D_SSZ = D_GR` intersection |
| **φ/2** | 0.809 | Coupling factor |
| **β** | 1 | PPN parameter (exact) |
| **γ** | 1 | PPN parameter (exact) |

---

## Objects & Experiments

| Term | Definition |
|------|------------|
| **Dark Star** | SSZ alternative to black hole — no singularity, no event horizon, finite D |
| **Natural Boundary** | SSZ replacement for event horizon: r_φ = (φ/2)·r_s·[1+β·Δ(M)] |
| **Pound-Rebka** | 1960 experiment confirming gravitational redshift over 22.6 m |
| **Cassini** | 2003 Shapiro delay measurement: γ = 1.000021 ± 0.000023 |
| **S2 Star** | Star orbiting Sgr A* — weak-field test (SSZ ≡ GR) |
| **G79.29+0.46** | LBV nebula — exploratory molecular-zone diagnostics; current all-tests note a parsec-conversion warning |

---

## Mathematical Terms

| Term | Definition |
|------|------------|
| **Hermite C² interpolation** | Quintic polynomial ensuring continuity of function, first, and second derivatives |
| **Δ(M)** | Mass-dependent correction: Δ = A·exp(-α/M^B). From φ-geometry, not fitting |
| **v_esc** | Escape velocity: c·√(r_s/r) |
| **v_fall** | Free-fall velocity: c·√(r/r_s) |
| **Kinematic closure** | v_esc × v_fall = c² (universal invariant) |

---

## Deprecated

| Term | Status |
|------|--------|
| **Ξ = (r_s/r)² × exp(-r/r_φ)** | ❌ FORBIDDEN — deprecated formula, never use |
| **90/110 regime boundaries** | ❌ These are probe radii, NOT regime boundaries |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
