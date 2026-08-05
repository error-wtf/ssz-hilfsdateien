# Technical Briefing (Scope & Internal Correctness)

Goal
- Provide a deterministic, no-fit evaluation of the SST projection model ("SSZ") on redshift data, and a covariant smoke-test of the metric ansatz. Baselines: GR, SR, and GR×SR.

Inputs
- `real_data_full.csv` (67 rows). Tools accept either a `z` column or frequency columns `f_emit_Hz` / `f_obs_Hz` (helpers can auto-detect).

Determinism and Provenance
- Fixed seeds; no parameter fitting anywhere.
- Model choices are fixed: phi/2 coupling and a mass-correction term Delta(M) with constants A=98.01, B=1.96, ALPHA=27177.0.
- Runners print SHA256 for both the CSV and the main module so results can be pinned to exact artifacts.

Core Scripts
- `run_all_ssz_terminal.py` — evaluates redshift errors, mass-binned medians, paired sign-test; emits a summary JSON.
- `ssz_covariant_smoketest_verbose_lino_casu.py` — checks PPN limits, classic weak-field GR tests, and strong-field invariants (photon sphere, shadow impact parameter, ISCO); prints acceptance checks.
- `shadow_predictions_exact.py` — prints spin-independent showcase shadow diameters for Sgr A* and M87* (with the masses/distances it echoes).
- `compute_vfall_from_z.py`, `phi_test.py` — v_fall / phi-lattice checks from either `z` or the pair (`f_emit_Hz`, `f_obs_Hz`).
- Consistency/self-tests: `test_ppn_exact.py`, `test_c1_segments.py`, `test_c2_segments_strict.py`, `test_energy_conditions.py`, `qnm_eikonal.py`.

Verified Internal Results (from included logs)
- Redshift accuracy (median absolute |Delta z|):
  - SSZ = 0.000131279
  - GR×SR = 0.224705
  - GR = 0.224511
  - SR = 0.0133925  
  Paired sign-test (SSZ vs GR×SR, per-row absolute errors): 66 wins out of 67; two-sided p ≈ 9.22e-19.
- PPN far-field (U -> 0): gamma = 1.000000000000, beta = 1.000000000000 (matches GR to machine precision).
- Weak-field (Sun): light deflection, Shapiro delay, and Mercury perihelion match GR with relative delta 0.
- Strong-field (finite values): photon sphere ~ GR; shadow impact parameter relative delta ~ 6.066%; ISCO relative delta ~ 5.079%.
- Shadow diameters (showcase): Sgr A* = 53.255 microarcseconds; M87* = 39.689 microarcseconds.
- Energy conditions: violations inside a few Schwarzschild radii; Weak/Null/Dominant/Strong energy conditions hold for r >= 5 r_s per `test_energy_conditions.py`.

Outputs
- Human-readable console logs and a machine-readable `full_pipeline/reports/summary_full_terminal_v3.json` plus per-tool output folders.

Run Notes
- Use relative paths in documentation and commands (the scripts print absolute paths and SHA256 at runtime for provenance).
- In PowerShell, use the backtick ` for line continuation (not the backslash). Changing the CSV or code will change the printed SHA256 and results.

---

# What This Repository Is (and Is Not)

This repository **is**:
- A reproducible evaluation harness for the SST/SSZ projection approach to redshift plus a covariant smoke-test of its metric ansatz, with deterministic scripts and printed provenance.
- A phenomenological, numerically consistent package that:
  - reproduces PPN gamma = beta = 1 and classic weak-field GR tests,
  - reports explicit strong-field deltas (shadow impact, ISCO) and prints showcase shadow diameters,
  - performs no fitting and uses fixed phi/2 coupling together with a fixed Delta(M).
- A starting point for independent reruns and for building pre-registered tests (for example, likelihood-level comparisons to EHT pipelines), with canonical commands and expected key outputs documented.

This repository **is not**:
- A complete Lagrangian field theory or a peer-reviewed publication stack.
- A claim of intrinsic variation of fundamental constants. The code implements an effective projection via alpha_loc or P(N, phi) at fixed alpha_0.

