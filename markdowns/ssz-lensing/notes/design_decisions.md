# Design Decisions: Gauge Gravitational Lensing Framework

## Core Philosophy: No-Fit Policy

This framework implements gravitational lens inversion **without any curve fitting or least-squares optimization**. This is not a limitation but a deliberate design choice rooted in physical and mathematical principles.

---

## 1. No-Fit Policy

### What We Forbid
- `np.linalg.lstsq` or any least-squares solver
- `scipy.optimize.minimize` or any gradient-based optimizer
- Any method that "minimizes" a cost function
- Any method that returns "best fit" parameters

### What We Allow
- **Exact linear solves**: `np.linalg.solve` for square invertible systems
- **Rootfinding**: Bisection, bracketing, Newton-Raphson for finding zeros
- **Consistency checks**: Evaluating residuals to validate solutions (not minimize)

### Why?
1. **Physical clarity**: A lens inversion is not a "best guess" but an exact geometric inversion.
2. **Uniqueness transparency**: Fitting hides degeneracies; exact solving exposes them.
3. **No hidden assumptions**: LS implicitly assumes Gaussian errors and uniform weights.
4. **Interpretable failures**: When exact solve fails, we know exactly why (missing constraints, not "poor convergence").

---

## 2. Observables Close the System

### Fundamental Principle
The number of independent equations must equal the number of unknowns.

### Image Positions Alone
- N image positions → 2N scalar equations (x, y components)
- Source position β → 2 unknowns
- Einstein radius θ_E → 1 unknown
- Quadrupole (a, b, φ_γ) → 3 unknowns (but φ_γ can be absorbed into orientation)

For minimal m=2 model with 4 images:
- Equations: 8 (from 4 images × 2 coordinates)
- Unknowns: 5 (β_x, β_y, θ_E, a, b) + 1 nonlinear (φ_γ)
- Strategy: Fix φ_γ → solve 5 linear equations → validate with remaining 3

### When More Unknowns
If model has more parameters (higher multipoles), we need:
1. **More images** (rare lenses with 6+ images)
2. **Time delays** Δt_ij between images
3. **Flux ratios** (with caution - affected by microlensing)
4. **External constraints** (velocity dispersion, stellar mass estimates)
5. **Extended source constraints** (arc geometry)

### When Fewer Observables
If we have fewer observables than unknowns:
1. **Reduce model complexity** (lower m_max)
2. **Fix parameters by physical assumption** (e.g., assume SIS profile)
3. **Report degeneracy explicitly** (not "fit with large error bars")

---

## 3. Gauge-Verankerung (Gauge Anchoring)

### The Scaling Function
In the Radial Scaling Gauge (RSG), spacetime geometry is encoded in:
```
s(r, φ) = 1 + Ξ(r, φ)
```
where Ξ is the deviation from flat spacetime.

### Deflection from Ξ
The reduced deflection angle is:
```
α_red ≈ (1/π) ∫ ∇⊥ Ξ dℓ
```
integrated along the line of sight through the lens.

### Multipole Interpretation
The multipole coefficients are Fourier coefficients of Ξ at the Einstein radius:
- m=0: Monopole (sets θ_E, the mass scale)
- m=1: Dipole (center offset - usually zero by choice of origin)
- m=2: Quadrupole (ellipticity/shear - dominant anisotropy)
- m≥3: Higher multipoles (substructure, external perturbations)

### Thin Lens Limit
All models assume the thin lens approximation:
- Lens thickness << distances to source/observer
- Valid for galaxy-scale lensing
- Breakdown requires multi-plane treatment

---

## 4. Output Format

Every inversion returns:

### Required Outputs
1. **Parameters**: Best (exact) solution or list of degenerate solutions
2. **Residuals**: Per-equation residuals (not just summary statistics)
3. **Residual statistics**: max |r|, RMS, mean
4. **Model adequacy flag**: PASS/FAIL based on threshold (not minimum)

### Diagnostic Outputs
5. **Pattern analysis**: Do residuals correlate with angle? With radius?
6. **Suggested extensions**: "Residuals suggest m=3 component" or "Need Δt data"
7. **DoF report**: Equations vs unknowns, which constraints used

### What We Never Report
- "Chi-squared" or goodness-of-fit statistics
- "Confidence intervals" from covariance matrices
- "Best fit" when multiple exact solutions exist

---

## 5. Conditional Linearity Strategy

### Key Insight
For multipole models, the system is **linear in amplitudes** when **phases are fixed**.

### Implementation
1. **Nonlinear variables**: Only the phase angles φ_m (m=2,3,...)
2. **Linear variables**: β, θ_E, amplitudes a_m, b_m
3. **Strategy**:
   - Scan/bracket phases to find roots of consistency function
   - At each candidate phase, solve linear system exactly
   - Validate via residuals

### Complexity Reduction
- Instead of N-dimensional optimization, we have ~m_max 1D rootfinds (nested or sequential)
- Bracketing is deterministic and guaranteed to find all roots
- No local minima issues

---

## 6. Degeneracy Handling

### Known Degeneracies
1. **Mass-sheet degeneracy**: λ scaling of mass and source position
   - Broken by: time delays, velocity dispersion, stellar masses
2. **Source position degeneracy**: Some configurations have multiple valid β
   - Handled by: returning all solutions, letting user select
3. **Orientation degeneracy**: φ_γ only defined mod 90° (for m=2)
   - Handled by: canonical range [0, π/2)

### Philosophy
We **expose** degeneracies, not hide them. If two parameter sets produce identical observables, both are reported with a note that additional data is needed to distinguish them.

---

## 7. Extension Protocol

### Adding New Observable Types
1. Add equation generator to model's `equations()` method
2. Update `count_equations()` in constraints module
3. Update DoF bookkeeping

### Adding Higher Multipoles
1. Extend `MultipoleModel` with new m
2. Phases become additional nonlinear variables
3. Amplitudes remain linear
4. Test with synthetic data showing residual improvement

### Adding External Constraints
1. Implement as additional equations (not priors)
2. Example: σ_v → mass within Einstein radius → θ_E constraint
3. Treat as exact (or with explicit tolerance), not as regularization

---

## Summary

| Aspect | Traditional Approach | Our Approach |
|--------|---------------------|--------------|
| Method | Least-squares fit | Exact solve + rootfinding |
| Unknowns > Equations | Regularization | Demand more observables |
| Multiple solutions | Return "best" | Return all |
| Residuals | Minimize | Validate |
| Degeneracies | Error bars | Explicit enumeration |
| Model selection | AIC/BIC | Residual patterns |

This design ensures **mathematical transparency**, **physical interpretability**, and **honest reporting** of what the data can and cannot constrain.

---

*Design document for gauge-gravitationslinse-quadratur framework*
*Authors: Carmen N. Wrede, Lino P. Casu*
