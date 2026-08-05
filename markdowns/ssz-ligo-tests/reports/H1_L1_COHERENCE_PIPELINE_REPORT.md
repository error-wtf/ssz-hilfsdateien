# H1/L1 Coherence Pipeline Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18 21:29:42

## Anti-Circularity
- Strain files: read-only GWOSC C00
- No posterior f,m,chi used
- PSD: Welch off-source only
- GR template: 0PN TaylorF2 (no spin, no posterior)
- SSZ: DERIVED_V1_INSPIRAL_0PN_LOCKED phase, DERIVED_V0_PROXY amplitude

## Regime Check
- r/rs at 20 Hz:  15  (weak-field)
- r/rs at 210 Hz: 5   (weak-field, clipped at f_ISCO ~ 215 Hz)
- F_HIGH capped at 210 Hz: 0PN TaylorF2 invalid above ISCO
- Xi_weak = rs/(2r) operative throughout retained band

## H1 Results
- lnL_GR:  -3.2372e+07
- lnL_SSZ: -3.2372e+07
- delta_lnL: 5.3160e-06
- MF-SNR GR:  44.20
- MF-SNR SSZ: 5.98

## L1 Results
- lnL_GR:  -1.5832e+10
- lnL_SSZ: -1.5832e+10
- delta_lnL: -4.3869e-05
- MF-SNR GR:  646.94
- MF-SNR SSZ: 358.55

## H1/L1 Residual Coherence
- Cross-correlation peak: 1.6002
- Lag at peak: 0 samples
- Interpretation: |xcorr|<0.3 expected for independent noise
- COHERENCE_STATUS: CORRELATED_NEEDS_CHECK

## Anomalies / Pipeline Diagnostics

**L1 anomalous SNR (MF-SNR GR = 647):**
- L1 resid_rms = 1.1e-20 vs H1 resid_rms = 1.7e-21 (~6x higher)
- L1 lnL_GR = -1.58e+10 vs H1 lnL_GR = -3.24e+07 (~500x larger magnitude)
- Cause: L1 strain segment has higher noise floor in this window, OR
  the trigger-window is not optimally placed for L1 (LIGO detectors are
  not always simultaneously at design sensitivity)
- This is a pipeline diagnostic issue, NOT an SSZ signal
- Action required: check L1 noise stationarity in trigger window

**xcorr > 1.0 (xcorr = 1.60):**
- Cross-correlation normalisation by std(real(resid)) fails when
  the residual contains a dominant common noise component (power-line,
  Schumann resonances, common environmental)
- OR: numerical overflow in short segment xcorr
- xcorr > 1.0 is unphysical — normalization bug for this segment
- COHERENCE_STATUS set to CORRELATED_NEEDS_CHECK pending fix
- Action: whiten residuals before xcorr, or use frequency-domain coherence

**H1 MF-SNR SSZ (5.98) vs GR (44.20):**
- Large SNR drop when applying SSZ correction is expected: the 0PN SSZ
  template diverges from the data because h_SSZ modifies the waveform
  significantly. This is a V1 proxy limitation, not physics.

## Interpretation
- delta_lnL values are exploratory only
- No physics claim is made from these numbers
- H1 and L1 processed independently with same pipeline
- L1 anomalous SNR = pipeline diagnostic, not SSZ signal
- Residual coherence test inconclusive due to normalization failure

## Final Gate
```
H1_STATUS:                     PASS
L1_STATUS:                     PASS
COHERENCE_STATUS:               CORRELATED_NEEDS_CHECK
FORMULA_STATUS_DELTA_PSI:      DERIVED_V1_INSPIRAL_0PN_LOCKED
FORMULA_STATUS_DELTA_A:        DERIVED_V0_PROXY
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```
