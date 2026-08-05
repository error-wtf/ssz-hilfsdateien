# phi-Lattice Discretization (Canonical Reference)

**Book reference:** Ch 3 (phi-lattice), Ch 18 (phi-lattice analysis), Appendix B.13  
**Test file:** `test_phi_lattice.py`  
**Paper:** 04 (Metric), 18 (Phi-Lattice Analysis)

---

## Definition

The SSZ metric has a natural discrete structure on the **phi-lattice**:

```
x_k = phi^k   (r/r_s, k = 0, 1, 2, 3, ...)
```

where `phi = (1+sqrt(5))/2 = 1.618034...` is the golden ratio.

## Canonical Table

| k | r/r_s  | Xi_SSZ | D_SSZ | D_GR  | Regime                  |
|---|--------|--------|-------|-------|-------------------------|
| 0 | 1.000  | 0.80171 | 0.55503 | 0     | Natural boundary        |
| 1 | 1.618  | 0.632  | 0.613 | 0.618 | Phi bracket edge        |
| 2 | 2.618  | 0.191  | 0.840 | 0.786 | Photon-sphere regime    |
| 3 | 4.236  | 0.118  | 0.894 | 0.874 | Strong regime           |
| 4 | 6.854  | 0.073  | 0.932 | 0.924 | Strong regime           |
| 5 | 11.09  | 0.045  | 0.957 | 0.954 | Weak field onset        |

The table follows the current formula-domain rule: inner decay form below `1.8`, Hermite blend from `1.8` to `2.2`, and the g1/weak-form branch above `2.2`.

## Bracket Theorem

```
r* in [r_s, phi * r_s]
```

The invariant statement is that both documented `D_SSZ = D_GR` comparison points lie inside this bracket:

- decay/global form: `r*/r_s = 1.594811`
- saturation/local form: `r*/r_s = 1.386562`

This is not a generic `Xi_weak = Xi_strong` regime-boundary equation.

## Algebraic Identity

```
D_GR(phi * r_s) = sqrt(1 - 1/phi) = 1/phi^(1/2) ≈ 0.786
```

More precisely:
```
D_GR(r) = sqrt(1 - r_s/r)
At r = phi * r_s:  D_GR = sqrt(1 - 1/phi) = sqrt(1/phi^2) = 1/phi ≈ 0.618
```

**Fibonacci identity:** `1/phi = phi - 1 = 0.6180...`

So `D_GR(phi * r_s) = 1/phi` — a pure Fibonacci/golden-ratio result.

## QNM Connection

Quasi-normal mode frequencies are modified by the phi-lattice structure:

```
f_QNM_SSZ / f_QNM_GR = 1 / D_SSZ(r*) ≈ 1 / 0.72 ≈ 1.39
```

This is a **testable SSZ-specific prediction** for gravitational wave ringdown frequencies.

## Why phi?

The golden ratio phi appears because:
1. **Self-similar structure:** The segment lattice is self-similar under scaling by phi
2. **Fine-structure connection:** `alpha_SSZ = 1/(phi^(2*pi) * N_0) ≈ 1/137.036`
3. **Euler identity bridge:** The derivation passes through `e^(i*pi) + 1 = 0` applied to the segment quantization condition
4. **Minimality:** phi satisfies the simplest quadratic `phi^2 = phi + 1`, making it the most natural discrete scale factor

## Derivation Sketch

Start from the segment counting condition: the number of complete segments N(r) between two radii must be an integer. For a self-similar lattice, N(r_k+1)/N(r_k) = const. The unique constant that satisfies both self-similarity AND the boundary condition D(r_s) = 1/(1 + Xi(r_s)) = finite is phi.

## Key Values at Lattice Points

```
Xi_SSZ(r_s)        = 1 - exp(-phi)      = 0.80171
Xi_decay(phi*r_s)  = 1 - exp(-1)        = 0.63212
D_SSZ(phi*r_s)     = 1/(1 + 0.63212)    = 0.61270
D_GR(phi*r_s)      = 1/phi              = 0.61803
```

## Relation to Other Sections

- [Segment Density Xi](segment_density.md) — the Xi formulas used in the table
- [Time Dilation D](time_dilation.md) — D(r) = 1/(1+Xi)
- [Regime Definitions](regime_definitions.md) — which formula applies at each lattice point
- [Structural Constants](structural_constants.md) — phi value and derivation
- [Intersection Invariance](intersection_invariance.md) — both r*/r_s comparisons lie within the bracket
- [QNM Spectrum](../06_STRONG_FIELD/qnm_spectrum.md) — observable consequences
