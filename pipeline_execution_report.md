# Consolidated Physics Pipeline Execution Report

Generated on: Wed Jul  1 02:00:31 CEST 2026

## CALCULATION_OF_NUMBER_PI
- **Entry Point:** `python3 fibonaci.py`
- **Status:** `SUCCESS`
---

## LOST_EINSTEIN_PAPERS
- **Entry Point:** `python3 einstein_primary_preserver.py --help`
- **Status:** `SUCCESS`
### Standard Output:
```text
usage: einstein_primary_preserver.py [-h] --biblio BIBLIO --out OUT
                                     [--concurrency CONCURRENCY]
                                     [--timeout TIMEOUT] [--retries RETRIES]
                                     [--delay DELAY] [--allow-licensed]
                                     [--use-browser]
                                     [--max-downloads MAX_DOWNLOADS]
                                     [--insecure] [--accept-scan-only]
                                     [--trust-host TRUST_HOST]

Einstein Primary-Only Preserver (Trusted-Scan Patch)

options:
  -h, --help            show this help message and exit
  --biblio BIBLIO       CSV/JSONL with title,year,doi,bibcode,url_hint
  --out OUT             Output directory
  --concurrency CONCURRENCY
  --timeout TIMEOUT
  --retries RETRIES
  --delay DELAY
  --allow-licensed      Allow licensed primary hosts (JSTOR/Springer)
  --use-browser         Use Playwright to capture real PDF downloads
  --max-downloads MAX_DOWNLOADS
                        Limit number of items (0 = no limit)
  --insecure            Skip TLS verification (not recommended)
  --accept-scan-only    Accept image-only PDFs from trusted hosts (if page
                        count sane)
  --trust-host TRUST_HOST
                        Mark a host as trusted for scan-only acceptance; can
                        be repeated
```
---

## Riemann-Zeta-Zero-Finding-Suite
- **Entry Point:** `python3 turing_check_few_data_demo_test.py --help`
- **Status:** `SUCCESS`
### Standard Output:
```text
usage: turing_check_few_data_demo_test.py [-h] --zeros-root ZEROS_ROOT --T0 T0
                                          --T1 T1 [--steps STEPS] [--no-clamp]
                                          [--bins BINS] [--csv CSV] [--no-S]

Turing-like zero count check (robust).

options:
  -h, --help            show this help message and exit
  --zeros-root ZEROS_ROOT
  --T0 T0
  --T1 T1
  --steps STEPS         Grundraster für S(T)-Unwrap.
  --no-clamp            Nicht auf T_max kappen, selbst wenn T1 > T_max ist.
  --bins BINS           Wenn >0: [T0,T1] in so viele Bins teilen und pro Bin
                        prüfen.
  --csv CSV             Optional: CSV-Report schreiben.
  --no-S                S(T) ignorieren (nur Hauptterm).
```
---

## SEGMENTED_SPACETIME
- **Entry Point:** `echo Documentation/Data repository - No execution required`
- **Status:** `SUCCESS`
### Standard Output:
```text
Documentation/Data repository - No execution required
```
---

## SSZ-HOW-TO-BEAM
- **Entry Point:** `python3 run_all_tests.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
================================================================================
SSZ-HOW-TO-BEAM v1.1.0-canonical - Comprehensive Test Runner
================================================================================


================================================================================
Generating report...
================================================================================

================================================================================
✅ ALL TESTS PASSED - v1.1.0-canonical FRAMEWORK READY (physics incomplete)
================================================================================

Full report saved to: FULL_REPORT.md
```
---

