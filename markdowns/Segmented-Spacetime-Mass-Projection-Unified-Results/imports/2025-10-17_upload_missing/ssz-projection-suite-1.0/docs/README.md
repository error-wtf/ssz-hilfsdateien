<img width="2400" height="1000" alt="segspace_comparison" src="https://github.com/user-attachments/assets/69e3e20d-6815-4a44-8d08-57ad646b96c5" />

# Segmented Spacetime – Mass Projection & Unified Results
© Carmen Wrede & Lino Casu

This repository contains a complete Python implementation and verification suite for the **Segmented Spacetime (SSZ) Mass Projection Model**. It ships runners, tests, datasets, and plotting routines to reproduce all reported results in a deterministic environment.

Status: Reproducible evidence of model functionality (theory + code + tests).  
Note: This is not a formal proof; independent replication and peer review are encouraged.

---

## Reproducibility — One-Click Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/SSZ_Colab_AutoRunner.ipynb)

This Colab runs our **deterministic SSZ pipeline** end-to-end (no fitting).
It fetches the pinned dataset, verifies checksums, runs the same scripts as `run_all_ssz_terminal.py`,
and **asserts** the key results (PPN=1, mass roundtrip≈0 error, φ-lattice BIC win, S-stars z-matching, dual-velocity invariant).

**Pinned input**
- `real_data_full.csv` — SHA256: `c6b503e14a822dbc465e0aae280255d33d602a8482f6136c0e2a4bceffb3f717`

**Quality gate (expected)**
- Paired sign-test: SEG better **≥ 66/67**, two-sided p ≤ `1e-18`
- PPN: β=1, γ=1 with |Δ| < `1e-12`
- Mass roundtrip: max relative error ≤ `1e-42` (numerical zero)
- φ-lattice evidence: ΔBIC (uniform − lattice) ≥ `+100`
- Dual invariant: max |(v_esc·v_fall)/c² − 1| ≤ `1e-15`
- Energy conditions: WEC/DEC/SEC hold for r/rs ≥ `~5`

---

## SSZ autorunner — quick start

Deterministic. No curve fitting. Prints SHA-256 of dataset, code, and runner. Writes a JSON summary.

```bash
python run_all_ssz_terminal.py
# Output: verbose terminal log + JSON at full_pipeline/reports/summary_full_terminal_v3.json
```

Optional artifacts:
```bash
python run_all_ssz_terminal.py --save-raws --plots
# CSV:   full_pipeline/reports/raws_full.csv
# Plots: full_pipeline/figures/
```

---

## Technical briefing (scope & internal correctness)

**What the SSZ projection variant is.**  
SSZ models spacetime as discrete segmentation and predicts observables via a **local projection parameter** (`alpha_loc`) in place of explicit metric curvature. In this repository it is a **phenomenology** designed to recover weak‑field tests and to generate strong‑field observables for comparison.

**What the code demonstrates (in‑repo).**
- **Weak‑field parity with GR:** `ssz_covariant_smoketest_verbose_lino_casu.py` reports PPN γ=1 and β=1 and reproduces light deflection, Shapiro delay, and Mercury perihelion numerically equal to GR. Note: the symbol β used elsewhere in SSZ is not PPN‑β.
- **Curated redshift comparisons:** `run_all_ssz_terminal.py` evaluates the SSZ projection with robust noise estimates (MAD) and a Chauvenet filter, logging MAE, ΔBIC/AIC, and an exact paired sign‑test. Seeds and SHA‑256 hashes are printed.
- **Strong‑field curves:** `shadow_predictions_exact.py` outputs analytic shadow diameters for Sgr A* and M87* for downstream EHT‑style comparisons.

**Internal consistency checks.**  
All runs are deterministic (fixed seeds). Inputs and modules are checksummed. Utility tests verify algebraic identities, such as escape/fall duality, within numerical tolerance.

---

## What this repository is

