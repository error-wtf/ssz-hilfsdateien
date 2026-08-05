# Discussion Context: Einstein Cross in the Radial Scaling Gauge

Technical lab log / discussion protocol for the gauge-based gravitational lensing analysis.

---

## 1. Initial Question / Intuition

**Core question:** Why does the Einstein Cross have 4 images, and not 6, 8, or a complete ring?

**Initial intuition:**
- The "quadrature of the circle" as an optimal case (the ring)
- Source offset as a "symptom" of being "out of quadrature"
- Offset changes angles -> splitting; brightest points not equally bright -> information about beta and axes

**Key insight:** The Einstein ring represents a degenerate symmetry case. Any deviation from this symmetry produces discrete images instead of a continuous ring.

---

## 2. Precision / Clarification

### The Ring as Optimal Case
- **Conditions:** beta = 0 (source on optical axis) AND rotationally symmetric lens
- **Result:** Continuous family of stationary solutions -> Einstein ring
- **Mathematical:** theta_E = alpha_red(theta_E)

### Breaking the Symmetry
- **Offset alone (beta != 0):** Breaks the ring, but typically results in 2-image geometry (plus possibly a weak central image) for a smooth, round lens
- **Quadrupole (m=2) active:** Required for robust 4-image (cross) configuration
- **Physical origin of quadrupole:** Lens ellipticity, external shear from neighboring masses

### Why 4 and Not 6/8?
- 4 images arise from m=2 (quadrupole) dominance
- 6 images would require m=3 (hexapole) dominance
- 8 images would require m=4 (octupole) dominance
- In realistic lenses, the first non-round term is almost always quadrupole -> 4 is generic

---

## 3. Eye-Lens Analogy (Precise)

### Optical Lens (Eye)
- Refractive index n(x) varies spatially
- Optical path: L_opt = integral of n(x) dl
- Fermat's principle: observed rays are stationary paths (delta L_opt = 0)
- Physical mechanism: material with varying density/composition

### Gravitational "Lens" (Gauge Picture)
- Geometric scaling s(r, phi) = 1 + Xi(r, phi)
- Effective "index": n_eff ~ s
- Phase accumulation path-dependent via integral of s dl
- Same variational logic: delta (integral of s dl) = 0
- **Key difference:** No material medium; geometry/metric causes the effect

### Common Ground
Both systems share the **stationary-path principle**. The mathematics is analogous:
- Eye: material index gradient
- Gravity: geometry/scaling gradient

This is NOT a claim that gravity "is" an optical medium, but that the phase/path formalism is structurally identical.

---

## 4. "Quadrature First -> Deviation as Measurement Signal"

### Calibration Strategy
1. Determine theta_E from the ring (or average image radius)
2. Any deviation from perfect ring symmetry becomes information:
   - **Dipole (beta):** Source offset direction and magnitude
   - **Quadrupole (a, b, phi_gamma):** Lens ellipticity/shear axis and strength

### What CAN Be Reconstructed from Angles
- Direction of source offset (phi_beta)
- Magnitude of angular offset (beta in angular units)
- Quadrupole axis orientation (phi_gamma, modulo 90 deg)
- Quadrupole strength parameters (a, b)

### What CANNOT Be Determined from Angles Alone
- **Cosmological distance to source:** Requires redshift measurements
- **Absolute mass of lens:** Requires time delays or velocity dispersions
- **3D position of source:** Only 2D sky projection is accessible

---

## 5. Mathematical Core (Minimal Model)

### Thin-Lens Equation
```
beta = theta - alpha_red(theta)
```
where alpha_red = (D_ds / D_s) * alpha is the reduced deflection.

### Gauge-Based Deflection
In the weak-field limit with s = 1 + Xi, |Xi| << 1:
```
alpha ~ integral of grad_perp(ln s) dl ~ integral of grad_perp(Xi) dl
```

### Einstein Ring Condition
```
beta = 0,  theta_E = alpha_red(theta_E)
```
This defines the ring radius as a "quadrature calibration" scale.

