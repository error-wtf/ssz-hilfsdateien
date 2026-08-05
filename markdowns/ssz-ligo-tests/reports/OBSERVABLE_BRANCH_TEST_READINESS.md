# Observable Branch Test Readiness Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Version:** 1.0  
**Date:** 2026-05-18  
**Basis:** SSZ_LIGO_OBSERVABLE_BRANCH_MATRIX.md  
**READY_FOR_REAL_LIGO_SSZ_CLAIM: NO**

---

## Executive Summary

Five distinct SSZ observable branches have been identified and separated.
Two branches (Inspiral Phase + Amplitude) have been run as exploratory pipelines.
Three branches (QNM 3%, D_min² amplitude, Photon sphere 39%) are NOT YET testable
because the mapping from their source-frame formula to detector-strain h(f) does not
exist. They require derivation before any real data test.

**Key insight:** Previous "epsilon_220 = 3%" language was wrong framing.
The 3%, 31%, 39% are three different observables. None of them is currently mapped
to a LIGO strain residual test. Only the inspiral branches are.

---

## Branch 1 — INSPIRAL_PHASE_RSG

```
STATUS:         YES_EXPLORATORY
FORMULA:        DERIVED_V1_INSPIRAL_0PN_LOCKED
H(F) ENTRY:     YES
TESTED:         YES (H1/L1 run 2026-05-18)
```

**Results (GW240925, H1, 20–210 Hz):**

| Metric | Value |
|--------|-------|
| delta_lnL H1 | +5.3e-06 |
| delta_lnL L1 | -4.4e-05 (anomalous noise) |
| MF-SNR GR | 44.2 |
| MF-SNR SSZ | 5.98 |

**Interpretation:**
- delta_lnL is indistinguishable from zero at 0PN
- SNR drop from GR→SSZ reflects that 0PN SSZ template is a poor match
  (expected — 0PN is a proxy, not a matched filter)
- Result is not a falsification; it shows the 0PN template is insufficient
- NO CLAIM

**Blocker for next step:**
Upgrade r(f) from 0PN Kepler to 3.5PN stationary phase approximation.

---

## Branch 2 — INSPIRAL_AMPLITUDE_POWER

```
STATUS:         PARTIAL
FORMULA:        DERIVED_V0_INSPIRAL_ONLY
H(F) ENTRY:     YES
TESTED:         YES (calibration scan 2026-05-18)
```

**Results:**

| Scan | delta_lnL | vs nominal |
|------|-----------|------------|
| Nominal | 6.3e-06 | — |
| Amp +5% | 6.4e-06 | WITHIN_NOMINAL |
| Amp -5% | 6.3e-06 | WITHIN_NOMINAL |
| Phase +0.05 rad | 6.3e-06 | WITHIN_NOMINAL |
| Phase -0.05 rad | 6.4e-06 | WITHIN_NOMINAL |

**SSZ_EFFECT_ABOVE_CALIBRATION: YES**
(effect 6.3e-06 > cal spread 7.1e-08)

**Interpretation:**
- The SSZ amplitude correction is stable against ±5% amp and ±0.05 rad phase errors
- But absolute magnitude is 6e-06 — far below noise
- This does NOT mean SSZ amplitude is detected
- It means: if the SSZ amplitude effect were real, it would not be confused
  with calibration uncertainty at this level
- NO CLAIM

**Blocker:**
Scope lock: define exactly where inspiral amplitude formula ends
(merger onset). Not valid past ISCO.

---

## Branch 3 — QNM_FREQ_3PCT_BRANCH

```
STATUS:         NO — NOT YET TESTABLE
FORMULA:        PARTIAL_EXPLORATORY (text claim, not derived)
H(F) ENTRY:     NOT YET
TESTED:         NO
```

**What is missing:**
1. A derived formula for `f_220_SSZ` from SSZ first principles (not just "book says ~3%")
2. A ringdown strain model: `h_rd(t) = A * exp(-t/tau) * cos(2*pi*f_220_SSZ * t + phi_0)`
3. Injection of this model into synthetic noise at GW240925 SNR
4. Sensitivity test: is 3% frequency shift distinguishable from GR at this SNR?

