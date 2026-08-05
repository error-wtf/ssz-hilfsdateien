# Physics Report: RSG Lensing Inversion Framework

## Complete Physical Foundation

**Authors:** Carmen N. Wrede, Lino P. Casu  
**Date:** January 2026  
**License:** Anti-Capitalist Software License v1.4

---

## 1. Gravitational Lensing Fundamentals

### 1.1 The Lens Equation

The fundamental equation of gravitational lensing relates the **true source position** β to the **observed image position** θ:

```
β = θ - α(θ)
```

Where:
- **β** = (β_x, β_y) : True source position (unlensed)
- **θ** = (θ_x, θ_y) : Observed image position
- **α(θ)** : Deflection angle (depends on lens mass distribution)

### 1.2 Reduced Deflection

For a lens at cosmological distance, we use the **reduced deflection**:

```
α_red(θ) = (D_LS / D_S) · α_true(θ)
```

Where:
- **D_LS** : Angular diameter distance from lens to source
- **D_S** : Angular diameter distance from observer to source

### 1.3 Einstein Radius

The characteristic scale of lensing is the **Einstein radius**:

```
θ_E = √(4GM / c² · D_LS / (D_L · D_S))
```

For a point mass, images form on a ring of radius θ_E when source is perfectly aligned.

---

## 2. Multipole Expansion

### 2.1 General Form

Real lenses are not point masses. We expand the deflection in multipoles:

```
α_r(r, φ) = θ_E + Σ_m [a_m · cos(mφ) + b_m · sin(mφ)]
```

Where:
- **m = 0**: Monopole (Einstein ring) - captured in θ_E
- **m = 1**: Dipole (lens center offset) - usually removed by choice of origin
- **m = 2**: Quadrupole (ellipticity) - dominant for elliptical galaxies
- **m ≥ 3**: Higher multipoles (twists, asymmetries)

### 2.2 Cartesian Components vs Amplitude/Phase

**Cartesian Form (Path A):**
```
Multipole m: (a_m, b_m)
Deflection: a_m·cos(mφ) + b_m·sin(mφ)
```

**Polar Form (Path B):**
```
Multipole m: (A_m, φ_m)
Deflection: A_m·cos(m(φ - φ_m))
```

**Conversion:**
```
A_m = √(a_m² + b_m²)
φ_m = (1/m) · atan2(b_m, a_m)
```

### 2.3 External Shear

Large-scale tidal fields add external shear:

```
α_shear_x = γ_1·x + γ_2·y
α_shear_y = γ_2·x - γ_1·y
```

Where:
- **γ = √(γ_1² + γ_2²)** : Shear magnitude
- **φ_γ = (1/2)·atan2(γ_2, γ_1)** : Shear direction

---

## 3. The Inversion Problem

### 3.1 Forward vs Inverse

**Forward Problem:** Given lens parameters, predict image positions  
**Inverse Problem:** Given image positions, recover lens parameters

The inverse problem is what we solve. It's fundamentally **linear** in our parametrization.

### 3.2 Linear System Structure

From N images of K sources, we get **2N constraints** (x and y for each image).

**Unknown Parameters:**
- θ_E : 1 parameter
- Multipoles: 2 per order (a_m, b_m for each m)
- External shear: 2 parameters (γ_1, γ_2) if included
- Source positions: 2K parameters (β_x, β_y for each source)

**System Matrix:**
```
A · p = b

Where:
- A : (2N × P) design matrix
- p : (P,) parameter vector
- b : (2N,) observed image positions
```

### 3.3 Degree of Freedom Analysis

| Configuration | Constraints | Typical Params (m=2) | DOF Status |
|---------------|-------------|----------------------|------------|
| 1 source, 4 images | 8 | 5 (lens) + 2 (source) = 7 | +1 redundant |
| 1 source, 2 images | 4 | 7 | -3 underdetermined |
| 2 sources, 4+4 images | 16 | 5 + 4 = 9 | +7 redundant |

---

## 4. Physical Interpretation of Regimes

### 4.1 DETERMINED System

**Physical meaning:** Exactly enough information to uniquely determine the lens.

**Example:** 4 images of 1 source with m_max=2, no shear.
- 8 constraints (4 images × 2 coords)
- 7 parameters (θ_E, a_2, b_2, β_x, β_y)
- DOF = +1 (minimal overdetermination)

### 4.2 OVERDETERMINED System

**Physical meaning:** More constraints than needed → consistency check available.

