# MINIMAL VERIFIED CORE PIPELINE — DERIVED_V1 RERUN

**Date:** 2026-05-20 23:43 UTC
**Pipeline:** run_strain_pipeline.py (patched, DERIVED_V1)
**Event:** GW240925, H1 4kHz
**No LIGO Runs besides this one:** YES
**No New Claims:** YES

---

## 1. Provenance

| Field | Value |
|-------|-------|
| HDF5 file | H-H1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5 |
| SHA256 | 4da44bd2e5e17716608f0acbc8c631cce3d9738aa9d19e03d2738cced7aeed14 |
| Dataset | strain/Strain |
| Detector | H1 |
| Channel | H1:GDS-CALIB_STRAIN_CLEAN |
| GPS start | 1411260416.0 |
| GPS end | 1411264512.0 |
| Trigger GPS | 1411261107.984 |
| Trigger offset | 691.984 s within file |
| Sample rate | 4096 Hz |
| Window | 4.000 s (16384 samples) |
| Strain min/max | -7.25e-18 / 7.09e-18 |
| NaN/Inf | None |

**VERIFIED: HDF5 provenance complete. SHA256 matches.**

---

## 2. PSD

| Parameter | Value |
|-----------|-------|
| Method | Welch |
| Window | Hann |
| nperseg | 4096 |
| Overlap | 50% |
| Off-source offset | 500 s before trigger |
| Off-source length | 256 s (1048576 samples) |
| PSD bins | 2049 |
| Frequency range | 1.0 – 2048.0 Hz |
| PSD median [20-800 Hz] | 1.757e-47 1/Hz |
| Source | RAW STRAIN — no posterior PSD |

---

## 3. GR Control

| Parameter | Value |
|-----------|-------|
| Template | TaylorF2 0PN stationary-phase |
| Chirp mass | 8.90 Msun (public alert) |
| eta | 0.25 (equal-mass assumption) |
| Distance | 300 Mpc |
| Band | 20-800 Hz |
| Status | GR_CONTROL_TEMPLATE_LIMITED |

---

## 4. SSZ Forward Model — DERIVED_V1

```
SSZ_FORWARD_MODE = DERIVED_V1
amplitude_source = derived_amplitude.py  (P_GW_SSZ Ch.31 Z.18696)
phase_source = derived_phase.py          (rdot_SSZ Ch.31 Z.18700)
waveform_source = derived_waveform.py    (constructed from deltaA + deltaPsi)
V0_FALLBACK_USED = NO
```

### deltaA (Amplitude Correction)

| Metric | Value |
|--------|-------|
| Range [20-800 Hz] | [-6.92e-01, -6.51e-02] |
| Mean | -4.81e-01 |
| At 20 Hz (r/rs ≈ 14.6) | -0.065 (weak field, expected) |
| At 800 Hz (r/rs ≈ 1.25) | -0.713 (strong field, near horizon) |
| Physical interpretation | Amplitude SUPPRESSED relative to GR at all frequencies |

### deltaPsi (Phase Correction)

| Metric | Value |
|--------|-------|
| Range [20-800 Hz] | [0.060, 10.76] rad |
| Mean | 0.395 rad |
| Physical interpretation | Phase ACCUMULATED (SSZ inspiral is faster due to rdot_SSZ > rdot_GR) |

### h_SSZ Waveform

| Metric | Value |
|--------|-------|
| |h_SSZ| / |h_GR| ratio | 0.754 |
| FORMULA_STATUS | DERIVED_V1 |
| READY_FOR_REAL_CLAIM | NO |

---

## 5. Residuals & Log-Likelihood

| Metric | GR (0PN) | SSZ DERIVED_V1 |
|--------|----------|-----------------|
| lnL | -3.2372e+07 | -3.2372e+07 |
| delta_lnL (SSZ - GR) | — | **6.3404e-06** |
| MF-SNR | 39.92 | 14.23 |
| Residual RMS | 8.502e-22 | 8.502e-22 |

**delta_lnL < 1 → INDISTINGUISHABLE from GR.**

