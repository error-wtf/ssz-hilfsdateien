# GR-SSZ Intersection Analysis Summary

**Generated:** 2025-10-28 06:20:04

---

## Equations

**General Relativity (Schwarzschild):**
$$
D_{\text{GR}}(r) = \sqrt{1 - \frac{r_s}{r}}
$$

**Segmented Spacetime:**
$$
D_{\text{SSZ}}(r) = \frac{1}{1 + \Xi(r)}
$$

$$
\Xi(r) = \Xi_{\max} \left(1 - e^{-arphi r_s / r}\right)
$$

**Intersection Condition:**
$$
D_{\text{GR}}(r_*) = D_{\text{SSZ}}(r_*)
$$

---

## Parameters

- φ = 1.618034
- Ξ_max = 1.0
- G = 6.674300e-11 m³ kg⁻¹ s⁻²
- c = 299792458 m/s

---

## Numeric Results

### Neutron Star (2 M☉)

- Mass: 2.00e+00 M☉
- Schwarzschild radius: 5.906679e+03 m (5.91 km)
- **Intersection found:**
  - r* = 8.189974e+03 m
  - r*/r_s = 1.386562
  - D* = 0.528007

### Sgr A* (4.1×10⁶ M☉)

- Mass: 4.10e+06 M☉
- Schwarzschild radius: 1.210869e+10 m (12108691.47 km)
- **Intersection found:**
  - r* = 1.678945e+10 m
  - r*/r_s = 1.386562
  - D* = 0.528007

---

## Interpretation

The intersection occurs (if it exists) where:

$$
\Xi(r_*) \approx \frac{GM}{r_* c^2}
$$

At this radius, both theories predict identical time dilation.

**Physical Meaning:**

- **Below r*:** GR and SSZ give same predictions (weak field limit)
- **Above r*:** Theories diverge
  - GR → Diverges to zero at r = r_s (time stops)
  - SSZ → Saturates at finite value (time slows but doesn't stop)

**Key Result:**

Intersection(s) found for specific parameter values. This marks the transition radius where SSZ corrections become dominant.

---

## Files Generated

- Plots: `gr_ssz_intersection_*.png`
- Data: `gr_ssz_intersection_points.csv`
- Sensitivity: `gr_ssz_sensitivity.csv`, `gr_ssz_sensitivity_map.png`
- Summary: `gr_ssz_intersection_summary.md` (this file)
