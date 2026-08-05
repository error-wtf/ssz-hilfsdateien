# Tensor Array Backend Guide

**Version:** v1.1.0-canonical  
**Date:** 2026-06-09  
**Note:** Array backend stable since v0.8, canonical SSZ formulas since v1.1.0

---

## Overview

The tensor array backend provides **numerical 4D tensor calculations** using proper array indices instead of string-key components. This is the recommended approach for v1.1.0-canonical.

---

## Quick Start

```python
from beam_ssz.tensor import (
    MetricArray,
    minkowski_metric,
    ssz_metric_array,
    flat_bridge_metric,
    compute_christoffel,
    compute_riemann_from_christoffel,
    check_flatness,
)

# 1. Create Minkowski metric (flat space)
mink = minkowski_metric()
print(f"g_tt = {mink[0,0]}")  # -1.0

# 2. Create SSZ metric
ssz = ssz_metric_array(r=2.0, theta=1.57, xi_val=0.1)
print(f"det(g) = {ssz.determinant():.6e}")

# 3. Check if flat
is_flat = check_flatness(riemann_array)  # For Minkowski: True
```

---

## Module Reference

### `metric_array.py`

#### `MetricArray`
Dataclass holding 4D metric tensor `g_μν` as numpy array.

**Indices:** μ, ν ∈ {0,1,2,3} = {t,r,θ,φ}

```python
from beam_ssz.tensor.metric_array import MetricArray
import numpy as np

# Create from components
g = np.diag([-1.0, 1.0, 4.0, 4.0])  # t, r, θ, φ
metric = MetricArray(components=g, coordinates=(0.0, 2.0, np.pi/2, 0.0))

# Access components
g_tt = metric[0, 0]   # -1.0
g_rr = metric[1, 1]   # 1.0
det_g = metric.determinant()
g_inv = metric.inverse()
```

#### `minkowski_metric(flat_signature=True)`
Create flat Minkowski metric η_μν = diag(-1, 1, 1, 1).

**Returns:** `MetricArray` with Minkowski components

**Example:**
```python
mink = minkowski_metric()
assert mink[0,0] == -1.0
assert mink[1,1] == 1.0
assert mink.determinant() == -1.0
```

#### `ssz_metric_array(r, theta, xi_val, D_factor=None)`
Create SSZ metric as proper 4D array.

**Args:**
- `r`: Radial coordinate
- `theta`: Polar angle
- `xi_val`: Xi function value at r
- `D_factor`: Optional custom D(r), else computed from xi

**Returns:** `MetricArray` with SSZ components

**Example:**
```python
ssz = ssz_metric_array(r=2.0, theta=np.pi/2, xi_val=0.1)
print(f"g_tt = {ssz[0,0]:.6f}")  # ~-1.21
```

#### `flat_bridge_metric(u, ell0, Xi_A, Xi_B, lambda_bridge)`
Create flat bridge metric (Ξ_A = Ξ_B = 0, λ = 0).

**For testing:** Should reduce to approximately flat Minkowski.

**Example:**
```python
flat = flat_bridge_metric(u=0.0, Xi_A=0.0, Xi_B=0.0, lambda_bridge=0.0)
assert abs(flat[0,0] - (-1.0)) < 0.01  # Approximately flat
```

---

### `christoffel_array.py`

#### `compute_christoffel(metric, dg_dx, coordinates)`
Compute Christoffel symbols Γ^λ_μν from metric and its derivatives.

**Formula:**
```
Γ^λ_μν = ½ g^λσ (∂_μ g_νσ + ∂_ν g_μσ - ∂_σ g_μν)
```

**Args:**
- `metric`: `MetricArray` with g_μν
- `dg_dx`: Partial derivatives ∂_λ g_μν, shape (4, 4, 4)
- `coordinates`: Which coordinates to use (t, r, θ, φ)

**Returns:** `numpy.ndarray` Gamma[λ, μ, ν], shape (4, 4, 4)

**Example:**
```python
from beam_ssz.tensor import minkowski_metric, compute_christoffel
import numpy as np

mink = minkowski_metric()
dg_dx = np.zeros((4, 4, 4))  # Flat space: no derivatives
gamma = compute_christoffel(mink, dg_dx)
assert np.max(np.abs(gamma)) < 1e-10  # Should be ~0
```

#### `christoffel_from_finite_diff(metric_func, point, h=1e-5)`
Compute Christoffel symbols using finite differences.

**Args:**
- `metric_func`: Function that returns `MetricArray` at (t, r, θ, φ)
- `point`: (t, r, θ, φ) where to compute Christoffels
- `h`: Step size for finite differences

**Returns:** `numpy.ndarray` Gamma[λ, μ, ν]

**Example:**
```python
def metric_at_point(t, r, theta, phi):
    return ssz_metric_array(r=r, theta=theta, xi_val=0.1)

gamma = christoffel_from_finite_diff(
    metric_at_point,
    point=(0.0, 2.0, np.pi/2, 0.0),
    h=1e-5
)
```

---

### `riemann_array.py`

