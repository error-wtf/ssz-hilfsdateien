# Coherence Collapse: g1 -> g2 Transition

**Book reference:** Ch 25 (Coherence-Collapse Law)  
**Test file:** `test_regime_transition.py`  
**Paper:** 25 (Coherence-Collapse Law)

---

## Overview

SSZ distinguishes two fundamental regimes, and the transition between them is **irreversible** (one-directional). This is called the coherence collapse.

```
g1 (Weak Field / PPN regime)  -->  g2 (Strong Field / structured)
           IRREVERSIBLE — cannot go back
```

## Regime Definitions

### g1: Weak Field (PPN Regime)
- Valid for: `r/r_s > 2.2`
- Formula: `Xi_g1(r) = r_s / (2r)` (PPN weak-field expansion)
- Physics: spacetime is approximately flat, gravitational effects are perturbative
- Tests: standard PPN tests (GPS, Shapiro, lensing) — all pass

### g2: Strong Field (Structured Regime)
- Valid for: `r_s/r < 1.8`
- Formula: `Xi_g2(r) = 1 - exp(-phi * r_s / r)` (phi-geometry, saturation)
- Physics: segment density approaches saturation, GR divergence is regularized
- Tests: neutron star redshift (+13% deviation from GR), black hole shadow (-1.3%)

## The Collapse Condition

The transition g1 -> g2 occurs when matter or radiation crosses into the blend zone `1.8 < r/r_s < 2.2`. Once in g2, the system **cannot** return to g1 description — the coherence of the weak-field segment arrangement is lost and the strong-field structure takes over.

```
Collapse criterion:  r/r_s < r_collapse/r_s  ≈ 2.0
```

## Physical Interpretation

In GR, spacetime curvature grows smoothly without any discrete transition. In SSZ, the segment lattice has a **maximum packing density** that creates a natural scale:

- When `r >> r_s`: segments are sparse, PPN describes them well
- When `r ~ r_s`: segments reach maximum density, phi-geometry takes over
- The transition is irreversible because re-expansion would require "un-packing" segments, which violates entropy

## Observable Consequences

| Observable | g1 (weak) | g2 (strong) | Delta |
|------------|-----------|-------------|-------|
| Time dilation | GR = SSZ | D_SSZ > D_GR | +13% for NS |
| Redshift | z = Xi | z = Xi_strong | measurable for NS |
| QNM frequency | same as GR | f * 1/D(r*) | +39% shift |
| BH shadow | same as GR | smaller | -1.3% |

## Irreversibility Proof Sketch

The collapse is irreversible because the segment density functional has a unique minimum-energy configuration in each regime. The blend zone `[1.8, 2.2]` is a C2-smooth transition (quintic Hermite), but the physical process of crossing it creates entropy that cannot be undone without external energy input exceeding the gravitational binding energy.

## Anti-Patterns

```
WRONG: Apply Xi_g1 inside r_s/r < 1.8 (gives divergence at r_s)
WRONG: Apply Xi_g2 for GPS calculations (wrong by 0.01%)
CORRECT: Use regime_selector(r) to pick automatically
```

## Relation to Other Sections

- [Regime Definitions](regime_definitions.md) — complete table of all 5 regimes, two-layer clarification
- [Regime vs formula domains](regime_and_formula_domain_clarification.md) — Formula boundaries ≠ regime boundaries, numerical evidence
- [Segment Density Xi](segment_density.md) — both formulas (g₁/g₂)
- [Time dilation D(r)](time_dilation.md) — D = 1/(1+Ξ)
- [phi-Lattice Discretization](phi_lattice_discretization.md) — why φ appears in Ξ_g2
- [Singularities Resolved](../06_STRONG_FIELD/singularities.md) — the g₂ regime prevents divergence
- [Forbidden formulas](../03_FORMULAS/forbidden_formulas.md) — Deprecated variants incl. Ξ=rₛ/(r−rₛ)

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
