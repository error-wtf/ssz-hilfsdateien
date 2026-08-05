# SSZ-LIGO Forward Model Test Suite

**Version:** 0.5.0 — 2026-05-21  
**Event:** GW240925 (O4b, GWOSC public release)  
**Status:** `PIPELINE_STATUS: PASS_EXPLORATORY` | `READY_FOR_REAL_LIGO_SSZ_CLAIM: NO`

---

> **Latest diagnostic conclusion (2026-05-21):**  
> **The off-source background test shows that the extreme L1 SSZ-SNR metric in the 20–100 Hz band is not trigger-specific. The trigger value is essentially equal to the off-source background mean. Therefore, this L1 metric is DQ-blocked for any physical SSZ interpretation.**  
> 
> *Der Off-source-Hintergrundtest zeigt, dass die extreme L1-SSZ-SNR-Metrik im 20–100-Hz-Band nicht trigger-spezifisch ist. Der Triggerwert liegt praktisch auf dem Off-source-Hintergrundmittel. Daher ist diese L1-Metrik für jede physikalische SSZ-Interpretation DQ-blockiert.*

---

> **Core methodological position:**
> We distinguish measured detector strain from model-conditioned inference products.
> Component masses, chirp mass, spins, and QNM parameters are not directly measured
> observables — they are outputs of a GR/CBC or Kerr-conditioned inference chain.
> Therefore they cannot serve as metric-neutral input for SSZ tests.
> **m₁ and m₂ do not exist as numbers anywhere in the detector.**

---

## What This Is

A **physics-first, anti-circular forward model** from SSZ (Segmented Spacetime)
theory to LIGO detector strain, tested against real public GWOSC data (GW240925, O4b).

This is **not** a posterior-parameter test.  
This is **not** a Kerr self-consistency test.  
This is **not** a claim engine.

The pipeline computes a documented DERIVED_V1 inspiral-only SSZ waveform component for diagnostic method testing,
applies it to public GWOSC strain, and reports likelihood differences for methodological analysis — without using
any LIGO parameter estimation output.

```text
SSZ Core (Xi, D, s)
  → rdot/P_GW correction (Ch.31, LOCKED)
  → Phase accumulation (0PN inspiral, RSG)
  → delta_psi_SSZ(f), delta_a_SSZ(f)
  → h_SSZ(f) = h_GR(f) * (1 + delta_a) * exp(i * delta_psi)
  → H1 / L1 / V1 diagnostic strain comparison
  → detector parity + off-source background tests
  → residuals + lnL + MF-SNR as diagnostic metrics only
```

---

## Contributors

| Name | Role |
|------|------|
| **Carmen Wrede** | Theory Development — SSZ framework, formula derivation, physics interpretation |
| **Lino Casu** | Programming & Testing — pipeline implementation, test suite, data analysis |

---

## How to Start Guide

If you are a new user, you can clone the repository, set up your environment, download/extract the raw scientific strain data, and run the entire validation suite with these quick commands:

### 1. Clone and Enter the Repository
```bash
git clone https://github.com/error-wtf/ssz-ligo-tests.git
cd ssz-ligo-tests
```

### 2. Set Up Virtual Environment
```bash
# Create virtual environment
python -m venv .venv

# Activate (Windows PowerShell)
.\.venv\Scripts\Activate.ps1

# Activate (Linux / macOS / Git Bash)
source .venv/bin/activate
```

### 3. Install Dependencies
```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Run the Integrated Main Runner
Run the high-level orchestrator script. It handles everything for you automatically:
```bash
python run_full_test.py
```

**What this orchestrator does in the background:**
1. **Fetch LIGO Strain Data (`scripts/fetch_data.py`):** Checks for the presence of the 6 official GW240925 HDF5 files. If missing, it downloads the official `GW240925-C00-Strain.tar` archive (~2.4 GB) directly from Zenodo (Record ID `18600070`) and extracts it.
2. **HDF5 Provenance Audit (`scripts/run_hdf5_provenance_audit.py`):** Computes SHA256 checksums, validates the HDF5 internal metadata, and verifies that the trigger event GPS time is inside the 4096-second raw files.
3. **Environment and Import Sanity Checks:** Ensures that packages can be resolved without path conflicts.
4. **Pytest Suite Execution:** Discovers and executes all unit, integration, and validation tests (over 490 tests).

---

## Reproducibility Critique

This project documents, on the basis of verifiable primary sources, a structural
reproducibility gap in LIGO/GWOSC public data releases.

**This is a reproducibility, provenance, and methodology project.**

**Five documented critique points:**

1. **Calibration chain not public.** GWOSC releases calibrated h(t), not the PCal channels,
   DARM signals, FIR/IIR filter archives, or CalibEnv files needed to reconstruct h(t) from
   scratch. Confirmed by LIGO (Mastodon, Dec 2025): *"Our full data management policy [...]
   covers calibrated data, not auxiliary channels."*

2. **Calibration deficit since 2016.** The GW150914 discovery paper (PRL 116, 061102) cited
   Reference [63] for PCal data — an unpublished e-print with no data. A petition of 3,028
   verified signatures raised three specific calibration traceability questions that remain
   structurally unanswered ten years later.

3. **Code provenance gaps.** The `bilby` inference library (core LVK tool) was migrated from
   LIGO GitLab to GitHub. Original merge requests are internal-only. Papers citing specific
   code versions cannot be fully externally audited.

4. **PB-scale gap.** O4a documentation confirms total detector data is several PB/year with
   10⁵+ channels. GWOSC releases ~4 TB/year/instrument of pre-processed strain
   (`CLEAN`, `NOLINES`, `AR`). The gap between raw observable and public product is not
   disclosed upfront.

5. **GW150914 exact replication limitation.** arXiv:2010.07244 reported that the main finding could be reproduced, but an exact replication of the original analysis was not possible because the original dataset was not publicly available.

```text
Open Data Product  !=  Fully reproducible measurement chain
```

This is a reproducibility and provenance limitation.

> [**Full Report → docs/LIGO_OPEN_DATA_FULL_REPORT.md**](docs/LIGO_OPEN_DATA_FULL_REPORT.md)  
> [Detailed critique → docs/LIGO_REPRODUCIBILITY_CRITIQUE.md](docs/LIGO_REPRODUCIBILITY_CRITIQUE.md)  
> [IGWN forum thread → ask.igwn.org](https://ask.igwn.org/t/request-for-fully-reproducible-calibration-chain-for-gwosc-strain-data/1397/2)

---

## Data Source

Real LIGO strain data from the **GWOSC O4b public release**:

> **GW240925 + GW250207 — O4b Data Release**  
> Zenodo: [https://zenodo.org/records/18600070](https://zenodo.org/records/18600070)  
> DOI: 10.5281/zenodo.18600070

Files used (read-only, no posterior):

- `H-H1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5`
- `L-L1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5`

PSD estimated from off-source Welch (−500 s window, 64 s duration).  
**No posterior samples used. No PE output used. No matched-filter templates from LIGO PE.**

---

## Core SSZ Formulas

```python
# Regime-dependent Xi
Xi_weak(r)   = r_s / (2r)                           # r/r_s > 10
Xi_strong(r) = min(1 - exp(-phi * r_s / r), Xi_max)   # r_s/r < 1.8  [CANONICAL]
Xi_blend(r)  = Hermite C2 interpolation              # 1.8 < r/r_s < 2.2

