# SSZ Mathematical Formulas

**Complete Mathematical Framework of Segmented Spacetime Theory**

© 2025 Carmen Wrede & Lino Casu

---

## Core Equations

### 1. Schwarzschild Radius

```
r_s = 2GM/c²
```

**Where:**
- G = 6.674×10⁻¹¹ m³/(kg·s²) - Gravitational constant
- M = Mass of object [kg]
- c = 2.998×10⁸ m/s - Speed of light

### 2. Segment Density Field (CORRECT)

```
Ξ(r) = Ξ_max · (1 - exp(-φ · r_s / r))
```

**Where:**
- Ξ_max = 1.0 - Maximum segment density (saturation value)
- φ = 1.618034 - Golden ratio
- r = radial coordinate [m]
- r_s = Schwarzschild radius [m]

**Properties:**
- Ξ(0) = 0
- Ξ(∞) = Ξ_max
- dΞ/dr > 0 everywhere
- C∞ smooth

### 3. SSZ Time Dilation (CORRECT)

```
D_SSZ(r) = 1 / (1 + Ξ(r))
```

**Expanded form:**
```
D_SSZ(r) = 1 / (1 + Ξ_max · (1 - exp(-φ · r_s / r)))
```

**Properties:**
- 0 < D(r) ≤ 1
- D(∞) = 1
- D(r_s) ≈ 0.555
- Monotonically increasing

### 4. GR Time Dilation

```
D_GR(r) = sqrt(1 - r_s/r)
```

**Valid for:** r > r_s

### 5. Universal Intersection

```
r* = 1.386562 · r_s  (dimensionless constant!)
D* = 0.528007        (universal value!)
```

**Condition:**
```
D_GR(r*) = D_SSZ(r*) = D*
∀ M (mass-independent!)
```

---

## Derived Quantities

### Proper Time

```
dτ = D(r) · dt
```

**SSZ:**
```
τ_SSZ = ∫ D_SSZ(r(t)) dt
```

**GR:**
```
τ_GR = ∫ D_GR(r(t)) dt
```

### Gravitational Redshift

```
z = (D_observer / D_emitter) - 1
```

**For light from r_emit observed at r_obs:**
```
z = D(r_obs) / D(r_emit) - 1
```

### Coordinate Velocity

```
v_coord = dr/dt
```

### Proper Velocity

```
v_proper = dr/dτ = (dr/dt) / D(r) = v_coord / D(r)
```

---

## Advanced Relations

### Circular Orbit Velocity

**Newtonian limit:**
```
v_orbit = sqrt(GM/r) = c · sqrt(r_s / (2r))
```

**With SSZ time dilation:**
```
D_orbit ≈ D(r) · sqrt(1 - v²/c²)
```

### Radial Infall

**Initial velocity at r₀:**
```
v(r₀) = 0
```

**Energy conservation (GR):**
```
(1 - r_s/r) · (dt/dτ)² = 1 - r_s/r₀
```

**SSZ equivalent:**
```
D(r)² · (dt/dτ)² = D(r₀)²
```

### Shapiro Delay

**GR (weak field):**
```
Δt_GR = (2GM/c³) · ln(4r_E r_R / b²)
```

**SSZ (path integral):**
```
Δt_SSZ = ∫ (n(r) - 1)/c dx
where n(r) = 1/D(r)
```

---

## Parameter Values

### Physical Constants

| Constant | Symbol | Value | Unit |
|----------|--------|-------|------|
| Speed of light | c | 2.998×10⁸ | m/s |
| Gravitational constant | G | 6.674×10⁻¹¹ | m³/(kg·s²) |
| Golden ratio | φ | 1.618034 | - |

### SSZ Parameters

| Parameter | Symbol | Value | Description |
|-----------|--------|-------|-------------|
| Max segment density | Ξ_max | 1.0 | Saturation value |
| Coupling parameter | α | 1.0 | Time dilation coupling |
| Golden ratio | φ | 1.618034 | Exponential scale |

### Universal Constants

| Quantity | Symbol | Value | Note |
|----------|--------|-------|------|
| Intersection radius | r*/r_s | 1.386562 | Mass-independent |
| Intersection dilation | D* | 0.528007 | Universal |
| Segment density at r* | Ξ* | 0.893914 | From equation |

---

## Example Calculations

### Neutron Star (M = 2 M☉)

