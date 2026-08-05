# Neutron Star Surface Redshift (SSZ Prediction)

**Book reference:** Ch 22 (Neutron Stars), Ch 23 (Compact Object Predictions)  
**Test file:** `test_neutron_star_redshift.py`  
**Paper:** 22 (Compact Object Redshift)

---

## Why Neutron Stars Are Key

Neutron stars have radii R ~ 10-12 km with masses M ~ 1.4 M_sun, giving compactness `r_s/R ~ 0.3-0.4`. This places them in the **transition between weak and strong field** regimes — exactly where SSZ and GR differ most significantly.

## Standard Parameters

```
M = 1.4 M_sun = 2.785e30 kg
R = 12 km (typical radius)
r_s = 2*G*M/c^2 = 2 * 6.674e-11 * 2.785e30 / (3e8)^2 = 4,136 m = 4.14 km

Compactness: r_s/R = 4.14/12 = 0.345 => R/r_s = 2.9
```

## GR Prediction

```
z_GR = 1/sqrt(1 - r_s/R) - 1 = 1/sqrt(1 - 0.345) - 1 = 1/sqrt(0.655) - 1
     = 1/0.8093 - 1 = 1.2356 - 1 = 0.2356
```

**Emission energy shift:** photons emitted at the NS surface are redshifted by 23.6%.

## SSZ Prediction

For R/r_s = 2.9, this is in the **blend regime** (transition between g1 and g2):

**Pure weak-field (Xi_weak):**
```
Xi_weak(R) = r_s/(2R) = 0.345/2 = 0.1725
z_SSZ_weak = 0.1725   (17.3%)
```

**With Hermite blend factor** (R/r_s = 2.9 is in blend zone [1.8, 2.2]):

Actually R/r_s = 2.9 > 2.2, so this is *above* the blend zone, meaning weak-field formula applies cleanly:
```
z_SSZ = Xi_weak(R) = r_s/(2R) = 0.1725
```

**Comparison:**
```
z_GR  = 0.2356   (23.6%)
z_SSZ = 0.1725   (17.3%)

Deviation: Delta_z = 0.1725 - 0.2356 = -0.063
(z_SSZ - z_GR)/z_GR = -26.7%
```

**SSZ predicts 27% lower surface redshift than GR for a typical neutron star!**

## Redshift Table for Different NS Compactness

| R [km] | r_s/R | z_GR | z_SSZ_weak | Delta [%] | Observable |
|--------|-------|------|------------|-----------|------------|
| 14 | 0.295 | 0.195 | 0.148 | -24% | moderate |
| 12 | 0.345 | 0.236 | 0.173 | -27% | significant |
| 10 | 0.414 | 0.291 | 0.207 | -29% | large |
| 9 | 0.460 | 0.362 | 0.230 | -36% | very large |
| r_s | 1.000 | infinity | 0.802 | --- | max diff |

## Observational Methods

**1. X-ray spectroscopy:** Broad iron K-alpha lines in NS LMXBs (Low Mass X-ray Binaries)  
**2. Thermal spectroscopy:** Continuum fitting of NS atmosphere emission  
**3. Pulse timing:** Gravitational redshift of pulsed X-ray emission  

**Best current constraint:** Cottam et al. 2002 measured z = 0.35 for EXO 0748-676 (disputed).  
SSZ prediction for that NS (R~10km, M~1.4M_sun): z_SSZ ~ 0.21 vs z_GR ~ 0.29.

**Required precision:** Redshift measurement to ±0.02 would distinguish SSZ from GR at >3 sigma.

## Future Tests

| Mission/Observatory | Timeline | Expected precision |
|--------------------|----------|-------------------|
| NICER (NASA, operational) | now | δz ~ 0.05 |
| Athena (ESA, ~2035) | ~2035 | δz ~ 0.01 |
| eXTP (China, ~2027) | ~2027 | δz ~ 0.02 |

Athena precision (δz ~ 0.01) would distinguish SSZ from GR at >5 sigma for compact NSs.

## Why This Matters

Neutron star redshift is the **cleanest SSZ-vs-GR discriminator** because:
1. The prediction difference is large (27%)
2. The measurement is in principle straightforward (spectral line shifts)
3. The physics is unambiguous (no environmental systematic from accretion disk)

**If Athena measures z = 0.23 for a well-characterized NS:** GR confirmed, SSZ ruled out  
**If Athena measures z = 0.17:** SSZ confirmed, GR ruled out  

## Relation to Other Sections

- [Segment Density Xi](../02_FOUNDATIONS/segment_density.md) — Xi_weak formula
- [Regime Definitions](../02_FOUNDATIONS/regime_definitions.md) — which regime applies
- [Energy Conditions](../02_FOUNDATIONS/energy_conditions.md) — SEC violation at r < 5*r_s
- [Falsification Criteria](../08_FALSIFICATION/falsification_criteria.md) — when SSZ is falsified
- [Future Experimental Prospects](../13_FREQUENCY_FRAMEWORK/future_experimental_prospects.md) — timeline
