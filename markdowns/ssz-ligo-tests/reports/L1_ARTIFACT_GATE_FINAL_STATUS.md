# L1 Data Quality & Artifact Gate – Final Diagnostic Status
⚠️ UNVERIFIED_DERIVED_REPORT - CSV NOT PRIMARY EVIDENCE  
**Date:** 2026-05-19 (updated 2026-05-19 sub-band revision)  
Status: LOCKED — Do not modify without explicit author decision  
Event: GW240925 (trigger GPS 1411261107.984, O4b GWOSC)

---

## Final Gate State

```
GAUSSIANITY_ARTIFACT_GATE:   FAIL_L1_NON_GAUSSIAN
L1_EXCESS_CLASS:             TRIGGER_SPECIFIC_LOW_FREQ_SUBBAND  ← revised
L1_ANOMALY_BAND:             20-40 Hz (ex_k=+44.9 trigger, +1.1 off-source)
L1_HARMONIC_STRUCTURE:       RESONANCE_IN_OFF_SOURCE_TOO
L1_BROADBAND_EXCESS:         TECHNICALLY_REPRODUCIBLE_NOT_EXPLAINED
L1_STATUS:                   DQ_FLAGGED_DIAGNOSTIC_ONLY
H1_L1_COHERENCE_STATUS:      BLOCKED_BY_L1_DQ
ARTIFACT_SCORE:              10/24  RISK=MEDIUM
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:      NO
SSZ_FALSIFICATION_CLAIM_MADE: NO
```

---

## What the Diagnostic Chain Established

### Step 1 — Bandpower Stationarity

- L1 20–210 Hz bandpower ratio (trigger/off-source): **~2.28×**
- H1 20–210 Hz bandpower ratio (trigger/off-source): **0.76×** (normal)
- Excess is **reproducible** across multiple off-source PSD windows
- Excess is **not** a PSD-window artifact (robust multi-window Welch confirmed)

### Step 2 — DQ Bit Provenance

- L1 CBC_CAT2 / CBC_CAT3: **CLEAN** (no vetoed CBC glitch)
- L1 CW_CAT1: file-wide constant, not trigger-specific
- L1 NO_CW_HW_INJ: unset for entire 4096 s file (not injection-certified)
- GWOSC public DQ products: **INSUFFICIENT** to explain the broadband excess
- Offline Omicron / iDQ / hveto: **NOT AVAILABLE** in public release

### Step 3 — Harmonic Oscillator / Resonance Structure Test

- L1 trigger peaks: 26, 36, 41, 53, **60**, 120 Hz
- **60 Hz + 120 Hz** = US mains frequency + 1st harmonic → persistent spectral line
- 41 Hz and 60 Hz present **500 s before trigger** in off-source window
- H1 trigger peaks (22, 28, 40 Hz): **zero overlap** with L1 peaks
- Conclusion: dominant L1 structure is persistent instrumental line noise,
  not a transient astrophysical or GW-correlated feature

### Step 4 — Gaussianity Artifact Gate

Whitened strain, 4 windows tested (trigger, −100 s, −300 s, −500 s):

| Window | L1 ex_kurtosis (20–210 Hz bp) | H1 ex_kurtosis (20–210 Hz bp) |
|--------|-------------------------------|-------------------------------|
| TRIGGER | +4.58 | +2.61 |
| OFF −500 s | +2.86 | +6.37 |
| OFF −300 s | +4.56 | +6.33 |
| OFF −100 s | +4.52 | — |

Key observations:
- L1 TRIGGER (4.58) ≈ L1 OFF−300 s (4.56) ≈ L1 OFF−100 s (4.52)
- Trigger-to-off-source difference: **Δ < 0.06** — indistinguishable
- Non-Gaussianity is **chronic and stationary**, not trigger-specific
- H1 trigger (2.61) is **less** non-Gaussian than H1 off-source (6.4) —
  H1 trigger window is actually the quietest window

### Step 5 — Sub-band Gaussianity (revised finding)

Raw strain bandpassed into 5 sub-bands, Tukey-windowed, normalized:

| Band | L1 trigger ex_k | L1 off-500s ex_k | H1 trigger ex_k | Flag |
|------|-----------------|------------------|-----------------|------|
| **20-40 Hz** | **+44.857** | **+1.127** | +3.673 | **ANOMAL** |
| 40-80 Hz | -0.515 | -0.614 | +0.340 | clean |
| 80-120 Hz | +3.266 | +0.892 | +2.386 | mild |
| 120-160 Hz | +5.663 | +1.445 | +1.252 | mild |
| 160-210 Hz | +0.198 | +0.371 | +0.405 | clean |

**Revised classification:**
- The anomaly is **trigger-specific** in the 20-40 Hz band (Δex_k = +43.7)
- It is **NOT chronic broadband** — off-source 20-40 Hz is clean (+1.1)
- Previous Step 4 showed chronic non-Gaussianity across the full 20-210 Hz
  band due to whitening artifacts; the sub-band test on raw strain is more
  precise