## SSZ-METRIC_COMPLETE
- **Entry Point:** `python3 run_all_tests.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
================================================================================
SSZ-METRIC-PURE v1.1.0-canonical-pure - COMPREHENSIVE TEST SUITE
================================================================================


--------------------------------------------------------------------------------
Running: Package Installation and Imports
--------------------------------------------------------------------------------
---------------------------------------- LIVE TEST OUTPUT ----------------------------------------
[OK] Anti-Faker blocker installed - faker is FORBIDDEN in this project
============================= test session starts ==============================
platform linux -- Python 3.13.2, pytest-9.1.1, pluggy-1.5.0 -- /root/miniconda3/bin/python3
cachedir: .pytest_cache
rootdir: /home/error/physics/SSZ-METRIC_COMPLETE
configfile: pyproject.toml
plugins: anyio-4.10.0
collecting ... collected 1 item

tests/test_package_import.py::test_package_import   Package version: 1.1.0-canonical-pure
  xi_canonical available: True
  D_from_xi available: True
  s_from_xi available: True
PASSED

============================== 1 passed in 2.01s ===============================
----------------------------------------------------------------------------------------
[OK] Package Installation and Imports: PASSED (1 tests)

--------------------------------------------------------------------------------
Running: Canonical Xi Primary Principles
--------------------------------------------------------------------------------
---------------------------------------- LIVE TEST OUTPUT ----------------------------------------
[OK] Anti-Faker blocker installed - faker is FORBIDDEN in this project
============================= test session starts ==============================
platform linux -- Python 3.13.2, pytest-9.1.1, pluggy-1.5.0 -- /root/miniconda3/bin/python3
cachedir: .pytest_cache
rootdir: /home/error/physics/SSZ-METRIC_COMPLETE
configfile: pyproject.toml
plugins: an
```
---

## Segmented-Spacetime-Mass-Projection-Unified-Results
- **Entry Point:** `python3 run_ssz_validation.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
================================================================================
SSZ vs GR VALIDATION SUITE
================================================================================

[1/6] Computing universal intersection point...
  r*/r_s = 1.594811
  D* = 0.610710
  Ξ* = 0.637439
  ✓ r*/r_s in range: True (|0.000000| < 0.01)
  ✓ D* in range: True (|-0.000000| < 0.01)
  ✓ Saved: gr_ssz_intersection_summary.json
  ✓ Saved: gr_ssz_intersection_points.csv

[2/6] Neutron star comparison (14% effect)...
  Max |delta| = -0.1367 at r/r_s = 3.31
  ~14% region (±3%): r/r_s in [2.21, 5.00]
  ✓ Saved: gr_vs_ssz_ns.csv

[3/6] Sensitivity analysis...
  Tested 81 parameter combinations
  Valid intersections: 81
  ✓ Saved: gr_ssz_sensitivity.csv

[4/6] Generating plots...
  ✓ Saved: gr_ssz_time_dilation_plot.png
  ✓ Saved: gr_vs_ssz_ns.png
  ✓ Saved: gr_ssz_sensitivity_map.png

[5/6] Generating validation summary...
  ✓ Saved: validation.json

[6/6] Generating Markdown report...
  ✓ Saved: SSZ_VALIDATION_SUMMARY.md

================================================================================
VALIDATION COMPLETE
================================================================================

Overall Status: ✅ PASSED

Generated Files:
  - COMPLETE_SSZ_VALIDATION.json (0.00 MB)
  - COMPLETE_TEST_SUMMARY.md (0.00 MB)
  - COMPLETE_VALIDATION_SUMMARY.md (0.00 MB)
  - OUTPUTS_INDEX.md (0.01 MB)
  - SSZ_SCIENTIFIC_INTERPRETATIONS.md (0.02 MB)
  - SSZ_VALIDATION_SUMMARY.md (0.00 MB)
  - TEST_INTERPRETATIONS.md (0.00 MB)
  - complete_test_results.json (0.02 MB)
  - debug_alpha_sweep.png (0.07 MB)
  - gr_ssz_audio_tracks (0.00 MB)
  - gr_ssz_intersection.gif (0.00 MB)
  - gr_ssz_intersection_neutron_star_2_mmsun.png (0.13 MB)
  - gr_ssz_intersection_points.csv (0.34 MB)
  - gr_ssz_intersection_sgr_a_4p1x10_mmsun.png (0.13 MB)
  - gr_ssz_intersection_summary.json (0.00 MB)
  - gr_ssz_intersection_summary.md (0.00 MB)
  - gr_ssz_sensitivity.csv (0.00 MB)
  - gr_ssz_sensitivity_map
```
---

## Segmented-Spacetime-Starmaps
- **Entry Point:** `python3 -c import test_gradio_physics; print('Gradio Interface successfully loaded without launching server.')`
- **Status:** `TIMEOUT`
### Error Output:
```text
/home/error/physics/Segmented-Spacetime-Starmaps/test_gradio_physics.py:38: UserWarning: The parameters have been moved from the Blocks constructor to the launch() method in Gradio 6.0: theme. Please pass these parameters to launch() instead.
  with gr.Blocks(theme=gr.themes.Soft()) as demo:
```
---