### Anisotropic Lens (Multipole Expansion)
```
Xi(r, phi) = Xi_0(r) + Xi_2(r) cos(2(phi - phi_gamma)) + ...
```
The m=2 term (quadrupole) dominates in realistic lenses.

---

## 6. Local Parameterization Near theta ~ theta_E

### Deflection Model
```
alpha(theta, phi) = theta_E * e_r + a * cos(2*Delta) * e_r + b * sin(2*Delta) * e_phi
```
where Delta = phi - phi_gamma.

### Resulting Equations

**Angular condition (determines image azimuths):**
```
beta * sin(phi - phi_beta) + b * sin(2*(phi - phi_gamma)) = 0
```
This typically has 4 solutions in the cross regime.

**Radial condition (determines image radii):**
```
r_i = theta_E + a * cos(2*(phi_i - phi_gamma)) + beta * cos(phi_i - phi_beta)
```

### Parameter Interpretation
| Parameter | Physical Meaning |
|-----------|------------------|
| theta_E | Einstein ring radius (reference scale) |
| beta | Source offset magnitude |
| phi_beta | Source offset direction |
| a | Radial quadrupole amplitude |
| b | Tangential quadrupole amplitude |
| phi_gamma | Quadrupole axis orientation |

---

## 7. Inversion Strategy ("No-Fit")

### Given
- Lens center M (assumed known)
- Four image positions (x_i, y_i) relative to M

### Unknown
- p = [beta_x, beta_y, theta_E, a, b] (5 linear unknowns)
- phi_gamma (1 nonlinear unknown)

### Algorithm
1. **For a given phi_gamma:** The system becomes linear in p. With 4 points (8 scalar equations) and 5 unknowns, we can:
   - Select 5 equations to form a 5x5 system
   - Solve exactly: p = A^(-1) * b

2. **Root condition for phi_gamma:**
   - Use a 6th equation as h(phi_gamma) = residual = 0
   - Find zeros via bracketing + bisection (NOT optimization)

3. **Selection among multiple roots:**
   - For synthetic data: residuals ~ machine precision at true phi_gamma
   - For real data: choose root with smallest max residual

4. **Final validation:**
   - Compute all 8 residuals
   - Report max_abs and RMS
   - Large residuals indicate: higher modes, substructure, centering error

### Symmetry Note
phi_gamma is only defined modulo 90 deg for a pure m=2 quadrupole. The inversion may return phi_gamma or phi_gamma + 90 deg with corresponding sign flips in (a, b). This is physics, not a bug.

---

## 8. Numerical Verification (Synthetic Test)

### Test Procedure
1. Generate synthetic Einstein cross from known parameters
2. Run no-fit inversion
3. Compare recovered vs true parameters
4. Check residuals

### Result from Initial Tests
- Residuals: ~1e-15 (machine precision)
- Parameter recovery: exact (within numerical precision)
- Conclusion: The inversion algorithm is mathematically correct

### Diagnostic for Real Data
If residuals are significantly above machine precision:
- Centering error in M
- Higher multipole modes (m > 2) present
- Observational noise
- Substructure in lens (multiple mass components)

---

## 9. Key Takeaways

1. **"Quadrature" = symmetry/degeneracy case:** The Einstein ring is not classical circle quadrature, but a degenerate limit where stationary solutions form a continuum.

2. **4 images require quadrupole:** Offset alone typically gives 2 images; robust 4-image cross needs m=2 anisotropy.

3. **No fitting:** The inversion uses exact linear algebra + rootfinding, not least-squares optimization.

4. **Angular information only:** Distances/depths require additional observables (redshifts, time delays).

5. **SSZ/Gauge perspective:** Consistent with s = 1 + Xi formalism; phase accumulation via geometric scaling.

---

## References

- Schneider, P., Ehlers, J., Falco, E. E., *Gravitational Lenses*, Springer (1992)
- Wrede, C. N., Casu, L. P., Bingsi, *Radial Scaling Gauge for Maxwell Fields* (2025)

---

*Document prepared as part of the SSZ/Radial Scaling Gauge development. Carmen N. Wrede & Lino P. Casu.*