# Metric functions
D(r) = 1 / (1 + Xi(r))
s(r) = 1 + Xi(r) = 1/D(r)

# Inspiral corrections  [SSZ Book Ch.31-32, LOCKED]
rdot_SSZ  = rdot_GR  * D(r)^2 / s(r)^4
P_GW_SSZ  = P_GW_GR  * D(r)^2 / s(r)^2

# Frequency-domain observables
delta_psi_SSZ(f) = [Omega(r(f)) / |rdot_GR(r(f))|] * [(1+Xi)^6 - 1] * |dr/df|
delta_a_SSZ(f)   = D(r(f))^2 - 1
h_SSZ(f)         = h_GR(f) * (1 + delta_a) * exp(i * delta_psi)
```

**Key constants:** `phi = 1.6180...` (golden ratio) | `Xi_max = 0.8017` | `D_min = 0.5550`

---

## Formula Lock Status

| Formula | Status | Source |
|---------|--------|--------|
| Xi_weak, Xi_strong, D, s | **LOCKED** | SSZ Book, formula_compendium.md |
| rdot_SSZ = rdot_GR·D²/s⁴ | **LOCKED** | SSZ Book Ch.31 |
| P_GW_SSZ = P_GW_GR·D²/s² | **LOCKED** | SSZ Book Ch.31 |
| delta_psi_SSZ(f) | **DERIVED_V1_INSPIRAL_0PN** | derived from rdot_SSZ / Ch.31 chain |
| delta_a_SSZ(f) | **DERIVED_V1_INSPIRAL_ONLY** | D²−1 from P_GW ratio |
| h_SSZ(f) | **DERIVED_V1_METHOD_COMPONENT** | constructed from deltaA + deltaPsi |
| epsilon_220 (ringdown) | **BLOCKED_BRANCH_CONFLICT** | not used for LIGO strain claims |

> **DERIVED_V1 does not mean LOCKED_FINAL. These are documented method-test components, not a complete claim-level LIGO strain model.**

The 39% QNM value is a source-frame strong-field frequency ratio, not a LIGO strain observable.

---

## Pipeline Results (GW240925, H1, 20–210 Hz)

| Metric | Value | Note |
|--------|-------|------|
| lnL GR control | −3.24×10⁷ | TaylorF2 0PN analytic |
| lnL SSZ V1 | −3.24×10⁷ | V1 inspiral correction |
| delta_lnL (H1) | +5.3×10⁻⁶ | indistinguishable at 0PN |
| delta_lnL (L1) | −4.4×10⁻⁵ | L1 diagnostic only |
| MF-SNR GR | 44.2 | |
| MF-SNR SSZ (with deltaA) | 14.2 | amplitude deformation reduces template match |
| FAIR_COMPARISON | NO | not a fair claim-level model comparison |
| CLAIM_LEVEL_LIGO | NO | metric-level claim blocked |

**F_HIGH capped at 210 Hz** (below f_ISCO ~ 215 Hz for M~20 M☉ — within 0PN regime).

> **Note:** MF-SNR 14.2 vs 44.2 reflects that an amplitude-deformed SSZ signal
> matches poorly against an undeformed GR template. This is not a physical result —
> it shows that a proper SSZ test would require an SSZ template bank.
> 
> **Note on delta_lnL:** The numerical delta_lnL scale is reported for diagnostic reproducibility only. It is not a physical SSZ effect claim because the current comparison is not a fair claim-level model comparison.

---

## L1 Diagnostic Results (Historical vs. Current)

### Current Verified Status after Off-source Background Test (2026-05-21)
The extreme L1 SSZ-SNR metric in the 20–100 Hz band is not trigger-specific. The trigger value is essentially equal to the off-source background mean. Therefore, this L1 metric is DQ-blocked for any physical SSZ interpretation.

```text
L1_TRIGGER_SPECIFIC: NO
L1_PERSISTENT_NOISE: YES
DQ_CONTEXT_REQUIRED: YES
CLAIM_LEVEL_LIGO:    NO
```

- **L1 20–100 Hz (Low-Frequency Noise):**
  - Trigger SSZ SNR: `436.96`
  - Off-source SSZ Mean (Max): `437.13` (`1482.36`)
- **L1 400–800 Hz (HF Noise / Calibration):**
  - Trigger SSZ SNR: `4417.03`
  - Off-source SSZ Mean (Max): `4066.61` (`14422.00`)

---

### Historical Diagnostics (2026-05-19 Archive)
Earlier diagnostic runs documented localized spectral line and kurtosis properties:

1. **Harmonic / Resonance Test:**
   - L1 trigger peaks: 26, 36, 41, 53, **60**, 120 Hz.
   - **60 Hz + 120 Hz** = US mains frequency + 1st harmonic -> persistent spectral lines.
   - 41 Hz and 60 Hz peaks were also present **500 s before the trigger** (off-source).

2. **Gaussianity Artifact Gate:**
   - L1 ex-kurtosis in the trigger window was evaluated at `+4.58` (compared to `+4.56` at 300s off-source).
   - This confirmed L1's non-Gaussianity is **chronic and stationarity-consistent**, rather than trigger-specific.
   - `L1_GAUSSIANITY: STRONGLY_NON_GAUSSIAN` (chronic, all windows)
   - `H1_L1_COHERENCE_STATUS: BLOCKED_BY_L1_DQ`

---

## Anti-Circularity Protocol

| Rule | Status |
|------|--------|
| No posterior f, m, χ used | ✅ ENFORCED |
| No pSEOBNR / PE output | ✅ ENFORCED |
| GR control = analytic 0PN only | ✅ ENFORCED |
| PSD from off-source Welch | ✅ ENFORCED |
| No ringdown epsilon claim | ✅ ENFORCED |
| No QNM posterior | ✅ ENFORCED |
| SSZ_SUPPORT_CLAIM_MADE | **NO** |
| SSZ_FALSIFICATION_CLAIM_MADE | **NO** |

---

## Test Suite

The repository features a fully integrated main runner script `run_full_test.py` that handles the entire pipeline, from fetching the necessary public scientific data to executing the provenance audit and running the full pytest suite.

### How to Run the Main Runner

To execute the entire test suite and validation pipeline with a single command:

```bash
python run_full_test.py
```

The main runner executes the following sequential stages:

1. **Fetch LIGO Strain Data (`scripts/fetch_data.py`):** Automatically checks for the presence of the 6 official GW240925 HDF5 strain files. If they are missing, it downloads the official `GW240925-C00-Strain.tar` archive directly from Zenodo (Record ID `18600070`) and extracts it to the correct path structure.
2. **HDF5 Provenance Audit (`scripts/run_hdf5_provenance_audit.py`):** Computes SHA256 checksums, extracts HDF5 structure/attributes, verifies strain statistics, and confirms that the event trigger GPS time is inside the 4096-second file windows.
3. **Environment and Import Sanity Checks:** Verifies the current Python environment path and ensures that the `ssz_ligo_tests` package is correctly imported and resolved.
4. **Pytest Suite Execution:** Discovers and runs all unit, integration, and validation tests (over 490 tests), checking the anti-circularity protocol, SSZ core formulas, and interferometry calculations.

```text
Current pytest status:
497 passed, 1 xfailed, exit code 0.