## chord-partition
- **Entry Point:** `python3 test_chord_partition_modes.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
=================================================================
CHORD-PARTITION EIGENMODES - SSZ TEST SUITE
=================================================================

[TestClosure]
  [SKIP] test_closure (parametrized)
  [SKIP] test_no_self_intersection_at_origin (parametrized)
  [SKIP] test_period_formula (parametrized)

[TestDerivatives]
  [SKIP] test_derivative_finite (parametrized)
  [SKIP] test_higher_modes_have_higher_curvature (parametrized)
  [SKIP] test_periodic_derivative (parametrized)

[TestEigenmodes]
  [PASS] test_circle_eigenmode
  [SKIP] test_eigenmode_index_positive (parametrized)
  [PASS] test_lissajous_2_3_eigenmode
  [PASS] test_winding_consistent
  [SKIP] test_winding_integers (parametrized)

[TestPhiResonance]
  [PASS] test_fib_13_21_phi_approx
  [PASS] test_fib_8_13_phi_approx
  [PASS] test_fibonacci_pair_closest_to_phi
  [SKIP] test_fibonacci_pairs_decreasing_resonance (parametrized)
  [PASS] test_phi_adjacent_modes_exist
  [PASS] test_phi_value

[TestPerimeter]
  [PASS] test_circle_perimeter
  [SKIP] test_perimeter_positive (parametrized)
  [SKIP] test_perimeter_scales_with_R (parametrized)

[TestStability]
  [PASS] test_circle_most_stable
  [PASS] test_stability_decreases_with_complexity
  [SKIP] test_stability_positive (parametrized)

[TestNumerical]
  [PASS] test_coprime_modes_close
  [PASS] test_large_winding
  [SKIP] test_radius_scaling_closure (parametrized)
  [PASS] test_same_winding_circle

[TestSSZConstants]
  [PASS] test_d_min
  [PASS] test_phi_reciprocal
  [PASS] test_phi_squared
  [PASS] test_r_star_over_rs
  [PASS] test_xi_max

=================================================================
TOTAL: 32 run | 19 PASS | 0 FAIL
=================================================================
```
---

## claudes-cycles
- **Entry Point:** `python3 test_claudes_cycles.py`
- **Status:** `SUCCESS`
---

## counterexample-commons
- **Entry Point:** `python3 app/main.py`
- **Status:** `SUCCESS`
---

## emergent-spacetime
- **Entry Point:** `python3 Temporal_Interference_Code.py`
- **Status:** `SUCCESS`
---

## frequency-curvature-validation
- **Entry Point:** `python3 run_all_tests.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
============================= test session starts ==============================
platform linux -- Python 3.13.2, pytest-9.1.1, pluggy-1.5.0 -- /root/miniconda3/bin/python3
cachedir: .pytest_cache
rootdir: /home/error/physics/frequency-curvature-validation
plugins: anyio-4.10.0
collecting ... collected 64 items

tests/test_dynamic_loops.py::test_gravity_probe_a_dynamic PASSED         [  1%]
tests/test_dynamic_loops.py::test_galileo_eccentric_dynamic PASSED       [  3%]
tests/test_dynamic_loops.py::test_iss_gps_ground_dynamic PASSED          [  4%]
tests/test_dynamic_loops.py::test_path_integral_independence PASSED      [  6%]
tests/test_nsr_ngr_separation.py::test_nsr_removal_by_frame_change PASSED [  7%]
tests/test_nsr_ngr_separation.py::test_ngr_persistence PASSED            [  9%]
tests/test_nsr_ngr_separation.py::test_loop_closure_with_separation PASSED [ 10%]
tests/test_nsr_ngr_separation.py::test_ngr_equals_xi PASSED              [ 12%]
tests/test_section2_constant_frequency.py::test_constant_proper_frequency PASSED [ 14%]
tests/test_section2_constant_frequency.py::test_delta_dimensionless PASSED [ 15%]
tests/test_section2_constant_frequency.py::test_delta_additivity PASSED  [ 17%]
tests/test_section2_constant_frequency.py::test_delta_antisymmetry PASSED [ 18%]
tests/test_section2_constant_frequency.py::test_delta_self_comparison PASSED [ 20%]
tests/test_section3_first_order_shifts.py::test_gravity_probe_a PASSED   [ 21%]
tests/test_section3_first_order_shifts.py::test_galileo_eccentric_orbit PASSED [ 23%]
tests/test_section3_first_order_shifts.py::test_pound_rebka_prediction PASSED [ 25%]
tests/test_section3_first_order_shifts.py::test_first_order_frame_absorbable PASSED [ 26%]
tests/test_section3_first_order_shifts.py::test_gps_relativistic_correction PASSED [ 28%]
tests/test_section4_differences_of_differences.py::test_flat_spacetime_loop_closure PASSED [ 29%]
tests/test_section4_differences_of_differences.py::test_loop_closure_mathematical_identity PASSED 
```
---

