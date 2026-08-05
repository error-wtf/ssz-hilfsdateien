# Implementation Documentation

## Gauge Gravitational Lens Inversion Tool

**Version:** 1.0  
**Date:** 2025-01-21  
**Authors:** Carmen N. Wrede, Lino P. Casu

---

## 1. Overview

This document provides complete technical documentation of the `gauge_lens_inversion.py` implementation.

### 1.1 Purpose

The tool performs **exact inversion** of Einstein Cross gravitational lens configurations to recover:
- Source position (β-vector)
- Einstein ring radius (θ_E)
- Quadrupole parameters (a, b, φ_γ)

### 1.2 Design Principles

| Principle | Implementation |
|-----------|----------------|
| **No curve fitting** | Only linear algebra + rootfinding |
| **No scipy.optimize** | Custom bisection implementation |
| **Exact solutions** | 5×5 matrix inversion, not least-squares |
| **Residual validation** | All 8 equations checked post-solution |

---

## 2. Module Structure

```
gauge_lens_inversion.py
├── Constants
│   └── DEFAULT_PARAMS          # Default synthetic test parameters
├── Core Algorithms
│   ├── bisection()             # Root-finding without scipy
│   ├── find_all_roots()        # Scan + bisect for all roots
│   ├── generate_synthetic_cross()  # Forward model
│   ├── build_linear_system()   # Construct A matrix and b vector
│   ├── solve_5x5_subset()      # Exact 5×5 solve
│   ├── compute_residuals()     # Residual statistics
│   ├── consistency_residual()  # h(φ_γ) function for rootfinding
│   └── invert_no_fit()         # Main inversion algorithm
├── Utilities
│   ├── moment_estimate()       # m2 diagnostic (not used for final)
│   ├── print_results()         # Formatted output
│   ├── load_points_from_json() # JSON input
│   └── save_example_json()     # JSON output
└── CLI
    └── main()                  # Argument parsing and execution
```

---

## 3. Function Documentation

### 3.1 `bisection(f, a, b, tol=1e-12, max_iter=100)`

**Purpose:** Find root of f in [a,b] via bisection.

**Algorithm:**
```
1. Check sign change: f(a) * f(b) < 0
2. Loop:
   - mid = (a + b) / 2
   - If |f(mid)| < tol or |b-a| < tol: return mid
   - If f(a) * f(mid) < 0: b = mid
   - Else: a = mid
3. Return midpoint
```

**Complexity:** O(log₂((b-a)/tol)) iterations

**Why not scipy.optimize.brentq?**
- Explicit control over algorithm
- No external dependencies beyond NumPy
- Guaranteed behavior (no heuristics)

---

### 3.2 `find_all_roots(f, x_min, x_max, n_samples=500, tol=1e-12)`

**Purpose:** Find ALL roots in interval by scanning for sign changes.

**Algorithm:**
```
1. Sample f at n_samples points in [x_min, x_max]
2. For each pair where f[i] * f[i+1] < 0:
   - Apply bisection to bracket [x[i], x[i+1]]
   - Collect root
3. Return array of all roots
```

**Trade-off:** n_samples controls resolution vs. speed.  
- Too few: may miss roots  
- Too many: slower  
- 500 is safe for smooth functions on [0, π/2]

---

### 3.3 `generate_synthetic_cross(theta_E, a, b, beta, phi_beta, phi_gamma)`

**Purpose:** Forward model - generate image positions from lens parameters.

**Model equations:**

```
Angular condition: β sin(φ - φ_β) + b sin(2(φ - φ_γ)) = 0
Radial condition:  r = θ_E + a cos(2(φ - φ_γ)) + β cos(φ - φ_β)
```

**Returns:**
- `points`: (N, 2) array of (x, y) positions
- `phi_solutions`: array of image azimuths
- `diagnostics`: dict with n_images, in_cross_regime flag

**Cross regime condition:**
For 4 images, need approximately |b| > β/2.

---

### 3.4 `build_linear_system(points, phi_gamma)`

**Purpose:** Construct the 8×5 linear system for a given φ_γ.

**Unknowns:** p = [β_x, β_y, θ_E, a, b]

**Equations per point (x_i, y_i):**

For image at angle φ_i with Δ_i = φ_i - φ_γ:

```
x-equation:
  β_x + θ_E cos(φ_i) + a cos(2Δ_i) cos(φ_i) - b sin(2Δ_i) sin(φ_i) = x_i

y-equation:
  β_y + θ_E sin(φ_i) + a cos(2Δ_i) sin(φ_i) + b sin(2Δ_i) cos(φ_i) = y_i
```

**Matrix structure:**
```
A[2i,   :] = [1, 0, cos(φ), cos(2Δ)cos(φ), -sin(2Δ)sin(φ)]
A[2i+1, :] = [0, 1, sin(φ), cos(2Δ)sin(φ),  sin(2Δ)cos(φ)]
b[2i]      = x_i
b[2i+1]    = y_i
```

**Dimensions:** A is 8×5, b is 8×1 (for 4 points)

---

### 3.5 `solve_5x5_subset(A, b_vec, rows)`

**Purpose:** Extract 5 rows and solve exactly.

**Algorithm:**
```
1. A_sub = A[rows, :]  # 5×5 matrix
2. b_sub = b_vec[rows] # 5×1 vector
3. Check det(A_sub) ≠ 0
4. p = A_sub^(-1) @ b_sub
```

**Returns:** (solution, success_flag)

**Singularity handling:** If |det| < 1e-14, return failure flag.

---

### 3.6 `consistency_residual(phi_gamma, points, row_subset, check_row)`

**Purpose:** Compute h(φ_γ) for rootfinding.