Historical note:
The earlier 2026-05-18 API/import-drift failures were re-audited and are no longer current.
```

| Test file | Status |
|-----------|--------|
| test_derived_delta_psi_v0.py | ✅ PASS |
| test_derived_delta_a_v0.py | ✅ PASS |
| test_h_ssz_v0_waveform_application.py | ✅ PASS |
| test_epsilon_220_branch_registry.py | ✅ PASS |
| test_xi_strong_branch_lock.py | ✅ PASS |
| test_08_anti_circularity.py | ✅ PASS |
| test_analytic_2pn_polarizations.py | ✅ PASS |
| test_geometric_algebra_interferometer.py | ✅ PASS |
| test_phase_transport_principle.py | ✅ PASS |
| tests/unit/ (all) | ✅ PASS |
| tests/validation/ (all) | ✅ PASS |
| tests/integration/ (all) | ✅ PASS |

---

## Repository Structure

```
src/
  ssz_ligo_tests/
    ssz_core.py              — Xi, D, s, regime detection
    constants.py             — PHI, XI_MAX, D_MIN, G, C, M_SUN
    derived_phase.py         — delta_psi_ssz (DERIVED_V1 inspiral-only phase component)
    derived_amplitude.py     — delta_a_ssz (DERIVED_V1 inspiral-only amplitude component)
    derived_waveform.py      — DERIVED_V1 h_SSZ(f) method-component construction
    ssz_inspiral.py          — rdot_SSZ, P_GW_SSZ (Ch.31 locked)
    ssz_phase.py             — phase accumulation
    ssz_ringdown.py          — QNM (BLOCKED_BRANCH_CONFLICT)
    epsilon_220_registry.py  — 3 branches, all BLOCKED
    anti_circularity.py      — observable classifier
    likelihood.py            — lnL, MF-SNR
    ligo_data.py             — read-only GWOSC HDF5 adapter
    forward_model.py         — full SSZ forward model
    equation_registry.py     — formula provenance registry
    provenance.py            — audit trail
    analytic_polarizations_2pn.py — 2PN h+/hx
    geometric_algebra_interferometer.py — GA detector model
    phase_transport.py       — photon phase transport
    source_propagation_twist.py — twist branch

  _legacy_ssz_ligo/          — archived legacy code (reference only)

tests/
  test_*.py                  — core formula tests
  unit/                      — unit tests
  validation/                — anti-circularity, book-value checks
  integration/               — forward model, inspiral-phase integration

scripts/
  run_strain_pipeline.py               — full H1+L1 strain pipeline
  run_h1_l1_coherence_pipeline.py      — H1/L1 coherence check
  run_calibration_psd_sensitivity.py   — calibration/PSD sensitivity scan
  run_derived_v0_pipeline.py           — V0 strain pipeline
  run_robust_multiwindow_psd.py        — multi-window Welch PSD
  run_l1_anomaly_diagnostic.py         — L1 stationarity/DQ diagnostic
  run_l1_glitch_stationarity.py        — L1 glitch / bandpower scan
  run_l1_dq_flag_check.py              — L1 DQ bit provenance
  run_l1_harmonic_oscillator_test.py   — harmonic/resonance structure test
  run_l1_gaussianity_test.py           — whitened Gaussianity stats
  run_gaussianity_artifact_gate.py     — full artifact gate (H1+L1)
  run_dq_aware_final_status.py         — master DQ-aware status report
  run_qnm_ringdown_injection_sensitivity.py — QNM injection sensitivity
  run_twist_branch_synthetic.py        — synthetic twist branch
  run_twist_branch_2pn_synthetic.py    — 2PN twist branch
  run_ga_interferometer_synthetic.py   — GA interferometer model
  run_source_propagation_twist_synthetic.py — source propagation 
  run_h1_l1_time_delay_replication.py  — single-window H1/L1 delay scan
  run_h1_l1_long_baseline_replication.py — 100 off-source windows, Z-score, subband
  run_twist_branch_real_h1_l1.py
  verify_real_ligo_tests.py            — quick verification runner
  forced_verify.py                     — forced verification suite

docs/
  DELTA_PSI_DERIVATION.md              — delta_psi formula derivation
  DELTA_PSI_V1_LOCK_ATTEMPT.md         — V1 lock attempt (0PN locked)
  DELTA_A_DERIVATION.md                — delta_a formula derivation
  H_SSZ_V0_DERIVATION.md              — h_SSZ construction
  EPSILON_220_DERIVATION_STATUS.md     — 3-branch conflict status
  EPSILON_220_BRANCH_LOCK.md           — branch classification
  QNM_OBSERVABLE_RENAMING.md           — 39%/31%/3% disambiguation
  FORMULA_BRANCH_LOCK.md               — Xi branch lock
  XI_STRONG_BRANCH_LOCK.md             — Xi_strong canonical form
  REGIME_BOUNDARY_LOCK.md              — r/rs regime boundaries
  MODEL_HISTORY.md                     — model version history
  SSZ_LIGO_OBSERVABLE_BRANCH_MATRIX.md — full observable branch matrix
  SSZ_LIGO_PHASE_TRANSPORT_PRINCIPLE.md — phase transport derivation
  SSZ_GEOMETRIC_ALGEBRA_INTERFEROMETER_MODEL.md — GA detector model
  SSZ_TWIST_ANHOLONOMY_BRANCH.md       — twist/anholonomy branch
  ANALYTIC_2PN_POLARIZATION_CONTROL.md — 2PN polarization control
  LIGO_OPEN_DATA_FULL_REPORT.md        — full report: calibration, provenance, auditability (8 parts, 14 sources)
  LIGO_REPRODUCIBILITY_CRITIQUE.md     — sourced critique of LIGO reproducibility gap

