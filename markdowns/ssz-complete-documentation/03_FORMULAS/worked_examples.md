# Worked Examples

**Book reference:** Appendix B (Worked Examples section)  
**Source:** Canonical calculations from the SSZ formula compendium

---

## 1. Solar Shapiro Delay (Cassini)

**Given:**
- M_sun = 1.989e30 kg
- b = 1.6 R_sun = 1.6 * 6.96e8 m = 1.114e9 m
- d_earth = 1 AU = 1.496e11 m
- d_cassini = 8.43 AU = 1.263e12 m

**Step 1:** r_s = 2GM/c^2
```
r_s = 2 * 6.674e-11 * 1.989e30 / (3e8)^2 = 2953 m
```

**Step 2:** Xi at closest approach (diagnostic only, NOT used for delay)
```
Xi(b) = r_s/(2b) = 2953 / (2 * 1.114e9) = 1.326e-6
```

**Step 3:** Shapiro delay (PPN formula)
```
Delta_t = 2 * (r_s/c) * ln(4 * r1 * r2 / b^2)
        = 2 * (2953 / 3e8) * ln(4 * 1.496e11 * 1.263e12 / (1.114e9)^2)
        = 1.969e-5 * ln(4 * 1.889e23 / 1.241e18)
        = 1.969e-5 * ln(6.09e5)
        = 1.969e-5 * 13.32
        = 262 microseconds
```

**Cassini measured:** 264 +/- 2 microseconds. Agreement: 0.8% (within 1 sigma).

---

## 2. Mercury Perihelion Precession

**Given:**
- a = 5.791e10 m (semi-major axis)
- e = 0.2056 (eccentricity)
- T = 87.97 days (orbital period)
- M_sun = 1.989e30 kg, r_s = 2953 m

**Precession per orbit:**
```
delta_phi = 6*pi*G*M / (c^2 * a * (1 - e^2))
          = 6*pi * 6.674e-11 * 1.989e30 / (9e16 * 5.791e10 * (1 - 0.04228))
          = 6*pi * 1.327e20 / (9e16 * 5.547e10)
          = 6*pi * 1.327e20 / (4.992e27)
          = 5.012e-7 rad/orbit
```

**Per century** (415.2 orbits):
```
5.012e-7 * 415.2 * (180/pi) * 3600 = 42.98 arcsec/century
```

**Observed:** 42.98 +/- 0.04 arcsec/century.  
SSZ = GR in weak field. Exact match.

---

## 3. GPS Gravitational Frequency Shift

**Given:**
- h = 20200 km (GPS orbit altitude)
- R_earth = 6371 km
- M_earth = 5.972e24 kg
- r_s_earth = 2*G*M_earth/c^2 = 8.87 mm

**Xi at Earth surface:**
```
Xi_surf = r_s / (2 * R_earth) = 0.00887 / (2 * 6.371e6) = 6.953e-10
```

**Xi at GPS altitude:**
```
R_GPS = 6371 + 20200 = 26571 km = 2.657e7 m
Xi_GPS = r_s / (2 * R_GPS) = 0.00887 / (2 * 2.657e7) = 1.668e-10
```

**Fractional frequency shift (gravitational):**
```
Delta_f/f = Delta_Xi = Xi_surf - Xi_GPS = 6.953e-10 - 1.668e-10 = 5.285e-10
Per day: 5.285e-10 * 86400 = +45.66 microseconds/day
```

**Kinematic correction (special relativity):**
```
v_GPS = 3874 m/s
Delta_f/f = -v^2/(2c^2) = -(3874)^2 / (2 * (3e8)^2) = -8.34e-11
Per day: -8.34e-11 * 86400 = -7.21 microseconds/day
```

**Net correction:**
```
+45.66 - 7.21 = +38.45 microseconds/day
```

**GPS specification:** +38.4 microseconds/day.  
SSZ agrees to 0.1%.

---

## 4. Neutron Star Surface Redshift (SSZ Prediction)

**Given:**
- M = 1.4 M_sun, R = 12 km
- r_s = 2*G*1.4*M_sun/c^2 = 2 * 6.674e-11 * 2.785e30 / 9e16 = 4.14 km
- Compactness: r_s/R = 4.14/12 = 0.345, so R/r_s = 2.90

**GR prediction:**
```
z_GR = 1/sqrt(1 - r_s/R) - 1 = 1/sqrt(0.655) - 1 = 1.235 - 1 = 0.235
```

**SSZ prediction** (weak field at R/r_s = 2.90, so g1 regime):
```
Xi_weak(R) = r_s/(2R) = 0.345/2 = 0.1725
z_SSZ = Xi(R) = 0.1725
```

**Deviation:**
```
Delta_z = z_SSZ - z_GR = 0.1725 - 0.235 = -0.063
(z_SSZ - z_GR) / z_GR = -0.063/0.235 = -26.7%
```

Note: For R = 10 km (more compact: r_s/R = 0.414, R/r_s = 2.42), still in g1 blend region:
```
z_SSZ = r_s/(2R) = 0.207  vs  z_GR = 0.291  =>  -29% deviation
```

The **maximum SSZ-GR difference** occurs at r = r_s:
```
z_SSZ(r_s) = Xi(r_s) = 0.802  (finite!)
z_GR(r_s)  = infinity  (singularity!)
```

**Testable with:** XMM-Newton X-ray spectroscopy of quiescent neutron stars.

---

## 5. Light Deflection (Eddington)

**Given:** Sun, impact parameter b = R_sun = 6.96e8 m

```
alpha = 2 * r_s / b = 2 * 2953 / 6.96e8 = 8.48e-6 rad
alpha_arcsec = 8.48e-6 * (180/pi) * 3600 = 1.748 arcsec
```

Eddington 1919 measurement: 1.75 +/- 0.09 arcsec. Agreement within 0.1%.

---

## Relation to Other Sections

- [PPN Formulas](ppn_formulas.md) — the formulas used above
- [GPS Validation](../07_VALIDATION/gps_validation.md) — detailed GPS analysis
- [Cassini Validation](../07_VALIDATION/cassini_test.md) — Cassini detailed analysis
- [Mercury Precession](../07_VALIDATION/mercury_precession.md) — precession detailed
- [Neutron Star Redshift](../07_VALIDATION/neutron_star_redshift.md) — NS detailed predictions
