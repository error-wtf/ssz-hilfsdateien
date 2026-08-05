# Scaling Factor s(r)

**Book reference:** Ch 1 (Radial Scaling Gauge), Ch 2  
**Test file:** `test_radial_scaling.py`  
**Paper:** 01 (Radial Scaling)

---

## Definition

The scaling factor s(r) is the inverse of the time dilation factor:

```
s(r) = 1 + Xi(r) = 1 / D(r)
```

| Quantity | Formula | Limit r->inf | At r = r_s |
|----------|---------|-------------|------------|
| Xi(r) | see segment_density.md | 0 | 0.80171 |
| D(r) | 1/(1+Xi) | 1 | 0.55503 |
| s(r) | 1+Xi = 1/D | 1 | 1.80171 |

## Physical Meaning

`s(r)` quantifies how much a physical quantity is **scaled up** relative to flat spacetime at radius r:

- At infinity: `s = 1` (no scaling, flat spacetime)
- At Earth surface: `s = 1 + 6.96e-10 ≈ 1.000000001` (negligible)
- At GPS orbit: `s = 1 + 1.67e-10` (tiny but measurable)
- At neutron star surface (`r_s/R = 0.35`): `s ≈ 1.17` (17% scaling)
- At Schwarzschild radius: `s = 1.80171` (80% scaling, finite!)

## Application to Electromagnetic Fields

The **Radial Scaling Gauge** for Maxwell fields uses s(r):

```
E'(r) = s(r) * E(r)    [scaled electric field]
B'(r) = s(r) * B(r)    [scaled magnetic field]
```

The modified Maxwell equations become:
```
nabla . (s^2 * E) = 0
nabla x (s^2 * B) = mu_0 * eps_0 * s^2 * dE/dt
```

This ensures energy conservation in the segment lattice.

## Connection to Wave Propagation

The group velocity of EM waves in the segment lattice:
```
v_group = L_seg * f / N
```

where the segment length `L_seg` is modified by s(r). This explains the additive light-travel time correction:
```
Delta_t_grav = integral[Xi(r)/c * dr]
```

## DO NOT confuse

```
WRONG: s(r) = 1 + 2*Xi(r)
CORRECT: s(r) = 1 + Xi(r)

WRONG: D(r) = 1 - Xi(r)
CORRECT: D(r) = 1/(1 + Xi(r))
```

## Relation to Other Sections

- [Segment Density Xi](segment_density.md) — Xi(r) definition
- [Time Dilation D](time_dilation.md) — D(r) = 1/s(r)
- [Radial Scaling Gauge](../05_ELECTROMAGNETISM/radial_scaling.md) — application to Maxwell
- [Energy in EM Fields](../05_ELECTROMAGNETISM/energy_em_field.md) — energy formula using s^2