**Residuals indicate:**
- Zero residual: Model perfectly describes lens
- Small residual: Noise or minor model imperfection
- Large residual: Model inadequate (need higher multipoles?)

**NOT a fitting error** - this is model adequacy diagnostic.

### 4.3 UNDERDETERMINED System

**Physical meaning:** Not enough images to uniquely determine all parameters.

**Examples:**
- 2 images → can't determine quadrupole orientation uniquely
- High m_max with 4 images → too many multipole parameters

**What we learn:**
- Nullspace dimension tells us how many "directions" are unconstrained
- Non-identifiable parameters can take any value within a family
- Need regularization (explicit assumption) to pick one solution

### 4.4 ILL-CONDITIONED System

**Physical meaning:** Small changes in data cause large parameter changes.

**Physical causes:**
- Near-caustic configuration (images nearly merging)
- Near-degenerate image configuration
- Strong parameter correlations

**What to do:**
- Report results with uncertainty
- Sensitivity analysis
- Consider if configuration is physically marginal

---

## 5. Phase Degeneracy

### 5.1 The m=2 Symmetry

For quadrupole (m=2), there's an inherent π/2 phase degeneracy:

```
φ_2 and φ_2 + π/2 give identical image configurations
```

This is because cos(2(φ - φ_2)) = cos(2(φ - (φ_2 + π/2)))

### 5.2 Path A vs Path B

**Path A (Algebraic):**
- Works in (a_2, b_2) → single, canonical solution
- Phase derived as OUTPUT: φ_2 = (1/2)·atan2(b_2, a_2)
- Picks ONE branch automatically

**Path B (Phase Scan):**
- Scans over φ_2 values → sees BOTH minima
- Shows the residual landscape explicitly
- Useful for confirming degeneracy structure

---

## 6. Multi-Source DOF Rescue

### 6.1 How More Sources Help

Each additional source adds:
- 2N new constraints (if N images)
- Only 2 new parameters (β_x, β_y for that source)

**Net gain:** 2(N-1) additional constraints per source

### 6.2 Example

| Sources | Images | Constraints | Params (m=2) | Nullspace |
|---------|--------|-------------|--------------|-----------|
| 1 | 4 | 8 | 7 | 0 |
| 1 | 4 (m=3) | 8 | 9 | 1 |
| 2 | 4+4 | 16 | 11 | 0 |
| 2 | 4+4 (m=3) | 16 | 13 | 0 |

Adding sources **rescues** underdetermined systems.

---

## 7. Physical Quantities Recovered

### 7.1 Direct Parameters

| Parameter | Physical Meaning | Units |
|-----------|------------------|-------|
| θ_E | Einstein radius | arcsec |
| a_2, b_2 | Quadrupole components | arcsec |
| γ_1, γ_2 | External shear components | dimensionless |
| β_x, β_y | Source position | arcsec |

### 7.2 Derived Quantities

| Quantity | Formula | Physical Meaning |
|----------|---------|------------------|
| A_2 | √(a_2² + b_2²) | Quadrupole amplitude |
| φ_2 | (1/2)·atan2(b_2, a_2) | Quadrupole orientation |
| ε | A_2 / θ_E | Ellipticity |
| γ | √(γ_1² + γ_2²) | Shear magnitude |
| M_lens | θ_E²·c²·D / (4G) | Enclosed mass |

---

## 8. Validation Against Observations

### 8.1 Einstein Cross (Q2237+0305)

Classic quadruple lens system:
- 4 images of background quasar
- Lens galaxy at z=0.039
- θ_E ≈ 0.9 arcsec
- Significant quadrupole (elliptical galaxy)

### 8.2 Expected Residuals

For well-modeled systems with m_max=2:
- Residual < 0.01 arcsec: Excellent
- Residual 0.01-0.1 arcsec: Good, may need higher multipoles
- Residual > 0.1 arcsec: Model inadequate or data issues

---

## 9. Summary

The RSG Lensing Inversion Framework provides:

1. **Exact linear inversion** - no optimization, no fitting
2. **Regime classification** - understand what can/cannot be determined
3. **Physics-based diagnostics** - residuals mean something physical
4. **No forbidden regions** - learn from every configuration
5. **Multi-path verification** - algebraic and scan modes cross-check

**Key Insight:** This is NOT curve fitting. We're solving physics equations exactly, and the regime tells us whether the answer is unique, overdetermined (testable), underdetermined (needs assumptions), or ill-conditioned (uncertain).