* A reproducible reference implementation of SSZ projection tests with a deterministic runner (`run_all_ssz_terminal.py`) and machine-readable reports.
* A battery of physics checks spanning weak- and strong-field regimes (PPN tests, light bending, Shapiro delay, perihelion precession; photon sphere/ISCO; QNM eikonal; shadow predictions).
* Geodesic/Lagrangian tests (no fitting): null & timelike circular orbits, orbital frequencies.
* Energy conditions: WEC/DEC/SEC evaluated for the metric; controlled violations only inside a few Schwarzschild radii.
* Dual-velocity invariant: verifies that escape-velocity × fall-velocity ≈ c² within numerical precision.
* Mass validation: round-trip/Newton inversion across 30+ astrophysical objects plus the electron with negligible numerical error.
* Redshift benchmarks: paired sign-tests vs. curated data; SSZ wins in the vast majority of pairs; detailed per-row explainers for S-stars.
* Effective stress–energy (diagnostic): reverse-engineers a conserved effective T(mu,nu) for the chosen static, spherically symmetric metric; compact symbolic rho(r), p_r(r), p_t(r); divergence check ~ 0.
* Action-based scalar (exterior, experimental): SSS module with anisotropic kinetic weight Z_parallel(phi) that generates the pressure anisotropy from an action. Numerically stabilized (caps, log-radius grid, horizon guard). CSV export with key diagnostics.
* A research artifact for independent re-runs, ablations, and plug-in comparisons; a living workspace for CI, curated datasets, and benchmark extensions.

## What this repository is not

* Not a complete field theory. The core repo provides an effective metric, geodesic/Lagrangian tests, and a reverse-engineered, divergence-free effective T(mu,nu) as a diagnostic.  
  The action-based scalar module is exterior-only by default and intended for experiments; it does not claim microphysical completeness or interior stellar modeling.
* Not a claim of intrinsic variation of fundamental constants: `alpha_loc` is a projection parameter for observables.
* Not an assertion about black-hole information release.
* Not a proof of EHT agreement (shadow predictions are included for reference only).
* Not a general-purpose cosmology/astrophysics pipeline beyond the documented tests.

---

## Action-based scalar (exterior and interior) — model & numerics (experimental)

Idea in one sentence: keep Einstein–Hilbert gravity and add a scalar field whose kinetic weight is direction-selective along the radial unit vector; this produces a physically motivated pressure anisotropy (tangential minus radial) proportional to the squared radial gradient of the field.

**Consistency with the Segmented-Spacetime principle.**

This module respects the SSZ projection picture: the metric/kinematics used elsewhere in the repo are unchanged; the anisotropy arises from the matter action via the radial kinetic weight Z_parallel(phi), not from ad-hoc Δ terms. The dual-velocity invariant and all GR/SR comparison tests remain intact; deviations appear only through the scalar’s Δφ and Z(φ) profiles in the exported CSV. Exterior-only by default.

Key properties
- SSS setup; only the radial derivative of the scalar is active.
- Anisotropy generated by Z_parallel(phi); no hand-tuned Δ.
- Stable numerics: smooth caps for phi and phi', log-radius grid (`coord=lnr`), LSODA→Radau fallback, horizon guard.

Quick start (exterior)
```
python ssz_theory_segmented.py --M 1.98847e30 --mode exterior --coord lnr --rmin-mult 1.05 --rmax-mult 12 --grid 200 --rho0 0 --pr0 0 --cs2 0.30 --phi0 1e-4 --phip0 0 --mphi 1e-7 --lam 1e-6 --Z0 1.0 --alpha 3e-3 --beta -8e-3 --phi-cap 5e-3 --phip-cap 1e-3 --Zmin 1e-8 --Zmax 1e8 --max-step-rs 0.02 --export out_theory_exterior.csv
```

Quick start (interior)
```
python ssz_theory_segmented.py --M 1.98847e30 --mode interior --coord lnr --rmin-mult 1.05 --rmax-mult 12 --grid 200 --m0 0 --rho0 1e-18 --pr0 1e-20 --cs2 0.30 --phi0 1e-4 --phip0 0 --mphi 1e-7 --lam 1e-6 --Z0 1.0 --alpha 3e-3 --beta=-8e-3 --phi-cap 5e-3 --phip-cap 1e-3 --Zmin 1e-8 --Zmax 1e8 --max-step-rs 0.02 --abort-on-horizon --horizon-margin 1e-6 --export out_theory_interior.csv
```

