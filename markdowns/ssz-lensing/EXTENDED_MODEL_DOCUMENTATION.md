# Extended Lens Model Documentation

**Version:** 2.0  
**Authors:** Carmen N. Wrede, Lino P. Casu  
**Date:** 2025-01-11

## Overview

This document describes the extended gravitational lens model that incorporates:

1. **Power-law radial profiles** (variable η)
2. **External shear** (γ, φ_γ) 
3. **Higher-order multipoles** (m=3 octupole, m=4 hexadecapole)
4. **Hermite C² blending** for smooth regime transitions

All extensions maintain the **no-fit philosophy**: exact algebraic solves + rootfinding, no curve fitting.

## Physical Motivation

### Power-Law Profiles

Real galaxies don't follow a perfect SIS (η=2) profile. The power-law generalizes:

```
ρ(r) ∝ r^(-η)

where:
  η = 2.0  → SIS (Singular Isothermal Sphere)
  η < 2.0  → Shallower core
  η > 2.0  → Steeper cusp
```

**From SSZ POWER_LAW_FINDINGS.md:**
- Universal scaling: E_obs/E_rest = 1 + α·(r_s/R)^β
- β ≈ 0.98 ≈ 1 suggests geometric origin
- Maps to η ≈ 2 for lensing (nearly isothermal)

### External Shear

External mass (neighboring galaxies, cluster) causes shear:

```
ψ_shear = -γ/2 × θ² × cos(2(φ - φ_γ))

α_x = γ × (x × cos(2φ_γ) + y × sin(2φ_γ))
α_y = γ × (x × sin(2φ_γ) - y × cos(2φ_γ))
```

Essential for systems like B1608+656 (two-galaxy lens).

### Higher Multipoles

| Order | Name | Physical Origin |
|-------|------|-----------------|
| m=2 | Quadrupole | Ellipticity |
| m=3 | Octupole | Bar structure, triangular distortion |
| m=4 | Hexadecapole | Boxy/disky isophotes |

**Q2237+0305 (Einstein Cross):** The bar in the lensing galaxy creates m=3 distortions that explain the observed image configuration.

### Hermite C² Blending

From SSZ: smooth transitions between regimes using:

```python
h(t) = 6t⁵ - 15t⁴ + 10t³  # C² continuous

# Usage: blend two profiles
value = (1-h) * profile_inner + h * profile_outer
```

## Module Structure

```
src/models/
├── profiles.py          # Power-law, cored profiles, Hermite blending
├── extended_model.py    # ExtendedMultipoleModel class
├── root_finders.py      # Bisection, grid search utilities
└── __init__.py          # Exports all components
```

## Usage

### Basic Inversion

```python
from models import ExtendedMultipoleModel
import numpy as np

# Image positions (arcsec)
images = np.array([
    [0.668, 0.784],
    [-0.610, 0.710],
    [-0.728, -0.310],
    [0.737, -0.404]
])

# Create model
model = ExtendedMultipoleModel(m_max=2, include_shear=False)

# Invert
solutions = model.invert(images, tol=1e-10)

if solutions:
    best = solutions[0]
    print(f"θ_E = {best['params']['theta_E']:.4f}")
    print(f"max|res| = {best['report']['max_abs']:.4f} arcsec")
```

### With External Shear

```python
model = ExtendedMultipoleModel(m_max=2, include_shear=True)
solutions = model.invert(images)

if solutions:
    gamma = solutions[0]['params'].get('gamma_ext', 0)
    print(f"External shear: γ = {gamma:.4f}")
```

### Profile Functions

```python
from models import kappa_power_law, alpha_power_law, hermite_blend

# Convergence for η=2.2 profile
theta_E = 1.0
eta = 2.2
kappa = kappa_power_law(0.5, theta_E, eta)

# Hermite blending
h = hermite_blend(x=0.5, x0=0.0, x1=1.0)  # Returns 0.5
```

## Validation Results

### Real Lens Systems

| System | m_max | max|res| (arcsec) |
|--------|-------|---------------------|
| Q2237+0305 | 2 | 0.069 |
| HE0435-1223 | 2 | 0.067 |

### Synthetic Data

- **Parameter recovery:** θ_E = 0.990 (true: 1.0)
- **Residuals:** max|res| = 0.003 arcsec

## Algorithm

### Conditionally Linear Structure

The lens equation β = θ - α(θ) is **linear** in:
- Source position (β_x, β_y)
- Einstein radius (θ_E)
- Shear strength (γ)
- Multipole amplitudes (a_m, b_m)

But **nonlinear** in:
- Multipole phases (φ_m)
- Shear angle (φ_γ)

### Inversion Strategy

1. **Grid search** over nonlinear phases
2. **Least squares** solve for linear parameters at each grid point
3. **Minimize** total residual
4. **Select** solutions with smallest RMS

This avoids traditional optimization and maintains the no-fit philosophy.

## Dependencies

- NumPy ≥ 1.20
- Python ≥ 3.8

No scipy required - all rootfinding is implemented from scratch using bisection and grid search.

## References

1. **SSZ Power Law:** E:\clone\POWER_LAW_FINDINGS.md
2. **SSZ Formulas:** E:\clone\ssz-qubits\docs\SSZ_FORMULA_DOCUMENTATION.md
3. **Hermite Blending:** E:\clone\ssz-metric-pure\src\ssz_metric_pure\segmentation.py

## License

ANTI-CAPITALIST SOFTWARE LICENSE v1.4
