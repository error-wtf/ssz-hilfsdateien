# Gravitational Lensing in SSZ

**Book reference:** Ch 9 (PPN), Ch 10 (Observational Tests), Appendix B.5.1  
**Test file:** `test_lensing_deflection.py`  
**Paper:** 01 (Radial Scaling), 10 (PPN Framework)

---

## CRITICAL: Use PPN Formula

```
alpha = (1+gamma) * r_s / b = 2 * r_s / b   [gamma=1 in SSZ]
```

**Do NOT** use `alpha = Xi(b)/b`. That only captures the temporal metric component. Light bending requires both g_tt and g_rr, which together give the factor of 2.

## Variables

- **alpha**: total deflection angle [radians]
- **b**: impact parameter (closest approach to the lensing mass)
- **r_s**: Schwarzschild radius of the lensing mass
- **gamma = 1**: SSZ PPN parameter (exact, same as GR)

## Eddington 1919 Solar Eclipse

**Setup:** Light from distant star grazing the solar limb during eclipse
- b = R_sun = 6.96e8 m
- r_s_sun = 2953 m

**Deflection:**
```
alpha = 2 * 2953 / 6.96e8 = 8.488e-6 rad
alpha_arcsec = 8.488e-6 * 206265 = 1.7506 arcsec
```

Newton (1/2 factor): 0.875 arcsec  
GR/SSZ (full factor): 1.750 arcsec  
Eddington measured: 1.75 +/- 0.09 arcsec  

**SSZ = GR = Observation** (confirms gamma=1).

## Why Factor of 2 (not 1)?

The deflection angle gets contributions from two metric components:

1. **Temporal component** (g_tt): curves the path in time, contributes `r_s/b` to deflection
2. **Spatial component** (g_rr): curves spatial geometry, contributes another `r_s/b`

Total: `alpha = 2 * r_s/b`

Newtonian gravity only has the temporal component (curved time, flat space), giving `alpha_Newton = r_s/b = 0.875 arcsec` (half the GR/SSZ value).

SSZ has gamma=1 (spatial curvature = temporal curvature), so the factor of 2 is exact.

## Strong Lensing

For stronger fields (b approaching photon sphere), higher-order corrections apply:

```
alpha_higher = 2 * r_s/b + (15*pi/16) * (r_s/b)^2 + O((r_s/b)^3)
```

For b >> r_s (weak field), the linear term dominates.

## Einstein Ring

When source, lens, and observer are perfectly aligned, a ring appears:

```
theta_E = sqrt(r_s * D_LS / (D_L * D_S))
```

where D_L = lens distance, D_S = source distance, D_LS = lens-source distance.

This formula is identical in SSZ and GR (gamma=1 means identical weak-field lensing).

## Microlensing

For stellar microlensing (point mass, weak field), the amplification:

```
A = (u^2 + 2) / (u * sqrt(u^2 + 4))
```

where `u = theta/theta_E` is the angular separation in units of Einstein ring radius.

**SSZ = GR** for all microlensing observables (both have gamma=1).

## VLBI Tests

Very Long Baseline Interferometry measures solar gravitational deflection with μas precision:

- Fomalont et al. 2009: `gamma = 0.9998 +/- 0.0003`
- SSZ prediction: `gamma = 1.0000 (exact)`

No deviation from GR in SSZ for lensing — this is by construction (both g_tt and g_rr reproduce Schwarzschild to PPN order).

## When Would SSZ Deviate from GR in Lensing?

SSZ lensing deviates from GR only in the **strong field** regime (b ~ r_s):

```
alpha_SSZ_strong / alpha_GR_strong = D(b)^2_SSZ / D(b)^2_GR
```

For b = 2 r_s: `D_SSZ(2r_s)^2 / D_GR(2r_s)^2 = (0.77)^2/(0.71)^2 = 1.17`  
The SSZ strong-field bending is ~17% stronger than GR for b = 2 r_s.

## Relation to Other Sections

- [PPN Formulas](../03_FORMULAS/ppn_formulas.md) — formula context
- [Shapiro Delay](shapiro_delay.md) — analogous factor-of-2 argument
- [Method Assignment](../11_GUARDRAILS/method_assignment.md) — when to use PPN
- [Falsification: Instruments](../08_FALSIFICATION/instruments.md) — VLBI and future tests