---

# Tests and runners — index, commands, acceptance criteria

### 0) SSZ smoketest (covariant, verbose)
**File:** `ssz_covariant_smoketest_verbose_lino_casu.py`  
**Goal:** Verify PPN and classic weak‑field observables without NaN/Inf.  
**Run:**
```bash
python ssz_covariant_smoketest_verbose_lino_casu.py
```
**Accept:** PPN β=1 and γ=1; classic tests match GR; no NaN/Inf.

### 1) PPN exact
**File:** `test_ppn_exact.py`  
**Run:**
```bash
python test_ppn_exact.py
```
**Accept:** |β−1| < 1e‑12 and |γ−1| < 1e‑12.

### 2) C¹ continuity
**File:** `test_c1_segments.py`  
**Run:**
```bash
python test_c1_segments.py
```
**Accept:** C¹ continuity at join radii rL, rR within 1e‑9.

### 3) C² continuity (strict)
**File:** `test_c2_segments_strict.py`  
**Run:**
```bash
python test_c2_segments_strict.py
```
**Accept:** C² at rL, rR; A, A’, A’’ match analytic expectations.

### 4) Energy conditions
**File:** `test_energy_conditions.py`  
**Run:**
```bash
python test_energy_conditions.py
```
**Accept:** WEC/SEC satisfied for r/rs ≥ 5.

### 5) Exact shadow benchmarks (GR, analytic)
**File:** `shadow_predictions_exact.py`  
**Run:**
```bash
python shadow_predictions_exact.py
```
**Inputs:** Sgr A* (M≈4.297e6 M☉, D≈8277 pc), M87* (M≈6.5e9 M☉, D≈16.8 Mpc).  
**Accept:** r_ph=1.5 r_s, b_ph=(3√3/2) r_s; deterministic; scales ∝ M/D.

### 6) BH QNM eikonal check
**File:** `qnm_eikonal.py`  
**Run:**
```bash
python qnm_eikonal.py
```
**Accept:** (Ω_c, λ) match GR’s eikonal relations.

### 7) **v_fall from z** — duality check
**File:** `test_vfall_duality.py`  
**Run:**
```bash
python test_vfall_duality.py --mass Earth --r-mults 1.1,1.2,2,5,10
```
**Accept:** `(v_esc * v_fall)/c^2 → 1` and `gamma_GR(r) = gamma_dual(v_fall)` within numerical precision.

### 8) φ‑lattice tests (model selection)
**Files:** `phi_test.py`, `phi_bic_test.py`  
**Run (examples):**
```bash
python phi_test.py --in real_data_full.csv --outdir out
python phi_bic_test.py --in real_data_full.csv --outdir out \
  --f-emit f_emit_Hz --f-obs f_obs_Hz --tol 1e-3
```
**Accept:** ΔBIC (uniform − lattice) > 0 for φ‑lattice preference; small two‑sided sign‑test p‑value.

### 9) Strict suite T1–T6 (CI‑style)
**File:** `segspace_final_test.py`  
**Run:**
```bash
python segspace_final_test.py --csv real_data_30_segmodel.csv --prefer-z
```
**Outputs (./out/):** `final_test_report.txt`, `final_junit.xml`, `_final_test_debug.csv`, `final_failures.csv`  
**Checks:**  
- T1 Nseg algebra consistency  
- T2 bound‑energy reconstruction (when frequencies are present)  
- T3 Seg‑FIT ≈ 0  
- T4 median |Δz| per category (**requires strong rows**)  
- T5 physicality filters (e.g., v < 0.2c)  
- T6 S‑stars: Seg ≤ 1.2×GR (median |Δz|)

**Strong row requirements:** `a_m` (meters), `e`, `f_true_deg` (degrees), `M_solar` (solar masses).

