
# Segmented Spacetime Mass Projection – API Overview

**Repository:** [Segmented-Spacetime-Mass-Projection-Unified-Results](https://github.com/LinoCasu/Segmented-Spacetime-Mass-Projection-Unified-Results)

---

## Overview

This API/Function overview documents all key computational routines and helper functions provided in the main scripts of the repository.  
It is aimed at users wishing to integrate, extend, or systematically test the segment-density and mass-reconstruction machinery.

**Theoretical background and derivations:** See the published preprints and documentation in `/docs/` and `/papers/`.

---

## 1. Core Segment Functions

### `sigma(r, r_phi, r_s, sigma_c=1.0, eps=1e-15)`

**Description:**  
Returns the segment density σ(r) at radius r, between the Schwarzschild radius r_s and the segment radius r_φ.

**Parameters:**
- `r`:      float, radius at which to evaluate segment density
- `r_phi`:  float, segment radius r_φ (outer boundary)
- `r_s`:    float, Schwarzschild radius r_s (inner boundary)
- `sigma_c`:float, critical segment density (default 1.0)
- `eps`:    float, numerical offset to avoid log(0) (default 1e-15)

**Returns:**  
- `float`: segment density at radius r. Returns `nan` if r is outside (r_s, r_φ).

**Example:**
```python
sigma_val = sigma(r=1.5, r_phi=2.0, r_s=1.0)
```

---

## 2. Mass and Radius Conversion Functions

### `r_phi(M, phi=phi)`

**Description:**  
Computes the segment radius r_φ for a given mass M.

**Parameters:**
- `M`: float, mass (kg)
- `phi`: float, Golden Ratio (default: calculated from (1+sqrt(5))/2)

**Returns:**  
- `float`: segment radius r_φ

### `r_schw(M)`

**Description:**  
Computes the Schwarzschild radius r_s for mass M.

**Parameters:**
- `M`: float, mass (kg)

**Returns:**  
- `float`: Schwarzschild radius r_s

### `r_phi_kerr(M, a, phi=phi)`

**Description:**  
Computes the segment radius for a Kerr (rotating) object.

**Parameters:**
- `M`: float, mass (kg)
- `a`: float, dimensionless spin/Kerr parameter |a|<1
- `phi`: float, Golden Ratio (optional)

**Returns:**  
- `float`: segment radius r_φ for Kerr metric

---

## 3. Error Propagation Utility

### `rel_mass_error(dr_phi, r_phi, dG, G, dphi, phi, dc, c)`

**Description:**  
Calculates the relative error of reconstructed mass M as a function of uncertainties in segment radius, G, c, and phi.

**Parameters:**
- `dr_phi`: float, absolute error in segment radius
- `r_phi`: float, segment radius
- `dG`: float, absolute error in gravitational constant G
- `G`: float, gravitational constant G
- `dphi`: float, absolute error in phi
- `phi`: float, value of phi
- `dc`: float, absolute error in c
- `c`: float, value of c

**Returns:**  
- `float`: relative error in M (as a fraction)

**Example:**
```python
err = rel_mass_error(0.01*r_phi, r_phi, 0.0001*G, G, 0.00001*phi, phi, 0.0, c)
```

---

## 4. Example: Segment Density Table and Plot

- Use the core functions above to generate a table of σ(r) for a range of r between r_s and r_φ (logarithmic spacing recommended).
- For visualization, use `matplotlib`:

```python
import numpy as np, matplotlib.pyplot as plt
r_vals = np.geomspace(r_s, r_phi, 100)
sigma_vals = [sigma(r, r_phi, r_s) for r in r_vals]
plt.plot(r_vals, sigma_vals)
plt.xlabel('r')
plt.ylabel('σ(r)')
plt.title('Segment Density Profile')
plt.show()
```

---

## 5. Demo and CLI Scripts

### `further-final.py`

- Combines both demo and physics modes.
- Produces tabular output and (if matplotlib installed) segment-density plot.
- Recommended entry point for new users.

---

## 6. Notes

- All scripts use SI units.
- Numerical stability at the interval boundaries is enforced via eps.
- See code comments for edge-case handling and special features (e.g., Kerr/rotation).

---

## 7. Contact / Contribution

For bug reports, feature requests, or contributions, please open an Issue or contact the maintainers via GitHub or ResearchGate (see main README).

---

**Last update:** 2025-08-07  
Maintainers: Lino Casu & Carmen Wrede  
License: Anti-Capitalist Software License v1.4
