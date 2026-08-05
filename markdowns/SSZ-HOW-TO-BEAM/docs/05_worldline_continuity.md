# 05 — Worldline Continuity

A candidate transfer is not a copy:

```math
C_B \ne \mathrm{copy}(C_A)
```

Instead it must define a continuous timelike worldline:

```math
x_C^\mu(\tau): A\to B,
\qquad \tau_2>\tau_1,
\qquad g_{\mu\nu}u^\mu u^\nu=-c^2.
```

For early testing, the repo uses a `WorldlineSegment` with positive proper-time, continuity, and CTC flags.
