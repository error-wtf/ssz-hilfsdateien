# SSZ Observable Method Matrix

This document defines the Prime Directive classifications, routing methods, and rules for evaluating physical observables in the Segmented Spacetime (SSZ) framework.

## Method Matrix

| Observable Class | Primary Method | Description & Implementation Rules | Target Examples |
| :--- | :--- | :--- | :--- |
| **`NULL_LIGHT`** | `PPN_COMPLETION` | Light-like propagation requires PPN completion ($1 + \gamma_{\text{PPN}}$) for spatial contributions. $\Xi$-only is insufficient. | Eddington Lensing, Cassini Shapiro delay, VLBI / Group delay |
| **`TIMELIKE_STATIC`** | `XI_DIRECT` | Static clock or frequency rate measurements evaluate the metric scaling factor $D(r)$ directly from the field $\Xi(r)$. | Gravitational Redshift, Pound-Rebka tower, GPS clock rate |
| **`TIMELIKE_ORBIT`** | `PPN_ORBIT` | Orbits are subject to non-linear geodesic pathing and PPN parameter limits. No $\Xi$-only shortcuts allowed. | Mercury Perihelion precession, frame dragging, orbit precession |
| **`KINEMATIC_INVARIANT`** | `SSZ_KINEMATIC_IDENTITY` | Exact local coordinate velocity invariants arising from algebraic metric definitions. | Escape-fall velocity closure ($v_{\text{escape}} \cdot v_{\text{fall}} = c^2$) |
| **`STRONG_FIELD_DIAGNOSTIC`** | `XI_STRONG_FIELD_DIAGNOSTIC` | Regularized coordinate limits at $r = r_s$ or checks of classical energy conditions. | Finite $D(r_s)$ dilation limit, WEC / SEC diagnostics |

## Routing Integrity

Every registered observable is assigned exactly one class and method under this matrix. If an observable's predicted calculation deviates from its assigned class rules (e.g. attempting to calculate a light-bending angle using `XI_DIRECT`), the verification suite automatically fails.
