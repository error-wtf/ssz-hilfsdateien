# SSZ Mathematics Findings

**Segmented Spacetime (SSZ) - Mathematical Framework**

© 2025 Carmen Wrede & Lino Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## 1. Core Metric

### SSZ Metric Function

```
A(U) = 1 - 2U + 2U² + ε₃U³

where:
  U = GM/(rc²)     (dimensionless gravitational potential)
  ε₃ = -4.80       (SSZ parameter)
  
Line element:
  ds² = -A(U)c²dt² + A(U)⁻¹dr² + r²dΩ²
```

### Comparison with Schwarzschild

```
Schwarzschild: A(U) = 1 - 2U
SSZ:           A(U) = 1 - 2U + 2U² + ε₃U³

Difference: ΔA = 2U² + ε₃U³
```

For weak fields (U << 1): ΔA ≈ 0 (matches GR)  
For strong fields (U ~ 1): ΔA significant

---

## 2. Golden Ratio (φ) in SSZ

### Fundamental Constants

```
φ = (1 + √5) / 2 = 1.6180339887...

Key identities:
  φ² = φ + 1
  1/φ = φ - 1
  φⁿ = φⁿ⁻¹ + φⁿ⁻²  (Fibonacci recursion)
```

### φ-Based Segment Density

```
N(x) = Σᵢ γᵢ · Kᵢ(||x - xᵢ||)

where:
  γᵢ = φ-based weight factor
  Kᵢ = kernel function with φ-scaling
```

### Universal Intersection Point

```
r*/r_s = φ/2 = 0.8090169944...

This is where multiple φ-spirals intersect.
```

---

## 3. Segment Density Field

### Definition

```
σ(r) = (r_s/r)^α

where:
  r_s = 2GM/c²  (Schwarzschild radius)
  α = 1         (default exponent)
```

### Properties

```
1. Monotonicity: dσ/dr < 0 (decreases with distance)
2. Boundary: σ(r_s) = 1 (at horizon)
3. Asymptotic: σ(∞) = 0 (flat space)
```

### Multi-Body Superposition

```
σ_total = Σᵢ σᵢ

Segment densities add linearly (superposition principle).
```

---

## 4. Time Dilation

### Gravitational Time Dilation

```
τ(r) = √(1 - r_s/r) = √(1 - 2U)

where τ is the proper time ratio (τ_local / τ_∞)
```

### φ-Based Time Dilation

```
τ(x) = φ^(-α·N(x))

where:
  N(x) = segment density at point x
  α = coupling constant
```

---

## 5. Refractive Index

### Effective Refractive Index

```
n(x) = 1 + κ·N(x)

where:
  κ = 0.02 (default)
  N(x) = segment density
```

### Properties

```
1. Causality: n ≥ 1 (no FTL propagation)
2. Vacuum: n(∞) = 1
3. Lensing: Δθ ∝ (n - 1)
```

---

## 6. Rapidity Formulation

### Definition

```
χ = arctanh(v/c)

Inverse: v = c · tanh(χ)
```

### Velocity Addition

```
Traditional (problematic):
  v₁₂ = (v₁ + v₂) / (1 + v₁v₂/c²)
  
Rapidity (correct):
  χ₁₂ = χ₁ + χ₂
  v₁₂ = c · tanh(χ₁₂)
```

### Angular Bisector

```
χ_bisector = (χ₁ + χ₂) / 2

At equilibrium (v₁ = -v₂):
  χ_bisector = 0
  v_bisector = 0 (smooth, no 0/0!)
```

---

## 7. PPN Expansion

### Parameterized Post-Newtonian

```
g₀₀ = -(1 - 2U + 2βU² + ...)
g_ij = (1 + 2γU + ...)δᵢⱼ

SSZ values:
  β = 1 (no preferred frame)
  γ = 1 (GR-like curvature)
```

### Weak-Field Limit

```
For U << 1:
  A(U) ≈ 1 - 2U + O(U²)
  
This matches Schwarzschild exactly.
```

---

## 8. Characteristic Radii

### Schwarzschild Radius

```
r_s = 2GM/c²

Examples:
  Sun:   r_s = 2,954 m
  Earth: r_s = 8.87 mm
  Sgr A*: r_s = 1.27 × 10¹⁰ m
  M87*:  r_s = 1.92 × 10¹³ m
```

### Photon Sphere

```
r_ph = (3/2) r_s = 3GM/c²

Light can orbit at this radius.
```

### ISCO

```
r_ISCO = 3 r_s = 6GM/c²

Innermost stable circular orbit.
```

### φ-Intersection

```
r* = (φ/2) r_s ≈ 0.809 r_s

Universal intersection of φ-spirals.
```

---

## 9. Energy Formulas

### Rest Energy

```
E_rest = Mc²
```

### Gravitational Binding Energy

```
E_bind = (3/5) GM²/R

For uniform density sphere.
```

### Total Energy

```
E_total = E_rest - E_bind + E_kinetic
```

### Compactness Parameter

```
ξ = r_s / R = 2GM/(Rc²)

Ranges:
  Stars: ξ ~ 10⁻⁶
  White dwarfs: ξ ~ 10⁻⁴
  Neutron stars: ξ ~ 0.2-0.4
  Black holes: ξ = 1 (at horizon)
```

---

## 10. Statistical Framework

### Paired Test

```
For each observation i:
  Δᵢ = |z_obs - z_SSZ| - |z_obs - z_GR|
  
SSZ wins if Δᵢ < 0
GR wins if Δᵢ > 0
```

### Binomial Test

```
H₀: P(SSZ wins) = 0.5
H₁: P(SSZ wins) > 0.5

p-value = P(X ≥ k | n, p=0.5)

where k = number of SSZ wins, n = total pairs
```

### Significance Levels

```
p < 0.05:  Significant
p < 0.01:  Highly significant
p < 0.001: Extremely significant
```

---

## 11. Numerical Methods

### High-Precision Arithmetic

```python
from decimal import Decimal, getcontext
getcontext().prec = 100  # 100 digits

phi = (Decimal(1) + Decimal(5).sqrt()) / Decimal(2)
```

### Convergence Criteria

```
|x_{n+1} - x_n| < ε

where ε = 10⁻¹² (default tolerance)
```

### Numerical Stability

```
1. Avoid 0/0: Use rapidity formulation
2. Avoid overflow: Use log-space for large numbers
3. Avoid underflow: Use scaled variables
```

---

## 12. Key Equations Summary

| Equation | Formula | Domain |
|----------|---------|--------|
| SSZ Metric | A(U) = 1 - 2U + 2U² + ε₃U³ | U ∈ [0, 1] |
| Segment Density | σ = (r_s/r)^α | r > r_s |
| Time Dilation | τ = √(1 - r_s/r) | r > r_s |
| Refractive Index | n = 1 + κN | N ≥ 0 |
| Rapidity | χ = arctanh(v/c) | |v| < c |
| Photon Sphere | r_ph = 1.5 r_s | - |
| ISCO | r_ISCO = 3 r_s | - |
| φ-Intersection | r* = φ/2 × r_s | - |

---

© 2025 Carmen Wrede & Lino Casu