#### `compute_riemann_from_christoffel(gamma, dgamma_dx)`
Compute Riemann tensor from Christoffels and their derivatives.

**Formula:**
```
R^ρ_σμν = ∂_μ Γ^ρ_νσ - ∂_ν Γ^ρ_μσ + Γ^ρ_μλ Γ^λ_νσ - Γ^ρ_νλ Γ^λ_μσ
```

**Args:**
- `gamma`: Christoffel symbols Γ^λ_μν, shape (4, 4, 4)
- `dgamma_dx`: Derivatives ∂_σ Γ^λ_μν, shape (4, 4, 4, 4)

**Returns:** `numpy.ndarray` Riemann[ρ, σ, μ, ν], shape (4, 4, 4, 4)

**Example:**
```python
from beam_ssz.tensor import (
    minkowski_metric, 
    compute_christoffel,
    compute_riemann_from_christoffel,
    check_flatness
)
import numpy as np

# For flat space: gamma = 0, riemann = 0
gamma = np.zeros((4, 4, 4))
dgamma = np.zeros((4, 4, 4, 4))
riemann = compute_riemann_from_christoffel(gamma, dgamma)
assert check_flatness(riemann)  # True
```

#### `check_riemann_symmetries(riemann, tol=1e-10)`
Verify Riemann tensor symmetries.

**Checks:**
1. Antisymmetry: R_ρσμν = -R_σμνρ
2. Pair symmetry: R_ρσμν = R_μνρσ
3. First Bianchi: R_ρσμν + R_ρμνσ + R_ρνσμ = 0

**Returns:** `dict` with symmetry names and boolean results

**Example:**
```python
syms = check_riemann_symmetries(riemann)
print(f"Antisymmetric: {syms['antisymmetric_first_pair']}")
print(f"Pair symmetry: {syms['pair_symmetry']}")
print(f"Bianchi identity: {syms['first_bianchi']}")
```

#### `check_flatness(riemann, tol=1e-10)`
Check if Riemann tensor vanishes (flat space).

**Returns:** `bool` - True if Riemann ≈ 0

**Example:**
```python
from beam_ssz.tensor import minkowski_metric, check_flatness

# Minkowski space is flat
is_flat = check_flatness(riemann_flat)
assert is_flat  # True
```

---

## Migration Guide: String-Keys → Arrays

### Old Way (v0.6/v0.8, Historical)
```python
from beam_ssz.tensor import MetricTensor

metric = MetricTensor(x=2.0)
print(metric.components[('t', 't')])  # String keys - deprecated
```

### Current Way (v1.1.0-canonical)
```python
from beam_ssz.tensor import ssz_metric_array

metric = ssz_metric_array(r=2.0, theta=np.pi/2, xi_val=0.1)
print(metric[0, 0])  # Integer indices - g_tt
```

### Benefits of Array Backend
1. **Faster:** NumPy array operations vs dict lookups
2. **Compatible:** Works with standard tensor libraries
3. **Testable:** Easy to verify symmetries algebraically
4. **Extensible:** Supports finite difference derivatives

---

## Required Tests

For any new metric implementation, verify:

```python
# 1. Minkowski → Riemann = 0
mink = minkowski_metric()
# ... compute riemann ...
assert check_flatness(riemann)

# 2. Flat bridge → curvature = 0
flat = flat_bridge_metric(u=0.0, Xi_A=0.0, Xi_B=0.0, lambda_bridge=0.0)
# ... compute riemann ...
assert np.max(np.abs(riemann)) < 1e-6

# 3. SSZ metric → finite components
ssz = ssz_metric_array(r=2.0, theta=1.57, xi_val=0.1)
assert ssz.is_finite()
assert not ssz.is_singular()

# 4. Riemann symmetries
syms = check_riemann_symmetries(riemann)
assert all(syms.values())
```

---

## Limitations

1. **Finite differences:** Christoffel computation uses numerical derivatives (error ~1e-10)
2. **Coordinate singularities:** Polar coordinates have θ=0,π singularities
3. **Memory:** 4D arrays use O(256) floats per tensor (trivial for modern systems)
4. **Not symbolic:** For exact algebraic results, use `sympy` instead

---

## When to Use Which Backend

| Use Case | Backend | Reason |
|----------|---------|--------|
| Quick checks, prototyping | Scaffold (old) | Simple, readable |
| Numerical relativity | **Array (new)** | Speed, precision |
| Unit tests | **Array (new)** | Verifiable symmetries |
| Production code | **Array (new)** | Standard interface |
| Symbolic derivations | SymPy | Exact algebra |

---

## References

- `metric_array.py` - Core metric implementation
- `christoffel_array.py` - Connection coefficients
- `riemann_array.py` - Curvature tensor
- Tests: `tests/test_tensor_array.py` (if exists)

---

## Status

**Current:** v1.1.0-canonical - Array backend with canonical SSZ formulas (Xi_horizon = 0.8017)  
**Next:** v0.9 - Complete tensor validation suite

---

© 2025-2026 Carmen N. Wrede, Lino P. Casu