reports/
  FINAL_INTERPRETATION_LOCK.md         — locked interpretation (2026-05-18)
  DQ_AWARE_FINAL_LIGO_STATUS.md        — master DQ gate
  DERIVED_FORMULAS_CODE_CONSISTENCY_AUDIT.md
  H1_L1_COHERENCE_PIPELINE_REPORT.md
  CALIBRATION_PSD_SENSITIVITY_REPORT.md
  ANTI_CIRCULARITY_FINAL_GATE.md
  L1_ANOMALY_DIAGNOSTIC_REPORT.md
  L1_20_210HZ_GLITCH_STATIONARITY_REPORT.md
  L1_DQ_FLAG_CHECK_REPORT.md
  L1_HARMONIC_OSCILLATOR_TEST.md       — harmonic/resonance test (2026-05-19)
  L1_GAUSSIANITY_TEST.md               — gaussianity stats (2026-05-19)
  GAUSSIANITY_ARTIFACT_GATE_REPORT.md  — artifact gate (2026-05-19)
  ROBUST_MULTIWINDOW_PSD_REPORT.md
  QNM_3PCT_SENSITIVITY_FINAL_REPORT.md
  OBSERVABLE_BRANCH_TEST_READINESS.md
  NEXT_PHYSICS_DERIVATION_TASKS.md     — open physics agenda
  H1_L1_TIME_DELAY_REPLICATION_REPORT.md — single-window delay scan
  H1_L1_ABS_CORRELATION_REPLICATION_REPORT.md — abs(corr) peak detection
  H1_L1_SUBBAND_REPLICATION_REPORT.md  — per-subband xcorr
  H1_L1_LONG_BASELINE_REPLICATION_REPORT.md — 100 off-source windows (PENDING run)

data_manifest/
  gaussianity_summary_stats.csv        — per-window Gaussianity statistics
  gaussianity_test_windows.csv         — window manifest
  h1_l1_long_baseline_xcorr.csv        — per-window abs_corr results (all bands)
  h1_l1_xcorr_quantiles.csv            — trigger vs off-source Z-score summary
```

---

## Installation

```bash
python -m venv .venv
.venv/Scripts/activate      # Windows
# source .venv/bin/activate  # Linux/macOS
pip install -r requirements.txt
pip install -e .
```

**Requirements:** `numpy`, `scipy`, `h5py`, `pytest`  
Optional (plots): `matplotlib`

---

## Running Tests

```bash
Current pytest status:
497 passed, 1 xfailed, exit code 0.

Historical note:
An earlier 2026-05-18 run reported 123 passed / 52 failed / 1 xfail due to API/import/status-string drift. Those failures were re-audited and are no longer the current test-suite status.
pytest tests/unit/                                # unit tests only
pytest tests/validation/                          # anti-circularity + book checks
pytest tests/test_xi_strong_branch_lock.py        # Xi branch lock
pytest tests/test_epsilon_220_branch_registry.py  # epsilon_220 blocked (xfail)
```

---

## Running Diagnostic Scripts

All scripts require the GWOSC HDF5 data files at the path configured inside each script.

```bash
# Full strain pipeline (H1 + L1)
python scripts/run_strain_pipeline.py

# L1 harmonic oscillator / resonance structure test
python scripts/run_l1_harmonic_oscillator_test.py

# L1 + H1 Gaussianity artifact gate
python scripts/run_gaussianity_artifact_gate.py

# L1 stationarity / glitch / bandpower diagnostic
python scripts/run_l1_glitch_stationarity.py

# Multi-detector Parity Test (H1 + L1 + V1)
python scripts/run_detector_parity_test.py

# Off-source Background Noise Test (50 windows)
python scripts/run_offsource_background_test.py

# DQ-aware master status report
python scripts/run_dq_aware_final_status.py
```

---

## Open Blockers Before Any Real Claim

```text
PHYSICS BLOCKERS:
1. delta_psi: upgrade from 0PN to 3.5PN r(f) mapping (RSG integral, Ch.31)
2. delta_a:   scope lock — inspiral only, no merger/ringdown
3. epsilon_220: resolve 3% vs 31% vs 39% — three different observables, needs author
4. GR control: replace 0PN with matched 3.5PN TaylorF2
5. RSG detector propagation phase: not yet included

DATA QUALITY BLOCKERS:
6. L1 20–100 Hz metric is not trigger-specific: trigger SNR lies at background mean (verified off-source 2026-05-21)
7. L1 harmonic structure: 60/120 Hz mains lines confirmed persistent
8. L1 Gaussianity gate: FAIL_L1_NON_GAUSSIAN (chronic, not trigger-specific)
9. H1/L1 coherence: frequency-domain coherence test needed
10. L1 excess is persistent noise: L1_PERSISTENT_NOISE = YES confirmed across 50 off-source windows

READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```

---

## Physical Interpretation of Current Results

The delta_lnL ~ 0 result admits three open interpretations:

- **Option A:** SSZ correction is intrinsically small in the LIGO band (weak field, r/rs >> 1 → SSZ → GR limit). This is physically expected.
- **Option B:** The DERIVED_V1 formula for delta_psi is too coarse (kappa=1.0 exploratory, not fully derived from Ch.31 RSG phase integral).
- **Option C:** The true SSZ-LIGO forward term (RSG phase integral from Ch.31) has not yet been fully implemented.

None of these options has been eliminated. No claim is permitted until all physics blockers are resolved and L1 passes the artifact gate.

---

## Code Quality

```bash
flake8 src/ tests/ scripts/ --select=F401,F541,F811,F841,E722,E712
# Exit code: 0  (all critical errors resolved, 2026-05-19)
```

---

## Critical Open-Data and Methodology Position

### Summary

It also does **not** claim that SSZ is confirmed or falsified by the current LIGO release data.

The central conclusion is narrower and more important:

> The public GWOSC strain products are useful for standard GR/CBC workflows and educational diagnostics. However, because they are already calibrated, cleaned, line-treated, and released without the full auxiliary, calibration, DQ, Omicron/iDQ, and preprocessing context, they are not sufficient by themselves for a claim-level independent forward test of non-Kerr / non-GR metric models.

- LIGO measures detector strain. The strain is real measurement input.
- Many higher-level products — masses, spins, QNM frequencies, remnant parameters,
  posterior samples, Bayes factors — are **not raw observables**.
- They are outputs of model-dependent inference pipelines.
- If those outputs are used as independent proof of the same model assumptions
  that produced them, a circularity problem arises.

We call this: **model-bound self-confirmation**.

The public strain products are useful measurement inputs, but they are not complete measurement-chain reconstruction packages. Outside the official GR/CBC pipeline, their
independent evidential power is much smaller than public communication often suggests.

**Canonical methodological statement of this project:**

> We distinguish between detector measurements and model-conditioned inference
> products. The calibrated strain is measurement input; chirp mass, component
> masses, spins, and QNM parameters are GR/CBC-conditioned estimates — not
> metric-neutral observables.

And on the L1 anomaly:

> The anomaly may be detector- or pipeline-induced. Current public GWOSC
> products are insufficient to decide whether the 20–100 Hz structure is
> instrumental, environmental, line-related, or signal-like.

---

### Standard Reproducibility vs. Alternative-Metric Forward Testing

GWOSC strain products are valid and useful public data products for standard GR/CBC workflows, tutorials, diagnostics, and many reproducibility exercises.

They are not, by themselves, sufficient for a claim-level independent forward test of a non-Kerr / non-GR metric model.

Reason: a non-GR forward test must distinguish between:

- physical model residuals
- calibration effects
- detector noise
- line subtraction / line contamination
- whitening and PSD choices
- DQ selections
- auxiliary-channel couplings
- Omicron/iDQ/offline detector-characterization information
- preprocessing choices such as CLEAN / NOLINES / AR products

Without that context, a residual or anomaly cannot be uniquely assigned to the alternative metric or to the detector/pipeline state.

Therefore, our position is:

- **Public GWOSC strain is measurement input.**
- **It is useful but not a complete external reconstruction package.**
- **For claim-level non-Kerr metric tests, additional calibration, DQ, auxiliary, and preprocessing provenance is required.**

Scope:

- **Methodology**
- **Provenance**
- **Anti-circular strain-level testing**
- **Limits of public data products for alternative-metric forward models**

---

### 1. Strain Is Data; Posterior Products Are Interpretation

LIGO measures calibrated detector strain: `h(t)`. Everything above that level is inferred.

Quantities such as `m1`, `m2`, chirp mass, final spin, QNM frequency, Bayes factors, and
posterior samples are **not directly observed in the detector**. They are estimated from
strain using waveform models, priors, noise assumptions, calibration, DQ selections, and
GR/Kerr/CBC parameter-estimation pipelines. Such products are **not metric-neutral**.

For alternative metrics, the correct test is not:
`Does SSZ match the Kerr-derived posterior?`

But:
`Can h_SSZ(f) explain the calibrated strain without using GR/Kerr posteriors as truth?`

---

### 2. The Chirp Mass Is Not a Direct Measurement

The chirp mass is mathematically well-motivated (not arbitrary):

```text
M_chirp = (m1 * m2)^(3/5) / (m1 + m2)^(1/5)
```

It governs the GR inspiral rate: `df/dt ∝ M_chirp^(5/3) * f^(11/3)`.

However, `m1` and `m2` are **not directly measured object properties**. They are
model-inferred from Bayesian template matching.

| Layer | What it is | Status |
|-------|-----------|--------|
| `h(t)` — strain | Raw observable | Directly measured |
| `M_chirp`, `m1`, `m2`, `chi` | GR/CBC Bayesian posterior | Model-dependent |
| `f_QNM`, `tau_QNM` — ringdown | Inferred under Kerr assumption | Model-dependent |

**`m1` and `m2` do not exist as numbers anywhere in the detector.**

Correct: *"Under GR/CBC assumptions, the strain is consistent with a source having
this inferred chirp mass."*

Not valid: *"The detector directly measured this chirp mass as a metric-neutral fact."*

---

### 3. The Circularity Problem

```text
1. Assume GR/Kerr/CBC waveform models.
2. Search strain with GR/Kerr/CBC templates.
3. Estimate masses, spins, QNMs via GR/Kerr/CBC parameter estimation.
4. Publish those posterior products.
5. Treat them as independent evidence that GR/Kerr/CBC is correct.
```

This is a reproducibility and provenance limitation. It means the evidential scope must be
stated honestly. The pipeline shows: *"Data are consistent with GR/CBC."* It cannot
alone prove: *"All alternative metric models are excluded."* For that, alternative models
need their own strain-level forward models tested directly against calibrated strain.

---

### 4. Open Data vs. Open Reproducibility

The public GWOSC releases are open in a formal sense — calibrated strain, some metadata,
some DQ bits, posterior products, tutorials. But this is **not** the same as full open
reproducibility.

For a fully independent non-GR test, one also needs:

```text
Omicron triggers      iDQ products          offline DQ reports
auxiliary channels    line lists            known instrumental couplings
calibration details   state-vector context  detector-characterization decisions
```

Without these, external groups cannot independently decide whether an anomaly is a signal,
a known glitch, an unvetoed transient, a line, a calibration feature, a whitening artifact,
or a seismic coupling.

We distinguish **formal open data** from **full open reproducibility**.

---

### 5. Why Public LIGO Products Are Not Enough for SSZ

SSZ is an alternative metric framework. A valid SSZ-LIGO test **cannot** use GR/Kerr
posterior parameters as neutral input.

Circular inputs:

```text
Kerr QNM posteriors     GR remnant mass/spin posteriors
pSEOBNR samples         PE-derived QNM frequencies as ground truth
```

Valid inputs start at strain level:

```text
calibrated H1/L1 strain     independent PSD + whitening
independent artifact gates  SSZ forward model h_SSZ(f)
direct residual / likelihood comparison
```

This is the **anti-circular principle** of this project.

---

### 6. GW240925 — What the Pipeline Found

The pipeline built and tested: PSD estimation, H1/L1 diagnostics, Gaussianity, line/notch,
STFT/Omicron-lite, phase-randomization, DQ-bit provenance, H1-only exploratory,
synthetic SSZ branches, source-propagation twist, and phase-transport formalism.

Key empirical finding:

```text
[Historical 2026-05-19 diagnostic note — superseded by 2026-05-21 off-source background test]
Current status:
L1_TRIGGER_SPECIFIC: NO
L1_PERSISTENT_NOISE: YES
DQ_CONTEXT_REQUIRED: YES
CLAIM_LEVEL_LIGO:    NO
```

Classification:

```text
H1: USABLE_EXPLORATORY      L1: DIAGNOSTIC_ONLY
H1/L1 coherence: BLOCKED    SSZ claim: NO    SSZ falsification: NO
```

Public products are insufficient to decide whether the L1 behavior is caused by
low-frequency detector noise, seismic coupling, suspension/control system, unvetoed
transient, line contamination, or filtering artifacts. Offline Omicron/iDQ/AUX needed.

---

### 7. What the L1 Anomaly Does and Does Not Mean

Does **not** establish a physical SSZ signal.
It indicates that L1 requires DQ/auxiliary/preprocessing context before physical interpretation.

Does mean:
`The released public data are not sufficient for a broadband non-GR H1/L1 coherence test.`

> The L1 behavior is technically reproducible but not sufficiently explained by public
> release DQ products. Without offline Omicron/iDQ/line/AUX context, L1 cannot be used
> for a claim-level broadband non-GR coherence test.

---

### 8. Detector Strain Is Not a Telescope Observable

For telescope SSZ tests, one may compare redshift, emission lines, or lensing. LIGO is
different — it measures local interferometer strain: laser phase differences, arm
projections, detector response, noise-weighted strain.

A valid SSZ-LIGO model must describe how SSZ affects source-frame emission, propagation,
phase transport, polarization/twist, detector projection, and calibrated strain.
The relevant target is `h_SSZ(f)`, not a Kerr-derived posterior table.

---

### 9. Phase Transport and Co-Scaling

If the detector, arms, optics, and local rulers co-scale, a pure local scale factor is
not directly observable. What is observable is the relative phase accumulated by photons:
`DeltaPhi = Phi_x - Phi_y`. Therefore SSZ-LIGO must be formulated as a phase-transport /
relative-holonomy problem. The local arm-length correction was found to be negligible.

The relevant signal chain:

```text
source / strong-field geometry
  -> SSZ scale and twist
  -> propagation
  -> polarization / phase transport
  -> detector projection
  -> strain residual
