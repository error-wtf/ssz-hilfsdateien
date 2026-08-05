# Relation to General Relativity

**Status:** CANONICAL

---

## SSZ as GR Extension, Not Replacement

A useful way to read SSZ is:

1. **GR provides a geometric description (curvature)** that works extremely well
2. **SSZ keeps the successful GR structure** in weak fields — identically
3. **SSZ adds one extra operational layer** — a segment density field Ξ — whose primary observational footprint is modified time dilation, saturating in strong fields

SSZ is not "anti-GR." It is closer to **"GR + structured strong-field correction,"** with an explicit cap that avoids runaway divergences.

---

## Weak-Field Identity

In the weak field (r/r_s > 2.2), SSZ and GR are **identical** to observational precision:

| Observable | GR | SSZ | Difference |
|-----------|-----|-----|------------|
| GPS time correction | 45.85 μs/day | 45.85 μs/day | < 1 ns/day |
| Pound-Rebka Δν/ν | 2.46×10⁻¹⁵ | 2.46×10⁻¹⁵ | < 0.01% |
| Mercury perihelion | 42.98"/century | 42.98"/century | 0.00% |
| Eddington lensing | 1.75" | 1.75" | 0.00% |
| Cassini Shapiro γ | 1.000021 | 1.000021 | 0.00% |
| S2 star redshift | 0.00018 | 0.00018 | < 0.01% |

SSZ is designed to pass every existing weak-field test exactly.

---

## Strong-Field Differences

SSZ deviates from GR **only** in the strong field (r/r_s < ~10):

### At the Schwarzschild Radius (r = r_s)

| Property | GR | SSZ | Interpretation |
|----------|-----|-----|----------------|
| Time dilation D | 0 | **0.555** | Finite vs infinite |
| Redshift z | ∞ | **0.802** | Bounded vs divergent |
| Proper time τ | 0 | **> 0** | Observable vs frozen |
| Singularity | YES | **NO** | SSZ resolves it |
| Energy conditions | Violated | **Satisfied** | SSZ is regular |

### For Neutron Stars (r/r_s ≈ 2–3)

| Object | z_GR | z_SSZ | Excess |
|--------|------|-------|--------|
| PSR J0030+0451 (r/r_s=3.06) | 0.219 | 0.328 | **+50%** |
| PSR J0740+6620 (r/r_s=2.23) | 0.346 | 0.413 | **+19%** |
| PSR J0348+0432 (r/r_s=2.10) | 0.380 | 0.457 | **+20%** |

**Systematic prediction:** NS redshift +13% higher than GR — testable with NICER.

---

## D-Intersection Comparisons

SSZ and GR agree at mass-independent comparison radii. The numerical value depends on the declared Xi form:
```
r*/r_s = 1.594811,  D* = 0.610710  for Xi_A(x)=1-exp(-phi/x)
r*/r_s = 1.386562,  D* = 0.528007  for Xi_B(x)=1-exp(-phi*x)
```

These intersection points are:
- Mass-independent (purely geometric)
- Derived from `D_SSZ = D_GR`, not fitted
- Meaningful only when the Xi form is stated

They are not hard regime boundaries. The operative blend remains fixed at `1.8 <= r/r_s <= 2.2`.

---

## PPN Parameters

| Parameter | GR | SSZ | Measurement |
|-----------|-----|-----|-------------|
| β | 1 | 1 (exact) | — |
| γ | 1 | 1 (exact) | Cassini: 1.000021 ± 0.000023 |

SSZ is **PPN-identical** to GR. All Solar System tests are passed by construction.

---

## Philosophical Difference

| Aspect | GR | SSZ |
|--------|-----|-----|
| Core object | Metric tensor g_μν | g_μν + Ξ(r) |
| Singularities | Present at r_s | Absent (D > 0 everywhere) |
| Information paradox | Problematic | Avoided (finite D) |
| Falsifiability | Weak-field confirmed | Explicit strong-field predictions |
| Free parameters | 0 | 0 |
| Strong-field behavior | Divergent | Saturating |

---

## In One Sentence

> SSZ = GR in the weak field + bounded segment density in the strong field, with zero free parameters and explicit falsification targets.

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
