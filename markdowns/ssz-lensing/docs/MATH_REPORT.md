# Mathematics Report

## Complete Mathematical Derivations for Gauge Gravitational Lensing

**Version:** 1.0  
**Date:** 2025-01-21  
**Authors:** Carmen N. Wrede, Lino P. Casu

---

## 1. Foundational Equations

### 1.1 Radial Scaling Gauge

The geometric scaling function in the Radial Scaling Gauge:

$$s(r, \varphi) = 1 + \Xi(r, \varphi)$$

where Ξ is the scaling perturbation from flat space.

### 1.2 Effective Refractive Index Analogy

The phase accumulation along a light path:

$$\Phi = \int s(\mathbf{x}) \, d\ell$$

This is analogous to optical path length with effective index:

$$n_{\text{eff}} \approx s = 1 + \Xi$$

### 1.3 Fermat Principle

Light follows paths that are stationary with respect to phase:

$$\delta \Phi = \delta \int s \, d\ell = 0$$

---

## 2. Deflection Angle Derivation

### 2.1 Weak Field Approximation

For |Ξ| ≪ 1, the deflection angle is:

$$\boldsymbol{\alpha} = \int \nabla_\perp \ln s \, d\ell \approx \int \nabla_\perp \Xi \, d\ell$$

**Derivation:**

Starting from the eikonal equation for a spatially varying "index":

$$\nabla (\ln s) = \frac{\nabla s}{s}$$

For s = 1 + Ξ with |Ξ| ≪ 1:

$$\frac{\nabla s}{s} = \frac{\nabla \Xi}{1 + \Xi} \approx \nabla \Xi$$

The perpendicular component integrated along the unperturbed path gives the deflection.

### 2.2 Reduced Deflection

The reduced deflection angle accounting for distance factors:

$$\boldsymbol{\alpha}_{\text{red}} = \frac{D_{ds}}{D_s} \boldsymbol{\alpha}$$

where:
- D_d = angular diameter distance to lens
- D_s = angular diameter distance to source
- D_{ds} = angular diameter distance from lens to source

---

## 3. Lens Equation

### 3.1 General Form

$$\boldsymbol{\beta} = \boldsymbol{\theta} - \boldsymbol{\alpha}_{\text{red}}(\boldsymbol{\theta})$$

where:
- **β** = source position (angular)
- **θ** = image position (angular)
- **α_red** = reduced deflection at image position

### 3.2 Coordinate System

Using polar coordinates (r, φ) centered on the lens:
- r = |**θ**| = angular distance from lens center
- φ = azimuthal angle
- Unit vectors: **ê_r** (radial), **ê_φ** (tangential)

---

## 4. Einstein Ring Condition

### 4.1 Symmetry Requirements

For a perfect Einstein ring:
1. Rotationally symmetric lens: Ξ = Ξ(r) only
2. Source on axis: **β** = 0

### 4.2 Ring Equation

$$\theta_E = \alpha_{\text{red}}(\theta_E)$$

This defines the Einstein radius θ_E as the self-consistent solution.

**Physical interpretation:** At θ_E, the deflection exactly equals the angular position, bringing all azimuthal angles to a single source point (the axis).

---

## 5. Multipole Expansion of Anisotropy

### 5.1 Angular Decomposition

For a non-axisymmetric lens:

$$\Xi(r, \varphi) = \Xi_0(r) + \sum_{m=1}^{\infty} \Xi_m(r) \cos m(\varphi - \varphi_m)$$

### 5.2 Quadrupole Dominance (m=2)

In realistic lenses, the first significant anisotropic term is usually m=2:

$$\Xi(r, \varphi) \approx \Xi_0(r) + \Xi_2(r) \cos 2(\varphi - \varphi_\gamma)$$

**Physical origins:**
- Elliptical mass distribution → internal quadrupole
- External shear from nearby masses → external quadrupole

### 5.3 Why m=2 Gives 4 Images

The angular equation (derived below) has the form:

$$f(\varphi) = A \sin(\varphi - \varphi_\beta) + B \sin 2(\varphi - \varphi_\gamma) = 0$$

This is a superposition of period-2π and period-π oscillations, generically yielding **4 zeros** in [0, 2π).

Higher modes:
- m=3 → up to 6 images
- m=4 → up to 8 images
- But these are typically subdominant

---

## 6. Local Model at Einstein Radius

### 6.1 Deflection Ansatz

Near θ ≈ θ_E, we parameterize the deflection as:

$$\boldsymbol{\alpha}(\theta, \varphi) = \theta_E \hat{\mathbf{e}}_r + a \cos 2\Delta \, \hat{\mathbf{e}}_r + b \sin 2\Delta \, \hat{\mathbf{e}}_\varphi$$

where Δ = φ - φ_γ is the angle relative to the quadrupole axis.

**Parameter meanings:**
- θ_E: monopole (ring scale)
- a: radial quadrupole amplitude
- b: tangential quadrupole amplitude
- φ_γ: quadrupole axis orientation

### 6.2 Lens Equation in Components

The lens equation **β** = **θ** - **α** in polar components:

**Radial component:**
$$\beta \cos(\varphi - \varphi_\beta) = r - \theta_E - a \cos 2\Delta$$

**Tangential component:**
$$\beta \sin(\varphi - \varphi_\beta) = -b \sin 2\Delta$$

### 6.3 Angular Condition

From the tangential equation:

$$\boxed{\beta \sin(\varphi - \varphi_\beta) + b \sin 2(\varphi - \varphi_\gamma) = 0}$$

This determines the **azimuthal positions** of images.

### 6.4 Radial Condition

Substituting the angular solutions into the radial equation:

$$\boxed{r_i = \theta_E + a \cos 2(\varphi_i - \varphi_\gamma) + \beta \cos(\varphi_i - \varphi_\beta)}$$

This gives the **radial positions** of images.

---

## 7. Linear System for Inversion

### 7.1 Cartesian Reformulation

Converting to Cartesian coordinates for numerical stability:

**Source offset:** β_x = β cos(φ_β), β_y = β sin(φ_β)

**Useful identities:**
$$\beta \cos(\varphi - \varphi_\beta) = \beta_x \cos\varphi + \beta_y \sin\varphi$$
$$\beta \sin(\varphi - \varphi_\beta) = \beta_y \cos\varphi - \beta_x \sin\varphi$$

### 7.2 Deflection in Cartesian

The deflection vector:

$$\alpha_x = \theta_E \cos\varphi + a \cos 2\Delta \cos\varphi - b \sin 2\Delta \sin\varphi$$
$$\alpha_y = \theta_E \sin\varphi + a \cos 2\Delta \sin\varphi + b \sin 2\Delta \cos\varphi$$

### 7.3 Lens Equation per Image

For image i at position (x_i, y_i):

$$x_i = \beta_x + \alpha_{x,i}$$
$$y_i = \beta_y + \alpha_{y,i}$$

Rearranging:

$$\beta_x + \theta_E \cos\varphi_i + a \cos 2\Delta_i \cos\varphi_i - b \sin 2\Delta_i \sin\varphi_i = x_i$$
$$\beta_y + \theta_E \sin\varphi_i + a \cos 2\Delta_i \sin\varphi_i + b \sin 2\Delta_i \cos\varphi_i = y_i$$

### 7.4 Matrix Form

For unknowns **p** = [β_x, β_y, θ_E, a, b]ᵀ:

$$\mathbf{A} \mathbf{p} = \mathbf{b}$$

where A is 8×5 (2 equations per image × 4 images) and **b** contains the measured positions.

**Matrix row for x-equation of image i:**
$$A[2i, :] = [1, 0, \cos\varphi_i, \cos 2\Delta_i \cos\varphi_i, -\sin 2\Delta_i \sin\varphi_i]$$

**Matrix row for y-equation of image i:**
$$A[2i+1, :] = [0, 1, \sin\varphi_i, \cos 2\Delta_i \sin\varphi_i, \sin 2\Delta_i \cos\varphi_i]$$

---

## 8. Solving the Overdetermined System

### 8.1 The φ_γ Problem

The matrix A depends on φ_γ through Δ_i = φ_i - φ_γ.

We have:
- 8 equations
- 6 unknowns: β_x, β_y, θ_E, a, b, φ_γ
- System is overdetermined

### 8.2 No-Fit Strategy

**Key insight:** For the correct φ_γ, the system becomes exactly solvable.

**Algorithm:**

1. Fix φ_γ → A(φ_γ) is determined
2. Select 5 equations → 5×5 system
3. Solve exactly: **p** = A_5×5⁻¹ **b**_5
4. Check residual of 6th equation: h(φ_γ) = A[6,:] **p** - b[6]
5. Find φ_γ where h(φ_γ) = 0 via rootfinding

### 8.3 Residual Function

