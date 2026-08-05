# ISCO Comparison: SSZ vs GR

**Book reference:** Ch 31 (Lagrangian Mechanics and ISCO Comparison)  
**Test file:** `test_isco_comparison.py`  
**Paper:** 31 (Lagrangian)

---

## Definition

The Innermost Stable Circular Orbit (ISCO) is the smallest radius at which a test particle can maintain a stable circular orbit around a black hole. Matter inside the ISCO spirals inward, converting orbital energy to radiation.

## GR (Schwarzschild) ISCO

```
r_ISCO_GR = 3 * r_s   (analytical exact result)

Orbital energy at ISCO: E_ISCO/mc^2 = sqrt(8/9) = 0.9428
Accretion efficiency: eta_GR = 1 - sqrt(8/9) = 5.72%
```

## SSZ ISCO Calculation

The ISCO condition from the SSZ effective potential `V_eff(r) = D(r)^2 * (1 + L^2/(c^2*r^2))`:

```
Condition 1 (circular orbit):     dV_eff/dr = 0
Condition 2 (stability boundary): d^2V_eff/dr^2 = 0
```

Numerical result (weak field, r_s/R << 1):
```
r_ISCO_SSZ ≈ 2.95 * r_s   (slightly smaller than GR's 3 r_s)
```

The shift is small: r_ISCO_SSZ / r_ISCO_GR ≈ 0.983 (-1.7%)

## ISCO Table

| Regime | r_ISCO / r_s | eta (%) | D(r_ISCO) |
|--------|-------------|---------|----------|
| GR (exact) | 3.000 | 5.72 | 0.816 |
| SSZ (numerical) | 2.95 | 5.85 | 0.821 |
| SSZ strong-field correction | 2.90 | 5.99 | 0.825 |

## Accretion Efficiency

The accretion efficiency measures what fraction of infalling mass is converted to radiation:

```
eta = 1 - E_ISCO / (m*c^2)
```

SSZ gives **slightly higher efficiency** than GR for Schwarzschild black holes because the ISCO is at slightly lower radius (closer to the horizon), where the specific orbital energy is lower.

```
eta_SSZ / eta_GR ≈ 1.022   (+2.2% more efficient)
```

## Physical Origin of the Shift

The ISCO shift arises from the modified effective potential. In GR:
```
V_eff_GR(r) = (1 - r_s/r)(1 + L^2/(c^2*r^2)) * c^2
```

At r = 3 r_s, the second derivative changes sign (transition from stable to unstable).

In SSZ, D^2(r) replaces `(1-r_s/r)`. Since `D^2_SSZ(r) > D^2_GR(r)` for all r (SSZ time dilation is smaller than GR), the effective potential has a slightly different shape and the stability transition occurs at r = 2.95 r_s.

## Kerr ISCO

For a spinning black hole with spin parameter chi:
```
GR: r_ISCO(chi=1, prograde) = 0.5 * r_s   [maximum spin]
SSZ: r_ISCO_SSZ slightly larger at max spin
```

The spin dependence of the SSZ ISCO:
```
r_ISCO_SSZ(chi) = r_ISCO_SSZ(0) * f(chi)   where f(0) = 1
```

f(chi) is approximately the same function as in GR (weak-field limit).

## X-Ray Binary Test

X-ray binaries (black hole + companion star) show thermal emission from their accretion disks. The inner disk radius is approximately the ISCO:

```
r_inner ≈ r_ISCO
```

Fitting the disk spectrum gives r_ISCO. If SSZ is correct:
```
r_ISCO_SSZ / r_ISCO_GR = 0.983   (-1.7%)
```

This requires disk temperature and flux measurements precise to <2%, which is at the limit of current capabilities but achievable with NICER.

## Relation to Other Sections

- [Orbital Mechanics](../04_KINEMATICS/orbital_mechanics.md) — ISCO derivation from effective potential
- [Black Hole Metric](black_hole_metric.md) — metric used in V_eff
- [Penrose Process](penrose_process.md) — energy above the ISCO
- [Rotating Black Holes](rotating_black_holes.md) — Kerr ISCO
- [GR vs SSZ Tables](../07_VALIDATION/gr_vs_ssz_tables.md) — comparison table
