# SSZ Forward Model Application Report
Generated: {NOW}

## LABEL: SSZ_FORWARD_DERIVED_V1

## Implementation
Uses `derived_waveform.py` — the documented DERIVED_V1 implementation.
NOT the V0 proxy that was previously in the pipeline.

## Formula Applied
```
deltaA(f)  = D(r(f))^2 - 1          [from P_GW_SSZ, Ch.31 Z.18696]
deltaPsi_V0(f) via rdot_SSZ chain  [from rdot_SSZ, Ch.31 Z.18700]
r(f)       = (GM/(pi*f)^2)^(1/3)    [Newtonian Kepler proxy]
h_SSZ(f)   = h_GR(f) * (1+deltaA) * exp(i*deltaPsi)
```

## FORMULA_STATUS: DERIVED_V1
- deltaA: AUTHORIZED_CH31 source → algebraically derived ✓
- deltaPsi: AUTHORIZED_CH31 source → Kepler-Approx derived ✓
- Hamiltonian-Jacobi S_r(r) integral (Ch.31 Z.18677): NOT IMPLEMENTED
- PN corrections beyond 0PN: NONE
- Spin: NONE

## Parameters
- Total mass: {M_kg/M_SUN:.2f} Msun
- Schwarzschild radius: {rs_m/1e3:.2f} km
- Regime: weak field (r >> rs in LIGO band)

## delta_psi Statistics [20–800 Hz]
- max:  {dpsi[mask].max():.4f} rad
- min:  {dpsi[mask].min():.4f} rad
- mean: {dpsi[mask].mean():.4f} rad

## Blocked Items
- HJ phase integral (Ch.31 Z.18677) not implemented → deltaPsi NOT LOCKED_FINAL
- epsilon_220 ringdown: BLOCKED_CONFLICT (3%/31%/39%)

## Mandatory Statements
```
READY_FOR_REAL_SSZ_CLAIM:      NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```

## Status
**SSZ_FORWARD_DERIVED_V1** — inspiral-only, methodological test, not claim-level
