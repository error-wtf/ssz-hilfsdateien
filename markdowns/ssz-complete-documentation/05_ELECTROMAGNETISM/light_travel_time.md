# Additive Light-Travel Time Decomposition

**Status:** CANONICAL
**Paper:** 23 — Additive Decomposition of the Observed Light-Travel Time

---

## Core Idea

The total observed light-travel time between two points can be decomposed additively:

```
Δt_total = Δt_flat + Δt_grav
```

where:
- Δt_flat = travel time in flat spacetime (Euclidean distance / c)
- Δt_grav = gravitational delay from segmentation

---

## Gravitational Delay

```
Δt_grav = (1/c) ∫ (s(r) - 1) dr = (1/c) ∫ Ξ(r) dr
```

This integral is taken along the light path. The delay is caused by the effective refractive index n_eff = s(r) = 1 + Ξ(r).

---

## Shapiro Delay

The Shapiro delay is a special case of the additive decomposition:
```
Δt_Shapiro = (1/c) ∫ Ξ(r) dr  (Ξ-only, g_tt contribution)
```

**CRITICAL:** For the full GR-equivalent Shapiro delay, PPN completion is required:
```
Δt_full = (1 + γ) · Δt_Ξ = 2 · Δt_Ξ    (γ=1)
```

The factor 2 comes from PPN (g_tt + g_rr), not from double counting.

### Shapiro Delay Formula
```
Δt_Shapiro = (1+γ) · (r_s/c) · ln(4r₁r₂/d²)
           = 2 · (r_s/c) · ln(4r₁r₂/d²)
```

**ALWAYS distinguish:**
- One-way signal delay vs round-trip radar echo (extra factor 2)
- This is **separate** from PPN (1+γ). Never conflate them.

---

## Cassini Measurement (2003)

The Cassini spacecraft provided the most precise measurement:
```
γ = 1.000021 ± 0.000023
```
SSZ predicts γ = 1 exactly → within measurement uncertainty.

---

## Tests

| Test | Repository |
|------|------------|
| test_shapiro_delay.py | frequency-curvature-validation |
| test_cassini.py | frequency-curvature-validation |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
