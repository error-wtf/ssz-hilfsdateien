# Mathematics Report: RSG Lensing Inversion Framework

## Complete Mathematical Foundation

**Authors:** Carmen N. Wrede, Lino P. Casu  
**Date:** January 2026

---

## 1. Linear Algebra Foundation

### 1.1 The Linear System

The lensing inversion problem reduces to:

```
A · x = b
```

Where:
- **A** ∈ ℝ^(n×p) : Design matrix (n constraints, p parameters)
- **x** ∈ ℝ^p : Parameter vector to solve for
- **b** ∈ ℝ^n : Observed image positions

### 1.2 Singular Value Decomposition (SVD)

The SVD of A is:

```
A = U · Σ · V^T
```

Where:
- **U** ∈ ℝ^(n×n) : Left singular vectors (constraint space)
- **Σ** ∈ ℝ^(n×p) : Diagonal singular values σ_1 ≥ σ_2 ≥ ... ≥ σ_r > 0
- **V** ∈ ℝ^(p×p) : Right singular vectors (parameter space)
- **r** = rank(A)

### 1.3 Key SVD Properties

| Property | Definition | Use |
|----------|------------|-----|
| Rank | r = #{σ_i > ε} | Effective constraints |
| Condition Number | κ = σ_1 / σ_r | Numerical stability |
| Nullspace Dimension | dim(N(A)) = p - r | Free parameters |
| Range Dimension | dim(R(A)) = r | Constrainable directions |

---

## 2. Regime Classification Mathematics

### 2.1 Classification Rules

```python
if κ > 10^10:
    regime = ILL_CONDITIONED
elif n < p or nullspace_dim > 0:
    regime = UNDERDETERMINED
elif n == p and nullspace_dim == 0:
    regime = DETERMINED
else:
    regime = OVERDETERMINED
```

### 2.2 Numerical Rank Computation

```python
tol = max(n, p) · ε_machine · σ_1
rank = sum(σ_i > tol for all i)
```

Where ε_machine ≈ 2.2×10^(-16) for 64-bit floats.

---

## 3. Design Matrix Construction

### 3.1 For Each Image at Position (x, y)

Compute polar coordinates:
```
r = √(x² + y²)
φ = atan2(y, x)
```

### 3.2 Row Construction (2 rows per image)

For image at angle φ, the design matrix rows are:

**Row for x-component:**
```
[cos(φ),  # θ_E contribution
 cos(2φ)·cos(φ), sin(2φ)·cos(φ),  # a_2, b_2
 cos(3φ)·cos(φ), sin(3φ)·cos(φ),  # a_3, b_3 (if m_max≥3)
 ...
 x, y,    # γ_1, γ_2 (if shear included)
 1, 0]    # β_x, β_y for this source
```

**Row for y-component:**
```
[sin(φ),  # θ_E contribution
 cos(2φ)·sin(φ), sin(2φ)·sin(φ),  # a_2, b_2
 cos(3φ)·sin(φ), sin(3φ)·sin(φ),  # a_3, b_3
 ...
 -y, x,   # γ_1, γ_2 shear contribution
 0, 1]    # β_x, β_y
```

### 3.3 Matrix Dimensions

| Configuration | n (rows) | p (cols) |
|---------------|----------|----------|
| K sources, N_k images each, m_max, shear | 2·Σ(N_k) | 1 + 2(m_max-1) + 2·(shear?) + 2K |

---

## 4. Solving the System

### 4.1 Determined Case (n = p, full rank)

Direct solve:
```
x = A^(-1) · b
```

In practice:
```python
x = np.linalg.solve(A, b)
```

### 4.2 Overdetermined Case (n > p, full column rank)

Least-norm solution (NOT least squares!):
```
x = A_subset^(-1) · b_subset  (use exactly p equations)
```

Then check consistency:
```
residual = A · x - b
```

**Critical:** We don't minimize ||Ax - b||. Non-zero residual means model mismatch, not fitting error.

### 4.3 Underdetermined Case (n < p or rank < p)

Minimal norm solution via pseudoinverse:
```
x_min = A^+ · b = V · Σ^+ · U^T · b
```

Where Σ^+ has entries 1/σ_i for σ_i > tol, else 0.

**Nullspace exploration:**
```
x_general = x_min + Σ α_i · v_i
```

Where v_i are nullspace basis vectors (rows of V^T where σ_i ≈ 0).

---

## 5. Nullspace Analysis

### 5.1 Nullspace Basis

The nullspace of A consists of vectors v where Av = 0:
```
N(A) = span{v_i : σ_i < tol}
```

These are the last (p - r) columns of V.

### 5.2 Parameter Identifiability

A parameter x_j is **non-identifiable** if:
```
∃ v ∈ N(A) : |v_j| > threshold
```

This means x_j can vary without changing the fit.

### 5.3 Parameter Ranges

For underdetermined systems, we compute:
```
x_j^min = min{(x_min + αv)_j : α ∈ [-1, 1], v ∈ N(A)}
x_j^max = max{...}
```

---

## 6. Condition Number Analysis

### 6.1 Sensitivity Formula

For perturbation δb in data:
```
||δx|| / ||x|| ≤ κ(A) · ||δb|| / ||b||
```

High κ means small data errors cause large parameter errors.

### 6.2 Condition Number Thresholds