## g79-cygnus-tests
- **Entry Point:** `python3 TEST_TEMPERATURE_EQUATIONS_COMPLETE.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
================================================================================
TEMPERATURE EQUATIONS TEST SUITE
Segmented Spacetime Framework
================================================================================

[TEST 1/6] Temporal Density Function γ_seg(r) [Eq. 10]
--------------------------------------------------------------------------------
Parameters:
  α = 0.120 ± 0.030
  r_c = 1.9 pc

Results:
  γ_seg(0) = 0.8800 (inner core)
  γ_seg(r_c) = 0.9559 (characteristic radius)
  γ_seg(5 pc) = 0.9999 (outer shell)

Physical Interpretation:
  • Regions with γ_seg < 1 experience slower time flow
  • Minimum γ_seg = 0.8803 at r ≈ 0
  • Temporal compression factor: 1.14×
✓ Plot saved: Eq10_gamma_seg.png

[TEST 2/6] Basic Temperature Profile T(r) [Eq. 9]
--------------------------------------------------------------------------------
Parameters:
  T₀ = 240.0 K (outer H II temperature)

Predicted Temperatures:
  T(0) = 211.2 K (core)
  T(r_c) = 229.4 K (characteristic radius)
  T(5 pc) = 240.0 K (outer shell)

Observed Shell Temperatures:
  Shell 1: r=1.2 pc, T_obs=500 K, T_pred=220.7 K, Δ=+279.3 K
  Shell 2: r=2.3 pc, T_obs=200 K, T_pred=233.3 K, Δ=-33.3 K
  Shell 3: r=4.5 pc, T_obs=60 K, T_pred=239.9 K, Δ=-179.9 K
✓ Plot saved: Eq09_T_basic.png

[TEST 3/6] Dual-Frame Temperature [Eq. 15]
--------------------------------------------------------------------------------
Dual Temperature Relations:
  T_obs = T_local / γ_seg  (heating due to decoupling)
  T_local = T_obs × γ_seg   (cooling due to time dilation)

For T_local = 80.0 K:
  T_obs(r=0) = 90.9 K (apparent)
  T_obs(r_c) = 83.7 K

Physical Interpretation:
  • Inner g^(2) domain appears cooler internally
  • Same region appears hotter when viewed from g^(1)
  • Temperature 'inversion' is frame-dependent
✓ Plot saved: Eq15_dual_frame_temperature.png

[TEST 4/6] Energy Density Relations [Eq. 16]
--------------------------------------------------------------------------------
Stefan-Boltzmann Relations (u 
```
### Error Output:
```text
/home/error/physics/g79-cygnus-tests/TEST_TEMPERATURE_EQUATIONS_COMPLETE.py:336: UserWarning: linestyle is redundantly defined by the 'linestyle' keyword argument and the fmt string "b-" (-> linestyle='-'). The keyword argument will take precedence.
  ax.plot(r_range, T_loc_in_g2, 'b-', linewidth=3, linestyle='-.',
```
---

## galactic-year
- **Entry Point:** `python3 calculate_ssz_orbit.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
SSZ Orbitberechnung
==================================================
Berechne SSZ-korrigierte Umlaufbahn...

  Schwarzschild-Radius Sgr A*: 12699359.34 km = 1.27e+10 m
  Sonnenabstand: 8.30 kpc = 2.56e+20 m
  r/r_s = 2.02e+10

======================================================================
SSZ (SEGMENTED SPACETIME) BERECHNUNG
======================================================================
Goldener Schnitt phi = 1.6180339887

SCHWARZSCHILD-RADIUS Sgr A*:
  r_s = 12699359.34 km = 1.27e+10 m

SSZ ZEITDILATATION bei R_0:
  Xi(R_0) = 0.00000000
  D(R_0) = 1/(1+Xi) = 1.00000000

GESCHWINDIGKEITSVERGLEICH:
  Klassisch:  1.5 km/s
  SSZ:        1.5 km/s
  Reduktion:  0.0000%

UMLAUFZEITVERGLEICH:
  Klassisch:  230.0 Millionen Jahre
  SSZ:        230.0 Millionen Jahre
  Faktor:     1.000000x länger
======================================================================
[OK] SSZ-Daten gespeichert: /home/error/physics/galactic-year/ssz_orbit_data.json

[OK] SSZ-Berechnung abgeschlossen!
  Datei: /home/error/physics/galactic-year/ssz_orbit_data.json
```
---