```

---

### 10. Source-Propagation Twist Branch

```text
[h_plus_SSZ, h_cross_SSZ]^T  =  S(f) * R(theta) * [h_plus_GR, h_cross_GR]^T
```

where `S(f)` = scale contribution, `R(theta)` = polarization/phase/frame twist.

```text
SOURCE_PROPAGATION_TWIST: synthetic pass
REAL_TWIST_SIGNAL:        not extractable from current GW240925 run
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```

---

### 11. What the Current Data Can and Cannot Be Used For

**Can be used for:**
`pipeline construction` / `PSD estimation` / `H1/L1 diagnostics` / `Gaussianity tests`
`line/notch analysis` / `STFT/Omicron-lite` / `background estimates`
`H1-only exploratory tests` / `synthetic SSZ validation` / `methodological demonstrations`

**Cannot currently be used for:**
`a final SSZ claim` / `a final SSZ falsification` / `a metric-neutral QNM test`
`a claim-level H1/L1 non-GR coherence test without offline DQ/Omicron/iDQ`

---

### 12. What We Need from LIGO — And the Reproducibility Gap

**For our specific non-GR test:**

```text
Omicron triggers for the relevant GPS windows
iDQ information and offline DQ reports
line lists and known instrumental couplings
auxiliary-channel context
calibration uncertainty context
state-vector interpretation
detector-characterization notes for the 20-100 Hz band
```

Concise question to LIGO:

> "For our non-Kerr forward-model diagnostic, the public GWOSC strain products are useful but insufficient at claim level without additional DQ/Omicron/iDQ/auxiliary/line/preprocessing context. In our GW240925 test, the L1 20–100 Hz SSZ-SNR metric is not trigger-specific: trigger ≈ off-source mean. Are offline DQ/iDQ/Omicron/line products available for this GPS window, or should L1 remain diagnostic-only for this type of non-GR forward test?"
> 
> *(Ref: LIGO Mastodon response, Dec 2025: [chaos.social](https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654))*

**Broader reproducibility and provenance limitation:**

The limitation extends beyond our specific test. GWOSC releases provide calibrated
strain, DQ segments, and posteriors — but not the full calibration chain required for a
fundamentally independent external reconstruction of h(t).

This was confirmed directly by LIGO in a public exchange (Mastodon, December 2025):

> "Our full data management policy [...] covers calibrated data, not auxiliary channels."
> — LIGO @scicomm.xyz, 3 Dec 2025 [[source]](https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654)

The missing components for full external reproducibility:

```text
PCal (Photon Calibrator) raw channels and injected waveform data
DARM error and control signals
Time-dependent FIR/IIR filter coefficient archives
CalibEnv / calibration model files (epoch-by-epoch)
Full auxiliary channel data via public API
```

Central distinction:

```text
Open Data Product  !=  Fully reproducible measurement chain
```

**Code provenance and migration:**

The `bilby` Bayesian inference library (core LVK analysis tool) changelog explicitly
documents migration from the internal LIGO GitLab to GitHub, with the original merge
requests remaining non-public:

> "Migration from LIGO GitLab to GitHub. Old merge requests are only visible on the
> LIGO GitLab."
> — [bilby CHANGELOG.md](https://github.com/bilby-dev/bilby/blob/main/CHANGELOG.md)

If published papers cite code versions whose development history (merge requests, review
threads, parameter decisions) is not publicly accessible, external full-chain audit is
structurally incomplete — independent of whether the current code is open.

**Scale of the gap:**

The O4a documentation states calibrated strain is ~4 TB/year per instrument. Total
detector data with all diagnostic channels is **several PB/year**. GWOSC releases a
small, pre-processed subset: channels named `CLEAN`, `NOLINES`, `AR` are already
noise-subtracted and analysis-ready — not raw observables.

```text
GWOSC releases:        ~4 TB/yr/instrument — pre-processed, analysis-ready
Total recorded data:   PB-scale, 10^5+ channels — not publicly available
```

The calibration question was raised publicly in 2016 in a petition (3,028 verified
signatures) asking where the photon-calibrator data — strain as a function of laser power
— from the GW150914 discovery paper had been published. The cited Reference [63] in
PRL 116, 061102 (2016) was an unpublished e-print containing no data.

A 2020 reproduction study noted explicitly:

> "An exact replication of the original LIGO analysis was not possible because the
> original dataset was not publicly available."
> — arXiv:2010.07244 [[source]](https://arxiv.org/abs/2010.07244)

Ten years after GW150914, a fully independent external reconstruction of the calibration
chain that produced the published h(t) remains practically impossible using only
publicly available data. This is a reproducibility and provenance limitation.

**Full report:** [docs/LIGO_OPEN_DATA_FULL_REPORT.md](docs/LIGO_OPEN_DATA_FULL_REPORT.md)  
**Detailed critique:** [docs/LIGO_REPRODUCIBILITY_CRITIQUE.md](docs/LIGO_REPRODUCIBILITY_CRITIQUE.md)

**Primary sources:**

| Document | Link |
|----------|------|
| IGWN forum: reproducibility request | [ask.igwn.org](https://ask.igwn.org/t/request-for-fully-reproducible-calibration-chain-for-gwosc-strain-data/1397/2) |
| LIGO Mastodon response (Dec 2025) | [chaos.social](https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654) |
| Petition: 3,028 verified signatures | [change.org](https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment?signed=true) |
| LIGO Data Management Plan v31 | [dcc.ligo.org](https://dcc.ligo.org/public/0009/M1000066/031/Data_Management_Plan-v31.pdf) |
| arXiv:1710.09973 — calibrated strain reconstruction | [arxiv.org](https://arxiv.org/abs/1710.09973) |
| arXiv:2412.04638 — iDQ O4 performance | [arxiv.org](https://arxiv.org/abs/2412.04638) |
| arXiv:1311.4898 — template mismodelling | [arxiv.org](https://arxiv.org/abs/1311.4898) |
| arXiv:2101.07743 — mismodelling / PE | [arxiv.org](https://arxiv.org/abs/2101.07743) |
| arXiv:2302.03676 — O3 open data | [arxiv.org](https://arxiv.org/abs/2302.03676) |
| arXiv:2010.07244 — GW150914 reproduction | [arxiv.org](https://arxiv.org/abs/2010.07244) |
| arXiv:2508.18079 — O4a open data | [arxiv.org](https://arxiv.org/abs/2508.18079) |
| LIGO Wikipedia (DE) — Danish group critique | [wikipedia.org](https://de.wikipedia.org/wiki/LIGO) |
| IGWN O3 aux channels release | [ask.igwn.org](https://ask.igwn.org/t/new-data-release-o3-auxiliary-channels/470) |

---

### 13. Public Petition / Transparency Context

**Petition:** [https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment](https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment)

A public petition questioning aspects of the LIGO experiment is not, by itself, scientific
proof that LIGO is wrong. However, it is relevant as a transparency signal.

```text
petition = transparency and trust signal
not:
petition = physical disproof of LIGO
```

This project does not use any petition as evidence against LIGO. It uses the existence
of public scrutiny as evidence that reproducibility limits deserve serious attention.

---

### 14. Political / Funding-Relevant Interpretation

For policymakers: the key issue is an evaluation of public data products. The key issue is whether
publicly funded large-scale science should provide enough data and context for independent
verification outside the collaboration's preferred model family.

Current situation:

```text
Open data:                       yes, in a limited formal sense
Open reproducibility:            only partially
Open alternative-model testing:  strongly limited
```

If public money funds the experiment, then public releases should clearly state: what the
data can prove, what they cannot prove, which products are model-dependent, and which
detector-characterization products are missing. Without that clarity, "open data" can
create an impression of complete openness while leaving decisive non-standard checks
impossible. That is not strong open science.

**Sharpest fair summary:**

> We limit our scope strictly to data-scope, provenance, and methodology. We state that the public GWOSC
> release provides calibrated strain and selected DQ information, but not the full
> detector-characterization context needed to independently resolve the L1 low-frequency
> anomaly for our non-GR forward-model test.

Or in the language of the data layers:

```text
Open data:                       yes, in a limited but useful formal sense
Open standard-analysis reproducibility:  partially yes
Open alternative-model reproducibility:  limited
```

A strong open-science release should clearly state what the data can support,
what they cannot support, which products are model-dependent, and which
detector-characterization products are missing from the public release.
This is a reproducibility and provenance limitation.

---

### 15. Final Position

```text
LIGO strain is real measurement input.
LIGO posterior products are model-dependent outputs.
The public releases are useful but incomplete for anti-circular non-GR tests.
GW240925 is useful for pipeline and artifact-gate development.
GW240925 is not sufficient for a final SSZ test.
L1 remains diagnostic-only without offline DQ/Omicron/iDQ clarification.
No SSZ support claim is made.
No SSZ falsification claim is made.
```

The strongest fair criticism:

> The public LIGO releases are formally open, but not fully open in the sense required
> for independent alternative-metric reproducibility. They allow standard analyses to be
> reproduced, but they do not always provide enough detector-characterization context for
> external groups to independently test non-GR forward models at claim level.

This is the central methodological result of this project.

---

### 16. What We Can and Cannot Say — Precisely

This section separates claims by evidential strength.

**What we can say with confidence:**

```text
1. We built and ran a reproducible, anti-circular LIGO strain pipeline.
2. It uses real H1 GWOSC strain, off-source PSD, an analytic GR control
   template, and a DERIVED_V1 inspiral-only SSZ method component.