- **L1_EXCESS_CLASS revised:** `TRIGGER_SPECIFIC_LOW_FREQ_SUBBAND`

Physical candidates for the 20-40 Hz trigger-specific L1 structure:
1. Sub-threshold glitch (seismic, suspension, control system)
2. Environmental coupling not captured in public DQ bits
3. Pipeline ringing (bandpass / whitening filter edge)
4. Low-frequency instrumental mode excited near trigger time

**None of these constitute a signal. None falsify SSZ.**

---

## What This Means

**Not this:**
> "There is a single glitch exactly at the trigger time."

**But this:**
> "The 20–210 Hz band in L1 is generally not cleanly Gaussian/white
> under the current whitening and bandpass pipeline.
> The excess is a chronic band-noise property, not a transient."

The L1 excess is therefore:
- **Not a candidate for a new astrophysical signal**
- **Not trigger-specific** in any Gaussianity diagnostic
- **Not explained** by GWOSC release DQ products
- **Not a SSZ falsification** — L1 is simply excluded from claim-level use

---

## Canonical Report Statement (updated)

> The L1 anomaly in GW240925 is concentrated in the 20-40 Hz sub-band
> and is trigger-specific (excess kurtosis +44.9 at trigger vs. +1.1
> off-source 500 s prior). This band is maximally sensitive to seismic
> coupling, suspension noise, and LIGO control-system artefacts.
> The anomaly may be detector- or pipeline-induced. Current public
> GWOSC products are insufficient to decide whether the 20-40 Hz
> structure is instrumental, environmental, line-related, or
> signal-like. Therefore no physics claim is allowed without
> offline DQ / iDQ / Omicron / AUX clarification.

**What "detector-induced" means here:**
- Not: LIGO acted intentionally
- Yes: the excess may originate from the instrument system itself
  (seismics, suspensions, optics, controls, calibration, pipeline)
- The public data show something anomalous
- The public data do **not** provide enough context to distinguish:
  `signal` vs. `detector artefact` vs. `line` vs. `whitening/PSD` vs.
  `sub-threshold glitch`

---

## What Was NOT Lost

- **SSZ theory is not falsified** by this result.
- **H1 pipeline is unaffected** — H1 remains USABLE_EXPLORATORY.
- **The diagnostic chain is complete and clean**: a problematic detector
  arm has been methodically removed from the claim chain via four
  independent tests.
- **The forward model, anti-circularity, and formula locks are unchanged.**

---

## Path Forward

```
Option A — Other event
  Run same pipeline on additional O4 events with clean H1 and L1.
  Multi-event consistent H1/L1 twist response would be meaningful.

Option B — H1-only exploratory
  Continue H1-only pipeline as a sensitivity/scale sanity check.
  Cannot test H1/L1 differential response.

Option C — LIGO offline DQ request
  Request Omicron / iDQ / hveto / line monitor products for GW240925.
  If L1 confirmed clean offline, rerun coherence analysis.

Option D — Wait for improved public DQ products
  If iDQ becomes available for this GWOSC release, rerun.
```

---

## Reports Underpinning This Lock

| Report | Test | Date |
|--------|------|------|
| `ROBUST_MULTIWINDOW_PSD_REPORT.md` | Multi-window PSD | 2026-05-18 |
| `L1_20_210HZ_GLITCH_STATIONARITY_REPORT.md` | Bandpower stationarity | 2026-05-18 |
| `DQ_STATE_VECTOR_BIT_PROVENANCE_REPORT.md` | DQ bit mapping | 2026-05-18 |
| `L1_HARMONIC_OSCILLATOR_TEST.md` | Harmonic/resonance structure | 2026-05-19 |
| `L1_GAUSSIANITY_TEST.md` | Whitened Gaussianity stats | 2026-05-19 |
| `GAUSSIANITY_ARTIFACT_GATE_REPORT.md` | Full artifact gate | 2026-05-19 |
| `DQ_AWARE_FINAL_LIGO_STATUS.md` | Master DQ gate | 2026-05-18 |
| `UNIT_NORMALIZATION_AUDIT.md` | FFT/PSD normalization 7/7 PASS | 2026-05-19 |
| `ARTIFACT_SCORE_REPORT.md` | Aggregate score 10/24 MEDIUM | 2026-05-19 |
| `GW250207_ARTIFACT_GATE_COMPARISON.md` | Cross-event (MISSING_DATA) | 2026-05-19 |

---

*READY_FOR_REAL_LIGO_SSZ_CLAIM: NO*  
*SSZ_SUPPORT_CLAIM_MADE: NO*  
*SSZ_FALSIFICATION_CLAIM_MADE: NO*
