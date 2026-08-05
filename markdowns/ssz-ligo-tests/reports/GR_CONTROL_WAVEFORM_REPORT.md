# GR Control Waveform Report
Generated: {NOW}

## LABEL: GR_CONTROL_TEMPLATE_LIMITED

## Warning
This is a 0PN TaylorF2 stationary-phase approximation.
It is NOT a full LIGO parameter estimation waveform.
It does NOT include: spin, higher modes, merger, ringdown.
It is used ONLY as a sanity control reference.

## Parameters (Public Alert / Analytic)
- Chirp mass: {MC_MSUN} Msun  (public estimate)
- eta: {ETA}  (equal-mass assumption)
- Total mass: {M_kg/M_SUN:.2f} Msun
- Distance: {DL_MPC} Mpc
- f_low: {F_LOW} Hz
- f_high: {F_HIGH} Hz

## Template Statistics
- |h_GR| max: {np.abs(h_gr).max():.3e}
- Active frequency bins: {mask.sum()}

## Status
**GR_CONTROL_TEMPLATE_LIMITED** — suitable for pipeline sanity only
