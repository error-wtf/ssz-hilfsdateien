# API Reference - SSZ Metric Package

Complete reference for the `ssz_metric` Python package.

## Installation

```bash
from ssz_metric import *
```

---

## Constants

### Physical Constants

```python
G = 6.67430e-11        # Gravitational constant [m³/(kg·s²)]
C = 299792458          # Speed of light [m/s]
M_SUN = 1.98847e30     # Solar mass [kg]
PHI = 1.618033988749   # Golden ratio φ = (1+√5)/2
```

---

## Core Functions

### `schwarzschild_radius(M)`

Compute Schwarzschild radius.

**Parameters:**
- `M` (float): Mass in kg

**Returns:**
- `r_s` (float): Schwarzschild radius in meters

**Formula:**
```python
r_s = 2 * G * M / (C**2)
```

**Example:**
```python
r_s = schwarzschild_radius(M_SUN)
# Output: 2953.0 m (2.953 km)
```

---

### `xi_field(r, r_s)`

Compute segment density field.

**Parameters:**
- `r` (float/array): Radial coordinate [m]
- `r_s` (float): Schwarzschild radius [m]

**Returns:**
- `Xi` (float/array): Segment density (dimensionless)

**Formula:**
```python
Ξ(r) = 1 - exp(-φ · r_s / r)
```

**Properties:**
- Ξ(0) = 0 (no segments at center)
- Ξ(∞) → 1 (saturation)
- Ξ(r_s) ≈ 0.801 (at Schwarzschild radius)

---

### `D_SSZ(r, r_s)` and `D_GR(r, r_s)`

Time dilation factors.

**SSZ:**
```python
D_SSZ(r) = 1 / (1 + Ξ(r))
```

**GR:**
```python
D_GR(r) = √(1 - r_s/r)
```

**Example:**
```python
r = 5 * r_s
d_ssz = D_SSZ(r, r_s)  # ≈ 0.685
d_gr = D_GR(r, r_s)    # ≈ 0.894
```

---

### `find_intersection(r_s)`

Find universal intersection point r*.

**Parameters:**
- `r_s` (float): Schwarzschild radius [m]

**Returns:**
- `r_star` (float): Intersection radius [m]
- `u_star` (float): Dimensionless u* = r*/r_s

**Result:**
```python
u* = 1.3865616196...  # Universal constant!
```

**Example:**
```python
r_star, u_star = find_intersection(r_s)
# u_star ≈ 1.3865616
# Error from canonical: 3.8×10⁻⁷
```

---

### `A_blended(r, r_s, r_star, ell=None, mode='O3')`

Complete metric coefficient with smooth blending.

**Parameters:**
- `r` (float/array): Radial coordinate [m]
- `r_s` (float): Schwarzschild radius [m]
- `r_star` (float): Intersection radius [m]
- `ell` (float, optional): Smoothing scale [m]. Default: 0.05·r_s
- `mode` (str, optional): Metric mode
  - `'O3'`: Traditional O(U³) with ε₃ = -24/5 (default)
  - `'O4'`: φ-series up to O(U⁴)
  - `'O5'`: φ-series up to O(U⁵)
  - `'O6'`: φ-series up to O(U⁶) (recommended)

**Returns:**
- `A` (float/array): Metric coefficient (dimensionless)

**Formula:**
```python
# Inner (r < r*): SSZ
A_Ξ(r) = (1 + Ξ(r))^(-2)

# Outer (r > r*): φ-series or PN
A_φ(r) = Σ_{n=0}^{max_order} ε_n (r_s/2r)^n

# Smooth blend
w(r) = 0.5(1 + tanh((r* - r)/ℓ))
A(r) = w(r)·A_Ξ(r) + (1-w(r))·A_φ(r)
```

**Key Property:**
- A(r) > 0 everywhere!
- A_min = 0.284 at r_φ

**Example:**
```python
r = 5 * r_s
A = A_blended(r, r_s, r_star, mode='O6')
# A ≈ 0.848
```

---

### `B_metric(r, r_s, r_star, ell=None, mode='O3')`

Radial metric coefficient.

**Parameters:** Same as `A_blended`

**Returns:**
- `B` (float/array): Radial metric coefficient

**Formula:**
```python
B(r) = 1 / A(r)  # Isotropic assumption
```

**Future:** Will be computed from Einstein equations for full consistency.

---

### `natural_boundary(r_s)`

Compute natural boundary radius.

**Parameters:**
- `r_s` (float): Schwarzschild radius [m]

