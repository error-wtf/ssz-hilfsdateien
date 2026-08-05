# Derived-V0 Strain Pipeline Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18 18:52:23

## Formula Status
- deltaPsi: DERIVED_V0_PROXY (rdot_SSZ=rdot_GR*D^2/s^4, SSZ Book Ch.31)
- deltaA:   DERIVED_V0_PROXY (D^2-1 from P_GW ratio)
- h_SSZ:    DERIVED_V0_PROXY = h_GR*(1+deltaA)*exp(i*deltaPsi)
- branch:   g2_decay (operative per formula_compendium.md)

## Parameters
- M_total: 20.45 Msun | mu: 5.11 Msun | rs: 60.40 km
- r/rs at 20 Hz: 14.6
- r/rs at 800 Hz: 1.2

## deltaPsi [20.0-800.0 Hz]
- min: 5.9759e-02 rad
- max: 1.0760e+01 rad
- median: 1.7152e-01 rad

## deltaA [20.0-800.0 Hz]
- min: -6.9194e-01
- max: -6.5077e-02
- median: -6.0203e-01

## Likelihood
| Model | lnL | MF-SNR |
|-------|-----|--------|
| GR control (0PN) | -3.2372e+07 | 39.92 |
| SSZ derived-V0   | -3.2372e+07 | 14.23 |

delta_lnL = 6.3404e-06

## Interpretation
DERIVED_V0_PROXY_INDISTINGUISHABLE_FROM_GR_CONTROL

## Final Gate
```
DELTA_PSI_STATUS: DERIVED_V0_PROXY
DELTA_A_STATUS: DERIVED_V0_PROXY
H_SSZ_STATUS: DERIVED_V0_PROXY
EPSILON_220_STATUS: BLOCKED_BRANCH_CONFLICT
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE: NO
SSZ_FALSIFICATION_CLAIM_MADE: NO
```
