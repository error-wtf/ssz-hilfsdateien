# Geodesics in SSZ

**Book reference:** Ch 6 (Geodesics), Ch 7 (Radial Motion)  
**Test file:** `test_geodesic_radial.py`  
**Paper:** 04 (Metric), 06 (Geodesics)

---

## SSZ Metric (Spherically Symmetric, Static)

The SSZ line element in Schwarzschild-like coordinates:

```
ds^2 = -D(r)^2 * c^2 dt^2 + [1/D(r)^2] * dr^2 + r^2 * dOmega^2
```

where `D(r) = 1/(1+Xi(r))` and `dOmega^2 = dtheta^2 + sin^2(theta) dphi^2`.

**Compare GR (Schwarzschild):**
```
ds^2 = -(1 - r_s/r) c^2 dt^2 + [1/(1-r_s/r)] dr^2 + r^2 dOmega^2
```

SSZ replaces `(1 - r_s/r)` with `D(r)^2 = 1/(1+Xi)^2`, which remains **finite and positive** at r = r_s.

## Geodesic Equations

For a massive test particle (timelike geodesic, ds^2 < 0):

**Energy conservation:**
```
E = D(r)^2 * c^2 * dt/dtau   (conserved along geodesic)
```

**Angular momentum conservation:**
```
L = r^2 * dphi/dtau   (conserved)
```

**Radial equation:**
```
(dr/dtau)^2 = E^2/c^2 - D(r)^2 * [c^2 + L^2/r^2]
```

## Effective Potential

The radial motion is governed by an effective potential:

```
V_eff(r) = D(r)^2 * [c^2 + L^2/r^2]
```

- **Circular orbits:** dV_eff/dr = 0
- **ISCO:** d^2V_eff/dr^2 = 0 (innermost stable circular orbit)
- **Photon sphere:** V_eff(r) = E^2/c^2 for radial null geodesic

## Radial Free-Fall (L=0)

For a particle falling radially from rest at infinity:
```
(dr/dtau)^2 = c^2 * [1 - D(r)^2]
```

Fall velocity:
```
v_fall(r) = c * sqrt(1 - D(r)^2)
```

At r = r_s (SSZ): `D(r_s) = 0.555`, so:
```
v_fall(r_s) = c * sqrt(1 - 0.555^2) = c * sqrt(0.692) = 0.832 c
```

The infalling particle reaches the horizon at **finite velocity** (not c), and the coordinate time to reach the horizon is also **finite** (no freezing).

**Compare GR:** v_fall(r_s) = c (particle reaches c at horizon), coordinate time diverges.

## Null Geodesics (Light)

For photons (ds^2 = 0, radial motion):
```
c * dt = +/- dr / D(r)^2
```

Integrated light-travel time:
```
Delta_t = integral[ dr / (D(r)^2 * c) ]
        = integral[ (1+Xi)^2 / c * dr ]
        ≈ (r2-r1)/c + 2/c * integral[ Xi(r) dr ]   [to first order in Xi]
```

The correction term `2 * integral[Xi/c * dr]` is the **additive Shapiro delay**.

## Geodesic Deviation (Tidal Forces)

The geodesic deviation equation measures tidal forces. In SSZ, at r = r_s:
```
d^2 xi^r / dtau^2 = -R^r_trt * u^t * xi^r * u^t  [finite!]
```

All Riemann components are **finite** at r = r_s in SSZ (no tidal divergence), in contrast to GR where they diverge.

## Comparison with GR at Key Radii

| r/r_s | v_fall SSZ | v_fall GR | tau to r_s |
|-------|------------|-----------|------------|
| 10 | 0.308 c | 0.316 c | similar |
| 3 | 0.730 c | 0.745 c | similar |
| 1.5 | 0.817 c | 0.816 c | similar |
| 1.0 | 0.832 c | c (limit) | finite vs divergent |

## Relation to Other Sections

- [Orbital Mechanics](orbital_mechanics.md) — circular orbits, ISCO
- [Time Dilation D](../02_FOUNDATIONS/time_dilation.md) — D(r) used in metric
- [Black Hole Metric](../06_STRONG_FIELD/black_hole_metric.md) — full metric tensor
- [Infalling Matter](../06_STRONG_FIELD/infalling_matter.md) — extended treatment