### 10) Explain runner (provenance audit)
**File:** `segspace_final_explain.py`  
**Run:**
```bash
python segspace_final_explain.py --csv real_data_30_segmodel.csv --prefer-z
```
**Output:** `./out/_explain_debug.csv` showing source of z vs frequency, r_eff path, GR/SR split, and residual composition.

### 11) Comparative runner (hint / deltaM / hybrid)
**File:** `segspace_enhanced_test_better_final.py`  
**Purpose:** Compare SEG vs GR, SR, GR×SR with modes `hint`, `deltaM`, `hybrid`.  
**Run (examples):**
```bash
python segspace_enhanced_test_better_final.py --csv real_data_full.csv --prefer-z --seg-mode hint --plots --junit
python segspace_enhanced_test_better_final.py --csv real_data_full.csv --seg-mode deltaM --deltam-A 3.5 --deltam-B 0.2 --plots
python segspace_enhanced_test_better_final.py --csv real_data_full.csv --seg-mode hybrid --plots --junit
```
**Combination rule:** `(1+z_tot) = (1+z_GR)*(1+z_SR) - 1` in all modes.  
`--prefer-z` forces using z when both z and frequencies are present.

### 12) Mass round‑trip demos and proofs
**Files:** `final_test.py`, `segmented_full_proof.py`, `segmented_full_calc_proof.py`, `segmented_full_compare_proof.py`  
**Run (examples):**
```bash
python final_test.py
python segmented_full_proof.py
python segmented_full_calc_proof.py
python segmented_full_compare_proof.py
```

---

# **v_fall from z** — module details

**Core identities**
- GR redshift: `gamma_GR = 1/sqrt(1 - r_s/r)`  
- Observation: `gamma_obs = 1 + z`  
- Dual Lorentz form: `gamma_dual(v_fall) = 1/sqrt(1 - (c/v_fall)^2)`  
- Set `gamma_dual = gamma_obs` ⇒  
  `v_fall(z) = c / sqrt(1 - 1/(1+z)^2)`  
- Newton/GR link: `v_esc(r) = sqrt(2GM/r)` and `v_esc * v_fall = c^2`

**Script:** `compute_vfall_from_z.py`  
**Function:** Compute `v_fall` per row and check:
- φ‑step residual: `abs(round( ln(1+z)/ln(phi) ) − ln(1+z)/ln(phi))`
- Product test: when `M,r` are present, verify `(v_esc * v_fall)/c^2 ≈ 1`

**Inputs**  
CSV with one of: `z` **or** `f_emit,f_obs` (uses `1+z=f_emit/f_obs`) **or** `ratio=f_emit/f_obs`; optional `M,r` for the product test.

**Examples**
```bash
# use z directly
python compute_vfall_from_z.py --in real_data_full.csv --outdir vfall_out --z-col z

# use frequencies instead of z
python compute_vfall_from_z.py --in real_data_full.csv --outdir vfall_out --f-emit f_emit_Hz --f-obs f_obs_Hz
```

**Console output (typical)**
- `rows used`: after cleaning  
- `abs_residual_median`: median |φ‑step residual| (→0 implies sharper φ‑stepping)  
- `prod_rel_err_median`: median relative error of `v_esc * v_fall = c^2` (0 ⇒ exact)

**Files in `--outdir`**  
`vfall_results.csv`, `vfall_summary.json`, optional plots.

**Additional tests for v_fall**
```bash
python phi_test.py     --in real_data_full.csv --outdir out
python phi_bic_test.py --in real_data_full.csv --outdir out --f-emit f_emit_Hz --f-obs f_obs_Hz --tol 1e-3
python test_vfall_duality.py --mass Earth --r-mults 1.1,1.2,2,5,10
```

**Interpretation**  
`abs_residual_median ≈ 0` → φ‑stepping; `ΔBIC (uniform − lattice) >> 0` → φ‑lattice preferred; `prod_rel_err_median ≈ 0` → `v_esc * v_fall = c^2` holds.

---

## φ‑step metric (quick start)