3. It does NOT use PE posteriors, PE-derived PSD, or Kerr self-tests.
4. PE/QNM posterior-based R_f tests are methodologically invalid for SSZ
   because posterior products are model-dependent.
5. The anti-circularity gate explicitly marks posterior samples, PE-PSD,
   and pSEOBNR products as invalid inputs; strain, off-source PSD, and
   the DERIVED_V1 inspiral-only SSZ component were used instead.
6. Formal open data is not the same as full open reproducibility.
```

**What we can say about SSZ/LIGO:**

```text
The current DERIVED_V1 inspiral-only strain pipeline produces no measurable deviation
from the GR control template in the tested range:

  delta_lnL ~= 0
  |delta_lnL| < 1  ->  indistinguishable

This does NOT mean SSZ is confirmed.
This does NOT mean SSZ is falsified.
It means:
  With the current DERIVED_V1 inspiral forward component and the limited
  0PN GR control, SSZ is indistinguishable in this setup.
```

**What we can say about GW240925:**

```text
H1: USABLE_EXPLORATORY
L1: DIAGNOSTIC_ONLY
  -> reproducible persistent background noise in the 20-100 Hz band
  -> [Historical 2026-05-19 diagnostic note — superseded by 2026-05-21 off-source background test]
  -> L1_TRIGGER_SPECIFIC: NO
  -> L1_PERSISTENT_NOISE: YES
  -> DQ_CONTEXT_REQUIRED: YES
  -> CLAIM_LEVEL_LIGO: NO
  -> without Omicron/iDQ/offline DQ: not claimable

