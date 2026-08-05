# Mercury Perihelion Precession Validation

**Book reference:** Ch 20 (PPN Tests), Ch 21 (Solar System Tests)  
**Test file:** `test_precession.py`  
**Paper:** 04 (Metric), 20 (Observational Tests)

---

## Observed Value

**Total measured precession of Mercury:** 5600.73 arcsec/century  
**Contributions:**
- Planetary perturbations (Jupiter, Venus, etc.): 5557.62 arcsec/century
- Earth's equatorial bulge (J2): 0.0254 arcsec/century
- **Relativistic (GR/SSZ):** 42.98 arcsec/century
- **Observed relativistic:** 43.11 ± 0.45 arcsec/century

## GR/SSZ Formula

In the weak field, both GR and SSZ give the same precession formula:

```
Delta_phi = 6*pi*G*M / (a * (1-e^2) * c^2)   [per orbit]
```

where:
- M = M_sun = 1.989e30 kg
- a = 5.791e10 m (semi-major axis)
- e = 0.2056 (eccentricity)
- G = 6.674e-11, c = 3e8

**Calculation:**
```
Delta_phi = 6*pi * 6.674e-11 * 1.989e30 / (5.791e10 * (1-0.04228) * (3e8)^2)
          = 6*pi * 1.327e20 / (5.550e10 * 9e16)
          = 6*pi * 1.327e20 / 4.995e27
          = 6*pi * 2.656e-8
          = 5.012e-7 rad/orbit
```

**Mercury orbital period:** T = 87.97 days = 0.2408 years  
**Orbits per century:** 100/0.2408 = 415.2

**Precession per century:**
```
5.012e-7 rad/orbit * 415.2 orbits * (3600 * 180/pi) arcsec/rad
= 5.012e-7 * 415.2 * 206265
= 42.98 arcsec/century
```

**Observed:** 43.11 ± 0.45 arcsec/century. Agreement within 0.3 sigma.

## Why SSZ = GR for Mercury

Mercury's orbit has r_s/a = 2953/5.791e10 = 5.1e-8 (extremely weak field). At this level:

```
Xi_SSZ(a) = r_s/(2a) = 2.55e-8
Xi_SSZ ≈ Xi_GR_equivalent
```

The precession formula `Delta_phi ~ Xi` is to first order in r_s/a, and both SSZ and GR give the same first-order result. SSZ deviates from GR only at order (r_s/a)^2 and higher, which is completely negligible for Mercury.

## SSZ Strong-Field Correction

For objects with smaller semi-major axis (r_s/a not negligible), SSZ gives a correction:

```
Delta_phi_SSZ = Delta_phi_GR * [1 + f(Xi(a))]
```

For Mercury: correction < 1e-7 (unmeasurable).  
For a hypothetical compact binary (a = 5*r_s): correction ~ 5%.

## PPN Connection

The general PPN precession formula:
```
Delta_phi = ((2+2*gamma-beta)/3) * 6*pi*G*M / (a*(1-e^2)*c^2)
```

For SSZ (gamma=1, beta=1): `(2+2-1)/3 = 1`, giving the standard formula.  

Any theory with `2*gamma - beta != 1` would give a different rate. Mercury precession constrains `2*gamma - beta = 1.00 ± 0.003`.

## Historical Significance

The 43 arcsec/century "anomalous" precession was unexplained by Newtonian mechanics for over 50 years before Einstein. SSZ reproduces this result because:

1. The weak-field Xi formula matches GR to first PPN order
2. The precession is entirely a first-PPN-order effect
3. No higher-order SSZ effects are detectable at this precision

## MESSENGER and BepiColombo

NASA's MESSENGER spacecraft (2004-2015) measured Mercury's perihelion with spacecraft tracking, improving the precession measurement to 1% precision. BepiColombo (2025 arrival at Mercury) will improve to 0.1%.

SSZ prediction for BepiColombo:
```
Delta_phi_SSZ = 42.98 arcsec/century   (identical to GR to this precision)
```

## Relation to Other Sections

- [PPN Formulas](../03_FORMULAS/ppn_formulas.md) — complete PPN context
- [Worked Examples](../03_FORMULAS/worked_examples.md) — full numerical calculation
- [Geodesics](../04_KINEMATICS/geodesics.md) — radial equation of motion
- [GR vs SSZ Tables](gr_vs_ssz_tables.md) — comparison summary