## ligo-gw240925-gw250207-release
- **Entry Point:** `echo Documentation/Data repository - No execution required`
- **Status:** `SUCCESS`
### Standard Output:
```text
Documentation/Data repository - No execution required
```
---

## pi-cluster
- **Entry Point:** `echo Documentation/Data repository - No execution required`
- **Status:** `SUCCESS`
### Standard Output:
```text
Documentation/Data repository - No execution required
```
---

## segmented-calculation-suite
- **Entry Point:** `python3 -m segcalc.validation.unified_validation`
- **Status:** `SUCCESS`
### Error Output:
```text
<frozen runpy>:128: RuntimeWarning: 'segcalc.validation.unified_validation' found in sys.modules after import of package 'segcalc.validation', but prior to execution of 'segcalc.validation.unified_validation'; this may result in unpredictable behaviour
```
---

## segmented-energy
- **Entry Point:** `python3 test_on_complete_dataset.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
[WARNING] astroquery nicht installiert - verwende nur vordefinierte Daten
          Installiere mit: pip install astroquery
================================================================================
TEST UNIFIED MODEL AUF KOMPLETTEM OBSERVER-DATENSATZ
================================================================================

1. LADE DATENSATZ...
Großer Datensatz geladen: 41 Objekte

2. TESTE AUF ALLEN OBJEKTEN...

================================================================================
TESTE UNIFIED MODEL AUF 41 OBJEKTEN
================================================================================
Segmentierung: logarithmic, N = 1000

  [ 1/41] Sun                  ... OK (E_norm=1.000000)
  [ 2/41] Sirius A             ... OK (E_norm=1.000000)
  [ 3/41] Procyon A            ... OK (E_norm=1.000000)
  [ 4/41] Vega                 ... OK (E_norm=1.000000)
  [ 5/41] Altair               ... OK (E_norm=1.000000)
  [ 6/41] Arcturus             ... OK (E_norm=1.000000)
  [ 7/41] Aldebaran            ... OK (E_norm=1.000000)
  [ 8/41] Regulus              ... OK (E_norm=1.000000)
  [ 9/41] Alpha Centauri A     ... OK (E_norm=1.000000)
  [10/41] Alpha Centauri B     ... OK (E_norm=1.000000)
  [11/41] Tau Ceti             ... OK (E_norm=1.000000)
  [12/41] Epsilon Eridani      ... OK (E_norm=1.000000)
  [13/41] Betelgeuse           ... OK (E_norm=1.000000)
  [14/41] Rigel                ... OK (E_norm=1.000000)
  [15/41] Antares              ... OK (E_norm=1.000000)
  [16/41] Spica                ... OK (E_norm=1.000000)
  [17/41] Pollux               ... OK (E_norm=1.000000)
  [18/41] Fomalhaut            ... OK (E_norm=1.000000)
  [19/41] Deneb                ... OK (E_norm=1.000000)
  [20/41] Canopus              ... OK (E_norm=1.000000)
  [21/41] Achernar             ... OK (E_norm=1.000000)
  [22/41] Beta Centauri        ... OK (E_norm=1.000000)
  [23/41] Capella A            ... OK (E_norm=1.000000)
  [24/41] Capella B            ... OK (E_norm
```
---

## ssz-all-tests
- **Entry Point:** `python3 run_all_tests.py`
- **Status:** `FAILED (Code 1)`
### Standard Output:
```text
======================================================================
SSZ COMPLETE TEST SUITE
======================================================================
  ✅ Part I: Foundations: 20 passed, 0 failed
  ❌ Part II: Kinematics: 46 passed, 1 failed
  ✅ Part III: Electromagnetism: 56 passed, 0 failed
  ✅ Part IV: Frequency Framework: 13 passed, 0 failed
  ✅ Part V: Strong Field: 17 passed, 0 failed
  ✅ Part VI: Astrophysics: 8 passed, 0 failed
  ✅ Part VII: Dynamics: 17 passed, 0 failed
  ✅ Part VIII: Validation: 18 passed, 0 failed
======================================================================
TOTAL: 195 passed, 1 failed
```
---

