# Physics Report

## Physical Foundations of Gauge Gravitational Lensing

**Version:** 1.0  
**Date:** 2025-01-21  
**Authors:** Carmen N. Wrede, Lino P. Casu

---

## 1. Physical Context

### 1.1 Gravitational Lensing Overview

Gravitational lensing occurs when light from a distant source is deflected by the gravitational field of an intervening mass (the lens). This produces:

- **Multiple images** of the source
- **Magnification** and distortion
- **Time delays** between images

### 1.2 Einstein Cross Configuration

The Einstein Cross is a specific 4-image configuration where:
- A distant quasar is lensed by a foreground galaxy
- Four bright images appear approximately symmetrically around the lens
- Named after the Q2237+0305 system (Huchra's Lens, discovered 1985)

---

## 2. Radial Scaling Gauge Framework

### 2.1 Core Concept

In the Radial Scaling Gauge (RSG) formulation, gravitational effects are encoded through a **geometric scaling function**:

$$s(r, \varphi) = 1 + \Xi(r, \varphi)$$

This represents how physical distances are scaled relative to coordinate distances near a gravitating mass.

### 2.2 Relation to Standard GR

In standard General Relativity, gravitational lensing arises from the Schwarzschild metric. The RSG formulation is equivalent but emphasizes the **optical analogy**:

| GR Formulation | RSG Formulation |
|----------------|-----------------|
| Metric perturbation h_μν | Scaling function s(r) |
| Geodesic equation | Fermat principle with s |
| Shapiro delay | Phase accumulation ∫s dℓ |

### 2.3 Physical Interpretation of Ξ

The scaling perturbation Ξ encodes:
- **Gravitational potential** (in weak field: Ξ ∝ Φ/c²)
- **Time dilation** effects
- **Spatial curvature** contributions

For a point mass in weak field:
$$\Xi(r) \approx \frac{r_s}{2r}$$

where r_s = 2GM/c² is the Schwarzschild radius.

---

## 3. Eye-Lens Analogy

### 3.1 Optical Lens (Eye)

In an optical lens:
- Material has refractive index n(x)
- Light follows Fermat principle: δ∫n dℓ = 0
- Index gradient causes bending

### 3.2 Gravitational "Lens"

In gravity (RSG picture):
- Geometry has scaling function s(x)
- Light follows: δ∫s dℓ = 0
- Scaling gradient causes bending

### 3.3 Key Distinction

| Aspect | Optical | Gravitational |
|--------|---------|---------------|
| Medium | Material (glass, water) | No medium (vacuum) |
| Mechanism | Electromagnetic interaction | Spacetime geometry |
| Index/scaling | n > 1 inside medium | s > 1 near mass |
| Cause | Density variation | Metric curvature |

**The analogy is structural, not physical.** Both systems obey stationary-path principles with similar mathematics, but the underlying physics differs fundamentally.

---

## 4. Einstein Ring Physics

### 4.1 Formation Conditions

An Einstein ring forms when:
1. **Axial alignment:** Source directly behind lens (β = 0)
2. **Circular symmetry:** Lens mass is spherically symmetric

### 4.2 Physical Interpretation

The ring represents **degenerate imaging**:
- All azimuthal angles φ are equivalent solutions
- Light from a point source spreads into a continuous ring
- The ring radius θ_E depends on:
  - Lens mass M
  - Distance configuration (D_d, D_s, D_{ds})

### 4.3 Einstein Radius Formula

$$\theta_E = \sqrt{\frac{4GM}{c^2} \frac{D_{ds}}{D_d D_s}}$$

For typical galaxy-scale lensing: θ_E ~ 1 arcsecond.

---

## 5. Breaking the Symmetry: Einstein Cross

### 5.1 Source Offset (Dipole)

When β ≠ 0:
- Ring degeneracy is broken
- For a round lens: typically **2 images** form
- Images lie along the source-lens axis

### 5.2 Lens Ellipticity (Quadrupole)

Real galaxies are not perfectly round. The dominant anisotropy is:
- **Internal:** Elliptical mass distribution
- **External:** Tidal shear from neighboring masses

This introduces a **quadrupole** (m=2) term in the potential.

### 5.3 Combined Effect: 4 Images

The interplay of dipole (offset) and quadrupole (ellipticity/shear) generically produces **4 images** arranged as a cross.

**Physical picture:**
- The lens creates a "saddle point" potential
- Light paths cluster around 4 critical directions
- These correspond to the 4 images of the cross

### 5.4 Image Multiplicity Table

| Configuration | Typical # Images |
|---------------|------------------|
| Axisymmetric, β=0 | Ring (∞) |
| Axisymmetric, β≠0 | 2 (+ weak central) |
| Quadrupole, β≠0 | 4 (cross) |
| Higher modes | 6, 8, ... (rare) |

---

## 6. Caustics and Critical Curves

### 6.1 Definitions

- **Critical curve:** Locus in image plane where magnification diverges
- **Caustic:** Mapping of critical curve to source plane

### 6.2 Cross Regime

The Einstein cross forms when the source lies **inside the caustic** structure created by the quadrupole.

For a quadrupole-dominated lens:
- Inner caustic is diamond-shaped (astroid)
- Source inside → 4 images
- Source outside → 2 images

### 6.3 Image Properties

| Image Type | Position | Parity | Magnification |
|------------|----------|--------|---------------|
| Minimum | Outside ring | + | Moderate |
| Saddle | Near ring | - | High |
| Maximum | Near center | + | Low (often invisible) |

---

## 7. Physical Parameters

### 7.1 Einstein Radius (θ_E)

**Physical meaning:** Characteristic angular scale of lensing.

**Determines:**
- Overall scale of image separation
- Total magnification
- Lens mass (if distances known)

### 7.2 Source Offset (β)

**Physical meaning:** Angular position of source relative to optical axis.

**Determines:**
- Asymmetry of image positions
- Relative magnifications
- Direction of "break" from ring

### 7.3 Quadrupole Parameters (a, b, φ_γ)

**Physical meaning:**
- a: Radial stretching from ellipticity
- b: Tangential shear
- φ_γ: Orientation of quadrupole axis

**Determines:**
- Four-fold symmetry breaking
- Cross orientation
- Image configuration details

---

## 8. Observable Quantities

### 8.1 What CAN Be Measured from Geometry

From the angular positions of 4 images:

| Quantity | Accessible? |
|----------|-------------|
| θ_E (Einstein radius) | ✓ Yes |
| β direction (φ_β) | ✓ Yes |
| β magnitude (angular) | ✓ Yes |
| Quadrupole axis (φ_γ) | ✓ Yes |
| Quadrupole strength (a, b) | ✓ Yes |

### 8.2 What CANNOT Be Determined from Geometry Alone

| Quantity | Why Not |
|----------|---------|
| Source distance | Requires redshift measurement |
| Lens mass | Requires θ_E + distances |
| Time delays | Requires light curves |
| Hubble constant | Requires delays + model |

### 8.3 The Distance Degeneracy

The lens equation:
$$\boldsymbol{\beta} = \boldsymbol{\theta} - \frac{D_{ds}}{D_s} \boldsymbol{\alpha}(\boldsymbol{\theta})$$

shows that angular quantities (β, θ) are dimensionless ratios. The absolute physical scale requires **distance measurements** (redshifts).

---

## 9. Physical Consistency Checks

### 9.1 Recovered Parameter Ranges

For a physically meaningful solution:

| Parameter | Valid Range | Physical Reason |
|-----------|-------------|-----------------|
| θ_E | > 0 | Positive ring radius |
| β | < θ_E | Source inside caustic for cross |
| a, b | < θ_E | Perturbative quadrupole |

### 9.2 Residual Interpretation

| Residual Level | Physical Meaning |
|----------------|------------------|
| ~10⁻¹¹ | Perfect local model |
| ~10⁻² | Higher multipoles present |
| ~10⁻¹ | Substructure or wrong center |

### 9.3 Known Limitations

1. **Local approximation:** Model valid only near θ ≈ θ_E
2. **Single plane:** No multi-plane lensing
3. **Point images:** No extended source effects
4. **Static:** No time-domain effects

---

## 10. Connection to SSZ/Gauge Framework

### 10.1 SSZ Consistency

This lensing model is consistent with the SSZ (Segmented Spacetime) framework:
- Scaling function s = 1 + Ξ matches SSZ radial scaling
- Phase accumulation matches SSZ time dilation formulation
- Weak field limit recovers standard GR predictions

### 10.2 Key SSZ Formula

In SSZ weak field:
$$\Xi(r) = \frac{r_s}{2r}$$

For strong field:
$$\Xi(r) = 1 - e^{-\varphi r_s / r}$$

The lensing model uses the weak-field form, valid for typical galaxy-scale lenses.

---

## 11. Real-World Application: Q2237+0305

### 11.1 System Parameters

| Parameter | Value |
|-----------|-------|
| Lens redshift | z_d = 0.0394 |
| Source redshift | z_s = 1.695 |
| Lens type | Barred spiral galaxy |
| θ_E (observed) | ~0.9" |
| Image separation | ~1.8" |

### 11.2 Observed Image Positions

| Image | RA offset (") | Dec offset (") |
|-------|---------------|----------------|
| A | +0.758 | +0.956 |
| B | -0.798 | +0.623 |
| C | -0.609 | -0.767 |
| D | +0.677 | -0.739 |

### 11.3 Physical Insights

From inversion of Q2237+0305:
- Significant quadrupole from bar structure
- Source position offset from center
- Higher-order residuals indicate substructure

---

## 12. Summary: Physical Validation

### 12.1 Consistency Checklist

| Aspect | Status |
|--------|--------|
| Fermat principle | ✓ Satisfied |
| Multipole physics | ✓ m=2 dominance confirmed |
| Caustic structure | ✓ 4 images inside diamond caustic |
| Parameter ranges | ✓ All physical |
| SSZ compatibility | ✓ Consistent with s = 1 + Ξ |

### 12.2 Limitations Acknowledged

| Limitation | Impact |
|------------|--------|
| No absolute distances | Cannot determine mass alone |
| Local approximation | Valid only near θ_E |
| No higher modes | May show in residuals |
| Static model | Cannot predict time delays |

---

*Physics Report generated 2025-01-21*
