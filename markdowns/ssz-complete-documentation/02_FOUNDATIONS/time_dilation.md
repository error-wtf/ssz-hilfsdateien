# Time Dilation D(r)

**Status:** CANONICAL

---

## The SSZ Time-Dilation Factor

```
D_SSZ(r) = 1 / (1 + Ξ(r))
```

This is the ratio of proper time (τ) to coordinate time (t):
```
dτ = D_SSZ(r) · dt
```

---

## Comparison with GR

```
D_GR(r)  = √(1 - r_s/r)
D_SSZ(r) = 1/(1 + Ξ(r))
```

| Property | D_GR | D_SSZ |
|----------|------|-------|
| r → ∞ | 1 | 1 |
| r = r_s | **0** (singular) | **0.555** (finite) |
| r < r_s | Imaginary | Still finite |
| Monotonic | Yes | Yes |
| Smooth | Yes (except r_s) | Yes (everywhere) |

---

## Values Across Object Classes

| Object | r/r_s | D_GR | D_SSZ | Δ(%) | Regime |
|--------|-------|------|-------|------|--------|
| Earth (surface) | ~7×10⁸ | 0.9999999993 | 0.9999999993 | ~0% | weak |
| Sun (surface) | ~5×10⁵ | 0.999999 | 0.999999 | ~0% | weak |
| White dwarf | ~10³ | 0.9995 | 0.9995 | <0.01% | weak |
| GPS satellite | ~10⁹ | 0.99999999994 | 0.99999999994 | ~0% | weak |
| Mercury perihelion | ~10⁷ | 0.99999997 | 0.99999997 | ~0% | weak |
| S2 star perihelion | ~2800 | 0.99982 | 0.99982 | <0.01% | weak |
| PSR J0030+0451 | 3.06 | 0.819 | 0.790 | **-3.5%** | strong |
| PSR J0740+6620 | 2.23 | 0.742 | 0.697 | **-6.1%** | strong |
| PSR J0348+0432 | 2.10 | 0.724 | 0.674 | **-6.9%** | strong |
| D-intersection (decay/global) | 1.595 | 0.611 | 0.611 | **0.0%** | comparison |
| D-intersection (saturation/local) | 1.387 | 0.528 | 0.528 | **0.0%** | comparison |
| Schwarzschild radius | 1.00 | 0.000 | **0.555** | **∞** | very_close |

---

## Gravitational Redshift from D

```
z_SSZ(r) = 1/D(r) - 1 = Ξ(r)
```

For two observers at r₁ and r₂:
```
1 + z = D(r_obs) / D(r_emit) = (1 + Ξ_emit) / (1 + Ξ_obs)
```

---

## Scaling Factor

The scaling factor s(r) is the reciprocal of time dilation:
```
s(r) = 1/D(r) = 1 + Ξ(r)
```

This appears in:
- Radial scaling gauge: dρ = s(r)·dr
- Maxwell equations: E' = s·E, B' = s·B
- Light-travel time: Δt_grav = ∫ Ξ(r) dr/c

---

## Weak-Field Expansion

For Ξ ≪ 1 (weak field):
```
D_SSZ ≈ 1 - Ξ + Ξ² - Ξ³ + ...
D_GR  ≈ 1 - r_s/(2r) + ...
```

With Ξ_weak = r_s/(2r):
```
D_SSZ ≈ 1 - r_s/(2r) + O(r_s²/r²)
```

Identical to GR's first-order expansion → **SSZ recovers GR in the weak field.**

---

## Horizon Behavior (CRITICAL)

### GR at r = r_s
```
D_GR(r_s) = √(1 - 1) = 0    → Infinite redshift, frozen time
```

### SSZ at r = r_s
```
Ξ(r_s) = 1 - e^(-φ) = 0.80171
D_SSZ(r_s) = 1/(1 + 0.80171) = 0.55503
```

**D is finite!** Consequences:
- Time does not freeze at the horizon
- Redshift is finite (z = 0.802, not ∞)
- No information paradox from frozen surfaces
- No singularity in the time-dilation function

---

## Tests

| Test File | Repository | What it tests |
|-----------|------------|---------------|
| test_time_dilation.py | [segmented-calculation-suite](https://github.com/error-wtf/segmented-calculation-suite) | D(r) computation |
| test_dilation_finite.py | [segmented-calculation-suite](https://github.com/error-wtf/segmented-calculation-suite) | D(r_s) > 0 |
| test_validation.py | [ssz-qubits](https://github.com/error-wtf/ssz-qubits) | GPS, Pound-Rebka, S2 |

---

## Cross-References

- [Segment density Ξ(r)](segment_density.md) — The field that determines D
- [Regime definitions](regime_definitions.md) — 5 regimes, where each Ξ formula applies
- [Regime vs formula domains](regime_and_formula_domain_clarification.md) — Formula boundaries ≠ regime boundaries
- [Scaling factor s(r)](scaling_factor.md) — s = 1+Ξ = 1/D
- [Special values](../03_FORMULAS/special_values.md) — D(rₛ)=0.555, Ξ(rₛ)=0.802
- [Formula compendium](../03_FORMULAS/formula_compendium.md) — Complete formula list
- [PPN formulas](../03_FORMULAS/ppn_formulas.md) — Lensing/Shapiro use PPN, not Ξ

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