**Algorithm:**
```
1. Build linear system for this φ_γ
2. Solve 5×5 subset exactly
3. Return residual of check_row equation
```

**Mathematical basis:**
If φ_γ is correct, ALL 8 equations should be satisfied.
The 6th equation residual h(φ_γ) = 0 determines the correct φ_γ.

---

### 3.7 `invert_no_fit(points, center=(0,0))`

**Purpose:** Main inversion - recover all parameters from 4 image points.

**Complete Algorithm:**

```
INPUT: 4 image positions (x_i, y_i), lens center

1. PREPROCESSING
   - Subtract center from points
   - Validate: exactly 4 points required

2. ROW COMBINATION LOOP
   For each (row_subset, check_row) combination:
   
   2.1 Define consistency function h(φ_γ)
   
   2.2 ROOT SEARCH
       - Scan φ_γ ∈ [0, π/2] for sign changes
       - Apply bisection to each bracket
       - Collect all candidate φ_γ values
   
   2.3 CANDIDATE EVALUATION
       For each φ_γ candidate:
       - Solve 5×5 system for p
       - Compute all 8 residuals
       - Track best (smallest max residual)

3. PARAMETER EXTRACTION
   - β_x, β_y, θ_E, a, b from solution vector
   - β = sqrt(β_x² + β_y²)
   - φ_β = atan2(β_y, β_x)
   - Normalize φ_γ to [0, 90°)

4. OUTPUT
   - params dict with all recovered values
   - residuals dict with max_abs, rms
   - diagnostics dict
```

**Row combinations tried:**
```python
[([0,1,2,3,4], 5), ([0,1,2,3,5], 4), ([0,1,2,4,5], 3),
 ([0,1,3,4,5], 2), ([0,2,3,4,5], 1), ([1,2,3,4,5], 0),
 ([0,1,2,5,6], 7), ([0,1,4,5,6], 7)]
```

**Why multiple combinations?**
- Some 5×5 subsets may be singular for certain configurations
- Robustness against numerical degeneracy

---

## 4. Data Structures

### 4.1 Input JSON Format

```json
{
  "center": [0.0, 0.0],
  "points": [[x1,y1], [x2,y2], [x3,y3], [x4,y4]],
  "units": "arcsec",
  "note": "Description"
}
```

### 4.2 Output params dict

```python
{
  'beta_x': float,      # Source offset x-component
  'beta_y': float,      # Source offset y-component
  'beta': float,        # Source offset magnitude
  'phi_beta': float,    # Source offset angle (radians)
  'phi_beta_deg': float,# Source offset angle (degrees, 0-360)
  'theta_E': float,     # Einstein radius
  'a': float,           # Radial quadrupole
  'b': float,           # Tangential quadrupole
  'phi_gamma': float,   # Quadrupole axis (radians)
  'phi_gamma_deg': float# Quadrupole axis (degrees, mod 90)
}
```

### 4.3 Output residuals dict

```python
{
  'residual_vector': ndarray,  # All 8 residuals
  'max_abs': float,            # max(|residual|)
  'rms': float                 # sqrt(mean(residual²))
}
```

---

## 5. Error Handling

| Condition | Detection | Response |
|-----------|-----------|----------|
| Wrong number of points | len(points) ≠ 4 | Return error in diagnostics |
| Singular matrix | |det| < 1e-14 | Try next row combination |
| No roots found | Empty root list | Try next row combination |
| All combinations fail | best_result is None | Return error message |

---

## 6. Numerical Considerations

### 6.1 Precision

- All computations use float64 (double precision)
- Expected residuals for synthetic data: ~1e-11 to 1e-15
- Tolerance for bisection: 1e-12

### 6.2 Symmetry

φ_γ is physically defined modulo 90° for pure m=2 quadrupole:
- φ_γ and φ_γ + 90° are equivalent
- Sign of b flips accordingly
- This is NOT a bug but physical symmetry

### 6.3 Degeneracies

| Configuration | Issue | Mitigation |
|---------------|-------|------------|
| Nearly circular images | Small quadrupole | May have larger relative error in a,b |
| Images at 90° intervals | Symmetric configuration | Multiple valid φ_γ solutions |
| β ≈ 0 | Near-ring | φ_β becomes undefined |

---

## 7. CLI Interface

```
usage: gauge_lens_inversion.py [-h] [--input INPUT] [--save-example SAVE_EXAMPLE]

options:
  -h, --help            show help message
  --input, -i INPUT     Path to JSON file with image points
  --save-example, -s    Save synthetic example to JSON file
```

**Default behavior (no arguments):** Run synthetic test with DEFAULT_PARAMS.

---

## 8. Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| numpy | ≥1.20 | Linear algebra, array operations |
| json | stdlib | File I/O |
| argparse | stdlib | CLI parsing |

**No scipy required.** All optimization/rootfinding is custom-implemented.

---

## 9. Testing

### 9.1 Synthetic Test

```python
# Parameters in cross regime
DEFAULT_PARAMS = {
    'theta_E': 1.0,
    'a': 0.05,
    'b': 0.15,
    'beta': 0.08,
    'phi_beta': np.radians(30),
    'phi_gamma': np.radians(20),
}
```

### 9.2 Expected Results

| Metric | Expected | Actual |
|--------|----------|--------|
| θ_E recovery | 1.000000 | 1.000000 |
| β recovery | 0.080000 | 0.080000 |
| Max residual | < 1e-10 | 2.48e-11 |
| RMS residual | < 1e-10 | 9.66e-12 |

### 9.3 Validation Criteria

- **Exact recovery:** All parameters match to >10 significant figures
- **Residuals:** At machine precision (~1e-11 to 1e-15)
- **Symmetry:** b may have opposite sign (φ_γ ambiguity)

---

*Documentation generated 2025-01-21*
