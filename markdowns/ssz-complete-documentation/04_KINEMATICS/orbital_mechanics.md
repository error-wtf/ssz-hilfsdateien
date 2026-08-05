# Orbital Mechanics in SSZ

**Book reference:** Ch 31 (Lagrangian Mechanics and ISCO), Ch 32 (Rotating Systems)  
**Test file:** `test_isco_comparison.py`, `test_orbital_stability.py`  
**Paper:** 04 (Metric), 31 (Lagrangian)

---

## Circular Orbit Condition

For circular orbits (dr/dtau = 0), the effective potential must satisfy:

```
V_eff(r) = E^2/c^2
dV_eff/dr = 0
```

From the SSZ metric, the circular orbit velocity:
```
v_circ^2(r) = (r/2) * d(D^2)/dr / [1 - (r/2) * d(D^2)/dr / D^2]
```

In the weak field (`D^2 ≈ 1 - r_s/r`):
```
v_circ ≈ sqrt(G*M/r) = (1/2) * c * sqrt(r_s/r)
```

This reproduces Newtonian circular velocity (SSZ = GR in weak field).

## Photon Sphere

The photon sphere is where light can orbit in circles:

```
GR:  r_photon = 3/2 * r_s = 1.5 * r_s
SSZ: r_photon ≈ 1.55 * r_s  (slight shift due to D vs sqrt formula)
```

At the photon sphere, captured photons orbit indefinitely (unstable). The photon sphere radius sets the scale for the **black hole shadow**:
```
b_shadow = r_photon / D(r_photon) * [shadow impact parameter factor]
```

**SSZ prediction:** black hole shadow diameter is ~1.3% smaller than GR prediction.

## ISCO (Innermost Stable Circular Orbit)

The ISCO is the smallest stable circular orbit for massive particles:

```
GR (Schwarzschild):  r_ISCO = 3 * r_s  (analytical result)
SSZ (weak field):    r_ISCO ≈ 3 * r_s  (SSZ = GR for r_s/R << 1)
SSZ (strong field):  r_ISCO < 3 * r_s  (slightly smaller, measurable deviation)
```

The ISCO difference is small (~few %) for typical stellar-mass black holes but may be measurable for extreme mass ratio inspirals (EMRI) with LISA.

## Orbital Energy and Angular Momentum at ISCO

**GR (Schwarzschild):**
```
E_ISCO/m c^2 = sqrt(8/9) ≈ 0.9428   [specific orbital energy]
L_ISCO/m c  = 2*sqrt(3)*r_s/2      [specific angular momentum]
Efficiency:   eta_GR = 1 - E_ISCO/mc^2 = 5.72%
```

**SSZ correction:**
```
eta_SSZ ≈ eta_GR * (1 + 0.5 * Xi(r_ISCO))
```

For stellar black holes (r_ISCO >> r_s), the correction is negligible (<< 1%).

## Effective Potential Comparison

```
V_eff_GR(r)  = (1 - r_s/r) * (1 + L^2/r^2)
V_eff_SSZ(r) = D(r)^2 * (1 + L^2/(r^2 * c^2)) * c^2
```

Key difference: at r = r_s, V_eff_GR = 0 (horizon) but V_eff_SSZ > 0 (finite barrier).

This means infalling particles experience a **finite potential barrier** in SSZ, not an infinite one. Particles can in principle be reflected (hypothetically), though the probability is negligible for macroscopic objects.

## Perihelion Precession

For bound orbits, the precession per orbit:

```
Delta_phi = 6*pi*G*M / (a*(1-e^2)*c^2)   [both SSZ and GR, weak field]
```

SSZ matches GR exactly in the weak-field regime. Deviation appears only for very compact objects with `r_s/a > 0.01`.

## Angular Momentum Barrier

The centrifugal barrier in SSZ:
```
V_centrifugal(r) = D(r)^2 * L^2 / r^2
```

At r = r_s: `V_centrifugal = 0.555^2 * L^2 / r_s^2` (finite, not zero).

In GR: `V_centrifugal(r_s) = 0` (barrier disappears at horizon). This is another manifestation of the SSZ regularization.

## Relation to Other Sections

- [Geodesics](geodesics.md) — effective potential derivation
- [ISCO Comparison](../06_STRONG_FIELD/isco_comparison.md) — detailed SSZ vs GR ISCO
- [Penrose Process](../06_STRONG_FIELD/penrose_process.md) — energy extraction above ISCO
- [Black Hole Metric](../06_STRONG_FIELD/black_hole_metric.md) — full metric details
- [Rotating Black Holes](../06_STRONG_FIELD/rotating_black_holes.md) — Kerr-SSZ
