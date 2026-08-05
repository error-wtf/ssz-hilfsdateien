# Model Zoo Report: Parallel Model Comparison

## Extended Observables and Multi-Path Analysis

---

## 1. Overview

The Model Zoo extension implements **parallel model comparison** with four models running simultaneously, not replacing each other. This enables learning from model differences.

### Key Innovation: FORBIDDEN = "Need More Data", Not "Abort"

When a model is underspecified, the system now tells you **what observables would make it legal**, rather than simply refusing.

---

## 2. Four Parallel Models

| Model | Parameters | DOF (4 images) | Status |
|-------|------------|----------------|--------|
| m=2 | 5 | +3 | OVERDETERMINED |
| m=2 + shear | 7 | +1 | STANDARD |
| m=2 + m=3 | 7 | +1 | STANDARD |
| m=2 + shear + m=3 | 9 | -1 | FORBIDDEN |

### Linear Parametrization (no grid search)

All models use linear forms:
- `(c_m, s_m)` instead of `(A_m, phi_m)`
- `(gamma_1, gamma_2)` instead of `(gamma, phi_gamma)`

This keeps inversion exact and algebraic.

---

## 3. Regime Gate Logic

```python
if dof >= 2:   -> OVERDETERMINED  (good redundancy)
if dof == 1:   -> STANDARD        (minimal redundancy)
if dof == 0:   -> MINIMAL         (exactly determined)
if dof < 0:    -> FORBIDDEN       (need more observables)
```

### FORBIDDEN Response

Instead of aborting, the system suggests:
- Add flux ratios (up to N-1 for N images)
- Add time delays (up to N-1 for N images)
- Add arc points (+2 constraints each)
- Add second source (typically +6 net constraints)

---

## 4. Extended Observables

### 4.1 Arc Points

Extended emission (arcs, rings) provides additional constraints:

```python
system = LensSystem(
    name="lens",
    images=[quad_images],
    arc_points=np.array([[1.0, 0.1], [0.9, 0.2], ...])
)
```

Each arc point adds **2 constraints** (x, y position).

### 4.2 Multi-Source

Multiple background sources share lens parameters:

```python
system = LensSystem(
    name="lens",
    images=[source1_images, source2_images],
    n_sources=2
)
```

For 2 sources with 4 images each:
- Constraints: 16 (8 per source)
- Additional params: 2 (extra beta_x, beta_y)
- Net gain: +6 constraints

### 4.3 Constraint Summary

| Observable | Constraints Added |
|------------|------------------|
| Image position | +2 per image |
| Arc point | +2 per point |
| Flux ratio | +1 per ratio |
| Time delay | +1 per delay |
| Second source (4 img) | +6 net |

---

## 5. Q2237+0305 Einstein Cross Results

Real-data diagnostic comparing models:

| Model | Max Residual | Improvement |
|-------|--------------|-------------|
| m=2 only | 0.0081 | baseline |
| m=2 + shear | 0.0065 | 20% |
| m=2 + m=3 | 0.0000 | 100% |

**Interpretation:** The bar structure of the lens galaxy requires either shear or m=3 (octupole) for accurate modeling. Pure quadrupole is insufficient.

---

## 6. Test Coverage

| Test | Purpose | Status |
|------|---------|--------|
| test_m2_allowed | Basic regime check | PASS |
| test_m2_shear_m3_forbidden | FORBIDDEN detection | PASS |
| test_arc_points_rescue | Arc points unlock model | PASS |
| test_multi_source_rescue | Multi-source unlock | PASS |
| test_shear_recovery | Shear param recovery | PASS |
| test_m3_recovery | m=3 param recovery | PASS |
| test_zoo_comparison | Report generation | PASS |
| test_q2237_model_comparison | Real data diagnostic | PASS |
| test_q2237_forbidden_info | Suggestion quality | PASS |
| test_q2237_full_report | Full report output | PASS |

**Total: 10/10 tests passed**

---

## 7. Usage Example

```python
from models.model_zoo import LensSystem, ModelZoo

# Define system
system = LensSystem(
    name="Q2237+0305",
    images=[image_positions]
)

# Run all models
zoo = ModelZoo(system)
results = zoo.run_all()

# Compare
print(zoo.compare())

# Access specific result
best = results[ModelType.M2_SHEAR]
print(f"theta_E = {best.params['theta_E']}")
```

---

## 8. Files Added

| File | Purpose |
|------|---------|
| `src/models/model_zoo.py` | Model Zoo implementation |
| `tests/test_model_zoo.py` | Core tests (7) |
| `tests/test_q2237_diagnostic.py` | Real-data diagnostic (3) |

---

## 9. Key Insights

1. **m=2 alone is often insufficient** for real lenses with structure
2. **Shear and m=3 are complementary**, not mutually exclusive
3. **FORBIDDEN is informative**, not terminal
4. **Extended observables** (arcs, multi-source) unlock complex models
5. **Parallel comparison** reveals which physical effects matter

---

**End of Model Zoo Report**