---

## 6. Comparison: V0 Proxy vs DERIVED_V1

| Metric | Previous V0 Proxy | DERIVED_V1 (this run) |
|--------|-------------------|----------------------|
| deltaA formula | NONE | D²-1 (Ch.31 Z.18696) |
| deltaPsi formula | kappa*(1-D(xi_weak)) | (1+Xi)^6 via rdot_SSZ (Ch.31 Z.18700) |
| Xi branch | xi_weak only | get_xi() w/ blend zone |
| delta_lnL | ~6e-6 | 6.34e-06 |
| MF-SNR SSZ | 14.23 | 14.23 |

**Result:** delta_lnL nearly identical. This is expected — both corrections are small in the LIGO weak-field band. The key difference is that DERIVED_V1 is CORRECTLY DERIVED from Ch.31 source equations, while V0 was HEURISTIC (kappa=1.0 locked by fiat).

---

## 7. deltaA Analysis: Why -0.48 Mean?

The large deltaA mean (-0.48 across 20-800 Hz) is DOMINATED by high-frequency bins near the horizon:

- **At 20 Hz:** r/rs ≈ 14.6 → deltaA ≈ -0.065 (weak field, tiny)
- **At 800 Hz:** r/rs ≈ 1.25 → deltaA ≈ -0.713 (strong field, near ISCO)

The TaylorF2 0PN template has amplitude ∝ f^(-7/6), so most power is at LOW frequencies where deltaA is small. The noise-weighted contribution of 800 Hz is minimal. This is why delta_lnL remains tiny despite large raw deltaA.

**MF-SNR SSZ = 14.23** reflects TEMPLATE MISMATCH, not physics. A proper SSZ template bank would use SSZ-specific templates rather than applying corrections to a GR template.

---

## 8. Anti-Circularity Gate

| Check | Status |
|-------|--------|
| H1 strain (GWOSC HDF5) | VALID_INDEPENDENT — used |
| PSD from off-source strain | VALID_INDEPENDENT — used |
| TaylorF2 analytic template | ANALYTIC_CONTROL — used |
| SSZ DERIVED_V1 | SSZ_FORWARD_DERIVED_V1 — used |
| Posterior samples | INVALID — NOT used |
| epsilon_220 | BLOCKED_CONFLICT — NOT used |
| **GATE: CLEAR** | ✅ |

---

## 9. Final Status

```
PIPELINE_STATUS:              PASS_EXPLORATORY_STRAIN_PIPELINE_RAN
PIPELINE_FORWARD_MODE:        DERIVED_V1
IMPLEMENTATION_ALIGNED:       YES
V0_FALLBACK_USED:             NO
READY_FOR_REAL_SSZ_CLAIM:     NO
SSZ_SUPPORT_CLAIM_MADE:       NO
SSZ_FALSIFICATION_CLAIM_MADE: NO
POSTERIOR_RF_TEST:            INVALID_FOR_SSZ
GR_CONTROL_TEMPLATE:          GR_CONTROL_TEMPLATE_LIMITED
CLAIM_LEVEL_LIGO:             NO
```

---

## 10. What Remains Blocked

1. **Hamiltonian-Jacobi S_r(r) integral (Ch.31 Z.18677)** — not implemented → deltaPsi remains DERIVED_V1, not LOCKED_FINAL
2. **epsilon_220** — BLOCKED_CONFLICT (3%/31%/39%), author decision required
3. **Merger/Ringdown** — not implemented. No SSZ IMR template exists.
4. **Detector projection** — not implemented (H1 implicitly assumed optimal)
5. **GR control** — 0PN TaylorF2 only (GR_CONTROL_TEMPLATE_LIMITED)

---

## 11. Verdict

**Pipeline now correctly uses DERIVED_V1 components (derived_waveform.py).**
**delta_lnL = 6.34e-06 → INDISTINGUISHABLE from GR in inspiral weak-field.**
**This is a METHODOLOGICAL result, not a physics claim.**
**No SSZ confirmation. No SSZ falsification.**