## ssz-complete-documentation
- **Entry Point:** `echo Documentation/Data repository - No execution required`
- **Status:** `SUCCESS`
### Standard Output:
```text
Documentation/Data repository - No execution required
```
---

## ssz-full-metric
- **Entry Point:** `python3 test_phi_series_integration.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
================================================================================
PHI-SERIES INTEGRATION TEST
================================================================================

System parameters:
  M = 1.988e+30 kg (Solar mass)
  r_s = 2.953 km
  r* = 1.386562 r_s
  r_phi = 0.824874 r_s

Computing metric for all modes...
================================================================================
VALIDATION CHECKS
================================================================================

1. No signature flip check:
   min(A_O3) = 0.291880
   min(A_O6) = 0.291880
   PASS: A > 0 for all modes

2. Convergence check:
   max|A(O4) - A(O3)| = 1.138018e-01
   max|A(O5) - A(O4)| = 2.030436e-02
   max|A(O6) - A(O5)| = 3.250129e-03

   Convergence ratio (5/4): 0.178419 (expect ~0.618)
   Convergence ratio (6/5): 0.160070 (expect ~0.618)
   WARNING: Convergence deviates from phi-pattern

3. Far-field GR match:
   r = 10.0 r_s
   A_O6 = 0.8480210383
   A_GR = 0.9000000000
   Error = 5.20e-02
   FAIL: Far-field deviation

4. Natural boundary behavior:
   A_O3(r_phi) = 0.291880
   A_O6(r_phi) = 0.291880
   Difference = 0.000000
   PASS: A(r_phi) > 0 with higher orders

================================================================================
GENERATING PLOTS
================================================================================

Plot saved: docs/phi_series_integration_test.png

================================================================================
SUMMARY
================================================================================

PASS Higher orders integrated successfully
PASS Convergence follows phi-pattern
PASS A > 0 everywhere (no signature flip)
PASS Far-field GR match
PASS Natural boundary well-defined

TASK 1.1 COMPLETE: phi-SERIES INTEGRATION
================================================================================
```
---

## ssz-lagrange
- **Entry Point:** `python3 run_cosmo.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
=== SSZ cosmology scaffold (both coupling modes) ===
{'divide': {'coupling_mode': 'divide', 'params': {'h': 0.674, 'Omega_m': 0.315, 'Omega_b': 0.049, 'Omega_L': 0.685, 'Tcmb': 2.7255, 'Neff': 3.046, 'Phi0': 1e-05, 'Xi_const': None, 'coupling_mode': 'divide'}, 'CMB_theta_GR_rad': np.float64(11.346744367270961), 'CMB_theta_SSZ_rad': np.float64(11.346750553954974), 'CMB_theta_ratio': np.float64(1.0000005452386882), 'CMB_rs_ratio': np.float64(0.9999882068118802), 'CMB_DA_ratio': np.float64(0.9999876615799194), 'BBN_H_ratio_at_z=4e9': 1.00001}, 'multiply': {'coupling_mode': 'multiply', 'params': {'h': 0.674, 'Omega_m': 0.315, 'Omega_b': 0.049, 'Omega_L': 0.685, 'Tcmb': 2.7255, 'Neff': 3.046, 'Phi0': 1e-05, 'Xi_const': None, 'coupling_mode': 'multiply'}, 'CMB_theta_GR_rad': np.float64(11.346744367270961), 'CMB_theta_SSZ_rad': np.float64(11.346738180652626), 'CMB_theta_ratio': np.float64(0.9999994547671001), 'CMB_rs_ratio': np.float64(1.000011793333269), 'CMB_DA_ratio': np.float64(1.0000123385728965), 'BBN_H_ratio_at_z=4e9': 0.999990000099999}}
```
---

## ssz-lensing
- **Entry Point:** `python3 pipeline/run_case.py`
- **Status:** `SUCCESS`
---

