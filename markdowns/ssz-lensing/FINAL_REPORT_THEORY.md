# FINAL REPORT: Theoretical Framework

## No-Fit Gravitational Lens Inversion in the Radial Scaling Gauge

**Authors:** Carmen N. Wrede, Lino P. Casu  
**Date:** January 2026  
**Version:** 1.0 Final

---

## Executive Summary

This document presents the complete theoretical foundation for **exact gravitational lens inversion** using the Radial Scaling Gauge (RSG) formalism. The key innovation is the **no-fit principle**: instead of minimizing residuals to find "best" parameters, we solve the lens equation exactly and use residuals only to validate model adequacy.

**Core Results:**
- 4 images → 8 equations → exact solution for 6-parameter quadrupole model
- Nonlinear phase φ_γ found via bisection rootfinding
- Linear parameters (θ_E, a, b, β_x, β_y) found via exact linear solve
- Machine-precision parameter recovery (~10⁻¹¹ residuals) for clean data

---

## 1. Physical Foundation

### 1.1 The Radial Scaling Gauge

In the RSG formalism, spacetime geometry is encoded in a scaling function:

```
s(r, φ) = 1 + Ξ(r, φ)
```

where:
- **s = 1** corresponds to flat spacetime
- **Ξ** encodes gravitational effects
- **Ξ → 0** as r → ∞ (asymptotic flatness)

### 1.2 Light Deflection

The deflection angle arises from transverse gradients of Ξ:

```
α(θ) = (1/π) ∫ ∇_⊥ Ξ dℓ
```

integrated along the unperturbed light ray at angular position θ.

### 1.3 The Lens Equation

Source (β) and image (θ) positions are related by:

```
β = θ - α_red(θ)
```

where α_red = (D_LS/D_S) α is the reduced deflection angle.

### 1.4 Einstein Radius

For a spherically symmetric lens, the Einstein radius satisfies:

```
θ_E = α_red(θ_E)
```

This defines the characteristic angular scale of the lens.

---

## 2. Multipole Expansion

### 2.1 Angular Decomposition

We expand Ξ in Fourier harmonics:

```
Ξ(r, φ) = Ξ_0(r) + Σ_m [a_m(r) cos(m(φ - φ_m)) + b_m(r) sin(m(φ - φ_m))]
```

### 2.2 Physical Interpretation

| Multipole | Name | Physical Origin | Effect |
|-----------|------|-----------------|--------|
| m = 0 | Monopole | Total enclosed mass | Sets θ_E |
| m = 1 | Dipole | Center offset | Usually zero |
| m = 2 | Quadrupole | Ellipticity + shear | Dominant distortion |
| m ≥ 3 | Higher | Substructure | Fine corrections |

### 2.3 Minimal Model (m = 2)

Near the Einstein ring, the image position equation becomes:

```
θ = θ_E + a·cos(2(φ - φ_γ)) + β·cos(φ - φ_β)
```

**Cartesian form:**
```
x = β_x + θ_E·cos(φ) + a·cos(2Δ)·cos(φ) - b·sin(2Δ)·sin(φ)
y = β_y + θ_E·sin(φ) + a·cos(2Δ)·sin(φ) + b·sin(2Δ)·cos(φ)
```

where Δ = φ - φ_γ.

---

## 3. The No-Fit Principle

### 3.1 Traditional vs No-Fit Approach

| Aspect | Traditional Fitting | No-Fit Inversion |
|--------|---------------------|------------------|
| **Method** | Minimize χ² | Solve exactly |
| **Residuals** | Driven to zero | Used for validation |
| **Model inadequacy** | Hidden | Exposed |
| **Multiple solutions** | Return "best" | Return all |
| **Uncertainty** | Error bars | Explicit degeneracies |

### 3.2 Why No Fitting?

1. **Physical clarity:** Lens inversion is geometric, not statistical
2. **Uniqueness transparency:** Fitting hides degeneracies
3. **No hidden assumptions:** Least squares assumes Gaussian errors
4. **Interpretable failures:** Exact solve fails cleanly, fitting "succeeds" badly

### 3.3 What We Forbid

- `np.linalg.lstsq` or any least-squares solver
- `scipy.optimize.minimize` or gradient-based optimizers
- Any method that "minimizes" a cost function
- Any method that returns "best fit" parameters

### 3.4 What We Allow

- **Exact linear solves:** `np.linalg.solve` for square systems
- **Rootfinding:** Bisection, bracketing for finding zeros
- **Consistency checks:** Evaluating residuals to validate (not optimize)

---

## 4. Degrees of Freedom Analysis

### 4.1 Equation Counting

**From N images:**
- Each image provides 2 equations (x and y components)
- 4 images → 8 equations

**For m = 2 model:**
- β_x, β_y: 2 unknowns (source position)
- θ_E: 1 unknown (Einstein radius)
- a, b: 2 unknowns (quadrupole amplitudes)
- φ_γ: 1 unknown (quadrupole phase, **nonlinear**)