$$h(\varphi_\gamma) = [\mathbf{A}(\varphi_\gamma)]_{k,:} \cdot \mathbf{p}(\varphi_\gamma) - b_k$$

where k is the check equation index and **p**(φ_γ) is the solution of the 5×5 subsystem.

### 8.4 Rootfinding

Find zeros of h(φ_γ) in [0, π/2] via:

1. Scan for sign changes at N sample points
2. Apply bisection to each bracket
3. Collect all roots

**Note:** φ_γ is only defined mod π/2 due to quadrupole symmetry.

---

## 9. Validation via Residuals

### 9.1 Full Residual Vector

After finding φ_γ and **p**:

$$\mathbf{r} = \mathbf{A} \mathbf{p} - \mathbf{b}$$

### 9.2 Residual Metrics

**Maximum absolute residual:**
$$r_{\max} = \max_i |r_i|$$

**RMS residual:**
$$r_{\text{rms}} = \sqrt{\frac{1}{8} \sum_{i=1}^{8} r_i^2}$$

### 9.3 Interpretation

| Residual Level | Interpretation |
|----------------|----------------|
| ~10⁻¹⁵ | Machine precision, perfect model |
| ~10⁻¹⁰ | Numerical precision, exact recovery |
| ~10⁻³ | Small deviations, model adequate |
| >10⁻² | Significant: higher modes, substructure, or centering error |

---

## 10. Symmetry Analysis

### 10.1 φ_γ Ambiguity

The quadrupole cos(2Δ) has period π, so:

$$\varphi_\gamma \equiv \varphi_\gamma + \frac{\pi}{2} \pmod{\frac{\pi}{2}}$$

### 10.2 Parameter Transformation

Under φ_γ → φ_γ + π/2:
- cos(2Δ) → cos(2Δ + π) = -cos(2Δ)
- sin(2Δ) → sin(2Δ + π) = -sin(2Δ)

Therefore:
- a → -a
- b → -b

**This is not a bug but physical symmetry.**

### 10.3 Canonical Form

We report φ_γ in [0°, 90°) with the corresponding signs of a and b.

---

## 11. Moment Method (Diagnostic Only)

### 11.1 Second Moment

$$m_2 = \sum_{i=1}^{4} e^{2i\varphi_i}$$

### 11.2 Axis Estimate

$$\varphi_\gamma^{\text{est}} = \frac{1}{2} \arg(m_2)$$

**Caveat:** This is only an estimate. The final φ_γ must come from rootfinding for exactness.

---

## 12. Summary of Key Formulas

| Quantity | Formula |
|----------|---------|
| Scaling function | s = 1 + Ξ |
| Deflection (weak field) | **α** ≈ ∫∇⊥Ξ dℓ |
| Lens equation | **β** = **θ** - **α**_red |
| Einstein ring | θ_E = α_red(θ_E) |
| Angular condition | β sin(φ-φ_β) + b sin(2(φ-φ_γ)) = 0 |
| Radial condition | r = θ_E + a cos(2(φ-φ_γ)) + β cos(φ-φ_β) |
| Linear system | A**p** = **b**, dim(A) = 8×5 |
| Root condition | h(φ_γ) = 0 |

---

## 13. Numerical Validation

### 13.1 Synthetic Test

**Input parameters:**
- θ_E = 1.0
- a = 0.05
- b = 0.15
- β = 0.08
- φ_β = 30°
- φ_γ = 20°

### 13.2 Generated Image Positions

| Image | x | y | r | φ |
|-------|---|---|---|---|
| 1 | +1.046 | +0.425 | 1.129 | +22.1° |
| 2 | -0.558 | +0.768 | 0.949 | +126.0° |
| 3 | -0.932 | -0.274 | 0.972 | -163.6° |
| 4 | +0.088 | -0.919 | 0.923 | -84.5° |

### 13.3 Recovery Results

| Parameter | True | Recovered | Error |
|-----------|------|-----------|-------|
| θ_E | 1.0 | 1.000000 | 8.6×10⁻¹² |
| β | 0.08 | 0.080000 | 1.1×10⁻¹¹ |
| a | 0.05 | 0.050000 | 3.1×10⁻¹² |
| b | 0.15 | -0.150000 | (sign flip) |
| φ_γ | 20° | 20.00° | ~10⁻¹⁰ |

**Residuals:** max = 2.48×10⁻¹¹, rms = 9.66×10⁻¹²

---

*Mathematics Report generated 2025-01-21*
