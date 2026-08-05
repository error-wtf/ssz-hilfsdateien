# Energy in Segmented Spacetime (EM Fields)

**Book reference:** Ch 12 (Segment-Based Group Velocity), Energy section  
**Test file:** `test_em_energy.py`  
**Paper:** 01 (Radial Scaling), 22 (Maxwell Waves)

---

## Standard EM Energy Density

In flat spacetime, the electromagnetic energy density is:

```
u_EM = (epsilon_0/2) * E^2 + (1/2*mu_0) * B^2
```

## SSZ Modification

In the segment lattice, the EM fields are scaled by s(r) = 1 + Xi(r). The effective energy density becomes:

```
u_EM_SSZ(r) = (epsilon_0/2) * [s(r) * E(r)]^2 + (1/(2*mu_0)) * [s(r) * B(r)]^2
           = s(r)^2 * u_EM_flat
           = (1+Xi(r))^2 * u_EM_flat
```

This scaling ensures **energy conservation** in the segment lattice: as photons climb out of a gravitational well, the field amplitude decreases by 1/s(r) but the energy density accounts for the gravitational work done.

## Total Field Energy

For an EM field configuration in a gravitational field:

```
U_total = integral[ s(r)^2 * u_EM_flat(r) * dV ]
```

where `dV = r^2 sin(theta) dr dtheta dphi` (coordinate volume element).

## Poynting Vector Modification

The energy flux (Poynting vector) in SSZ:

```
S_SSZ = s(r)^2 * (E x B) / mu_0
```

This gives the correct energy conservation equation:
```
dU/dt + nabla . S_SSZ = 0
```

## Connection to Wave Propagation

A photon propagating radially outward loses energy to the gravitational field:

```
hf_obs / hf_emit = D(r_obs) / D(r_emit)
               = [1 + Xi(r_emit)] / [1 + Xi(r_obs)]
               ≈ 1 - [Xi(r_emit) - Xi(r_obs)]
               = 1 - Delta_Xi
```

This is the gravitational redshift formula: `z = Delta_Xi`.

## Effective Dielectric Properties

The segment lattice acts as an effective medium with:

```
epsilon_eff(r) = epsilon_0 * s(r)^2 = epsilon_0 * (1+Xi)^2
mu_eff(r)     = mu_0 * s(r)^2    = mu_0 * (1+Xi)^2
```

But note: `c_eff = 1/sqrt(epsilon_eff * mu_eff) = c/s(r)^2` is NOT the local speed of light.

The actual **local speed of light** is always c (by postulate). The effective medium description is a coordinate artifact.

## Energy in Segment Lattice vs Continuum

| Regime | s(r) | u_SSZ/u_flat | Physical Meaning |
|--------|------|-------------|------------------|
| r >> r_s | ~1 | ~1 | flat spacetime limit |
| GPS orbit | 1 + 1.67e-10 | ~1 | negligible correction |
| NS surface | 1.17 | 1.37 | 37% energy enhancement |
| r = r_s | 1.802 | 3.25 | 225% enhancement |

## Do Not Confuse

```
WRONG: u_EM_SSZ = Xi^2 * u_flat
CORRECT: u_EM_SSZ = (1+Xi)^2 * u_flat = s^2 * u_flat

WRONG: The local speed of light changes
CORRECT: Local speed of light is always c; the COORDINATE speed changes
```

## Relation to Other Sections

- [Radial Scaling Gauge](https://github.com/error-wtf/ssz-complete-documentation/blob/main/05_ELECTROMAGNETISM/radial_scaling.md) — E' = s*E definition
- [Scaling Factor s(r)](https://github.com/error-wtf/ssz-complete-documentation/blob/main/02_FOUNDATIONS/scaling_factor.md) — s = 1+Xi
- [Group Velocity](https://github.com/error-wtf/ssz-complete-documentation/blob/main/05_ELECTROMAGNETISM/group_velocity.md) — how EM waves propagate
- [Redshift](https://github.com/error-wtf/ssz-complete-documentation/blob/main/05_ELECTROMAGNETISM/redshift.md) — energy loss = redshift formula


---

# Energy Conditions in SSZ

**Book reference:** Ch 14 (Energy Conditions), Appendix B.8  
**Test file:** `test_energy_conditions.py`  
**Paper:** 16 (Singularity Resolution)

---

## Overview

SSZ satisfies or violates standard GR energy conditions in specific, predictable ways. The violations are **features, not bugs** — they are required for singularity resolution.

## Standard Energy Conditions

| Condition | Formula | SSZ Status | Radius |
|-----------|---------|------------|--------|
| WEC | T_uv u^u u^v >= 0 | Satisfied | r > 5 r_s |
| DEC | T_uv u^u is future-directed | Satisfied | r > 5 r_s |
| SEC | (T_uv - 1/2 T g_uv) u^u u^v >= 0 | **VIOLATED** | r < 5 r_s |
| NEC | T_uv k^u k^v >= 0 | Always satisfied | all r |

## SEC Violation is a Prediction

The **Strong Energy Condition (SEC) violation at r < 5 r_s is an SSZ-specific prediction**, not an error:

1. The segment lattice creates effective repulsion at high densities
2. This repulsion prevents the formation of the spacetime singularity
3. The result: `D(r_s) = 0.555` (finite!) instead of `D(r_s) = 0` (GR singularity)

```
GR:  SEC satisfied everywhere  =>  Singularity at r = r_s
SSZ: SEC violated for r < 5*r_s  =>  D(r_s) = 0.555 (FINITE)
```

## Effective Stress-Energy in SSZ

The segment density Xi contributes an effective stress-energy tensor:

```
T_eff_uv = (c^4 / 8*pi*G) * (G_SSZ_uv - G_GR_uv)
```

where `G_SSZ` is the Einstein tensor derived from the SSZ metric.

The key component:
```
T_eff_rr = -(c^4 / 8*pi*G) * d^2(Xi)/dr^2 * f(r)
```

For `r < 5 r_s`, this is negative (pressure), creating repulsion.

## NEC Always Satisfied

The **Null Energy Condition is always satisfied** in SSZ:

```
T_uv k^u k^v >= 0   for all null vectors k^u
```

This means SSZ does not permit:
- Warp drives
- Traversable wormholes (without exotic matter)
- Violation of the area theorem for horizons

## Penrose-Hawking Theorems

The classical singularity theorems require SEC. Since SSZ violates SEC at `r < 5 r_s`, the Penrose-Hawking theorems do **not** apply — singularity formation is not guaranteed. This is the mathematical basis for `D(r_s) = 0.555`.

## Observable Test

The SEC violation creates a **measurable deviation** from GR for compact objects:

- At `r/r_s < 2.2` (strong field), the effective repulsion modifies the redshift
- Neutron star with `r_s/R = 0.345`: SSZ predicts z = 0.172 vs GR z = 0.236 (+13%)
- Observable with XMM-Newton or future X-ray telescopes

## Relation to Other Sections

- [Segment Density Xi](https://github.com/error-wtf/ssz-complete-documentation/blob/main/02_FOUNDATIONS/segment_density.md) — source of effective stress-energy
- [Singularities Resolved](https://github.com/error-wtf/ssz-complete-documentation/blob/main/06_STRONG_FIELD/singularities.md) — consequence of SEC violation
- [Neutron Star Redshift](https://github.com/error-wtf/ssz-complete-documentation/blob/main/07_VALIDATION/neutron_star_redshift.md) — measurable consequence
- [Falsification Criteria](https://github.com/error-wtf/ssz-complete-documentation/blob/main/08_FALSIFICATION/falsification_criteria.md) — how to test this
