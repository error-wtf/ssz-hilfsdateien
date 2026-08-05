# Xi_strong Branch Lock
Status: LOCKED_DOCUMENTATION
Generated: 2026-05-18
Source: ssz-complete-documentation/02_FOUNDATIONS/regime_and_formula_domain_clarification.md
Source: ssz-complete-documentation/03_FORMULAS/formula_compendium.md §B.1

---

## Two Forms — Classification

| Form | Formula | Classification | Valid For |
|------|---------|----------------|-----------|
| **Saturation / g2** | `Xi = min(1 - exp(-phi * r/rs), Xi_max)` | **CANONICAL_OPERATIONAL** | r/rs < 1.8 (g2 domain) |
| Decay / didactic | `Xi = 1 - exp(-phi * rs/r)` | **DIDACTIC_COMPLEMENTARY** | Complementary, not operative |
| Old exponential | `Xi = (rs/r)^2 * exp(-r/r_phi)` | **INVALID_DEPRECATED** | FORBIDDEN everywhere |

### Source Text (regime_and_formula_domain_clarification.md §Saturation vs Decay)

> "Two variants of the strong-field formula exist. Only the saturation form is operative:
>  Saturation (operative): Xi = min(1−exp(−φ·r/rₛ), Xi_max)
>  Decay (didactic only): Xi = 1−exp(−φ·rₛ/r)"

> "Both agree exactly at r = rₛ but differ in asymptotic limits."

### Asymptotic Comparison

| Limit | Saturation (CANONICAL) | Decay (didactic) |
|-------|----------------------|-----------------|
| r → 0 | Xi → 0 (regular) | Xi → Xi_max (saturates) |
| r → ∞ | Xi → Xi_max ≈ 0.802 | Xi → 0 (decays) |
| r = rs | Xi = 0.802 | Xi = 0.802 (**identical**) |

---

## Current ssz_core.py Audit

- Function `xi_strong(r, rs)` uses: `1 - exp(-phi * rs/r)` → **DECAY FORM (DIDACTIC_COMPLEMENTARY)**
- Comment says: `Formula: Ξ_strong(r) = min(1 - exp(-φr_s / r), Ξ_max)` → contradicts implementation
- At r = rs: both forms give Xi = 0.802 → no error in past D_min tests
- At other r: results DIFFER

**STATUS: MISMATCH_DECAY_NOT_CANONICAL**
**ACTION: xi_strong_saturation() added as CANONICAL; xi_strong_decay() preserved as DIDACTIC_COMPLEMENTARY**

---

## LIGO Pipeline Implication

The LIGO inspiral band covers r >> rs (weak field, g1 domain).
Xi_weak = rs/(2r) is used in the LIGO band — this is correct and unambiguous.
Xi_strong form difference is LIGO-band-irrelevant for current pipeline.
However: explicit labelling is required; implicit branch selection is FORBIDDEN.

---

## Required Implementation

```python
def xi_strong_saturation(r, rs, phi=PHI):
    """CANONICAL_OPERATIONAL — g2 domain, r/rs < 1.8."""
    xi = 1 - np.exp(-phi * r / rs)
    return np.minimum(xi, XI_MAX)

def xi_strong_decay(r, rs, phi=PHI):
    """DIDACTIC_COMPLEMENTARY — not for production use."""
    xi = 1 - np.exp(-phi * rs / r)
    return np.minimum(xi, XI_MAX)
```

Default in production code: xi_strong_saturation only.
Tests must verify branch is never implicit.

---

## 39% QNM Branch — Model History

The 39% QNM shift (f_SSZ/f_GR ≈ 1.39) comes from:
  `1/D(r*)` at r* = 1.387 rs (photon sphere), D(r*) = 0.72

Classification: **HISTORICAL_PHOTON_SPHERE_OR_QNM_SPECTRUM_BRANCH**
Status: **DISCARDED_FOR_LIGO_STRAIN_TEST**

Reason: LIGO measures calibrated laboratory strain after strong→weak propagation.
The 39% is a raw strong-field frequency ratio, not a strain deformation.
The correct LIGO observable is deltaPsi_SSZ(f) after RSG phase accounting.

---
© 2026 SSZ-LIGO Test Suite
