# SSZ Black Hole Metric

**Status:** CANONICAL
**Paper:** 04 — On the Metric of Black Holes

---

## The SSZ Metric Tensor

The SSZ metric modifies the Schwarzschild metric by replacing the standard time-dilation factor with the Ξ-based version:

### Standard Schwarzschild (GR)
```
ds² = -(1 - r_s/r) c²dt² + (1 - r_s/r)⁻¹ dr² + r² dΩ²
```

### SSZ Metric
```
ds² = -D²(r) c²dt² + s²(r) dr² + r² dΩ²
```

where:
- D(r) = 1/(1 + Ξ(r)) — time-dilation factor
- s(r) = 1 + Ξ(r) = 1/D(r) — radial scaling factor
- dΩ² = dθ² + sin²θ dφ² — angular part (unchanged)

---

## Metric Components

```
g_tt = -D²(r) = -1/(1+Ξ)²
g_rr = +s²(r) = (1+Ξ)²
g_θθ = r²
g_φφ = r²sin²θ
```

### Comparison with GR

| Component | GR | SSZ |
|-----------|-----|-----|
| g_tt(r_s) | 0 (singular) | -0.308 (finite) |
| g_rr(r_s) | ∞ (singular) | 3.248 (finite) |
| g_tt(r→∞) | -1 | -1 |
| g_rr(r→∞) | +1 | +1 |

---

## Key Properties

### No Coordinate Singularity at r_s
In GR, the Schwarzschild coordinates break down at r = r_s. In SSZ:
```
g_tt(r_s) = -D²(r_s) = -(0.555)² = -0.308    (finite!)
g_rr(r_s) = s²(r_s) = (1.802)² = 3.248        (finite!)
```
No coordinate change needed — the SSZ metric is regular at the horizon.

### Finite Curvature
All curvature invariants (Ricci scalar, Kretschmer scalar) remain finite at r_s.

### Asymptotic Flatness
As r → ∞, Ξ → 0, and:
```
g_tt → -1,  g_rr → +1  (Minkowski limit)
```

---

## Einstein Tensor

The SSZ metric generates a non-trivial Einstein tensor G_μν:
- G^t_t (energy density) — positive for r ≥ 5r_s
- G^r_r (radial pressure) — related to Ξ gradient
- G^θ_θ = G^φ_φ (tangential pressure)

The Einstein equations G_μν = (8πG/c⁴)T_μν are satisfied with an effective stress-energy tensor that represents the segmentation field.

---

## 4D Tensor Package

The complete tensor calculations are in `ssz-metric-pure`:

| Tensor | File | Status |
|--------|------|--------|
| Metric g_μν | SSZ_METRIC_TENSOR_COMPLETE.tex | ✅ |
| Christoffel Γ^λ_μν | SSZ_METRIC_TENSOR_COMPLETE.tex | ✅ |
| Riemann R^ρ_σμν | SSZ_EINSTEIN_RICCI_CURVATURE.tex | ✅ |
| Ricci R_μν | SSZ_EINSTEIN_RICCI_CURVATURE.tex | ✅ |
| Ricci scalar R | SSZ_EINSTEIN_RICCI_CURVATURE.tex | ✅ |
| Einstein G_μν | SSZ_EINSTEIN_RICCI_CURVATURE.tex | ✅ |
| Weyl C_μνρσ | Computed in tests | ✅ |
| Kretschmer K | Computed in tests | ✅ |

---

## Tests

| Test | Repository |
|------|------------|
| test_metric_tensor.py | ssz-metric-pure |
| test_einstein_equations.py | ssz-metric-pure |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
