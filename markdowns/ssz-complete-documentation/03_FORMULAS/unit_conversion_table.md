# Unit Conversion Table

**Book reference:** Appendix B (Unit Conversion section)  
**Note:** Xi and D are dimensionless in ALL unit systems.

---

## Key Point

The fundamental SSZ variables Xi(r) and D(r) are **pure dimensionless numbers** — they are identical in SI, CGS, and natural units. This is a structural feature of SSZ: the physically meaningful quantities are ratios, not dimensional quantities.

```
Xi = (dimensionless ratio of radii)
D  = (dimensionless time dilation factor)
s  = (dimensionless scaling factor)
```

## Schwarzschild Radii

| Object | SI [m] | CGS [cm] | r_s/R_object |
|--------|--------|----------|--------------|
| Sun | 2953 | 2.953e5 | 4.25e-6 |
| Earth | 8.87e-3 | 0.887 | 1.39e-9 |
| Neutron star (1.4 M_sun, R=12km) | 4140 | 4.14e5 | 0.345 |
| Stellar BH (10 M_sun) | 29530 | 2.953e6 | ~1 |
| Sgr A* (4e6 M_sun) | 1.18e10 | 1.18e12 | ~1 |

## Xi Values (Dimensionless)

| Location | Xi | D = 1/(1+Xi) | Notes |
|----------|----|--------------|-------|
| Earth surface | 6.97e-10 | 0.999999999303 | GPS base |
| GPS orbit (20200 km) | 1.67e-10 | 0.999999999833 | GPS satellite |
| Sun surface | 2.12e-6 | 0.999997880 | solar redshift |
| NS surface (r_s/R=0.35) | 0.172 | 0.853 | strong field |
| r = r_s (horizon) | 0.80171 | 0.55503 | natural boundary |
| r = r_s/2 (inside) | 0.99 | 0.502 | hypothetical |

## Physical Constants

| Constant | SI | CGS | Natural (G=c=1) |
|----------|----|----|------------------|
| G | 6.674e-11 m^3 kg^-1 s^-2 | 6.674e-8 cm^3 g^-1 s^-2 | 1 |
| c | 2.998e8 m/s | 2.998e10 cm/s | 1 |
| hbar | 1.055e-34 J*s | 1.055e-27 erg*s | 1 |
| phi | 1.618034 | same | same |
| alpha | 1/137.036 | same | same |

## r_s Formula in Different Units

```
SI:   r_s = 2*G*M/c^2  [meters, with G in SI]
CGS:  r_s = 2*G*M/c^2  [cm, with G in CGS]
Natural (G=c=1): r_s = 2*M  [mass units]
```

## Time Dilation Conversion

Given Xi (dimensionless), time dilation in practical units:

```
Frequency shift:  Delta_f/f = Delta_Xi = Xi(r_emit) - Xi(r_obs)
Time difference per day: Delta_Xi * 86400 seconds
Time difference per year: Delta_Xi * 3.156e7 seconds
```

## Angular Units for Lensing

```
Deflection angle alpha [radians] = 2*r_s/b
alpha [arcsec] = alpha [rad] * (180/pi) * 3600 = alpha [rad] * 206265
alpha [microarcsec] = alpha [arcsec] * 1e6
```

**Sun lensing at edge:** alpha = 1.748 arcsec = 1748 milliarcsec

## Frequency Shift for NS

```
z = Delta_lambda/lambda = Xi   [dimensionless]
Delta_E = z * E_photon   [energy shift in same units as E_photon]
Delta_f = z * f_photon   [frequency shift in Hz]
```

## Relation to Other Sections

- [Structural Constants](../02_FOUNDATIONS/structural_constants.md) — phi, alpha_SSZ values
- [Special Values](special_values.md) — key dimensionless values
- [Quick Reference](quick_reference.md) — top-10 formulas
