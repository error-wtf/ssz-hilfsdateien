# SSZ Weak/Strong Field Specification

**AUTHORITATIVE SPECIFICATION** extracted from source repositories.  
**Date:** 2025-01-16  
**Sources:**  
- `ssz-metric-pure/01_MATHEMATICAL_FOUNDATIONS.md`
- `ssz-metric-pure/02_PHYSICS_CONCEPTS.md`
- `ssz-qubits/docs/SSZ_FORMULA_DOCUMENTATION.md`

---

## 1. Regime Definition (CANONICAL)

```
┌─────────────────────────────────────────────────────────────┐
│   r/r_s > 100  →  WEAK FIELD (Newtonian Limit)              │
│   r/r_s < 100  →  STRONG FIELD (Saturation Form)            │
└─────────────────────────────────────────────────────────────┘
```

**Transition Boundary:** r/r_s = 100  
**Blend Zone:** [90, 110] r_s with C² Quintic Hermite Interpolation

---

## 2. Weak Field Formulas

**Condition:** `r/r_s > 100`

### Segment Density
```
Ξ(r) = r_s / (2r)
```

### Gradient
```
dΞ/dr = -r_s / (2r²)  < 0  (Ξ decreases with r)
```

### Time Dilation
```
D_SSZ(r) = 1 / (1 + Ξ(r))
         = 2r / (2r + r_s)
```

### Properties
| Property | Value | Meaning |
|----------|-------|---------|
| Ξ(r) | << 1 | Very small segment density |
| dΞ/dr | < 0 | Ξ decreases with distance |
| D_SSZ | ≈ 1 | Almost no time dilation |
| Scaling | 1/r | Newtonian-like |

### GR Consistency
```
D_SSZ ≈ 1 - Ξ = 1 - r_s/(2r) ≈ √(1 - r_s/r) = D_GR  (for r >> r_s)
```

---

## 3. Strong Field Formulas

**Condition:** `r/r_s < 100`

### Segment Density (Saturation Form)
```
Ξ(r) = 1 - exp(-φ × r_s / r)

where φ = (1 + √5) / 2 = 1.618033988749895
```

### Gradient
```
dΞ/dr = (φ / r_s) × exp(-φ × r_s / r)  > 0  (Ξ increases with r)
```

### Time Dilation
```
D_SSZ(r) = 1 / (1 + Ξ(r))
         = 1 / (2 - exp(-φ × r_s / r))
```

### Properties
| Property | Value | Meaning |
|----------|-------|---------|
| Ξ(0) | = 0 | **No singularity!** |
| Ξ(∞) | → 1 | Saturation |
| dΞ/dr | > 0 | Ξ increases with r |
| D_SSZ(r_s) | = 0.555 | **Finite at horizon!** |

### Key Values at Horizon
```
Ξ(r_s) = 1 - exp(-φ) = 1 - 0.198 = 0.802
D_SSZ(r_s) = 1 / (1 + 0.802) = 0.555
```

---

## 4. Transition/Blend Zone

**Range:** 90 < r/r_s < 110

### C² Quintic Hermite Interpolation
```python
def hermite_blend(t):
    """Quintic Hermite blend for C² continuity"""
    return t * t * t * (t * (6.0 * t - 15.0) + 10.0)

def xi_blended(r, r_s):
    x = r / r_s
    r_low = 90
    r_high = 110
    
    if x <= r_low:
        return xi_strong(r, r_s)
    elif x >= r_high:
        return xi_weak(r, r_s)
    else:
        t = (x - r_low) / (r_high - r_low)
        h = hermite_blend(t)
        return (1 - h) * xi_strong(r, r_s) + h * xi_weak(r, r_s)
```

### Continuity Requirements
- Value continuity at boundaries
- 1st derivative continuous
- 2nd derivative continuous
- **Curvature Proxy:** K ≈ 10⁻¹⁵ – 10⁻¹⁶ (extremely smooth)

---

## 5. Universal Intersection Point

```
r* / r_s = 1.594811  (korrigierte Formel: r_s/r statt r/r_s)

At r*: D_GR(r*) = D_SSZ(r*) = 0.610710  (EXACTLY!)
```

**Critical:** This is **MASS-INDEPENDENT**!

---

## 6. GR vs SSZ Comparison

### Time Dilation at Key Points

