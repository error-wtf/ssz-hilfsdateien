# Rotating Black Holes in SSZ (Kerr-SSZ)

**Book reference:** Ch 32 (Rotating Black Holes and Frame Dragging)  
**Test file:** `test_rotating_bh.py`, `test_penrose_efficiency.py`  
**Paper:** 32 (Rotating Systems)

---

## Kerr-SSZ Metric

For a rotating black hole with mass M and spin parameter a = J/(Mc):

```
ds^2 = -D(r,theta)^2 * dt^2 + Sigma/Delta_SSZ * dr^2 + Sigma*dtheta^2
     + (r^2 + a^2 + a^2*D^2*sin^2(theta))*sin^2(theta)*dphi^2
     - 2*a*D^2*sin^2(theta)*dt*dphi
```

where:
```
Sigma  = r^2 + a^2 * cos^2(theta)
Delta_SSZ = r^2 - r*r_s + a^2 + [SSZ correction]
D(r)  = 1/(1 + Xi(r))   [SSZ time dilation, replaces sqrt(1-r_s/r)]
```

## Ergosphere

The ergosphere is the region where static observers cannot exist (must co-rotate with the black hole):

```
GR:  r_ergo = r_s/2 + sqrt((r_s/2)^2 - a^2*cos^2(theta))
SSZ: r_ergo_SSZ is slightly different due to modified metric
```

At the equator (theta = pi/2):
```
GR:  r_ergo(equator) = r_s = 2GM/c^2
SSZ: r_ergo_SSZ(equator) ~ r_s * (1 + 0.15 * Xi(r_s)) = r_s * 1.12  [approximate]
```

The SSZ ergosphere is **larger** than in GR due to the finite D(r_s) = 0.555 (the modified metric does not reach zero at r_s).

## Frame Dragging Rate

The angular velocity of frame dragging (Lense-Thirring effect):

```
Omega_LT(r) = G*J / (c^2 * r^3)   [weak field, SSZ = GR]
```

In the strong field, the SSZ correction:
```
Omega_LT_SSZ(r) = Omega_LT_GR(r) * [D_SSZ(r)/D_GR(r)]^2
```

At r = 2 r_s: `D_SSZ/D_GR = 0.77/0.71 = 1.085`, so `Omega_LT_SSZ = 1.17 * Omega_LT_GR` (+17%).

## Gravitomagnetic Effects

The gravitomagnetic field B_grav in SSZ:
```
B_grav_SSZ = B_grav_GR * s(r)   where s(r) = 1+Xi(r)
```

Precession of gyroscopes (geodetic precession):
```
Omega_geodetic = (3/2) * (v/c)^2 * (G*M/r^3*c^2) * r_hat x v
```

SSZ matches GR for geodetic precession in the weak field (Gravity Probe B confirmed).

## Spin-Orbit Coupling

For a test mass with spin s orbiting a Kerr-SSZ black hole:
```
Omega_spin-orbit = (G*M/r^3) * (1 + 3*a^2/r^2 * cos(theta)^2)
```

This is identical to Kerr in the weak field. SSZ strong-field corrections scale as `D^2(r)` ratio.

## Innermost Stable Circular Orbit (Kerr)

For maximally rotating black hole (a = r_s/2):
```
GR:  r_ISCO(prograde)   = 0.5 * r_s   [at maximum spin]
GR:  r_ISCO(retrograde) = 4.5 * r_s
```

SSZ shifts these slightly due to the modified metric. The prograde ISCO is larger in SSZ (no singularity = no extreme compression of ISCO).

## SSZ-Specific Prediction

The **shadow of a rotating black hole** in SSZ:
```
r_shadow_SSZ / r_shadow_GR = D_SSZ(r_photon) / D_GR(r_photon)
```

For maximally spinning case: shadow ~2-4% smaller than Kerr GR prediction.

**EHT observable:** if Sgr A* or M87 shadow can be measured to <2% precision, SSZ rotating prediction becomes testable.

## Relation to Other Sections

- [Black Hole Metric](black_hole_metric.md) — Schwarzschild-SSZ baseline
- [Frame Dragging](../04_KINEMATICS/frame_dragging.md) — weak-field limit
- [Penrose Process](penrose_process.md) — energy extraction from ergosphere
- [ISCO Comparison](isco_comparison.md) — ISCO in SSZ vs GR
- [Future Experimental Prospects](../13_FREQUENCY_FRAMEWORK/future_experimental_prospects.md) — EHT tests