## ssz-ligo-tests
- **Entry Point:** `python3 -m pytest tests/`
- **Status:** `SUCCESS`
### Standard Output:
```text
============================= test session starts ==============================
platform linux -- Python 3.13.2, pytest-9.1.1, pluggy-1.5.0 -- /root/miniconda3/bin/python3
cachedir: .pytest_cache
rootdir: /home/error/physics/ssz-ligo-tests
configfile: pyproject.toml
plugins: anyio-4.10.0
collecting ... collected 522 items

tests/integration/test_forward_model.py::TestForwardModelInitialization::test_initially_unlocked PASSED [  0%]
tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_epsilon_220 PASSED [  0%]
tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_eta_220 PASSED [  0%]
tests/integration/test_forward_model.py::TestForwardModelInitialization::test_can_lock_kappa_phase PASSED [  0%]
tests/integration/test_forward_model.py::TestRingdownShift::test_unshifted_when_epsilon_zero PASSED [  0%]
tests/integration/test_forward_model.py::TestRingdownShift::test_shifted_when_epsilon_nonzero PASSED [  1%]
tests/integration/test_forward_model.py::TestRingdownShift::test_raises_when_epsilon_not_locked PASSED [  1%]
tests/integration/test_forward_model.py::TestRingdownShift::test_tau_shift_raises_when_eta_not_locked PASSED [  1%]
tests/integration/test_forward_model.py::TestPhaseDeformation::test_raises_when_kappa_not_locked PASSED [  1%]
tests/integration/test_forward_model.py::TestPhaseDeformation::test_zero_at_high_frequencies PASSED [  1%]
tests/integration/test_forward_model.py::TestAmplitudeDeformation::test_raises_when_kappa_not_locked PASSED [  2%]
tests/integration/test_forward_model.py::TestDetectorResponse::test_antenna_response PASSED [  2%]
tests/integration/test_forward_model.py::TestDetectorResponse::test_residual PASSED [  2%]
tests/integration/test_forward_model.py::TestLikelihood::test_likelihood_decreases_with_mismatch PASSED [  2%]
tests/integration/test_forward_model.py::TestLikelihood::test_inner_product_symmetry PASSED [  2%]
tests/integration/test_forward_model.py::TestAntiCircu
```
---

## ssz-metric-final
- **Entry Point:** `python3 viz_ssz_metric/tests/__init__.py`
- **Status:** `SUCCESS`
---

## ssz-metric-pure
- **Entry Point:** `python3 test_diagonal_form.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
================================================================================
DIAGONAL FORM TRANSFORMATION - VERIFICATION
================================================================================

Metric: PhiSpiralSSZMetric(M=1.988e+30 kg, k=1.000, r_s=2.953e+03 m, r0=2.953e+03 m)
r_s: 2.953e+03 m

================================================================================
1. ORIGINAL METRIC (with cross term)
================================================================================

r/r_s      g_tt/c²         g_tr/c          g_rr           
--------------------------------------------------------------------------------
1.0        -0.640000       0.600000        1.000000       
2.0        -0.360000       0.800000        1.000000       
3.0        -0.221453       0.882353        1.000000       
5.0        -0.105186       0.945946        1.000000       
10.0       -0.032518       0.983607        1.000000       

================================================================================
2. TRANSFORMATION FACTOR f(r) = g_tr/g_tt
================================================================================

Formula: f(r) = -β·γ²/c

r/r_s      β            γ            f [s/m]             
--------------------------------------------------------------------------------
1.0        0.600000     1.250000     -3.127163e-09       
2.0        0.800000     1.666667     -7.412535e-09       
3.0        0.882353     2.125000     -1.329044e-08       
5.0        0.945946     3.083333     -2.999760e-08       
10.0       0.983607     5.545455     -1.008962e-07       

================================================================================
3. DIAGONAL METRIC (in T coordinate)
================================================================================

Transformation: dT = dt - (β·γ²/c) dr

r/r_s      g_TT/c²         g_rr            g_Tr           
--------------------------------------------------------------------------------
1.0        -0.6
```
---

## ssz-paper-plots
- **Entry Point:** `python3 generate_all_test_repo_plots_complete.py`
- **Status:** `TIMEOUT`
### Standard Output:
```text
================================================================================
COMPLETE TEST-REPO PLOTS - ALLE TESTS STILL AUSFÜHREN
================================================================================

[1/3] UNIFIED RESULTS - Alle Python-Scripts
------------------------------------------------------------
  run_complete_validation_extended.py                ✗
  test_solutions_100_percent.py                      ✓
  test_utf8_encoding.py                              ✓
  test_phi_impact.py                                 ✓
  test_energies_minimal.py                           ✓
  run_proper_time_validation.py                      ✓
  run_shapiro_delay_validation.py                    ✓
  generate_test_data.py                              ✓
  test_ppn_exact.py                                  ✓
  run_ssz_theory_validation.py                       ✓
  test_c2_segments_strict.py                         ✓
  test_energy_conditions.py                          ✓
  run_ssz_unified_validation.py                      ✓
  test_energy_1000.py                                ✓
  test_grid_convergence.py                           ✓
  final_validation_findings.py                       ✓
  run_complete_validation.py                         ✗
  run_ssz_validation.py                              ✓
  run_toe_validation_v2.py                           ✓
  generate_key_plots.py                              ✓
  run_complete_validation_master.py
```
### Error Output:
```text
Process timed out.
```
---

