# Regime Boundary Lock
Status: LOCKED_DOCUMENTATION
Generated: 2026-05-18
Source: ssz-complete-documentation/02_FOUNDATIONS/regime_and_formula_domain_clarification.md
Source: ssz-complete-documentation/03_FORMULAS/formula_compendium.md §B.2

---

## Canonical Boundaries (Formula Domains)

| Constant Name | Value (r/rs) | Source | Formula Applied |
|--------------|-------------|--------|----------------|
| BLEND_END (g1 starts) | **2.2** | formula_compendium §B.2 | Xi_weak = rs/(2r) |
| BLEND_START (g2 ends) | **1.8** | formula_compendium §B.2 | Xi_strong (saturation) |
| g2 domain | < 1.8 | regime_and_formula_domain_clarification.md | saturation form |
| blend zone | 1.8 – 2.2 | formula_compendium §B.2 | Hermite C² |
| g1 domain | > 2.2 | formula_compendium §B.2 | Xi_weak |

### Source Text (formula_compendium.md §B.2)

> "| very_close | < 1.8 | inner exponential / g2 |"
> "| blended    | 1.8–2.2 | Hermite C²             |"

---

## Physical Regime Classification (Interpretive, NOT formula boundaries)

| Regime | r/rs | Xi Formula Used | Note |
|--------|------|----------------|------|
| very_close | < 1.8 | g2 saturation | near horizon |
| blended | 1.8–2.2 | Hermite C² | transition |
| photon_sphere | 2.2–3.0 | g1 weak | photon orbit |
| strong | 3.0–10.0 | g1 weak | compact objects |
| weak | > 10.0 | g1 weak | Solar System, GPS |

**WARNING:** "g1 formula above 2.2" ≠ "weak field above 2.2".
Physical regime 'strong' uses g1 formula for r/rs in 3.0–10.0.

---

## ssz_core.py Boundary Audit

| Item | Canonical | ssz_core.py | Match |
|------|-----------|-------------|-------|
| BLEND_END | 2.2 | 2.2 | ✅ |
| BLEND_START | 1.8 | **1.0** (regime_label) | ❌ MISMATCH |
| constants.py REGIME_STRONG_THRESHOLD | 0.8 | 0.8 | partial — different from 1.8 |

**STATUS: REGIME_BOUNDARY_LOWER_MISMATCH**
- `constants.py` has `REGIME_STRONG_THRESHOLD = 0.8` (< canonical 1.8)
- `ssz_core.py regime_label()` uses `ratio <= 1.0` for STRONG
- Canonical lower boundary of g2 domain is **1.8**

---

## Required Named Constants

```python
# Regime boundaries — source-locked, never silently hardcoded
BLEND_START: float = 1.8   # r/rs below this → g2 domain (saturation)
BLEND_END:   float = 2.2   # r/rs above this → g1 domain (weak)
# Between 1.8 and 2.2 → Hermite C² blend

# Physical regime thresholds (interpretive, uses g1 formula above BLEND_END)
STRONG_FIELD_R_OVER_RS_MAX: float = 10.0   # above → weak regime
WEAK_FIELD_R_OVER_RS_MIN:   float = 10.0   # below → strong regime
PHOTON_SPHERE_R_OVER_RS:    float = 1.387  # universal intersection
```

---

## Continuity Requirements at Blend Boundaries

Xi, D = 1/(1+Xi), and phase proxy must be C² continuous across blend zone.
Tests must verify:
- Xi is continuous at r = 1.8 rs and r = 2.2 rs
- dXi/dr is continuous at both boundaries
- No jumps in D or deltaPsi proxy

---
© 2026 SSZ-LIGO Test Suite
