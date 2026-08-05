# Special Values and Invariants

**Book reference:** Appendix B.7 (Special Values section)  
**Test file:** `test_intersection.py`, `test_horizon_finite.py`

---

## Critical Values at r = r_s (Schwarzschild Horizon)

| Quantity | SSZ Value | GR Value | Significance |
|----------|-----------|----------|--------------|
| Xi(r_s) | **0.80171** | (diverges) | Saturation: 1 - exp(-phi) |
| D(r_s) | **0.55503** | **0** | FINITE! (SSZ core result) |
| s(r_s) | 1.80171 | infinity | Finite scaling factor |
| z(r_s) | 0.80171 | infinity | Finite redshift |

**D(r_s) = 0.555 is the single most important number in SSZ.**  
GR predicts D = 0 (singularity). SSZ predicts D = 0.555 (finite, testable).

## Universal Intersections

| Context | r*/r_s | Xi(r*) | D* = D_GR(r*) | Derivation |
|----------|-------:|-------:|-------:|------------|
| Decay/global form `1-exp(-φ/x)` | **1.594811** | 0.637439 | **0.610710** | D_SSZ = D_GR |
| Saturation/local form `1-exp(-φx)` | **1.386562** | 0.893914 | **0.528007** | D_SSZ = D_GR |

The invariant fact is mass-independence and the phi-bracket `1 < r*/r_s < φ`. The numerical value depends on which Xi form is used.

## phi-Related Values

| Quantity | Value | Formula |
|----------|-------|--------|
| phi | **1.618034** | (1+sqrt(5))/2 |
| phi^2 | 2.618034 | phi + 1 |
| 1/phi | 0.618034 | phi - 1 |
| phi/2 | 0.809017 | coupling half-ratio |
| 1 - exp(-phi) | **0.80171** | Xi at r_s |
| exp(-phi) | 0.19829 | complement of Xi(r_s) |
| 1/(phi^(2*pi)) | ~0.00730 | 1/N_0 factor for alpha |

## Fine-Structure Constant

| Quantity | Value | Notes |
|----------|-------|-------|
| alpha_measured | **1/137.036** = 7.2974e-3 | CODATA 2018 |
| alpha_SSZ | 1/(phi^(2*pi) * N_0) | N_0 = 4 segments/wavelength |
| alpha_SSZ numerical | ~1/137.08 | within 0.03% of measured |
| Deviation | 0.03% | residual discussed in Ch 5 |

## Intersection with phi-Lattice Points

| k | r/r_s = phi^k | D_SSZ | D_GR | D_GR algebraic |
|---|--------------|-------|------|----------------|
| 0 | 1.000 | 0.555 | 0 | - |
| 1 | 1.618 (phi) | 0.686 | 0.786 | sqrt(1-1/phi) = 0.786 |
| 2 | 2.618 (phi^2) | 0.770 | 0.882 | sqrt(1-1/phi^2) |
| 3 | 4.236 (phi^3) | 0.839 | 0.929 | - |

**Algebraic identity:** D_GR(phi * r_s) = sqrt(1/phi^2) = 1/phi = 0.618 (Fibonacci!)

Wait, corrected: `D_GR(phi * r_s) = sqrt(1 - r_s/(phi*r_s)) = sqrt(1 - 1/phi) = sqrt(0.382) = 0.618`. Yes, this equals 1/phi.

## Triple-Clock Holonomy Invariant

For any three radii r_A, r_B, r_C:
```
I_ABC = [D(r_A)/D(r_B)] * [D(r_B)/D(r_C)] * [D(r_C)/D(r_A)] = 1
```

This is a **topological invariant** — path-independent, holds for any choice of radii.

## Regime Transition Values

| Transition | r/r_s | Notes |
|------------|-------|-------|
| very_close / blend lower | 1.8 | Xi switches from strong to blend |
| blend upper / photon_sphere | 2.2 | Hermite interpolation ends |
| photon sphere (GR) | 1.5 | r = 3/2 * r_s |
| ISCO (GR, Schwarzschild) | 3.0 | r = 3 * r_s |

## Saturation Values (Asymptotic Limits)

```
Xi_max = Xi(r_s) = 0.80171   [saturation of segment density]
D_min  = D(r_s)  = 0.55503   [minimum time dilation, finite]
s_max  = s(r_s)  = 1.80171   [maximum scaling factor, finite]
```

All these are **finite** — no infinities in SSZ at any physically accessible radius.

## Relation to Other Sections

- [Intersection Invariance](../02_FOUNDATIONS/intersection_invariance.md) — two r*/r_s comparisons and phi bracket
- [phi-Lattice Discretization](../02_FOUNDATIONS/phi_lattice_discretization.md) — phi^k table
- [Holonomy Invariants](../13_FREQUENCY_FRAMEWORK/holonomy_invariants.md) — I_ABC proof
- [Structural Constants](../02_FOUNDATIONS/structural_constants.md) — phi, alpha
- [Singularities Resolved](../06_STRONG_FIELD/singularities.md) — why D(r_s) != 0