```bash
python phi_test.py --in real_data_full_filled.csv --outdir agent_out_phi2
python phi_bic_test.py --in real_data_full.csv --outdir out --f-emit f_emit_Hz --f-obs f_obs_Hz --tol 1e-3
python phi_bic_test.py --in real_data_full_filled.csv --outdir out --f-emit f_emit_Hz --f-obs f_obs_Hz --tol 0 --jitter 1e-12 --n-rand 20000
```

---

## Dataset schema (`real_data_full.csv`)

Minimum header (order not strict):
```
case,category,M_solar,a_m,e,P_year,T0_year,f_true_deg,z,f_emit_Hz,f_obs_Hz,
lambda_emit_nm,lambda_obs_nm,v_los_mps,v_tot_mps,z_geom_hint,N0,source,r_emit_m
```
Notes:
- `a_m` is in **meters**.  
- If both `z` and frequencies are present, frequencies win unless `--prefer-z` is set.  
- `z_geom_hint` may contain the GR‑only part.  
- **Strong rows** require `a_m, e, f_true_deg, M_solar`.

**S2 example (2018 pericenter)**
```csv
S2_SgrA*,S-stars,4297000.0,1.530889e+14,0.8843,16.0518,2018.379,0.0,
0.0006671281903963041,,,,,0,,0.0003584,1.0000000028,GRAVITY 2018 Pericenter (z); orbit per table
```

---

## Snapshot model comparison

Median |Δz| (lower is better):
- SEG (φ/2 + Δ(M)): 1.31e‑4
- SR: 1.34e‑2
- GR ≈ GR×SR: 2.25e‑1

Paired comparison: SEG better in 66/67 cases (two‑sided p ≪ 1).  
Mass bins: in all bins SEG < GR×SR.

---

## One‑line repro
```bash
python -m venv .venv && . .venv/bin/activate && pip install -r requirements.txt && python segspace_final_test.py --csv real_data_30_segmodel.csv --prefer-z
```

---

## Full execution (`run_all.py`)

End‑to‑end: optional ESO Brγ fetch → analysis → mass validation → energy bounds.

```bash
# without fetching
python run_all.py --fetch-mode skip --csv real_data_full.csv --out-dir results --prefer-z --top 10

# with fetching (ESO token required)
python run_all.py --fetch-mode full --csv real_data_full.csv --out-dir results --prefer-z --top 10 --token YOUR_ESO_BEARER_TOKEN
```

Clone:
```bash
git clone https://github.com/LinoCasu/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

---

## Environment
```bash
python -m venv venv && source venv/bin/activate     # Windows: venv\Scripts\activate
pip install -r requirements.txt
mkdir -p out
```

---

## All‑in‑one runner (enhanced)

**File:** `segspace_all_in_one_enhanced.py`  
**Purpose:** A consolidated CLI to run typical pipelines without switching scripts.  
**Examples:**
```bash
# Full pipeline
python segspace_all_in_one_enhanced.py all

# Redshift evaluation only (geodesic baseline), with paired stats and plots
python segspace_all_in_one_enhanced.py eval-redshift --csv ".\real_data_full.csv" --mode geodesic --prefer-z --ci 2000 --paired-stats --plots

# Mass validation
python segspace_all_in_one_enhanced.py validate-mass --csv ".\real_data_full.csv"

# Bound energy plots
python segspace_all_in_one_enhanced.py bound-energy --csv ".\real_data_full.csv" --plots
```

---

## Outputs (by convention)

```
agent_out/
  figures/        # hist/ECDF/box plots (when --plots is used)
  reports/
    MANIFEST.json
    mass_validation.csv
    redshift_medians.json
    redshift_cis.json            # when --ci > 0
    redshift_paired_stats.json   # when --paired-stats
    redshift_binned.csv          # when --bins > 0
    bound_energy.txt
  logs/
  data/
