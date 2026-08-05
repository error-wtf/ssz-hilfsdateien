# Quasi-Normal Mode Spectrum in SSZ

**Book reference:** Ch 32 (Rotating Black Holes), Ch 18 (phi-Lattice Analysis), Appendix B.13  
**Test file:** `test_qnm_spectrum.py`  
**Paper:** 32 (Rotating Systems), 04 (Metric)

---

## Definition

Quasi-normal modes (QNMs) are the characteristic damped oscillations of a black hole after a perturbation. They appear as ringdown in gravitational wave observations (LIGO/Virgo/KAGRA).

## SSZ QNM Frequency Shift

The fundamental QNM frequency in SSZ is modified relative to GR:

```
f_QNM_SSZ / f_QNM_GR = 1 / D_SSZ(r*)   where r* is the photon sphere / effective scattering radius
```

Numerical value at r* = 1.387 * r_s:
```
D_SSZ(r*) = 1/(1 + Xi(r*)) = 1/(1 + 0.360) = 0.72...

f_QNM_SSZ / f_QNM_GR ≈ 1/0.72 ≈ 1.39
```

**SSZ QNMs are ~39% higher frequency** than GR QNMs for the same black hole mass.

## phi-Lattice Connection

From the phi-lattice canonical table, at r* = 1.387 * r_s (between k=0 and k=1):

```
D_SSZ(r*) ≈ 0.72   (interpolated from table)
f_SSZ / f_GR = 1/D_SSZ(r*) ≈ 1.39
```

This connects the QNM spectrum directly to the phi-lattice discretization.

## GR QNM Reference Formulas

For Schwarzschild GR, the fundamental QNM frequency:
```
omega_QNM_GR = (1/(r_s * sqrt(27))) * (1 - i * something) * c
f_QNM_GR = omega_QNM_GR / (2*pi) = c / (3*sqrt(3) * pi * r_s)
          = 0.0614 * c / r_s
```

For a 10 M_sun black hole: `r_s = 29530 m`
```
f_QNM_GR = 0.0614 * 3e8 / 29530 = 624 Hz
```

**SSZ prediction:**
```
f_QNM_SSZ = 1.39 * 624 = 867 Hz
```

## QNM Table for Different Black Hole Masses

| M / M_sun | r_s [m] | f_GR [Hz] | f_SSZ [Hz] | Delta_f [Hz] |
|-----------|---------|-----------|------------|-------------|
| 10 | 29,530 | 624 | 867 | +243 |
| 30 | 88,590 | 208 | 289 | +81 |
| 100 | 295,300 | 62 | 87 | +25 |
| 1e6 | 2.953e9 | 0.0062 | 0.0087 | 0.0025 |

## Damping Time

The QNM damping time (imaginary part):
```
tau_GR = (r_s * 4) / c   [in units of r_s/c]
tau_SSZ = tau_GR / D_SSZ(r*)  ≈ 1.39 * tau_GR
```

SSZ QNMs ring for **~39% longer** before damping.

## Observable Consequences

1. **Ringdown frequency:** f_SSZ/f_GR = 1.39 (must match to <5% for current detectors)
2. **Ringdown duration:** tau_SSZ/tau_GR = 1.39 (longer ringing)
3. **Spectral peak:** shifted to higher frequencies vs GR

**Current LIGO sensitivity:** QNM tests are statistics-limited. Next-generation detectors (Einstein Telescope, Cosmic Explorer) will test QNM frequencies to 1% precision, allowing SSZ vs GR discrimination.

## Schwarzschild vs Kerr QNMs in SSZ

For a Kerr black hole with spin parameter chi = a/a_max:
```
f_QNM_SSZ(chi) = f_QNM_SSZ(0) * [1 + f_correction(chi)]
```

The spin correction is the same as in GR (since SSZ = GR at PPN level). The SSZ modification is multiplicative: all QNM frequencies are shifted by the factor 1/D_SSZ(r*).

## Falsification Conditions

SSZ QNM prediction is FALSIFIED if:
```
f_observed / f_GR_predicted < 1.1   (for BH masses where QNM is measured)
```

SSZ QNM prediction is CONFIRMED if:
```
f_observed / f_GR_predicted > 1.2   (at >3 sigma)
```

## Relation to Other Sections

- [phi-Lattice Discretization](../02_FOUNDATIONS/phi_lattice_discretization.md) — bracket theorem and table
- [Intersection Invariance](../02_FOUNDATIONS/intersection_invariance.md) — r* value
- [Black Hole Metric](black_hole_metric.md) — metric basis
- [Rotating Black Holes](rotating_black_holes.md) — Kerr QNMs
- [Future Experimental Prospects](../13_FREQUENCY_FRAMEWORK/future_experimental_prospects.md) — ET/CE tests
