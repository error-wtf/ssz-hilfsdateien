# SSZ-LIGO Model History
Status: LOCKED_DOCUMENTATION — do not modify without author decision
Generated: 2026-05-18

---

## IMPORTANT MODEL-INTERPRETATION CORRECTION

**Do not treat "smaller than 39%" as failure.**

The 39% value was only a rough approximation from a specific branch/regime,
not a locked LIGO interferometer strain prediction.

If the refined SSZ/RSG strain pipeline gives a much smaller effect, or an
effect indistinguishable from GR in the current LIGO band, that may be good
and physically expected.

**Reason:**
LIGO does not measure telescope-like emitted object frequencies directly.
It measures calibrated laboratory strain.
The correct SSZ-LIGO observable is phase/strain deformation after
strong-field-to-weak-field radial scaling, NOT a raw 39% QNM ratio.

**However:**
Do not move goalposts after seeing data.
The split below is the model history as it existed BEFORE pipeline results.

---

## 1. HISTORICAL_APPROXIMATION

```
Value:    ~39%
Branch:   C_photon_sphere
Formula:  f_SSZ/f_GR = 1/D(r*) at r* = 1.387 rs, D(r*)=0.72
Source:   qnm_spectrum.md
Status:   DISCARDED_FOR_LIGO_STRAIN_TEST
Reason:   Source-frame strong-field ratio, not a strain prediction.
          LIGO chain: strong-field → RSG phase accounting → weak-field
          propagation → deltaPsi(f) → strain.
          39% is NOT the end of that chain.
```

---

## 2. CANONICAL_RINGDOWN_NOTE

```
Value:    ~3%
Branch:   A_v51_ch30
Formula:  fundamental mode QNM shift, approximately 3%
Source:   SSZ_BOOK_DE_CLEAN.md Ch.30 / V51 PDF
Status:   PARTIAL_EXPLORATORY
Context:  Below single-event LIGO precision.
          Testable via stacking or next-generation detectors (ET/CE).
          Exact derivation not yet locked.
```

---

## 3. CURRENT_FORWARD_MODEL

```
Approach: Strong-field → Radial Scaling Gauge → weak-field propagation
Formula:  deltaPsi_SSZ(f): V0_PROXY only
          h_SSZ(f) = h_GR(f) * exp(i * deltaPsi_SSZ(f))
Source:   radial_scaling.md (RSG concept, LOCKED)
          formula_compendium.md (D(r), Xi(r), LOCKED)
          known_limitations.md §3 (complete GW waveform NOT YET IN CORPUS)
Status:   SSZ_FORWARD_V0_PROXY — not a locked prediction

Current pipeline result (GW240925 H1 exploratory run):
  lnL_GR  ≈ -3.237e7
  lnL_SSZ ≈ -3.237e7
  ΔlnL    ≈ -4.47e-8
  MF-SNR GR  ≈ 39.92
  MF-SNR SSZ ≈ 40.27
  deltaPsi_max ≈ 0.286 rad
  Residual max ≈ 8.5e-22

Interpretation:
  PASS_EXPLORATORY_STRAIN_PIPELINE_RAN
  V0_PROXY_INDISTINGUISHABLE_FROM_GR_CONTROL
  This is compatible with: "39% was wrong branch for LIGO strain"
  This is NOT: SSZ supported / SSZ falsified
```

---

## 4. CLAIM STATUS

```
READY_FOR_REAL_SSZ_CLAIM:      NO
PIPELINE_STATUS:               PASS_EXPLORATORY_STRAIN_PIPELINE_RAN
POSTERIOR_RF_TEST:             INVALID_FOR_SSZ
39_PERCENT_QNM_BRANCH:         DISCARDED_FOR_LIGO_STRAIN_TEST
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```

---

## What Must Happen Before Any Real Claim

1. Author resolves epsilon_220 conflict (3% vs 31% vs 39%)
2. h_SSZ(f) is fully derived from RSG equations in corpus
3. Calibration-safe adapter between SSZ forward model and LIGO strain is built
4. Xi_strong form confirmed as saturation (canonical g2) by author
5. Regime boundaries confirmed as 1.8/2.2 for LIGO pipeline
6. Full model-independent test executed with locked equations

---

## Forbidden Interpretations

```
SSZ supported by GW240925:     FORBIDDEN
SSZ falsified by GW240925:     FORBIDDEN
39% disproven as whole theory: FORBIDDEN
LIGO confirms SSZ:             FORBIDDEN
GR beaten by SSZ:              FORBIDDEN
```

## Allowed Interpretations

```
PASS_EXPLORATORY_STRAIN_PIPELINE_RAN:           ALLOWED
V0_PROXY_INDISTINGUISHABLE_FROM_GR_CONTROL:     ALLOWED (not a verdict)
MODEL_REFINEMENT_39PCT_WAS_WRONG_BRANCH:        ALLOWED (history note)
PIPELINE_TECHNICALLY_WORKS:                     ALLOWED
READY_FOR_NEXT_STEP_AFTER_AUTHOR_DECISIONS:     ALLOWED
```

---
© 2026 SSZ-LIGO Test Suite
