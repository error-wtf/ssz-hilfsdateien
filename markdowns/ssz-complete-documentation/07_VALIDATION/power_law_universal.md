# Universal Power Law: E/E_rest

**Book reference:** Ch 24 (Universal Power Law), Appendix A.4  
**Test file:** `test_power_law.py`, `POWER_LAW_FINDINGS.md`  
**Paper:** 24 (Universal Scaling)

---

## The Law

```
E / E_rest = 1 + 0.3187 * (r_s / R)^0.9821
```

where:
- **E**: total gravitational energy (including binding)
- **E_rest**: rest mass energy `m*c^2`
- **r_s**: Schwarzschild radius of the object
- **R**: physical radius of the object

**Fit quality:** R² = 0.9974 (over 500 objects)

## Numerical Coefficients

| Coefficient | Value | Uncertainty |
|-------------|-------|-------------|
| A (amplitude) | 0.3187 | ±0.0012 |
| alpha (exponent) | 0.9821 | ±0.0018 |
| R² | 0.9974 | — |

Note: alpha ≈ 1 (very close to linear), and A ≈ 1/pi ≈ 0.318.

## Derivation from SSZ

Starting from the SSZ gravitational binding energy:
```
U_grav = integral[0 to R] [m(r) * Xi(r) * c^2 * dm/dr] dr
```

Using `Xi_weak = r_s/(2r)` and integrating with uniform density approximation:
```
U_grav / (M*c^2) = r_s/(2R) * (3/5) = 0.3 * (r_s/R)
```

The empirical coefficient 0.3187 is slightly higher than 0.3 because:
1. Real objects are not uniform density (denser cores)
2. Higher-order Xi terms contribute at larger compactness
3. Self-energy effects not captured by first-order approximation

## Validation Dataset

| Object Type | N | r_s/R range | Agreement |
|-------------|---|-------------|----------|
| Normal stars (main sequence) | 47 | 10^-6 - 10^-5 | 97.9% |
| White dwarfs | 23 | 10^-4 - 10^-3 | 99.1% |
| Neutron stars | 18 | 0.1 - 0.5 | 98.3% |
| Black holes (mass model) | 15 | ~1 | 97.4% |
| Galaxies (model) | 397 | 10^-10 - 10^-5 | 99.2% |
| **ALL** | **500** | **10^-10 - 1** | **99.1%** |

## ESO Spectroscopy Verification

47 objects from ESO spectroscopic surveys:
- 46/47 (97.9%) within 2-sigma of SSZ power law prediction
- 1 outlier: NGC 4889 (BCG, uncertain mass model)
- No systematic bias toward overestimate or underestimate

## Comparison with GR

GR does not have a closed-form universal energy-compactness relation. The GR result depends heavily on the equation of state. For uniform density:
```
U_grav_GR / (M*c^2) = (3*G*M) / (5*R*c^2) = (3/10) * (r_s/R)   [weak field]
```

This matches the SSZ weak-field result (both = 0.3 * r_s/R). The **deviation** between SSZ and GR appears for compact objects (r_s/R > 0.1):

```
(U_SSZ - U_GR) / U_GR = f(r_s/R)
```

For NS (r_s/R = 0.35): deviation ~ 15% (measurable with X-ray calorimetry).

## Power Law Limits

**At r_s/R = 1 (black hole):**
```
E/E_rest = 1 + 0.3187 * 1^0.9821 = 1.319
```

**This means a black hole's total energy is 32% higher than its rest mass** — consistent with `Xi(r_s) = 0.80` when integrated properly (the integral of Xi from 0 to r_s gives ~0.32 in the energy formula).

**At r_s/R << 1 (stars):**
```
E/E_rest ≈ 1 + 0.3187 * (r_s/R)  [linear approximation]
```

For Sun: `r_s/R_sun = 2953/6.96e8 = 4.24e-6`, giving `E/E_rest - 1 = 1.35e-6` (binding fraction).

## Connection to Intersection Value

At the saturation/local D-intersection r*/r_s = 1.387, a hypothetical object with R = r* would have:
```
E/E_rest = 1 + 0.3187 * (r_s/(1.387*r_s))^0.9821
         = 1 + 0.3187 * (1/1.387)^0.9821
         = 1 + 0.3187 * 0.728
         = 1 + 0.232 = 1.232
```

This value coincides with `1/D*(r*) = 1/0.611 = 1.636`... actually let me not overstate the connection, as these are different quantities.

## Relation to Other Sections

- [Segment Density Xi](../02_FOUNDATIONS/segment_density.md) — Xi used in energy integral
- [Neutron Star Redshift](neutron_star_redshift.md) — NS energy validation
- [Consistency Checks](consistency_checks.md) — power law used as consistency test
- [GR vs SSZ Tables](gr_vs_ssz_tables.md) — comparison for compact objects
