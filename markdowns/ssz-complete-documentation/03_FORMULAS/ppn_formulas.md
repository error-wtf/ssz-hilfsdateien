# PPN Formulas (Parametrized Post-Newtonian)

**Book reference:** Ch 9, Ch 10, Appendix B.5  
**Test files:** `test_lensing_deflection.py`, `test_shapiro_delay.py`, `test_ppn_exact.py`  
**Paper:** 01 (Radial Scaling), 10 (PPN Framework)

---

## CRITICAL RULE

> **Lensing and Shapiro delay use PPN (gamma=1), NOT Xi-based formulas.**  
> Xi only captures g_tt (time-time metric component), not g_rr.  
> Lensing depends on BOTH components: `(1 + gamma) = 2` for SSZ.

```
WRONG: alpha = Xi(r)/b
CORRECT: alpha = (1+gamma) * r_s / b = 2 * r_s / b

WRONG: Delta_t = integral[Xi/c * dr]
CORRECT: Delta_t = (1+gamma) * r_s/c * ln(4*r1*r2/d^2)
```

## PPN Parameters in SSZ

```
beta  = 1  (exact)
gamma = 1  (exact)
```

SSZ reproduces **exact GR** in PPN limit. There is no PPN deviation from GR in the weak field.

## Gravitational Lensing

```
alpha = (1 + gamma) * r_s / b = 2 * r_s / b
```

- **alpha**: deflection angle [radians]
- **b**: impact parameter (closest approach distance)
- **r_s**: Schwarzschild radius of lensing mass

**Eddington 1919 value:**
```
alpha_Sun = 2 * 2953 / (6.96e8) = 8.48e-6 rad = 1.748 arcsec
```

Observed: 1.75 +/- 0.09 arcsec. SSZ agrees with GR and observation.

## Shapiro Delay

```
Delta_t = (1 + gamma) * (r_s/c) * ln(4 * r1 * r2 / d^2)
        = 2 * (r_s/c) * ln(4 * r1 * r2 / d^2)
```

- **r1**: distance from mass to signal emitter
- **r2**: distance from mass to receiver  
- **d**: closest approach distance

**Cassini 2003 measurement:**  
`gamma = 1.000021 +/- 0.000023` (best current test of GR/SSZ PPN)

## Perihelion Precession

```
Delta_omega = 6*pi*G*M / (a * (1-e^2) * c^2)  [per orbit]
```

This formula is identical in SSZ and GR (both have beta = gamma = 1).

**Mercury:**  
`Delta_omega = 42.98 arcsec/century` (SSZ = GR, observation: 42.98 +/- 0.04)

## Gravitomagnetic (Frame Dragging) PPN

For rotating bodies, the PPN gravitomagnetic parameter:
```
zeta = 1  (SSZ, same as GR)
```

Lense-Thirring precession rate (SSZ = GR in weak field):
```
Omega_LT = (G * J) / (c^2 * r^3)   [frame dragging]
```

## Why PPN for Lensing but Xi for Redshift?

Light deflection probes the **spatial curvature** (g_rr component) as well as the **time curvature** (g_tt component). Redshift probes only g_tt. The SSZ Xi function modifies only the radial structure entering through g_tt; the spatial metric in SSZ is constructed to reproduce GR at PPN level, giving gamma = 1 and thus the factor of 2 in lensing.

## Test Verification

```python
# test_ppn_exact.py
assert abs(beta_SSZ - 1.0) < 1e-10
assert abs(gamma_SSZ - 1.0) < 1e-10

# test_lensing_deflection.py  
alpha = 2 * r_s / b   # NOT Xi(b)/b

# test_shapiro_delay.py
Delta_t = 2 * (r_s/c) * log(4*r1*r2/d**2)  # NOT integral of Xi
```

## Relation to Other Sections

- [Segment Density Xi](../02_FOUNDATIONS/segment_density.md) — NOT used for lensing/Shapiro
- [Shapiro Delay](../05_ELECTROMAGNETISM/shapiro_delay.md) — detailed derivation
- [Gravitational Lensing](../05_ELECTROMAGNETISM/gravitational_lensing.md) — detailed derivation
- [Cassini Validation](../07_VALIDATION/cassini_test.md) — experimental confirmation
- [Method Assignment](../11_GUARDRAILS/method_assignment.md) — which method for which observable
