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

- [Radial Scaling Gauge](radial_scaling.md) — E' = s*E definition
- [Scaling Factor s(r)](../02_FOUNDATIONS/scaling_factor.md) — s = 1+Xi
- [Group Velocity](group_velocity.md) — how EM waves propagate
- [Redshift](redshift.md) — energy loss = redshift formula
