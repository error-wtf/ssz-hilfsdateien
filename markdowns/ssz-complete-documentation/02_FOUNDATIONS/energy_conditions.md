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

- [Segment Density Xi](segment_density.md) — source of effective stress-energy
- [Singularities Resolved](../06_STRONG_FIELD/singularities.md) — consequence of SEC violation
- [Neutron Star Redshift](../07_VALIDATION/neutron_star_redshift.md) — measurable consequence
- [Falsification Criteria](../08_FALSIFICATION/falsification_criteria.md) — how to test this
