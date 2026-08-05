# Intersection Invariance: two r* values, two formula contexts

**Book reference:** Ch 3, Ch 4, Appendix B.7.1  
**Test files:** `test_intersection.py`, `test_ssz_physics.py`  
**Primary sources:** `06_STRONG_FIELD/GR_SSZ_INTERSECTION_PHI_DISCRETIZATION.md`, `really-full-output.md`

---

## Definition

The symbol `r*` is used in two related but distinct comparisons. Do not collapse them into one number.

Both comparisons solve the same invariant equation:

```
D_SSZ(x) = D_GR(x),   x = r/r_s
D_GR(x) = sqrt(1 - 1/x)
D_SSZ(x) = 1/(1 + Xi(x))
```

The value of `r*/r_s` depends on which SSZ `Xi` form is being compared with GR.

---

## Canonical comparison table

| Context | Xi form | r*/r_s | Xi(r*) | D*(=D_GR) | Use |
|---|---|---:|---:|---:|---|
| Decay / global comparison | `Xi_A(x)=1-exp(-phi/x)` | 1.594811 | 0.637439 | 0.610710 | segcalc constants, global D comparison |
| Saturation / local metric-pure comparison | `Xi_B(x)=1-exp(-phi*x)` | 1.386562 | 0.893914 | 0.528007 | metric-pure/local saturation tests |

Both values are mass-independent because the equation contains only `x=r/r_s`.

---

## What is not correct

`r*` is not the solution of `Xi_weak = Xi_strong` in the outer domain. With `Xi_weak=1/(2x)`, the weak branch is a first-order GR-matching proxy; it is not the same object as the GR time-dilation comparison above.

Therefore the phrase "universal intersection" must always say which comparison is meant:

- `r*/r_s = 1.594811` for the decay/global `D_SSZ = D_GR` comparison.
- `r*/r_s = 1.386562` for the saturation/local `D_SSZ = D_GR` comparison.

---

## Horizon agreement

The two exponential forms agree at the Schwarzschild radius:

```
Xi_A(1) = Xi_B(1) = 1 - exp(-phi) = 0.801711847
D(r_s) = 1/(1 + Xi(r_s)) = 0.555027710
```

This is why both notations can appear in papers without contradicting the finite-horizon result.

---

## Bracket theorem

Both intersection values lie in the phi bracket:

```
1 < r*/r_s < phi = 1.618033988...
```

This bracket is the invariant statement. The exact numerical value inside the bracket depends on the selected `Xi` comparison.

---

## Relation to regime boundaries

`r*` is not itself the hard code boundary of the operational blend. The canonical computational blend remains:

```
very_close: x < 1.8
blended:    1.8 <= x <= 2.2
outer:      x > 2.2
```

Physical regimes then classify the outer side further into photon-sphere, strong, and weak contexts. See [regime definitions](regime_definitions.md) and [regime/formula domain clarification](regime_and_formula_domain_clarification.md).

---

## Relation to Other Sections

- [GR/SSZ Intersection and Phi Discretization](../06_STRONG_FIELD/GR_SSZ_INTERSECTION_PHI_DISCRETIZATION.md) — detailed two-form derivation
- [Regime Definitions](regime_definitions.md) — hard boundaries and physical regimes
- [Special Values](../03_FORMULAS/special_values.md) — Xi(r_s), D(r_s), D*
- [Confusion Prevention](../11_GUARDRAILS/confusion_prevention.md) — false-alarm patterns
