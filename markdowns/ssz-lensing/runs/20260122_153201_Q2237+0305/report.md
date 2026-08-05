============================================================
DERIVATION CHAIN REPORT
============================================================
ObservablesBundle: Q2237+0305
  Sources: 1
  Total images: 4
  Total constraints: 8


[Step 1] m=2 only
----------------------------------------
  Regime: OVERDETERMINED
  Constraints: 8
  Parameters: 5
  Max Residual: 8.1155e-03

[Step 2] m=2 + shear
----------------------------------------
  Regime: OVERDETERMINED
  Constraints: 8
  Parameters: 7
  Max Residual: 6.5393e-03
  Improvement: 19.4% vs previous

[Step 3] m=2 + m=3
----------------------------------------
  Regime: OVERDETERMINED
  Constraints: 8
  Parameters: 7
  Max Residual: 2.2204e-16
  Improvement: 100.0% vs previous

[Step 4] m=2 + shear + m=3
----------------------------------------
  Regime: FORBIDDEN
  Constraints: 8
  Parameters: 9
  Status: FORBIDDEN
    -> Need 1 more constraint(s)
    -> Options: flux ratios, time delays, arc points, or multi-source

[Step 5] m=2 + m=4
----------------------------------------
  Regime: OVERDETERMINED
  Constraints: 8
  Parameters: 7
  Max Residual: 2.2204e-16

[Step 6] m=2 + shear + m=4
----------------------------------------
  Regime: FORBIDDEN
  Constraints: 8
  Parameters: 9
  Status: FORBIDDEN
    -> Need 1 more constraint(s)
    -> Options: flux ratios, time delays, arc points, or multi-source

[Step 7] m=2 + m=3 + m=4
----------------------------------------
  Regime: FORBIDDEN
  Constraints: 8
  Parameters: 9
  Status: FORBIDDEN
    -> Need 1 more constraint(s)
    -> Options: flux ratios, time delays, arc points, or multi-source

[Step 8] m=2 + shear + m=3 + m=4 (maximal)
----------------------------------------
  Regime: FORBIDDEN
  Constraints: 8
  Parameters: 11
  Status: FORBIDDEN
    -> Need 3 more constraint(s)
    -> Options: flux ratios, time delays, arc points, or multi-source

============================================================
SUMMARY
============================================================
Best model: m=2 + m=3
Best residual: 2.2204e-16

FORBIDDEN models (need more observables):
  - m=2 + shear + m=3
      Need 1 more constraint(s)
      Options: flux ratios, time delays, arc points, or multi-source
  - m=2 + shear + m=4
      Need 1 more constraint(s)
      Options: flux ratios, time delays, arc points, or multi-source
  - m=2 + m=3 + m=4
      Need 1 more constraint(s)
      Options: flux ratios, time delays, arc points, or multi-source
  - m=2 + shear + m=3 + m=4 (maximal)
      Need 3 more constraint(s)
      Options: flux ratios, time delays, arc points, or multi-source