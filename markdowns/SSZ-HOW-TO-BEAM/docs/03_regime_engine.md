# 03 — Regime Engine

All Xi computations use x = r/r_s.

| x range | Regime | Formula domain |
|---:|---|---|
| x < 1.8 | very_close | g2 inner exponential |
| 1.8 <= x <= 2.2 | blended | derivative-matched Hermite C² blend |
| 2.2 < x <= 3.0 | photon_sphere | g1 branch |
| 3.0 < x <= 10.0 | strong | g1 branch |
| x > 10.0 | weak | g1 branch |

Formulas:

```math
\Xi_\mathrm{weak}(x)=\frac{1}{2x},\qquad
\Xi_\mathrm{strong}(x)=1-e^{-\phi/x}.
```

The blend is a quintic polynomial p(t), t=(x-1.8)/0.4, matching value, first derivative, and second derivative at both boundaries.
