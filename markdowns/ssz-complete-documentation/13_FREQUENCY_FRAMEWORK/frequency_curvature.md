# Frequency-Based Curvature Detection

**Book reference:** Ch 17 (Frequency-Based Curvature Detection)  
**Test file:** `test_frequency_curvature.py`  
**Paper:** 17 (Holonomy Invariants)

---

## Concept

Instead of measuring spacetime curvature through geodesic deviation (tidal forces), SSZ proposes measuring it through **frequency gradients** — the way clock rates change across space.

The curvature is encoded in the second derivative of the time dilation factor D(r):

```
R_curvature ~ d^2(D)/dr^2
```

This can be measured using three or more clocks at different radii and comparing their frequency ratios.

## Frequency Gradient

The first derivative of D(r) gives the **frequency gradient** (how fast clock rates change with radius):

```
dD/dr = -(1/(1+Xi)^2) * dXi/dr
```

For the weak-field formula `Xi = r_s/(2r)`:
```
dXi/dr = -r_s/(2r^2)
dD/dr = r_s/(2r^2) * 1/(1+Xi)^2 ≈ r_s/(2r^2)   [for Xi << 1]
```

**Physical meaning:** 1 km upward at Earth's surface changes clock rate by:
```
Delta_D = |dD/dr| * Delta_r = r_s/(2R^2) * 1000 m
         = 0.00887/(2*(6.371e6)^2) * 1000 = 1.09e-13
```

This is measurable with optical atomic clocks (sensitivity ~ 10^-18 fractional frequency).

## Frequency Curvature

The **second derivative** gives the frequency curvature:

```
d^2D/dr^2 = d/dr [r_s/(2r^2)] ≈ -r_s/r^3   [weak field]
```

Physical meaning: the frequency gradient itself changes with radius. This represents the spacetime curvature as seen by a clock network.

## SSZ vs GR Frequency Curvature

**GR time dilation:** `D_GR(r) = sqrt(1 - r_s/r)`
```
d^2D_GR/dr^2 = -r_s/(4r^3) * (1 - r_s/r)^{-3/2} * (1 + r_s/(2r))
             ≈ -r_s/(4r^3)   [weak field]
```

**SSZ time dilation:** `D_SSZ(r) = 1/(1 + r_s/(2r))`  
```
d^2D_SSZ/dr^2 ≈ -r_s/r^3   [weak field]
```

**Ratio:**
```
(d^2D_SSZ/dr^2) / (d^2D_GR/dr^2) ≈ 4
```

SSZ frequency curvature is **4x larger** than GR in the weak field! This is a potentially measurable difference with next-generation clock networks.

## Three-Clock Curvature Measurement

With three clocks at r_1, r_2 = r_1 + h, r_3 = r_1 + 2h (evenly spaced):

**Measure frequency ratios:**
```
f_21 = f_2/f_1 = D(r_1)/D(r_2)
f_32 = f_3/f_2 = D(r_2)/D(r_3)
```

**Compute discrete curvature:**
```
kappa_discrete = (f_21 - f_32) / (h * f_21)
               = [D(r_1)/D(r_2) - D(r_2)/D(r_3)] / (h * D(r_1)/D(r_2))
```

This is a **second-order finite difference** approximation to `d^2(ln D)/dr^2`.

**SSZ prediction for 3 clocks at Earth surface (h = 1 km):**
```
kappa_SSZ = r_s/R^3 = 0.00887 / (6.371e6)^3 = 3.4e-25 m^{-1}
```

**Required clock precision:** 10^-18 fractional frequency gives:  
`Delta_kappa = Delta_f/f / h = 10^{-18} / 1000 m = 10^{-21} m^{-1}`

This is 4 orders of magnitude more sensitive than needed — the measurement is **in principle feasible today** with optical clocks.

## Geodetic Clock Experiment Design

Proposed experiment:
1. Three optical clocks on a satellite at three radii (separated by 10 m)
2. Measure frequency ratios continuously
3. Compute curvature from finite differences
4. Compare SSZ prediction (kappa = r_s/r^3) vs GR prediction (kappa = r_s/(4r^3))

**Expected discrimination:** factor of 4 difference between SSZ and GR.

## Connection to LIGO/LISA

Gravitational wave detectors measure the **time derivative** of the holonomy:
```
h_GW(t) = d/dt [I_loop(t) - 1]
```

In SSZ language, GW detectors measure the deviation of the holonomy from its static value. The SSZ modification to GW signals:
```
h_SSZ / h_GR = D_SSZ(r_source) / D_GR(r_source)
```

For a binary merger at distance >> r_s from each component: `D_SSZ ≈ D_GR` and no detectable difference in the GW amplitude.

For a **ringdown** (post-merger): the QNM frequency shift applies (see qnm_spectrum.md).

## Key Formulas Summary

| Quantity | Formula | SSZ vs GR |
|----------|---------|----------|
| D(r) | 1/(1+Xi) | different at r ~ r_s |
| dD/dr | r_s/(2r^2*D^2) | 4x larger than GR (weak) |
| d^2D/dr^2 | -r_s/r^3 * D^3 | 4x larger than GR (weak) |
| Holonomy I_ABC | = 1 (static) | same as GR |
| kappa(r) | r_s/r^3 | 4x larger |

## Relation to Other Sections

- [Holonomy Invariants](holonomy_invariants.md) — topological context
- [Time Dilation D](../02_FOUNDATIONS/time_dilation.md) — D(r) derivation
- [Scaling Factor s(r)](../02_FOUNDATIONS/scaling_factor.md) — s = 1/D
- [Curvature Detection](../07_VALIDATION/curvature_detection.md) — observational implementation
- [Future Experimental Prospects](future_experimental_prospects.md) — clock network experiments
