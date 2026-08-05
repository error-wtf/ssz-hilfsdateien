# Holonomy Invariants in SSZ

**Book reference:** Ch 17 (Frequency-Based Curvature Detection), Ch 18 (phi-Lattice Analysis)  
**Test file:** `test_holonomy_invariants.py`  
**Paper:** 17 (Holonomy Invariants)

---

## Definition

A **holonomy invariant** is a quantity computed by transporting a physical reference (clock rate) around a closed loop in spacetime. If spacetime is curved, the ratio of clock rates does NOT equal 1 after a round trip.

However, in SSZ, a specific combination DOES equal 1 — this is the **triple-clock holonomy invariant**.

## Triple-Clock Holonomy

For any three clocks at radii r_A, r_B, r_C:

```
I_ABC = [D(r_A)/D(r_B)] * [D(r_B)/D(r_C)] * [D(r_C)/D(r_A)] = 1
```

**This is trivially true** (telescoping product), but it encodes a deep physical principle:

> **The product of all pairwise frequency ratios around any closed loop equals exactly 1.**

This is the SSZ version of the **path independence of gravitational redshift**: the frequency shift between two fixed points is independent of the path taken.

## Non-Trivial Holonomy: Rate of Change

The physically interesting holonomy involves the **rates of change** of D(r):

```
H_ABC = [d/dt(D(r_A)/D(r_B))] * [d/dt(D(r_B)/D(r_C))] * [d/dt(D(r_C)/D(r_A))]
```

This is NOT generally 1 if the clocks are moving (changing r). The deviation from 1 measures the **curvature** encountered along the path.

## Frequency-Based Curvature Detection

The holonomy invariant provides a direct operational definition of curvature:

```
Curvature(path) = 1 - I_path
```

where `I_path` is computed from frequency comparisons of clocks sent along different paths.

**For a closed spatial loop at fixed time:**
```
I_loop = product_i [D(r_i)/D(r_{i+1})] = 1
```

This is trivially satisfied in SSZ (static metric). The deviation from 1 appears only for **dynamical** situations (changing metric, gravitational waves, expanding universe).

## Four-Clock Square Loop

Consider four clocks at the corners of a radial-angular "square":
- A: (r, 0)
- B: (r+dr, 0)  
- C: (r+dr, pi/2)
- D: (r, pi/2)

```
I_ABCDA = [D(A)/D(B)] * [D(B)/D(C)] * [D(C)/D(D)] * [D(D)/D(A)]
```

For a spherically symmetric metric (SSZ), D depends only on r, not on angle. Therefore `D(B) = D(C)` and `D(A) = D(D)`, giving:

```
I_ABCDA = [D(A)/D(B)] * 1 * [D(B)/D(A)] * 1 = 1
```

Perfectly trivial. The interesting case is **non-spherically symmetric metrics** (near rotating bodies, gravitational waves), where the holonomy deviation gives the curvature.

## Key Formulas (Chapter 17)

**Frequency ratio between two clocks:**
```
f_A/f_B = D(r_B)/D(r_A) = (1 + Xi(r_A)) / (1 + Xi(r_B))
```

**Differential frequency curvature:**
```
kappa = -d^2(D)/dr^2 / D   [curvature from frequency gradient]
```

**SSZ curvature at r:**
```
kappa_SSZ(r) = d^2(Xi)/dr^2 * D(r) / (1 + higher order)
```

## Connection to Gravitational Waves

A passing gravitational wave modulates D(r,t):
```
D_GW(r,t) = D_0(r) * [1 + h(t) * f(r)]
```

where h(t) is the GW strain. The holonomy around a loop then:
```
I_loop(t) = 1 + h(t) * [integral of curvature around loop]
```

A **three-arm interferometer** (like LISA) measures exactly this holonomy.

## LISA Connection

The LISA gravitational wave detector is, in SSZ language, a **triple-clock holonomy detector**:
- Three spacecraft form a triangle
- Each measures frequency ratios along its arm
- The combination `I_ABC` = 1 in absence of GW
- Deviation from 1 = GW signal

SSZ predicts: LISA holonomy measurements will show systematic offset from GR predictions by `Delta_D = D_SSZ - D_GR`, particularly for signals from compact binary mergers.

## Topological Invariance

The holonomy invariant is **topologically invariant**: it does not depend on the specific path, only on the enclosed topology. This makes it a robust observable:

- Not affected by instrumental phase noise
- Not affected by calibration errors
- Only affected by genuine spacetime curvature

## Relation to Other Sections

- [Frequency Curvature](frequency_curvature.md) — operational implementation
- [Time Dilation D](../02_FOUNDATIONS/time_dilation.md) — D(r) used in all formulas
- [Special Values](../03_FORMULAS/special_values.md) — I_ABC = 1 listed as invariant
- [Future Experimental Prospects](future_experimental_prospects.md) — LISA tests
- [phi-Lattice Discretization](../02_FOUNDATIONS/phi_lattice_discretization.md) — phi-lattice structure behind D(r)
