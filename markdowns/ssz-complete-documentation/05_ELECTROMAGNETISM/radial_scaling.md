# Radial Scaling Gauge

**Status:** CANONICAL
**Paper:** 01 — Radial Scaling Gauge for Maxwell Fields

---

## The Scaling Factor

SSZ defines a radial scaling factor:
```
s(r) = 1 + Ξ(r) = 1/D(r)
```

This factor transforms the radial coordinate to a "physical" (segmented) coordinate:
```
dρ = s(r) · dr
```

where ρ is the physical (segmented) radial distance and r is the coordinate distance.

---

## Electromagnetic Field Scaling

In the presence of segmentation, electromagnetic fields are scaled:
```
E'(r) = s(r) · E(r)
B'(r) = s(r) · B(r)
```

This means fields are **stronger** in regions of higher segmentation.

---

## Effective Refractive Index

The scaling factor acts as an effective refractive index:
```
n_eff(r) = s(r) = 1 + Ξ(r)
```

This is the key connection between segmentation and light propagation:
- Light travels slower (in coordinate terms) through highly segmented regions
- The Shapiro delay arises naturally from this effective index
- No new physics is needed — just the geometric consequence of segmentation

---

## Maxwell Equations with Scaling

The modified Maxwell equations in segmented spacetime:
```
∇ · (s² E) = 0
∇ × (s² B) = μ₀ε₀ s² ∂E/∂t
```

### Wave Equation
The transformed wave equation in 1D:
```
(1/s) ∂/∂r [(1/s) ∂E/∂r] - (1/c²) ∂²E/∂t² = 0
```

**CRITICAL:** When transforming dρ = s(r)·dr, the second-derivative operator includes an extra s·s' term. Missing this term is a **technical error**, not physics (see Paper 01, Section 4).

---

## Key Values

| Location | s(r) | n_eff | Effect |
|----------|------|-------|--------|
| r → ∞ | 1 | 1 | No scaling |
| Sun surface | 1.000001 | 1.000001 | Tiny |
| NS surface | 1.3–1.5 | 1.3–1.5 | Measurable |
| r = r_s | **1.802** | **1.802** | Strong scaling |

---

## Validation

- 45/45 tests PASS (2025-12-28)
- GPS, Pound-Rebka, S2 star validated
- 13 astronomical objects consistent
- PPN correction (1+γ) for Shapiro/Lensing confirmed

---

## Tests

| Test | Repository |
|------|------------|
| test_radial_scaling.py | frequency-curvature-validation |
| All 45 tests | maxwell (FINAL_TEST_REPORT_2025-12-28.md) |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