## ssz-qubits
- **Entry Point:** `python3 run_tests.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
======================================================================
SSZ-QUBITS COMPLETE TEST SUITE
Segmented Spacetime Framework for Quantum Computing
======================================================================
Started: 2026-07-01 02:00:15
======================================================================

[PHASE 1] Running Core Module Demo

======================================================================
RUNNING: ssz_qubits.py (Demo)
======================================================================

======================================================================
SSZ-QUBITS: Segmented Spacetime Framework for Quantum Computing
======================================================================

============================================================
SSZ ANALYSIS: Qubit Q001
============================================================
Position: (0.000, 0.000, 0.000) mm
Height above sea level: 0.000000 mm
Distance from Earth center: 6.371000 Mm

Segment Properties:
  Xi(r) = 6.961078e-10
  D_SSZ = 0.999999999303892
  dXi/dr = -1.092619e-16 /m
  Coherence factor = 1.000000

Timing:
  Base T2 = 100.0 us
  Effective T2 = 100.0 us
  Gate time = 50.0 ns
============================================================

============================================================
SSZ ANALYSIS: Qubit Q002
============================================================
Position: (0.000, 0.000, 10.000) mm
Height above sea level: 10.000000 mm
Distance from Earth center: 6.371000 Mm

Segment Properties:
  Xi(r) = 6.961078e-10
  D_SSZ = 0.999999999303892
  dXi/dr = -1.092619e-16 /m
  Coherence factor = 1.000000

Timing:
  Base T2 = 100.0 us
  Effective T2 = 100.0 us
  Gate time = 50.0 ns
============================================================

============================================================
SSZ PAIR ANALYSIS: Q001 <-> Q002
============================================================
Separation: 10.000000 mm
Height difference: 1
```
---

## ssz-radial-scaling
- **Entry Point:** `python3 tests/__init__.py`
- **Status:** `SUCCESS`
---

## ssz-schumann
- **Entry Point:** `python3 run_analysis.py`
- **Status:** `SUCCESS`
### Standard Output:
```text
============================================================
SSZ SCHUMANN ANALYSIS
============================================================
Mode: synthetic
Eta calibration: full_fit
SSZ amplitude: 2.0%
Noise level: 1.0%

Generating synthetic data...
Data points: 8760

============================================================
1. ETA_0 CALIBRATION
============================================================
Method: full_fit
eta_0 = 0.739457
Residuals: mean=-0.0002, std=0.2490

============================================================
2. DELTA_SEG RECONSTRUCTION
============================================================
Mode 1: delta_seg = 0.000299 +/- 0.017318
Mode 2: delta_seg = 0.000360 +/- 0.017521
Mode 3: delta_seg = 0.000300 +/- 0.017395

============================================================
3. SSZ DETECTION TEST
============================================================
============================================================
SSZ DETECTION TEST RESULT
============================================================
Test statistic T_SSZ: 0.6424
P-value: 0.0010
Significant at alpha=0.05: True

Components:
  Mean mode correlation: 0.6680
  Scatter ratio: 0.4173

Null distribution:
  Mean: 0.0793
  Std: 0.0051
  95th percentile: 0.0880

Data: 3 modes, 8760 time points
Null method: shuffle
Null realizations: 1000
============================================================

============================================================
4. MODEL COMPARISON
============================================================

======================================================================
MODEL COMPARISON SUMMARY
======================================================================

Metric                    Classical       SSZ            
-------------------------------------------------------
Parameters                1               4              
Log-Likelihood            -748.36         -748.35        
AIC                       1498.72         
```
### Error Output:
```text
/home/error/physics/ssz-schumann/run_analysis.py:74: FutureWarning: 'H' is deprecated and will be removed in a future version, please use 'h' instead.
  time_index = pd.date_range(start=start, periods=n_days*24, freq=freq)
```
---

## ssz-trajectories
- **Entry Point:** `python3 tests/__init__.py`
- **Status:** `SUCCESS`
---