| κ | Interpretation |
|---|----------------|
| < 10^3 | Well-conditioned |
| 10^3 - 10^6 | Moderate conditioning |
| 10^6 - 10^10 | Poorly conditioned |
| > 10^10 | Ill-conditioned (numerical issues likely) |

### 6.3 Sensitivity Directions

The most sensitive parameter directions are:
```
v_1 (corresponding to σ_1) : amplified most
v_r (corresponding to σ_r) : least stable
```

---

## 7. Regularization Mathematics

### 7.1 Tikhonov Regularization

Instead of x = A^+ b, solve:
```
x_reg = (A^T A + λI)^(-1) A^T b
```

This biases toward smaller ||x||.

### 7.2 Constrained Minimization

Minimize specific parameter subsets:
```
min ||x_multipoles||^2  subject to  Ax = b
```

### 7.3 Regularizers Implemented

| Name | Objective | Physical Meaning |
|------|-----------|------------------|
| minimal_norm | min ||x||_2 | Occam's razor |
| minimal_multipole | min Σ(a_m² + b_m²) | Smooth lens |
| minimal_shear | min (γ_1² + γ_2²) | Intrinsic over external |

---

## 8. Phase Mathematics

### 8.1 Component to Polar Conversion

```
A_m = √(a_m² + b_m²)
φ_m = (1/m) · atan2(b_m, a_m)
```

### 8.2 Phase Symmetry

For multipole order m:
```
φ_m  and  φ_m + π/m  are equivalent
```

This is because:
```
cos(m(φ - φ_m)) = cos(m(φ - (φ_m + π/m)))
```

### 8.3 m=2 Specific Degeneracy

For quadrupole:
```
φ_2 + π/2  gives identical deflection to φ_2
```

This creates two minima in residual landscape, separated by π/2.

---

## 9. Residual Analysis

### 9.1 Residual Vector

```
r = A · x - b
```

### 9.2 Residual Metrics

| Metric | Formula | Meaning |
|--------|---------|---------|
| Max residual | max|r_i| | Worst constraint violation |
| RMS residual | √(Σr_i²/n) | Average violation |
| Relative residual | ||r|| / ||b|| | Normalized error |

### 9.3 Interpretation

| Residual | Interpretation |
|----------|----------------|
| ~10^(-15) | Machine precision (exact solve) |
| ~10^(-8) | Numerical precision of solve |
| ~10^(-3) | Model slightly inadequate |
| > 0.01 | Model definitely inadequate |

---

## 10. Multi-Source Mathematics

### 10.1 Block Structure

For K sources, the design matrix has block structure:
```
A = [A_lens | B_1 | 0 | ... | 0  ]  ← source 1 images
    [A_lens | 0  | B_2| ... | 0  ]  ← source 2 images
    [  ...  |    |   |     |    ]
    [A_lens | 0  | 0 | ... | B_K]  ← source K images
```

Where:
- A_lens: columns for lens parameters (shared)
- B_k: identity-like blocks for source k position

### 10.2 DOF Gain from Multiple Sources

Each source adds:
- +2 parameters (β_x, β_y)
- +2N_k constraints (if N_k images)

Net gain per source: 2(N_k - 1) constraints

---

## 11. Algorithms Summary

### 11.1 Path A: Algebraic Solve

```python
def solve_algebraic(images):
    A, b = build_design_matrix(images)
    x = np.linalg.solve(A, b)  # or lstsq
    residuals = A @ x - b
    phases = derive_phases(x)  # OUTPUT
    return x, phases, residuals
```

### 11.2 Path B: Phase Scan

```python
def solve_phase_scan(images, phi_grid):
    residuals = []
    for phi in phi_grid:
        A_phi = build_matrix_at_fixed_phase(images, phi)
        x_phi = solve_linear(A_phi, b)
        residuals.append(compute_residual(x_phi))
    best_phi = phi_grid[argmin(residuals)]
    return best_phi, residuals
```

### 11.3 Path C: Underdetermined Explorer

```python
def explore_underdetermined(A, b):
    U, s, Vt = svd(A)
    x_min = pseudoinverse_solve(A, b)
    nullspace = Vt[s < tol]
    variants = [x_min + alpha * v for v in nullspace for alpha in [-1, 1]]
    ranges = compute_param_ranges(variants)
    return x_min, nullspace, ranges
```

---

## 12. Numerical Considerations

### 12.1 Floating Point Precision

- Use 64-bit floats (numpy default)
- Tolerance for zero: tol = n · ε · σ_max
- Avoid direct matrix inversion; use solve() or lstsq()

### 12.2 Avoiding Numerical Issues

1. Scale parameters to similar magnitudes
2. Check condition number before solving
3. Use SVD-based solve for near-singular systems
4. Report uncertainty when κ > 10^6

### 12.3 Verification

Always verify: ||A·x - b|| should be ≈ 0 for exact solve, or ≈ expected model error for overdetermined.

---

## 13. Summary of Key Formulas

| Concept | Formula |
|---------|---------|
| Lens equation | β = θ - α(θ) |
| Deflection | α_r = θ_E + Σ(a_m cos(mφ) + b_m sin(mφ)) |
| Design matrix | A · x = b |
| SVD | A = U Σ V^T |
| Condition | κ = σ_max / σ_min |
| Nullspace dim | p - rank(A) |
| Minimal norm | x = A^+ b |
| Phase from components | φ_m = (1/m) atan2(b_m, a_m) |
| Residual | r = Ax - b |
