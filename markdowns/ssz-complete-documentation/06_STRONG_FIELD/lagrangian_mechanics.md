# Lagrangian Mechanics in SSZ

**Book reference:** Ch 31 (Effective Lagrangian for Orbits)  
**Test file:** `test_lagrangian_orbits.py`  
**Paper:** 31 (Lagrangian)

---

## Effective Lagrangian

The motion of a test particle in the SSZ metric follows from the effective Lagrangian:

```
2*L = -D(r)^2 * c^2 * (dt/dlambda)^2 + [1/D(r)^2] * (dr/dlambda)^2
    + r^2 * (dtheta/dlambda)^2 + r^2*sin^2(theta) * (dphi/dlambda)^2
```

where lambda is an affine parameter (proper time tau for massive particles, or affine for photons).

## Euler-Lagrange Equations

**t-equation (energy conservation):**
```
d/dlambda [D^2 * dt/dlambda] = 0
=> E = D^2 * c^2 * dt/dlambda = const
```

**phi-equation (angular momentum conservation):**
```
d/dlambda [r^2 * dphi/dlambda] = 0
=> L = r^2 * dphi/dlambda = const
```

**theta-equation:**
```
d/dlambda [r^2 * dtheta/dlambda] = r^2 * sin(theta)*cos(theta) * (dphi/dlambda)^2
```

For equatorial orbits (theta = pi/2): automatically satisfied.

**r-equation (radial motion):**
```
d/dlambda [D^{-2} * dr/dlambda] = 
  -D * D' * c^2 * (dt/dlambda)^2 - D' * D^{-3} * (dr/dlambda)^2 + r * (dphi/dlambda)^2
```

where `D' = dD/dr`.

## First Integral (Energy Equation)

For equatorial orbits, substituting the conserved quantities:

```
(dr/dlambda)^2 = E^2/c^2 - D^2 * [epsilon + L^2/(c^2*r^2)]
```

where `epsilon = 1` (massive particle) or `epsilon = 0` (photon).

This is the **fundamental orbit equation** from which all orbital dynamics follow.

## Effective Potential from Lagrangian

```
V_eff(r) = D(r)^2 * [epsilon + L^2/(c^2*r^2)]
```

Properties:
- V_eff(r_s) = D(r_s)^2 * [epsilon + L^2/(c^2*r_s^2)] = **FINITE** (SSZ!)
- V_eff(inf) = epsilon (flat spacetime limit)
- Local minimum -> stable circular orbit
- Local maximum -> unstable circular orbit (photon sphere)

## Circular Orbit Conditions

**Condition 1:** dV_eff/dr = 0
```
2*D*D' * [epsilon + L^2/(c^2*r^2)] + D^2 * (-2*L^2/(c^2*r^3)) = 0
=> 2*D'/D = 2*L^2/(c^2*r^3) / [epsilon + L^2/(c^2*r^2)]
```

**Condition 2 for ISCO:** d^2V_eff/dr^2 = 0

This is a transcendental equation solved numerically, giving `r_ISCO_SSZ ≈ 2.95 * r_s`.

## Segment-Based Lagrangian Interpretation

The SSZ Lagrangian has a natural interpretation in terms of segments: 

The kinetic energy term `[1/D^2] * (dr/dlambda)^2` represents work done against the increasing segment density as a particle moves into the gravitational field. The factor `1/D^2 = (1+Xi)^2` grows from 1 at infinity to `(1.802)^2 = 3.25` at r = r_s.

Physically: radial motion requires progressively more energy per unit coordinate distance as the segment density increases.

## Comparison of Kinetic Terms

| r/r_s | D^2_SSZ | 1/D^2_SSZ | D^2_GR | 1/D^2_GR |
|-------|---------|-----------|--------|----------|
| 10 | 0.901 | 1.110 | 0.900 | 1.111 |
| 3 | 0.744 | 1.344 | 0.667 | 1.500 |
| 1.5 | 0.668 | 1.497 | 0.333 | 3.000 |
| 1.0 | 0.308 | 3.247 | 0 | diverges |

**Key insight:** At r = r_s, SSZ kinetic term is `3.247`, not infinity. The particle still has finite coordinate velocity at the horizon.

## Relation to Other Sections

- [Geodesics](../04_KINEMATICS/geodesics.md) — geodesic equations derived from this Lagrangian
- [Orbital Mechanics](../04_KINEMATICS/orbital_mechanics.md) — ISCO from the effective potential
- [ISCO Comparison](isco_comparison.md) — SSZ vs GR ISCO numerical comparison
- [Black Hole Metric](black_hole_metric.md) — the metric used in the Lagrangian