| Location | r/r_s | D_GR | D_SSZ | Difference |
|----------|-------|------|-------|------------|
| Earth Surface | 7×10⁸ | 0.9999999993 | 0.9999999993 | ~0% |
| Sun Surface | 5×10⁵ | 0.999999 | 0.999999 | ~0% |
| White Dwarf | 10³ | 0.9995 | 0.9995 | <0.01% |
| Neutron Star | 2-4 | 0.707 | 0.697 | **1.4%** |
| Event Horizon | 1 | 0 (singular!) | 0.555 | **∞** |

### GR Formula (for comparison)
```
D_GR(r) = √(1 - r_s/r)

At r = r_s: D_GR(r_s) = √(1 - 1) = 0  (SINGULARITY!)
```

---

## 7. Physical Justification

### Why Two Formulas?

**Weak Field Formula in Strong Field:**
```
Ξ = r_s/(2r)  at r = 0  →  Ξ = infinity (SINGULARITY!)
```
This fails near black holes.

**Strong Field Formula in Weak Field:**
```
Ξ = 1 - exp(-φ×r_s / r)  at r = R_Earth  →  Ξ ≈ 1.0
```
This is **WRONG** - Earth is not "fully segmented".

### Solution: Regime-Dependent Selection
- **Weak field:** Gravity is a small perturbation, Xi ∝ 1/r
- **Strong field:** Nonlinear effects, saturation necessary

---

## 8. Experimental Validation

### GPS Time Dilation
```
Satellite: h = 20,200 km
Δt/day = 45.7 μs (SSZ prediction)
Measured: ~45 μs/day ✓
```

### Pound-Rebka Experiment
```
Height: h = 22.5 m
Δν/ν = 2.46×10⁻¹⁵ (SSZ prediction)
Measured: (2.57 ± 0.26)×10⁻¹⁵ ✓
```

---

## 9. Implementation Rules

### Method Selection (MANDATORY)

| Application | Use Method | Formula |
|-------------|------------|---------|
| Time dilation | Xi-based | D = 1/(1+Ξ) |
| Frequency shift | Xi-based | ν_obs = ν_emit × D |
| **Lensing** | **PPN** | α = (1+γ)r_s/b = 2r_s/b |
| **Shapiro delay** | **PPN** | Δt = (1+γ)r_s/c × ln(...) |
| Perihelion precession | PPN | Standard formula |

**CRITICAL:** Lensing and Shapiro use PPN, NOT Xi-based!

### Regime Boundaries (EXACT)
```python
REGIME_WEAK_THRESHOLD = 110   # r/r_s above this → weak field
REGIME_STRONG_THRESHOLD = 90  # r/r_s below this → strong field
```

---

## 10. Deprecated Formulas

**FORBIDDEN - DO NOT USE:**
```
Ξ = (r_s/r)² × exp(-r/r_φ)  ❌ DEPRECATED
```

This old formula was used in early development but is **incorrect**.

---

## 11. Constants (EXACT VALUES)

```python
PHI = 1.6180339887498948      # Golden ratio (1+√5)/2
G = 6.67430e-11               # m³/(kg·s²)
c = 299792458.0               # m/s
M_SUN = 1.98847e30            # kg
XI_MAX = 0.802                # Ξ(r_s) in strong field
D_HORIZON = 0.555             # D_SSZ(r_s)
R_STAR_OVER_RS = 1.595        # Universal intersection (corrected)
```

---

## 12. Traceability

| Specification | Source File | Line Reference |
|---------------|-------------|----------------|
| Weak field: Ξ = r_s/(2r) | 01_MATHEMATICAL_FOUNDATIONS.md | §16.2 |
| Strong field: Ξ = 1-exp(-φr_s / r) | 01_MATHEMATICAL_FOUNDATIONS.md | §3.2 |
| Boundary r/r_s = 100 | SSZ_FORMULA_DOCUMENTATION.md | §2 |
| Blend zone [90, 110] | 01_MATHEMATICAL_FOUNDATIONS.md | §16.1 |
| C² Hermite interpolation | 01_MATHEMATICAL_FOUNDATIONS.md | §12.2 |
| Ξ(r_s) = 0.802 | 02_PHYSICS_CONCEPTS.md | §3.2 |
| D(r_s) = 0.555 | 02_PHYSICS_CONCEPTS.md | §3.2 |
| r*/r_s = 1.595 | 01_MATHEMATICAL_FOUNDATIONS.md | §4.3 |

---

**© 2025 Carmen Wrede & Lino Casu**  
**This specification is BINDING for all SSZ implementations.**