```python
M = 2 * 1.989e30  # kg
r_s = 2 * 6.674e-11 * M / (2.998e8)**2
r_s ≈ 2953 m ≈ 3 km

r* = 1.386562 * r_s
r* ≈ 4095 m ≈ 4 km
```

### Sgr A* (M = 4.1×10⁶ M☉)

```python
M = 4.1e6 * 1.989e30  # kg
r_s ≈ 1.21e10 m
r* ≈ 1.68e10 m
```

### Time Dilation at r = 2r_s

```python
# GR
D_GR(2r_s) = sqrt(1 - 1/2) = 0.707107

# SSZ
Ξ(2r_s) = 1.0 * (1 - exp(-1.618034 * 2))
Ξ(2r_s) ≈ 0.960682
D_SSZ(2r_s) = 1 / (1 + 0.960682)
D_SSZ(2r_s) ≈ 0.510027
```

---

## Limiting Behavior

### r → ∞ (Flat Spacetime)

```
Ξ(r) → Ξ_max
D_SSZ(r) → 1 / (1 + Ξ_max) ≈ 0.5
D_GR(r) → 1
```

**Note:** SSZ does NOT recover flat spacetime at infinity!
This is a feature, not a bug - represents vacuum Ξ field.

### r → r_s (Event Horizon)

**GR:**
```
D_GR(r_s) = 0  (divergence!)
```

**SSZ:**
```
Ξ(r_s) = 1.0 * (1 - exp(-1.618034))
Ξ(r_s) ≈ 0.802
D_SSZ(r_s) = 1 / (1 + 0.802) ≈ 0.555  (finite!)
```

### Near r* (Intersection)

**Taylor expansion around r*:**
```
D_SSZ(r* + δr) ≈ D* + A·δr + O(δr²)
D_GR(r* + δr) ≈ D* + B·δr + O(δr²)
```

**At r*, derivatives differ:**
```
dD_SSZ/dr|_{r*} ≠ dD_GR/dr|_{r*}
```

---

## Coordinate Systems

### Schwarzschild Coordinates (r, t)

**Line element (GR):**
```
ds² = -(1 - r_s/r)c²dt² + dr²/(1 - r_s/r) + r²dΩ²
```

**SSZ equivalent:**
```
dτ² = D²(r) dt² - dr²/c² - r²dΩ²/c²
```

### Proper Distance

**GR:**
```
dℓ_proper = dr / sqrt(1 - r_s/r)
```

**SSZ:**
```
dℓ_proper = dr  (in coordinate frame)
```

---

## Numerical Precision

### Required Accuracy

For scientific validation:
- r*/r_s: 6 significant figures (1.386562)
- D*: 6 significant figures (0.528007)
- φ: 6 significant figures (1.618034)

### Computational Stability

**Recommended:**
- Use double precision (float64)
- Check causality: 0 < D ≤ 1
- Handle r → r_s carefully
- Use exp(-x) for large x

---

## Validation Formulas

### Crossover Test

```python
def test_crossover(M):
    r_s = schwarzschild_rs(M)
    r_star = 1.386562 * r_s
    D_GR = sqrt(1 - r_s/r_star)
    D_SSZ = 1 / (1 + 1.0 * (1 - exp(-1.618034 * r_star/r_s)))
    assert abs(D_GR - D_SSZ) < 1e-6
```

### Causality Test

```python
def test_causality(r, r_s):
    D = time_dilation_ssz(r, r_s)
    assert 0 < D <= 1 + 1e-12
```

---

## Common Mistakes

### ❌ WRONG Formulas

```python
# WRONG segment density:
Ξ(r) = Ξ_max * (1 - exp(-r_s/r))  # r_s/r is WRONG!

# WRONG time dilation:
D = φ^(-α·Ξ)  # Completely wrong!
D = 1 - Ξ     # Also wrong!
```

### ✅ CORRECT Formulas

```python
# CORRECT segment density:
Ξ(r) = Ξ_max * (1 - exp(-φ * r_s / r))  # φ·r/r_s is CORRECT!

# CORRECT time dilation:
D = 1 / (1 + Ξ)  # Simple inverse!
```

---

## Next Steps

**[← Back: Core Principles](01_CORE_PRINCIPLES.md)** | **[Next: Physical Interpretation →](03_PHYSICAL_INTERPRETATION.md)**

**See also:**
- **[Numerical Validation](15_NUMERICAL_VALIDATION.md)** - Implementation details
- **[Test Results](16_TEST_RESULTS.md)** - Validation with correct formulas
