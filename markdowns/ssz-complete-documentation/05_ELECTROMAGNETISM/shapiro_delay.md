# Shapiro Delay in SSZ

**Book reference:** Ch 9 (PPN), Ch 10 (Tests), Appendix B.5.2  
**Test file:** `test_shapiro_delay.py`  
**Paper:** 01 (Radial Scaling)

---

## CRITICAL: Use PPN Formula

```
Delta_t_Shapiro = (1+gamma) * (r_s/c) * ln(4*r1*r2/d^2)
               = 2 * (r_s/c) * ln(4*r1*r2/d^2)    [gamma=1 in SSZ]
```

**Do NOT** compute Shapiro delay as `integral[Xi/c * dr]`. That formula only captures g_tt. The full Shapiro delay includes spatial curvature (g_rr) and requires the PPN factor (1+gamma) = 2.

## Setup

```
       Mass M
         |
   r1 *--+--* r2
         |  (d = closest approach)
   Emitter    Receiver
```

- r1: distance from mass to emitter
- r2: distance from mass to receiver  
- d: closest approach distance to mass (impact parameter)
- r_s = 2GM/c^2

## Derivation from Null Geodesics

For a radial null geodesic:
```
dt = dr / (D^2 * c) = (1+Xi)^2/c * dr
```

Expanding to first order in Xi:
```
Delta_t = (r2-r1)/c + (2/c) * integral[Xi(r) dr]   [first order]
```

However, the spatial curvature contributes a second integral of the same form, giving the total factor of 2 (= 1+gamma):
```
Delta_t_total = (r2-r1)/c + (2/c) * integral[r_s/(2r) dr]
             = (r2-r1)/c + (r_s/c) * [ln(r2) - ln(r1)]
```

For the two-way path (radar experiment), the round-trip excess delay is:
```
Delta_t_round_trip = 2 * (r_s/c) * ln(4*r1*r2/d^2)
```

## Cassini Measurement (2003)

**Setup:** Cassini spacecraft at Saturn opposition, signal passing near Sun
- r1 = 1 AU = 1.496e11 m (Earth-Sun)
- r2 = 8.43 AU = 1.263e12 m (Saturn-Sun)
- d = 1.6 R_sun = 1.114e9 m (closest approach)
- r_s_sun = 2953 m

**Calculated:**
```
Delta_t = 2 * (2953/3e8) * ln(4 * 1.496e11 * 1.263e12 / (1.114e9)^2)
        = 1.97e-5 * ln(6.09e5)
        = 1.97e-5 * 13.32
        = 262 microseconds
```

**Measured:** 264 +/- 2 microseconds

**PPN test result:** `gamma = 1.000021 +/- 0.000023`  
SSZ prediction (gamma=1) confirmed at 1 part per 50,000.

## One-Way vs Two-Way

**One-way Shapiro delay** (signal from emitter to receiver):
```
Delta_t_one_way = (r_s/c) * ln(4*r1*r2/d^2)
```

**Round-trip** (radar echo, e.g. to planets):
```
Delta_t_round_trip = 2 * (r_s/c) * ln(4*r1*r2/d^2)
```

## Gravitational vs SSZ Additive Delay

SSZ splits the Shapiro delay into two physically distinct contributions:

1. **Temporal delay** (from g_tt): `Delta_t_xi = integral[Xi/c * dr]`
2. **Spatial delay** (from g_rr): same magnitude = `Delta_t_xi`
3. **Total:** `Delta_t = 2 * Delta_t_xi = (1+gamma) * Delta_t_xi`

This is not two separate effects — it is one integral evaluated twice because both metric components contribute equally (gamma=1).

## Relation to Other Sections

- [PPN Formulas](../03_FORMULAS/ppn_formulas.md) — complete PPN context
- [Light Travel Time](light_travel_time.md) — additive form of travel time
- [Gravitational Lensing](gravitational_lensing.md) — analogous factor-of-2
- [Cassini Validation](../07_VALIDATION/cassini_test.md) — measurement details
- [Method Assignment](../11_GUARDRAILS/method_assignment.md) — when to use PPN