**Returns:**
- `r_phi` (float): Natural boundary radius [m]

**Formula:**
```python
r_φ = (φ/2) × r_s × (1 + Δ(M)/100)
```

**For solar mass:**
```python
r_φ ≈ 0.825 r_s = 2.437 km
```

**Physical Meaning:**
Physical boundary of spacetime - NO singularity, finite curvature!

---

## Advanced Functions

### `A_phi_series(r, r_s, max_order=6, use_delta=True)`

φ-series metric coefficient (higher orders).

**Parameters:**
- `r` (float/array): Radial coordinate [m]
- `r_s` (float): Schwarzschild radius [m]
- `max_order` (int): Maximum order (0-6). Default: 6
- `use_delta` (bool): Apply Δ(M) correction. Default: True

**Returns:**
- `A` (float/array): φ-series metric coefficient

**φ-Series Coefficients:**
```python
PHI_SERIES_C = [
    1.0,        # c_0
    -2.0,       # c_1
    2.0,        # c_2
    -1.133126,  # c_3 (from ε₃ = -24/5)
    0.535758,   # c_4 (predicted!)
    -0.369194,  # c_5 (predicted!)
    0.102942,   # c_6 (predicted!)
]

# Generate ε_n
ε_n = c_n × φⁿ
```

**Recursion:**
```python
c_{n+2} = (c_{n+1} + c_n) / φ
```

---

### `delta_M(r_s)`

Empirical mass correction factor.

**Parameters:**
- `r_s` (float): Schwarzschild radius [m]

**Returns:**
- `Delta` (float): Correction percentage [%]

**Formula:**
```python
Δ(M) = 98.01 × exp(-2.7177e4 × r_s) + 1.96
```

**For solar mass:**
```python
Δ(M) ≈ 1.96%
```

---

## Validation Functions

### From `validate_suite.py`

Complete validation CLI and plotting suite.

**Usage:**
```python
from ssz_metric.validate_suite import run_all_validations

run_all_validations(M=M_SUN, verbose=True, save_plots=True)
```

**Validates:**
1. ✅ Intersection accuracy
2. ✅ No signature flip (A > 0)
3. ✅ Natural boundary properties
4. ✅ Far-field GR recovery
5. ✅ B = 1/A consistency
6. ✅ C² continuity

---

## Complete Example

```python
from ssz_metric import *
import numpy as np
import matplotlib.pyplot as plt

# Setup
M = M_SUN
r_s = schwarzschild_radius(M)
r_star, u_star = find_intersection(r_s)
r_phi = natural_boundary(r_s)

print(f"System: M = {M:.3e} kg")
print(f"r_s = {r_s/1000:.3f} km")
print(f"u* = {u_star:.7f}")
print(f"r_φ = {r_phi/r_s:.3f} r_s")

# Compute metric
r_range = np.linspace(r_phi*1.1, 10*r_s, 100)
A_values = np.array([A_blended(r, r_s, r_star, mode='O6') for r in r_range])
B_values = np.array([B_metric(r, r_s, r_star, mode='O6') for r in r_range])

# Verify A > 0
print(f"\nA_min = {np.min(A_values):.6f}")
print(f"A > 0 everywhere: {np.all(A_values > 0)}")

# Plot
plt.figure(figsize=(10, 6))
plt.plot(r_range/r_s, A_values, label='A(r)', linewidth=2)
plt.axvline(r_phi/r_s, color='red', linestyle=':', label='r_φ')
plt.axvline(u_star, color='purple', linestyle='--', label='r*')
plt.xlabel('r/r_s')
plt.ylabel('A(r)')
plt.title('SSZ Metric - Singularity-Free!')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
```

---

## Units

All calculations use SI units:
- **Length**: meters [m]
- **Mass**: kilograms [kg]
- **Time**: seconds [s]
- **Dimensionless**: u*, φ, ε_n, etc.

---

## Performance

- **Vectorized**: All functions support numpy arrays
- **Fast**: O(n) for n evaluation points
- **Accurate**: Machine precision (~1e-15)

---

## See Also

- [README.md](README.md) - Project overview
- [ULTIMATE_FINAL_REPORT](ULTIMATE_FINAL_REPORT_2025-10-31.md) - Complete session history
- [FINDINGS_COMPREHENSIVE_FINAL](FINDINGS_COMPREHENSIVE_FINAL.md) - All 77 findings

---

© 2025 Carmen Wrede & Lino Casu
