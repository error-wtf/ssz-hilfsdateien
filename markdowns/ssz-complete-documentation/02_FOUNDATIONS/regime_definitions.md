# Regime Definitions

**Status:** CANONICAL

---

## Overview

SSZ defines five regimes based on the ratio r/r_s (distance to Schwarzschild radius):

| Regime | r/r_s range | Operative Xi branch | Physical context |
|--------|------------|---------------------|------------------|
| **very_close** | < 1.8 | g2 / inner exponential | At/near horizon |
| **blended** | 1.8–2.2 | Hermite C² interpolation | Smooth transition |
| **photon_sphere** | 2.2–3.0 | g1 formula, photon-sphere regime | Photon orbit zone |
| **strong** | 3.0–10.0 | g1 formula, strong physical regime | Neutron stars, compact objects |
| **weak** | > 10.0 | Ξ_weak = r_s/(2r) | Solar System, GPS, stars |

The operative formula domain and the physical regime label are not identical. Above `r/r_s=2.2`, the current calculation branch uses the g1/weak-form expression for Xi, but the physical regime is still "photon_sphere" up to 3.0 and "strong" up to 10.0.

---

## Regime Check (MANDATORY)

**Before using any Ξ formula, determine regime via r/r_s.**

The wrong formula in the wrong regime produces incorrect results. This is the most common source of apparent contradictions in SSZ.

```python
def get_regime(r, r_s):
    ratio = r / r_s
    if ratio < 1.8:
        return 'very_close'   # g2 / inner exponential
    elif ratio <= 2.2:
        return 'blended'      # Hermite C²
    elif ratio <= 3.0:
        return 'photon_sphere' # physical regime; operative branch is g1
    elif ratio <= 10.0:
        return 'strong'       # physical regime; operative branch is g1
    else:
        return 'weak'         # Ξ_weak
```

---

## Regime Transition: The Blend Zone

The transition between Ξ_weak and Ξ_strong is NOT a discontinuity. It uses Hermite C² interpolation:

```
t = (r/r_s - 1.8) / 0.4      (normalized: 0 at r/r_s=1.8, 1 at r/r_s=2.2)
Ξ_blend = H₅(t)               (quintic Hermite polynomial)
```

This guarantees:
- **C⁰ continuity:** Ξ matches at both boundaries
- **C¹ continuity:** dΞ/dr matches at both boundaries
- **C² continuity:** d²Ξ/dr² matches at both boundaries

**Never mix formulas without an explicit blend rule.**

For the exact formula-domain table, see [regime and formula domain clarification](regime_and_formula_domain_clarification.md). That file is authoritative for deciding which `Xi` branch is evaluated.

---

## Irreversible Coherence-Collapse: g₁ → g₂

The transition from weak (g₁) to strong (g₂) is **unidirectional**:

```
g₁ → g₂: Irreversible (spacetime regime assignment)
g₂ → g₁: FORBIDDEN (spacetime does not spontaneously de-segment)
```

This is a fundamental postulate, not a computational convenience. Once a region of spacetime enters the strong-field segmentation regime, it does not spontaneously return to weak-field behavior.

### Important Clarification: Two Layers of Transition

SSZ distinguishes two conceptually different processes that must not be conflated:

**Layer 1 — Spacetime regime assignment (irreversible):**
Once a spatial region acquires g₂ segmentation (e.g., by gravitational collapse), the regime label is permanent. The spacetime itself does not "un-segment." This is what "g₂ → g₁: FORBIDDEN" means.

**Layer 2 — Matter/radiation moving through regimes (physical process):**
Matter and radiation CAN physically move from a g₂ region outward into g₁ space (e.g., during supernova explosion, black hole ringdown, or metric perturbation emission). When this happens, the coherence structure of the segment lattice undergoes an **irreversible collapse** — the ordered g₂ packing is destroyed as the material expands into the disordered g₁ environment. This process is described in detail in Book Chapter 25.

The g₂ → g₁ coherence collapse (Layer 2) is NOT the reversal of the g₁ → g₂ regime assignment (Layer 1). It is a distinct, entropy-producing physical process analogous to melting: the spacetime region remains g₂, but matter ejected from it loses its coherent segment structure as it enters g₁ space. ΔS_seg > 0 always.

**Summary:**
- Spacetime regime: g₁ → g₂ irreversible, g₂ → g₁ forbidden
- Matter motion: matter CAN move from g₂ regions to g₁ regions; when it does, coherence collapses irreversibly (ΔS > 0)

---

## IMPORTANT: 90/110 vs 1.8/2.2

Some repositories use r/r_s = 90–110 as boundaries. **These are NOT regime boundaries!**

They are **probe radii** (test sampling points) for continuity checks in `unified_validation.py`. The actual physical regime boundaries are at r/r_s = 1.8 and 2.2.

---

## Typical Ξ Values per Regime

| Regime | Ξ range | Example objects |
|--------|---------|----------------|
| very_close | 0.5–0.802 | Horizon, near-BH |
| blended | 0.22–0.5 | Compact NS, r* zone |
| photon_sphere | 0.13–0.22 | Photon orbits |
| strong | 0.05–0.13 | Outer NS envelope |
| weak | < 0.05 | Everything in Solar System |

---

## Cross-References

- [Segment density Ξ(r)](segment_density.md) — Weak, strong, blend formulas
- [Regime vs formula domains](regime_and_formula_domain_clarification.md) — Why formula boundaries ≠ regime boundaries
- [Coherence collapse](coherence_collapse.md) — g₁→g₂ irreversible transition
- [Time dilation D(r)](time_dilation.md) — D = 1/(1+Ξ)
- [Formula compendium §B.2](../03_FORMULAS/formula_compendium.md) — Hermite C² details
- [Special values](../03_FORMULAS/special_values.md) — Ξ(rₛ)=0.802, D(rₛ)=0.555
- [Forbidden formulas](../03_FORMULAS/forbidden_formulas.md) — Deprecated variants
- Test: `test_regime_definitions.py` in [segmented-calculation-suite](https://github.com/error-wtf/segmented-calculation-suite)

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