**Sensitivity estimate (analytic):**
For a ringdown SNR ~ rho, frequency resolution ~ 1/(rho * tau_ring).
For GW240925 with expected ringdown SNR ~ 5–10 and tau_220 ~ 4 ms:
```
delta_f / f_220 ~ 1/(rho * 2*pi*f_220 * tau_220)
               ~ 1/(8 * 2*pi * 250 * 0.004)
               ~ 0.02  (2%)
```
A 3% shift is marginally above this threshold at SNR~8, but only barely.

**Next required action:**
Build `scripts/run_qnm_ringdown_injection_sensitivity.py`:
- Inject synthetic ringdown at GR f_220 and SSZ f_220 * 1.03
- Use off-source PSD from H1
- Compute lnL difference between the two models
- Report: DETECTABLE / MARGINAL / UNDETECTABLE

**NO CLAIM until sensitivity test is done.**

---

## Branch 4 — AMPLITUDE_DMIN2_BRANCH

```
STATUS:         NO — BLOCKED
FORMULA:        DIFFERENT_OBSERVABLE (amplitude, not frequency)
H(F) ENTRY:     NOT YET
TESTED:         NO
```

**What is missing:**
- A derived equation for ringdown amplitude damping as a function of D_min
- The 31% figure comes from `D_min^2 = 0.308` but this is a scaling ratio,
  not a ringdown amplitude observable in h(f)
- Requires: SSZ ringdown amplitude model `A_SSZ = A_GR * D_min^2`
  (or whatever the correct coupling is — NOT DERIVED)

**This branch cannot be tested until the formula is derived.**

---

## Branch 5 — PHOTON_SPHERE_39PCT_BRANCH

```
STATUS:         NO — BLOCKED (source-frame only)
FORMULA:        SOURCE_FRAME_QNM_RATIO
H(F) ENTRY:     NO
TESTED:         NO
```

**What is missing:**
- The 39% is a ratio `f_SSZ/f_GR = 1/D(r*) ~ 1.39` at the photon sphere
- This is a source-frame quantity
- To enter h(f) requires: source-frame orbital frequency → GW frequency →
  redshifted detector-frame frequency
- This mapping does not exist as a derived SSZ formula
- Also: at the photon sphere (r* ~ 1.59 r_s), the weak-field Xi approximation
  breaks down entirely — requires full strong-field treatment

**This branch requires a separate derivation program.**

---

## Test Execution Status

| Test | Branch | Script | Run | Report |
|------|--------|--------|-----|--------|
| A: Inspiral Phase H1/L1 | INSPIRAL_PHASE_RSG | run_h1_l1_coherence_pipeline.py | ✅ | H1_L1_COHERENCE_PIPELINE_REPORT.md |
| B: Amplitude Cal Scan | INSPIRAL_AMPLITUDE_POWER | run_calibration_psd_sensitivity.py | ✅ | CALIBRATION_PSD_SENSITIVITY_REPORT.md |
| C: QNM 3% Injection | QNM_FREQ_3PCT | run_qnm_ringdown_injection_sensitivity.py | ❌ NOT YET | — |
| D: D_min² amplitude | AMPLITUDE_DMIN2 | not built | ❌ | — |
| E: 39% photon sphere | PHOTON_SPHERE_39PCT | not built | ❌ | — |

---

## Final Gate

```
BRANCH_1_INSPIRAL_PHASE:         YES_EXPLORATORY (run, no claim)
BRANCH_2_INSPIRAL_AMPLITUDE:     PARTIAL (run, cal scan done, no claim)
BRANCH_3_QNM_3PCT:               NO — build injection sensitivity first
BRANCH_4_AMPLITUDE_DMIN2:        NO — derive formula first
BRANCH_5_PHOTON_SPHERE_39PCT:    NO — derive source-frame mapping first

EPSILON_220_COLLAPSED_TEST:      FORBIDDEN — different observables
READY_FOR_REAL_LIGO_SSZ_CLAIM:   NO
SSZ_SUPPORT_CLAIM_MADE:          NO
SSZ_FALSIFICATION_CLAIM_MADE:    NO
```