```

---

## Complete file list

| File / Dir | Description |
|---|---|
| `run_all.py` | Top‑level runner (sequential). |
| `run_all_ssz_terminal.py` | Deterministic SSZ CLI runner (no fitting). |
| `segspace_all_in_one.py` | Legacy all‑in‑one toolkit. |
| `segspace_all_in_one_enhanced.py` | Enhanced all‑in‑one runner for common tasks. |
| `segspace_all_in_one_extended.py` | Extended v2 pipeline (legacy). |
| `segspace_final_test.py` | T1–T6 strict suite, writes report + JUnit + debug CSV. |
| `segspace_final_explain.py` | Per‑row provenance audit. |
| `segspace_enhanced_test_better_final.py` | Comparative SEG vs GR/SR/GR×SR runner. |
| `segspacetime_quick_tests.py` | Convenience wrapper. |
| `phi_test.py` | φ‑step residuals and summary. |
| `phi_bic_test.py` | ΔBIC (uniform vs φ‑lattice) + sign tests. |
| `compute_vfall_from_z.py` | **v_fall** computation and `v_esc * v_fall = c^2` check. |
| `test_vfall_duality.py` | γ‑duality and product test. |
| `ssz_covariant_smoketest_verbose_lino_casu.py` | Covariant SSZ smoketest. |
| `ssz_covariant_smoketest_ext.py` | Extended smoketest. |
| `test_ppn_exact.py` | PPN β=1, γ=1. |
| `test_c1_segments.py` | C¹ continuity at joins. |
| `test_c2_segments_strict.py` | C² continuity at joins. |
| `test_energy_conditions.py` | WEC/SEC checks. |
| `shadow_predictions_exact.py` | Exact shadow sizes (Sgr A*, M87*). |
| `qnm_eikonal.py` | Eikonal QNM check. |
| `segmented_full_proof.py` | Proof/round‑trip routines. |
| `segmented_full_calc_proof.py` | Calculation trace. |
| `segmented_full_compare_proof.py` | Proof comparison. |
| `segmented_mass.py` | Mass inversion utilities. |
| `bound_energy.py` | Bound‑energy derivation. |
| `bound_energy_english.py` | Simplified bound‑energy demo. |
| `bound_energy_plot.py` | Bound‑energy comparisons; CSV + plot. |
| `bound_energy_plot_with_frequenz_shift_fix.py` | Bound‑energy with emission‑frequency shift fix. |
| `paper.py` | Reproduces numeric example from bound‑energy paper. |
| `check.py` | Fine‑structure‑constant checks. |
| `calculation_test.py` | Sanity checks for basic calculations. |
| `complete-math.py` | Collated formula path. |
| `Segmentdichte-Analyse.py` | Segment density profile σ(r). |
| `vergleich.py` | Comparison chart. |
| `vergleich_2.py` | Updated comparison chart. |
| `real_data_full.csv` | Master dataset. |
| `bound_energy_results.csv` | Bound‑energy results. |
| `bound_energy_with_deltaM.csv` | Bound‑energy with Δ(M). |
| `segmented_spacetime_mass_validation*.csv` | Mass validation tables. |
| `segment_mass_results.csv` | Per‑object mass/segment outputs. |
| `README.md` | Project overview & quickstart. |
| `API.md` | Public API of scripts/modules. |
| `commands.md` | Usage guide. |
| `DATA_SOURCE(S).md` | Data provenance. |
| `Sources.md` | External sources and links. |
| `CITATION.cff` | Citation metadata. |
| `requirements.txt`, `requirements-freeze.txt` | Dependencies and pinned environment. |
| `.github/workflows/ci.yml` | CI workflow. |

---

## Independent replication call

Environment: Python 3.11  
One‑command run:
```
python ssz_covariant_smoketest_verbose_lino_casu.py && python test_ppn_exact.py && python test_c1_segments.py && python test_energy_conditions.py && python shadow_predictions_exact.py && python qnm_eikonal.py && python test_c2_segments_strict.py
```
Expected: PPN β=1, γ=1; Sgr A* shadow ~53.255 µas; M87* ~39.689 µas; no NaN/Inf. Please report OS/CPU/Python/results.

---

## Notes on reproducibility

- Deterministic execution. PPN far‑field unchanged (β=γ=1).  
- Runs print SHA‑256 hashes of dataset, code, and runner.  
- Please report OS/CPU/Python when replicating.

---

**License:** ANTI‑CAPITALIST SOFTWARE LICENSE (v 1.4).

**End.**