GW240925 tests the method. It does not adjudicate SSZ.
```

**What we must not claim:**

```text
- SSZ is confirmed by LIGO.
- SSZ is falsified by LIGO.
- L1 shows SSZ.
- The 39% branch is refuted.
- The current public release is sufficient for a claim-level non-Kerr forward test.
```

**What we may say:**

```text
- The public GWOSC strain products are useful for standard workflows and diagnostics.
- For this alternative-metric forward-test use case, they are insufficient by themselves at claim level because full calibration, DQ, auxiliary, Omicron/iDQ, line and preprocessing context is missing.
- The L1 20–100 Hz SSZ-SNR metric is not trigger-specific and is DQ-blocked for physical interpretation.
```

**Best public short statement:**

> We built an anti-circular strain-level diagnostic pipeline for SSZ-like non-GR forward models. PE/QNM posteriors are not used as metric-neutral observables. For GW240925, the public GWOSC strain data support method diagnostics only. The current DERIVED_V1 inspiral-only SSZ component is technically operational but not LOCKED_FINAL and not claim-level. L1 20–100 Hz is DQ-blocked by the off-source background test.

---

### 17. Paper-Ready Status Statement

> **GW240925 supports method validation, not physical adjudication of SSZ. The strain-level pipeline is reproducible and anti-circular, but the current SSZ component is DERIVED_V1 inspiral-only, not a complete IMR/detector-response model, and L1 is DQ-blocked by persistent off-source background metrics. No SSZ confirmation, no SSZ falsification, no claim-level LIGO test.**

This is the most defensible single-sentence summary of the project's current state.

**The data access hierarchy:**

| Level | What it is | Publicly available | Sufficient for non-GR test |
|-------|-----------|--------------------|--------------------------|
| Level 1: Strain `h(t)` | Calibrated interferometer output | Yes (GWOSC) | Partially |
| Level 2: DQ bits CAT1-3 | Standardized quality flags | Yes (GWOSC) | Partially |
| Level 3: Omicron / iDQ | Glitch triggers, glitch probability | No (internal / AR only) | Yes, critical |
| Level 4: Aux channels | Environmental/control monitors | Very limited | Often needed |
| Level 5: Posteriors, QNM | GR/Kerr model-inferred parameters | Yes (GWOSC) | **NOT metric-neutral** |

The public LIGO release is strong at Level 1-2 and 5, but weak at Level 3-4.
For standard GR/CBC: Level 1-2 is sufficient.
For anti-circular non-GR tests: Level 3-4 is often decisive, and Level 5 is methodologically invalid as input.

---

### 18. Public Criticism and Open-Science Context

**Primary sources (all publicly verifiable):**

| Document | Link |
|----------|------|
| Petition: 3,028 verified signatures (2016) | [change.org](https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment) |
| LIGO Mastodon response (Dec 2025) | [chaos.social](https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654) |
| IGWN forum reproducibility request (Dec 2025) | [ask.igwn.org](https://ask.igwn.org/t/request-for-fully-reproducible-calibration-chain-for-gwosc-strain-data/1397/2) |
| bilby CHANGELOG — GitLab migration | [github.com/bilby-dev/bilby](https://github.com/bilby-dev/bilby/blob/main/CHANGELOG.md) |
| GW150914 reproduction study (2020) | [arXiv:2010.07244](https://arxiv.org/abs/2010.07244) |
| LIGO Data Management Plan v31 | [dcc.ligo.org](https://dcc.ligo.org/public/0009/M1000066/031/Data_Management_Plan-v31.pdf) |

**The 2016 petition — three concrete calibration questions:**

The petition raised three precise, technical questions addressed to Prof. Karsten Danzmann:

1. Where are the photon-calibrator data (strain as function of laser power) from GW150914
   published? Reference [63] in PRL 116, 061102 (2016) was an unpublished e-print with no data.
2. The PCal method was last documented in 2003 (LIGO-T030266-00-D, Bruursema) achieving
   ~10⁻¹⁵ m excursions. GW150914 required ~10⁻¹⁸ m. Was this method re-applied and documented?
3. If not, is there a plan to do so retroactively?

These are **specific, traceable calibration questions** — not conspiracy claims. Their absence
of complete public answers over ten years is a documented open-science gap, a material reproducibility and provenance limitation.

**The epistemic asymmetry:**

GWOSC is a genuine public service. The data release is real. But there is a structural gap:

```text
Formally available:   calibrated strain, DQ segments, GR/CBC posteriors
Not available:        PCal channels, DARM signals, FIR/IIR filter archives,
                      CalibEnv files, full aux channels, Omicron/iDQ,
                      offline DQ, pre-migration code merge requests
```

This means:

- **Standard GR/CBC analyses:** fully supported by public data
- **Non-GR forward-model tests:** partially supported — decisive context is missing
- **Full independent calibration audit:** structurally impossible from public data alone

For policymakers and funders: the question is not about intent or institutional wrongdoing. It is whether
a publicly funded, Nobel Prize-winning experiment provides enough material for independent
verification **outside its own model family**. Currently, it does not.

**Strongest fair single statement:**

> **The public GWOSC strain products are useful for standard reproducibility exercises and diagnostic studies, but they are not sufficient for a claim-level independent SSZ test. The missing full calibration, DQ, auxiliary-channel and preprocessing provenance prevents a unique physical interpretation of persistent L1 excess metrics.**
>
> *Die öffentlichen GWOSC-Strain-Produkte sind für Standard-Reproduktion und Diagnostik nutzbar, aber nicht ausreichend für einen claimfähigen unabhängigen SSZ-Test. Die fehlende vollständige Kalibrations-, DQ-, Auxiliary- und Preprocessing-Provenienz verhindert eine eindeutige physikalische Interpretation der persistenten L1-Exzessmetriken.*

This is a reproducibility and provenance limitation.

---

## License

ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## Related Repositories

- [ssz-complete-documentation](https://github.com/error-wtf/ssz-complete-documentation)
- [ssz-all-tests](https://github.com/error-wtf/ssz-all-tests)
- [ssz-metric-pure](https://github.com/error-wtf/ssz-metric-pure)
- [ssz-qubits](https://github.com/error-wtf/ssz-qubits)

---

*Part of the SSZ (Segmented Spacetime) research project.*

---

## GitHub Search, Tags & SEO Optimization

If you are the repository owner, you can dramatically increase the visibility of this project on GitHub by adding these optimized **Topics/Tags** in your repository settings:

### Copy-Paste Topics (Tags) for GitHub Repository Settings:
```text
ssz, ligo, gravitational-waves, ssz-ligo, ligo-open-data, gwos, zenodo, astrophysics, physics, spacetime, gw240925, gw250207, black-holes, pytest, data-audit, open-science, reproducibility, calibration, data-provenance, einstein-telescope
```

### Search Keywords & Synonyms Indexed:
- **SSZ Theory:** Segmented Spacetime, Segmentierte Raumzeit, SSZ Forward Model, SSZ likelihood, SSZ strain, SSZ waveform.
- **LIGO Data:** Gravitational Wave Open Science Center (GWOSC), GWOSC strain, LIGO HDF5, H1, L1, V1 Hanford Livingston Virgo detectors.
- **Events:** GW240925, GW250207, O4b public data release.
- **Physics Concepts:** General Relativity (GR), Kerr metric, non-Kerr spacetime, alternative gravity, photon phase transport, geometric algebra interferometer.
- **Analysis & Testing:** Matched filter SNR, log-likelihood, Welch PSD, pytest validation, anti-circularity protocol.
- **Open Science Critique:** Calibration chain, PCal photon calibrator, DARM error, Bilby codebase migration, raw data provenance, reproducibility gap.