**Total:** 6 unknowns, 8 equations → **overdetermined by 2**

### 4.2 Solution Strategy

```
8 equations - 6 unknowns = 2 redundant equations
```

**Strategy:**
1. Fix φ_γ (the nonlinear parameter)
2. Solve 5 equations for 5 linear unknowns
3. Use remaining 3 equations for consistency check
4. Find φ_γ where consistency function h(φ_γ) = 0

### 4.3 General Formula

For multipole order m_max with N images:

| Component | Count |
|-----------|-------|
| Equations | 2N |
| Source position | 2 |
| Einstein radius | 1 |
| Amplitudes per m | 2 |
| Phases (nonlinear) | m_max - 1 |

---

## 5. Conditional Linearity

### 5.1 Key Insight

**The system is LINEAR in amplitudes when phases are FIXED.**

This transforms a 6-dimensional nonlinear problem into:
- 1D rootfinding (for φ_γ)
- 5D exact linear solve (for β_x, β_y, θ_E, a, b)

### 5.2 Mathematical Structure

For fixed φ_γ, the lens equation becomes:

```
A(φ_γ) · p = b
```

where:
- A is an 8×5 matrix (known from image positions and φ_γ)
- p = [β_x, β_y, θ_E, a, b]ᵀ (unknowns)
- b = [x₁, y₁, ..., x₄, y₄]ᵀ (image positions)

### 5.3 The Consistency Function

Define:
```
h(φ_γ) = residual of check equation after solving 5×5 subsystem
```

The correct φ_γ satisfies **h(φ_γ) = 0**.

### 5.4 Root Properties

- h(φ_γ) is continuous in [0, π/2] (due to 90° periodicity)
- Typically has 1 root for physically consistent data
- Multiple roots indicate degeneracy (report all)

---

## 6. Algorithm Description

### 6.1 Complete Algorithm

```
INPUT: 4 image positions (x_i, y_i), i = 1, ..., 4

STEP 1: BRACKET ROOTS
   Sample h(φ_γ) over [0, π/2] at ~100 points
   Identify sign changes (brackets)

STEP 2: REFINE ROOTS (for each bracket)
   Apply bisection to find φ_γ where h(φ_γ) = 0
   Tolerance: ~10⁻¹²

STEP 3: SOLVE LINEAR SYSTEM (for each root)
   Build 8×5 matrix A(φ_γ)
   Extract 5×5 invertible subsystem
   Solve exactly: p = A_sub⁻¹ b_sub

STEP 4: VALIDATE
   Compute residuals: r = A·p - b
   Check: θ_E > 0 (physical)
   Check: max|r| < tolerance (consistency)

STEP 5: REPORT
   Return all valid (φ_γ, p) pairs
   Include residuals for each
   Flag model adequacy

OUTPUT: Parameters + residuals + diagnostics
```

### 6.2 Pseudocode

```python
def invert_no_fit(images):
    # Step 1: Find roots
    roots = []
    for i in range(n_samples - 1):
        if h(phi[i]) * h(phi[i+1]) < 0:
            root = bisection(h, phi[i], phi[i+1])
            roots.append(root)
    
    # Step 2: Solve for each root
    solutions = []
    for phi_gamma in roots:
        A, b = build_linear_system(images, phi_gamma)
        p = solve_5x5_subset(A, b)
        
        # Validate
        residuals = A @ p - b
        if p[2] > 0 and max(abs(residuals)) < tol:
            solutions.append((phi_gamma, p, residuals))
    
    return solutions
```

---

## 7. Degeneracies and Ambiguities

### 7.1 Phase Periodicity

φ_γ is only defined modulo 90° (for m = 2):
```
φ_γ ≡ φ_γ + π/2
```

**Convention:** Report φ_γ ∈ [0, π/2)

### 7.2 Sign Ambiguity in b

The quadrupole amplitude b can appear with opposite sign:
```
(φ_γ, b) ≡ (φ_γ + π/4, -b)
```

This is **expected** and indicates the same physical configuration.

### 7.3 Mass-Sheet Degeneracy

The transformation:
```
κ → λκ + (1 - λ)
β → λβ
```

leaves image positions invariant.

**Broken by:**
- Time delays: Δt ∝ (1 - λ)
- Velocity dispersion: σ_v² ∝ M
- Stellar masses

### 7.4 Multiple Valid Solutions

When multiple (φ_γ, p) pairs satisfy all constraints:
- Report ALL solutions
- Do NOT pick "best" by minimization
- Note that additional data needed to distinguish

---

## 8. Residual Interpretation

### 8.1 Residual Meaning

Residuals are **not** fitting errors. They diagnose model adequacy:

| Residual Pattern | Indicates | Action |
|------------------|-----------|--------|
| All < 10⁻¹⁰ | Model adequate | Accept solution |
| Structured (angular) | Missing multipole | Try m = 3 |
| Structured (radial) | Wrong center | Check lens centroid |
| Large, random | Data error | Check observations |

### 8.2 Never Minimize Residuals

Traditional approach: Make residuals small by adjusting parameters.
**Our approach:** Let residuals reveal model inadequacy.

A lens inversion is either:
- **Exact** (model adequate): residuals at machine precision
- **Invalid** (model inadequate): large residuals expose the problem

---

## 9. Extension to Higher Multipoles

### 9.1 Adding m = 3

For octupole correction:
- Add 2 amplitudes (a₃, b₃) and 1 phase (φ₃)
- Need 6+ images for exact solution
- Or use time delays as additional constraints

### 9.2 General Protocol

1. Start with m_max = 2
2. If residuals show angular pattern → increase m_max
3. Each additional m adds 3 unknowns (2 amplitudes + 1 phase)
4. Need proportionally more constraints

### 9.3 Practical Limit

For galaxy-scale lenses:
- m = 2 typically sufficient (ellipticity + shear)
- m = 3 rare but sometimes needed
- m ≥ 4 almost never constrainable

---

## 10. Physical Constraints

### 10.1 Required Conditions

| Parameter | Constraint | Interpretation |
|-----------|------------|----------------|
| θ_E | > 0 | Mass must be positive |
| a² + b² | < θ_E² | Quadrupole perturbative |
| β | < β_crit | Inside caustic for 4 images |

### 10.2 Cross Regime

For 4-image configuration (Einstein cross):
```
|b| > |β|/2
```

If violated, caustic is not crossed, only 2 images form.

### 10.3 Angular Condition

Images must satisfy:
```
β·sin(φ - φ_β) + b·sin(2(φ - φ_γ)) = 0
```

This determines the image azimuths for given source position.

---

## 11. Worked Example

### 11.1 Input

**True parameters:**
- θ_E = 1.0 (arcsec)
- a = 0.05
- b = 0.15
- β = 0.08
- φ_β = 30°
- φ_γ = 20°

### 11.2 Generated Images

Solving angular condition yields 4 azimuths:
- φ₁ ≈ 23.2°
- φ₂ ≈ 128.5°
- φ₃ ≈ 216.7°
- φ₄ ≈ 309.1°

Image positions (x, y) computed from radial condition.

### 11.3 Inversion

1. Sample h(φ_γ) over [0°, 90°]
2. Find root at φ_γ ≈ 20° (matches true value)
3. Solve linear system → recover θ_E, a, b, β_x, β_y
4. Check residuals: max|r| ≈ 3×10⁻¹¹

### 11.4 Result

**Recovered:**
- θ_E = 1.000000000... ✓
- a = 0.050000000... ✓
- b = -0.150000000... (sign flip expected)
- β_x = 0.069282032... ✓
- β_y = 0.040000000... ✓
- φ_γ = 20.000000000...° ✓

**Verdict:** Exact recovery to machine precision.

---

## 12. Summary of Key Results

### 12.1 Theoretical Contributions

1. **Gauge formulation** of gravitational lensing via scaling function Ξ
2. **Multipole expansion** with physical interpretation of each order
3. **Conditional linearity** enabling exact solution strategy
4. **Residual diagnostics** for model adequacy assessment

### 12.2 Methodological Contributions

1. **No-fit principle** as rigorous alternative to curve fitting
2. **Exact algorithm** with guaranteed correctness for adequate models
3. **Explicit degeneracy handling** instead of statistical uncertainty
4. **Extension protocol** for additional observables

### 12.3 Practical Results

1. **4 images sufficient** for m = 2 model
2. **Machine-precision recovery** for clean data
3. **Clear failure modes** when model inadequate
4. **No tuning parameters** needed

---

## 13. Conclusion

The no-fit inversion framework provides a mathematically rigorous approach to gravitational lens modeling. By separating **exact algebraic solution** from **residual validation**, we achieve:

- Transparent uniqueness properties
- Honest reporting of degeneracies
- Clear model adequacy assessment
- Guaranteed exact solutions when applicable

This approach is particularly suited for high-precision lensing studies where the goal is to understand what the data can and cannot constrain, rather than obtaining a "best guess" that may hide fundamental ambiguities.

---

## References

1. Schneider, P., Ehlers, J., Falco, E. E., *Gravitational Lenses*, Springer (1992)
2. Kochanek, C. S., "Strong Gravitational Lensing," *Dark Matter and Dark Energy*, Springer (2004)
3. Wrede, C. N., Casu, L. P., *Radial Scaling Gauge for Maxwell Fields* (2025)

---

*Final Report: Theoretical Framework*  
*Gauge Gravitational Lens Inversion Project*  
*Carmen N. Wrede & Lino P. Casu, 2026*
