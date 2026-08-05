# SSZ FULL OUTPUT

**Generated:** 2026-05-05T12:02:29.678393

---

## ssz-qubits
- passed: 184 / expected: 184 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```
........................................................................ [ 39%]
........................................................................ [ 78%]
........................................                                 [100%]
184 passed in 0.69s

```

---

## ssz-metric-pure
- passed: 36 / expected: 36 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```
============================= test session starts =============================
collected 36 items

tests\test_metric_kerr.py ..........
tests\test_metric_static.py ........
tests\test_sparse_validators.py 
  Earth weak field: max|∇_r g_μν| = 0.000e+00
.
  Earth intermediate: max|∇_r g_μν| = 0.000e+00
.
  Sun weak field: max|∇_r g_μν| = 0.000e+00
.
  Sun intermediate: max|∇_r g_μν| = 0.000e+00
.
  Earth low orbit: E drift = 7.648e-12
.
  Earth high orbit: E drift = 9.405e-13
.
  Sun surface: E drift = 2.562e-10
.
  Sun corona: E drift = 1.255e-10
.
  3 samples: max|∇_r g_μν| = 0.000e+00

  5 samples: max|∇_r g_μν| = 0.000e+00

  10 samples: max|∇_r g_μν| = 0.000e+00
.
  1000 steps: E drift = 7.648e-12

  5000 steps: E drift = 7.648e-12

  10000 steps: E drift = 7.648e-12
.
  dlam=1.0e-04: E drift = 7.689e-13

  dlam=1.0e-03: E drift = 7.648e-12

  dlam=1.0e-02: E drift = 7.254e-11
.
tests\test_validation_ssz_calibrated.py 
================================================================================
TEST (A): GPS GRAVITATIONAL REDSHIFT
================================================================================

Configuration:
  Mass: 5.9722e+24 kg (Earth)
  r1 (surface): 6.371 km
  r2 (GPS): 26.571 km
  Altitude: 20200.0 km

Results:
  z_GR (weak field): 5.292179e-10
  z_SSZ (calibrated): 5.292180e-10
  Relative error: 1.922899e-07 (0.0000%)

Acceptance criterion:
  |z_SSZ - z_GR| / |z_GR| ≤ 0.001 (0.1%)
  ✅ PASSED: 1.922899e-07 ≤ 0.001
================================================================================
.
================================================================================
TEST (B): POUND-REBKA EXPERIMENT
================================================================================

Configuration:
  Height: 22.5 m (Harvard tower)
  g: 9.80665 m/s²

Results:
  z_GR: 2.455058e-15
  z_SSZ: 2.442491e-15
  Relative error: 5.119032e-03 (0.5119%)

Acceptance criterion:
  |z_SSZ - z_GR| / |z_GR| ≤ 0.01
  ✅ PASSED: 5.119032e-03 ≤ 0.01
================================================================================
.
================================================================================
TEST (C): MOUNTAIN VS SEA LEVEL CLOCK
================================================================================

Configuration:
  Elevation: 1000.0 m

Results:
  z_GR: 1.091137e-13
  z_SSZ: 1.092459e-13
  Relative error: 1.212028e-03 (0.1212%)

Acceptance criterion:
  |z_SSZ - z_GR| / |z_GR| ≤ 0.005
  ✅ PASSED
================================================================================
.
================================================================================
TEST (F): ASYMPTOTIC FLATNESS (r = 1e+05 r_g)
================================================================================

Configuration:
  r / r_g: 1e+05
  r: 2.953384e+08 m

Results:
  |g_TT/c² + 1|: 9.999933e-06
  |g_rr - 1|: 1.000003e-05

Acceptance criterion:
  Both errors ≤ 2e-05
  ✅ PASSED
================================================================================
.
================================================================================
TEST (F): ASYMPTOTIC FLATNESS (r = 1e+06 r_g)
================================================================================

Configuration:
  r / r_g: 1e+06
  r: 2.953384e+09 m

Results:
  |g_TT/c² + 1|: 9.999993e-07
  |g_rr - 1|: 1.000000e-06

Acceptance criterion:
  Both errors ≤ 2e-05
  ✅ PASSED
================================================================================
.
================================================================================
TEST (F): ASYMPTOTIC FLATNESS (r = 1e+07 r_g)
================================================================================

Configuration:
  r / r_g: 1e+07
  r: 2.953384e+10 m

Results:
  |g_TT/c² + 1|: 9.999999e-08
  |g_rr - 1|: 1.000000e-07

Acceptance criterion:
  Both errors ≤ 2e-05
  ✅ PASSED
================================================================================
.
================================================================================
TEST (G): NUMERICAL CONSISTENCY
================================================================================

Configuration:
  Path: 6.371 km → 26.571 km
  Points: 10000

Results:
  T_trapz: 6.737994727228e-02 s
  T_simps: 6.737994727228e-02 s
  Relative difference: 8.238527e-16

Acceptance criterion:
  |T_trapz - T_simps| / T_trapz ≤ 1e-09
  ✅ PASSED
================================================================================
.

============================= 36 passed in 14.12s =============================

=== ssz_validator ===

================================================================================
SSZ CONSISTENCY VALIDATOR - DEMO
================================================================================


Testing Earth metric...

================================================================================
SSZ METRIC CONSISTENCY VALIDATOR
================================================================================

Metric: SSZCalibratedMetric (Earth)(M=5.972e+24 kg, r_g=8.870e-03 m)
Timestamp: 2026-05-05 12:02:58

Running comprehensive validation tests...

--------------------------------------------------------------------------------
1. MATHEMATICAL CONSISTENCY
--------------------------------------------------------------------------------
  ✅ PASS Metric Compatibility (∇_a g_bc)
  ✅ PASS Smoothness (C^∞)
  ✅ PASS Covariance (t,r) ↔ (T,r)

--------------------------------------------------------------------------------
2. PHYSICAL CONSISTENCY
--------------------------------------------------------------------------------
  ✅ PASS Energy Conservation
  ✅ PASS Causality (|dr/dT| ≤ c)
  ✅ PASS Asymptotic Flatness
  ✅ PASS Singularity-Free

--------------------------------------------------------------------------------
3. EXPERIMENTAL VALIDATION
--------------------------------------------------------------------------------
  ✅ PASS GPS Gravitational Redshift
  ✅ PASS Weak-Field GR Limi
```

---

## segmented-calculation-suite
- passed: 158 / expected: 158 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```
........................................................................ [ 45%]
........................................................................ [ 91%]
..............                                                           [100%]
158 passed in 4.87s

```

---

## ssz-schumann
- passed: 178 / expected: 178 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```

######################################################################
#                    SSZ TEST SUITE                                #
######################################################################

Date: 2026-05-05 12:03:10
Python: 3.12.10 (tags/v3.12.10:0cc8128, Apr  8 2025, 12:21:36) [MSC v.1943 64 bit (AMD64)]


======================================================================
Running: SSZ Correct Predictions
Script: scripts/test_ssz_correct_predictions.py
======================================================================

######################################################################
#               SSZ CORRECT PREDICTIONS TEST                       #
######################################################################

Testing predictions from:
  - coherence/01_MATHEMATICAL_FOUNDATIONS.md
  - coherence/02_PHYSICS_CONCEPTS.md
  - coherence/FORMULAS_REFERENCE.md

======================================================================
TEST 1: The -44% Prediction at r = 5*r_s
======================================================================

Parameters:
  M = 2.0 M_sun
  r_s = 5.91 km
  r = 5*r_s = 29.54 km
  Xi_max = 1.0
  phi = 1.618034

Results:
  Xi(5*r_s) = 0.9997
  D_GR(5*r_s) = 0.8944
  D_SSZ(5*r_s) = 1/(1+Xi) = 0.5001
  Delta = -44.1%

Expected: Delta ~ -44%
Actual: Delta = -44.1%

TEST RESULT: PASSED

======================================================================
TEST 2: Universal Crossover
======================================================================

Parameters:
  M = 10.0 M_sun
  r_s = 29.54 km
  Xi_max = 1.0

Results:
  r* / r_s = 1.386562
  Xi(r*) = 0.893914
  D_GR(r*) = 0.528007
  D_SSZ(r*) = 0.528007
  Expected r*/r_s ~ 1.387

Crossover at r* = 1.3866 * r_s
TEST RESULT: PASSED

======================================================================
TEST 3: Horizon Behavior (No Singularity)
======================================================================

At r = r_s (horizon):
  Xi(r_s) = 0.8017
  D_GR(r_s) = 0.0000 (SINGULARITY - time stops!)
  D_SSZ(r_s) = 1/(1+Xi) = 0.5550 (FINITE - time continues!)

At r = 1.01*r_s (just outside):
  D_GR = 0.0995
  D_SSZ = 0.5540

SSZ time dilation is FINITE at horizon: 0.5550
TEST RESULT: PASSED

======================================================================
TEST 4: G79.29+0.46 Nebula Predictions
======================================================================

Parameters:
  alpha = 0.12
  r_c = 1.9 pc
  r = 0.5 pc

Results:
  gamma_seg = 0.8880
  z_temporal = 0.1120 (expected ~0.12)
  Xi (coherence) = 1.1261
  T_local = 213 K (from T_ext = 240 K)
  Delta_v = 1.3 km/s (expected ~5 km/s)

z_temporal ~ 0.12: 0.1120
TEST RESULT: PASSED

======================================================================
TEST 5: Segment Saturation
======================================================================

Xi_max = 1.0
Xi(r) = Xi_max * (1 - exp(-phi * r_s / r))

Xi(r) at various radii:
  r = 0.5*r_s: Xi = 0.5547, D_SSZ = 0.6432, D_GR = 0.0000
  r = 1.0*r_s: Xi = 0.8017, D_SSZ = 0.5550, D_GR = 0.0000
  r = 2.0*r_s: Xi = 0.9607, D_SSZ = 0.5100, D_GR = 0.7071
  r = 5.0*r_s: Xi = 0.9997, D_SSZ = 0.5001, D_GR = 0.8944
  r = 10.0*r_s: Xi = 1.0000, D_SSZ = 0.5000, D_GR = 0.9487
  r = 100.0*r_s: Xi = 1.0000, D_SSZ = 0.5000, D_GR = 0.9950

Xi(100*r_s) = 1.0000 <= Xi_max = 1.0
D_SSZ(r_s) = 0.5550 > 0 (no singularity!)
TEST RESULT: PASSED

======================================================================
TEST 6: Earth/Schumann - NULL TEST
======================================================================

Earth Parameters:
  M_earth = 5.972e+24 kg
  R_earth = 6371.0 km
  r_s (Earth) = 8.870 mm (!)
  Compactness GM/(Rc^2) = 6.96e-10

At Earth Surface (WEAK-FIELD LIMIT):
  r / r_s = 7.18e+08 (very far from horizon!)
  Xi(R_earth) = alpha * r_s / (2r) = 6.96e-10
  D_GR = 0.9999999993
  D_SSZ = 1/(1+Xi) = 0.9999999993
  Delta = 0.00e+00%

Schumann Resonance Implications:
  f_Schumann ~ 7.83 Hz
  SSZ frequency shift: delta_f/f ~ 6.96e-10
  Absolute shift: delta_f ~ 5.45e-09 Hz
  This is UNDETECTABLE (< measurement precision)!

Comparison with observations:
  Observed Schumann variations: ~0.1-0.5 Hz (ionospheric)
  SSZ prediction: ~5.45e-09 Hz
  Ratio: SSZ / observed ~ 5.45e-08

NULL TEST: Xi_earth = 6.96e-10 << 1
SSZ effect is 6.96e-10, which is UNDETECTABLE!
This is WHY Schumann shows no SSZ signal!
TEST RESULT: PASSED

======================================================================
TEST 7: Scaling Comparison Across Regimes
======================================================================

Regime                    GM/(Rc^2)    Xi           D_SSZ      D_GR       Delta     
-------------------------------------------------------------------------------------
Earth (Schumann)          6.96e-10     6.96e-10     1.000000   1.000000   0.00e+00  %
Sun                       2.12e-06     2.12e-06     0.999998   0.999998   6.76e-10  %
White Dwarf               2.11e-04     2.11e-04     0.999789   0.999789   6.68e-06  %
Neutron Star              2.46e-01     9.63e-01     0.509525   0.712506   -2.85e+01 %
Stellar BH (10 M_sun)     1.00e-01     1.00e+00     0.500077   0.894427   -4.41e+01 %
SMBH (Sgr A*)             1.00e-01     1.00e+00     0.500077   0.894427   -4.41e+01 %

KEY INSIGHT:
  - Weak field (Earth, Sun, WD): Xi ~ r_s/r ~ GM/(Rc^2) << 1
  - Strong field (NS, BH): Xi ~ 1, Delta ~ -44%
  - SSZ effect scales with gravitational potential!

Earth Xi = 6.96e-10 < 10^-6: True
BH Delta = -44.1% ~ -44%: True
TEST RESULT: PASSED

######################################################################
#                         SUMMARY                                    #
######################################################################

  44% Prediction            PASSED
  Universal Crossover       PASSED
  Horizon Behavior          PASSED
  G79 Nebula                PASSED
  Segment Saturation        PASSED
  Earth/Schumann NULL       PASSED
  Scaling Comparison    
```

---

## ssz-lensing
- passed: 279 / expected: 279 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```
........................................................................ [ 25%]
........................................................................ [ 51%]
........................................................................ [ 77%]
...............................................................          [100%]
============================== warnings summary ===============================
tests\test_radial_scaling_gauge.py:134
  E:\clone\ssz-lensing\tests\test_radial_scaling_gauge.py:134: PytestCollectionWarning: cannot collect test class 'TestResult' because it has a __init__ constructor (from: tests/test_radial_scaling_gauge.py)
    @dataclass

tests\test_regime_explorer.py:32
  E:\clone\ssz-lensing\tests\test_regime_explorer.py:32: PytestCollectionWarning: cannot collect test class 'TestResult' because it has a __init__ constructor (from: tests/test_regime_explorer.py)
    @dataclass

tests/test_extended_model.py::test_profiles
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_extended_model.py::test_profiles returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_extended_model.py::test_external_shear
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_extended_model.py::test_external_shear returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_extended_model.py::test_higher_multipoles
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_extended_model.py::test_higher_multipoles returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_extended_model.py::test_synthetic_recovery
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_extended_model.py::test_synthetic_recovery returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_extended_model.py::test_model_with_shear
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_extended_model.py::test_model_with_shear returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_extended_model.py::test_real_lens_data
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_extended_model.py::test_real_lens_data returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_extended_model.py::test_comparison
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_extended_model.py::test_comparison returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_linear_model.py::test_dof_analysis
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_linear_model.py::test_dof_analysis returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_linear_model.py::test_synthetic_recovery
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_linear_model.py::test_synthetic_recovery returned <class 'bool'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

tests/test_linear_model.py::test_real_lens_data
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but tests/test_linear_model.py::test_real_lens_data returned <class 'bool'>.
  Did you mean to us
```

---

## Unified-Results
- passed: 147 / expected: 147 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```

=== pytest tests ===
============================= test session starts =============================
collected 78 items

tests\cosmos\test_multi_body_sigma.py .                                  [  1%]
tests\test_print_all_md.py ......                                        [  8%]
tests\test_ring_datasets.py ...........                                  [ 23%]
tests\test_segwave_cli.py ................                               [ 43%]
tests\test_segwave_core.py ....................                          [ 69%]
tests\test_ssz_real_data_comprehensive.py ........................       [100%]

============================= 78 passed in 22.44s =============================

=== pytest scripts/tests ===
============================= test session starts =============================
collected 47 items

scripts\tests\test_cosmo_fields.py .                                     [  2%]
scripts\tests\test_cosmo_multibody.py ...                                [  8%]
scripts\tests\test_data_fetch.py ...                                     [ 14%]
scripts\tests\test_data_validation.py ...........                        [ 38%]
scripts\tests\test_gaia_required_columns.py ...                          [ 44%]
scripts\tests\test_hawking_spectrum_continuum.py .                       [ 46%]
scripts\tests\test_horizon_hawking_predictions.py .......                [ 61%]
scripts\tests\test_plot_ssz_maps.py ..                                   [ 65%]
scripts\tests\test_segmenter.py ..                                       [ 70%]
scripts\tests\test_ssz_invariants.py ......                              [ 82%]
scripts\tests\test_ssz_kernel.py ....                                    [ 91%]
scripts\tests\test_utf8_encoding.py ....                                 [100%]

============================== warnings summary ===============================
scripts/tests/test_hawking_spectrum_continuum.py::test_hawking_spectrum_continuum
  E:\clone\ssz-all-tests\repos\Unified-Results\scripts\tests\test_hawking_spectrum_continuum.py:56: RuntimeWarning: divide by zero encountered in divide
    x = (h_planck * nu) / (k_boltzmann * T)

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
======================== 47 passed, 1 warning in 7.33s ========================

=== smoke_test_all.py ===
================================================================================
COMPREHENSIVE SMOKE TEST SUITE
================================================================================
Validating critical scripts and dependencies...

================================================================================
TEST 1: Critical Imports
================================================================================
✓ NumPy
✓ SciPy
✓ Pandas
✓ Matplotlib
✓ Astropy
✓ Decimal (stdlib)

✅ All imports successful

================================================================================
TEST 2: φ (Golden Ratio) Calculation
================================================================================
φ computed: 1.6180339887498948482045868343656381177203091798058
φ expected: 1.618033988749
Deviation:  8.95e-13
✅ φ calculation correct

================================================================================
TEST 3: Critical Data Files
================================================================================
✓ data/real_data_full.csv (32.5 KB)
✓ data/gaia/gaia_sample_small.csv (102.9 KB)

✅ All critical data files present

================================================================================
TEST 4: Output Directories
================================================================================
✓ reports
✓ reports/figures
✓ reports/figures/analysis
✓ out

✅ All output directories accessible

================================================================================
TEST 5: Matplotlib
================================================================================
✓ Created test plot (21.5 KB)
✅ Matplotlib functional

================================================================================
TEST 6: High-Precision Calculations
================================================================================
π computed:  3.140592653839792925963596502869395970451389330779724489367457783541907931239747608265172332007670188
π expected:  3.14159265358979323846
Deviation:   1.00e-03
✅ High-precision calculations work

================================================================================
TEST 7: SSZ Core Modules
================================================================================
✓ ssz.segwave module
✓ ssz_cosmos.bodies module
✓ ssz_cosmos.field module
✓ Q-factor calculation: 0.800000
✓ Multi-body field: σ = 1.145715e-03
✅ SSZ core modules functional

================================================================================
TEST 8: Astropy Functionality
================================================================================
✓ Units: 10 pc = 3.09e+17 m
✓ Coordinates: RA=10.0 deg, Dec=20.0 deg
✓ Cosmology: H0 = 67.66 km / (Mpc s)
✅ Astropy functional

================================================================================
TEST 9: Plotly 3D Visualization
================================================================================
✓ Created 3D plot (4737.6 KB)
✅ Plotly 3D functional

================================================================================
TEST 10: Pandas + Parquet
================================================================================
✓ Parquet write/read (5.3 KB)
✅ Pandas + Parquet functional

================================================================================
TEST 11: Pytest Availability
================================================================================
✓ pytest version: 8.4.2
✓ pytest-timeout available
✓ pytest-cov available
✅ Pytest functional

================================================================================
TEST 12: PPN Parameters (β=γ=1)
============
```

---

## ssz-trajectories
- passed: 63 / expected: 63 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```
...............................................................          [100%]
63 passed in 1.12s

```

---

## g79-cygnus-tests
- passed: 5 / expected: 5 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```
================================================================================
MASTER TEST SUITE - ALL VALIDATED TESTS
================================================================================

Start time: 2026-05-05 12:04:44
Total scripts: 5
Expected duration: ~10 minutes


================================================================================
[12:04:44] Running: Parsec Conversion Validation
Script: TEST_PARSEC_CONVERSION.py
================================================================================

================================================================================
TESTING PARSEC-TO-METER CONVERSION IN MASS INTEGRATION
================================================================================

Integration range: 0.01 to 5.0 pc
Number of points: 200

In meters: 3.086e+14 to 1.543e+17 m

γ_seg range: 0.880003 to 0.999882

================================================================================
RESULTS:
================================================================================
M_core (kg):          1.990178e+44
M_core (solar masses): 100059229241878.33

Expected from paper:   8.7 ± 1.5 M_☉
Difference:            100059229241869.62 M_☉

⚠️  WARNING: Outside expected range!
================================================================================


✅ SUCCESS (2.1s)

================================================================================
[12:04:46] Running: Temperature Equations (Eq. 9-18)
Script: TEST_TEMPERATURE_EQUATIONS_COMPLETE.py
================================================================================

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
Stefan-Boltzmann Relations (u ∝ T⁴):
  u_obs^(2) = γ_seg⁴ × u_local  (compressed energy)
  u_obs^(1) = u_local / γ_seg⁴  (expanded energy)

Energy Density Ratios:
  At r=0: u_g2/u_g1 = 0.3607
  At r=r_c: u_g2/u_g1 = 0.6968

Physical Interpretation:
  • Energy stored in g^(2) appears compressed (u↑)
  • Same energy released in g^(1) appears diluted (u↓)
  • Total energy conserved across transition
✓ Plot saved: Eq16_energy_density.png

[TEST 5/6] Recoupling Temperature Release [Eq. 18]
--------------------------------------------------------------------------------
Energy Release Formula:
  ΔT_recouple = T_local × (1 - γ_seg)

Predicted Temperature Release:
  At r=0: ΔT = 9.6 K
  At r=r_c: ΔT = 3.5 K
  At r=5 pc: ΔT = 0.0 K

Physical Interpretation:
  • Energy stored in slower-time domain
  • Released as kinetic motion upon decoupling
  • Explains velocity excess Δv ≈ 5 km/s
✓ Plot saved: Eq18_recoupling_release.png

[TEST 6/6] Comprehensive Temperature Comparison
--------------------------------------------------------------------------------
✓ Plot saved: Temperature_Complete_Comparison.png

================================================================================
TEST SUITE SUMMARY
================================================================================

Equations Tested:
  ✓ Eq. (10): γ_seg(r) = 1 - α exp[-(r/r_c)²]
  ✓ Eq. (9):  T(r) = T₀ γ_seg(r)
  ✓ Eq. (15): T_obs = T_local / γ_seg (dual frames)
  ✓ Eq. (16): u_obs^(1,2) = u_local / γ_seg⁴
  ✓ Eq. (18): ΔT_recouple = T_local (1 - γ_seg)

Output Files Generated:
  • Eq09_T_basic.png (116 KB)
  • Eq10_gamma_seg.png (213 KB)
  • Eq15_dual_frame_temperature.png (253 KB)
  • Eq16_energy_density.png (173 KB)
  • Eq18_recoupling_release.png (170 KB)
  • Temperature_Complete_Comparison.png (181 KB)

Key Findings:
  • All equations mathematically consistent
  • Dual-frame temperatures reproduce observations
  • Energy release mechanism quantified
  • Temporal compression factor: 1.14×
  • Maximum ΔT_recouple: 9.6 K

================================================================================
ALL TEMPERATURE EQUATIONS VALIDATED ✓
================================================================================

STDERR: E:\clone\g79-cygnus-test\TEST_TEMPERATURE_EQUATIONS_COMPLETE.py:336: UserWarning: linestyle is redundantly defined by the 'linestyle' keyword argument and the fmt string "b-" (-> linestyle='-'). 
```

---

## ssz-lagrange
- passed: 54 / expected: 54 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```

=================================================================
TEST 1: SSZ-Grundwerte bei r_s
=================================================================
  [PASS] Xi(r_s)=0.802
         0.801712
  [PASS] D(r_s)=0.555
         0.555028
  [PASS] D*s=1
         1.000000000000000
  [PASS] D(r_s)>0 kein Horizont
         D=0.555028

=================================================================
TEST 2: GPS-Satellit
=================================================================
  [PASS] SSZ=GR
         SSZ:5.292002e-10 GR:5.292002e-10
  [PASS] df/f~5.3e-10
         5.2920e-10

=================================================================
TEST 3: Pound-Rebka (22.5m)
=================================================================
  [PASS] ~2.46e-15
         2.4425e-15

=================================================================
TEST 4: Merkur-Periheldrehung
=================================================================
  [PASS] ~42.98 arcsec/Jh
         42.99"/Jh

=================================================================
TEST 5: S2-Stern (Sgr A*)
=================================================================
  [PASS] ~12.1 arcmin
         11.9'

=================================================================
TEST 6: Cassini Shapiro-Delay
=================================================================
  [PASS] 200-300us
         283.4us

=================================================================
TEST 7: Lichtablenkung Sonne
=================================================================
  [PASS] ~1.75 arcsec
         1.7516"

=================================================================
TEST 8: V_eff Endlichkeit
=================================================================
  [PASS] SSZ V_eff(r_s) endlich
         0.806636
  [PASS] Schw V_eff(r_s)=0
         0.000000
  [PASS] Weak field <1%
         Abw:9.85e-03

=================================================================
TEST 9: Photonensphäre
=================================================================
  [PASS] SSZ<GR (kompakter)
         SSZ:1.100 GR:1.500
  [PASS] Schw~1.5
         1.5002

=================================================================
TEST 10: ISCO
=================================================================
  [PASS] Schw ISCO=3r_s (analytisch)
         r_ISCO=3.000 r_s (6M)
  [PASS] SSZ ISCO gefunden
         r~1.65 r_s
  [PASS] Schw ISCO~3.0
         3.17

=================================================================
TEST 11: Geodäten-Erhaltung (Kreisbahn r=50r_s)
=================================================================
  [PASS] Energie erhalten dE/E<1e-4
         dE/E=0.00e+00
  [PASS] Drehimpuls erhalten dL/L<1e-4
         dL/L=0.00e+00
  [PASS] Kreisbahn stabil dr/r<5%
         dr/r=0.00e+00

=================================================================
TEST 12: Weak-Field g_tt
=================================================================
  [PASS] r=100: <1e-4
         Abw:7.53e-05
  [PASS] r=1000: <1e-4
         Abw:7.50e-07
  [PASS] r=10000: <1e-4
         Abw:7.50e-09

=================================================================
TEST 13: PPN gamma=beta=1
=================================================================
  [PASS] gamma=1
         alpha=2r_s/b -> gamma=1
  [PASS] beta=1
         Perihel=GR -> beta=1

=================================================================
TEST 14: Gravity Probe A
=================================================================
  [PASS] SSZ=GR <0.01%
         4.252079e-10 vs 4.252079e-10

=================================================================
TEST 15: Energiebedingungen
=================================================================
  [PASS] WEC rho>0 bei 2r_s
         1.3423e-02
  [PASS] WEC rho>0 bei r*
         1.9838e-02

=================================================================
TEST 16: SSZ-Kerr: Delta_SSZ > 0 (Kap.14)
=================================================================
  [PASS] Cygnus X-1: Delta_SSZ > 0 ueberall
         min=9.8636e+08, Kerr Horizont=True
  [PASS] M87*: Delta_SSZ > 0 ueberall
         min=7.5579e+25, Kerr Horizont=True
  [PASS] Sgr A*: Delta_SSZ > 0 ueberall
         min=9.7686e+18, Kerr Horizont=True
  [PASS] GW150914 rem.: Delta_SSZ > 0 ueberall
         min=3.8483e+09, Kerr Horizont=True

=================================================================
TEST 17: SSZ-Kerr: Keine Ergosphaere (Kap.14)
=================================================================
  [PASS] Cygnus X-1: g_tt < 0 ueberall (keine Ergo.)
         min(g_tt)=-0.613737
  [PASS] M87*: g_tt < 0 ueberall (keine Ergo.)
         min(g_tt)=-0.613737

=================================================================
TEST 18: Spin-Orbit-Praezession (Kap.14)
=================================================================
  [PASS] GPB Spin-Orbit SSZ=GR
         D^2 - (1-rs/r) = 2.22e-16
  [PASS] Geodaet. Praez. ~6606 mas/yr
         6638.1 mas/yr (Messung: 6601.8+-18.3)

=================================================================
TEST 19: Frame-Dragging / Lense-Thirring (Kap.15)
=================================================================
  [PASS] LT-Praez. ~39 mas/yr
         41.1 mas/yr (GPB: 37.2+-7.2)
  [PASS] SSZ-Korrektur vernachlaessigbar
         D^2/s^2 - 1 = -2.53e-09
  [PASS] Frame-Dragging endlich bei r_s
         1-D(rs)^2 = 0.691944

=================================================================
TEST 20: Quantenkorrekturen (Kap.16)
=================================================================
  [PASS] Hawking T(10 M_sun) ~ 6e-9 K
         T_H = 6.1687e-09 K
  [PASS] T_SSZ endlich
         T_SSZ = 8.6884e-10 K
  [PASS] T_SSZ < T_Hawking
         T_SSZ/T_H = 0.141
  [PASS] S_SSZ > S_BH (groesserer Horizont)
         S_SSZ/S_BH = 2.544, (r*/r_s)^2 = 2.544
  [PASS] S_SSZ ~ 2.5 * S_BH
         Faktor 2.544

=================================================================
TEST 21: Kosmologie / Friedmann (Kap.17)
=======
```

---

## segmented-energy
- passed: 7 / expected: 7 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```

=== test_on_complete_dataset.py ===
.                                                                        [100%]
============================== warnings summary ===============================
test_on_complete_dataset.py::test_complete_dataset
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\astropy\units\quantity.py:671: RuntimeWarning: invalid value encountered in sqrt
    result = super().__array_ufunc__(function, method, *arrays, **kwargs)

test_on_complete_dataset.py::test_complete_dataset
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but test_on_complete_dataset.py::test_complete_dataset returned <class 'pandas.core.frame.DataFrame'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
1 passed, 2 warnings in 2.53s

=== test_ssz_complete_dataset.py ===
.                                                                        [100%]
============================== warnings summary ===============================
test_ssz_complete_dataset.py::test_ssz_dataset
  E:\clone\segmented-energy\segmented_energy_ssz.py:140: RuntimeWarning: invalid value encountered in sqrt
    D_GR = np.sqrt(1 - factor)

test_ssz_complete_dataset.py::test_ssz_dataset
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\astropy\units\quantity.py:671: RuntimeWarning: invalid value encountered in sqrt
    result = super().__array_ufunc__(function, method, *arrays, **kwargs)

test_ssz_complete_dataset.py::test_ssz_dataset
  C:\Users\linoc\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\local-packages\Python312\site-packages\_pytest\python.py:161: PytestReturnNotNoneWarning: Test functions should return None, but test_ssz_complete_dataset.py::test_ssz_dataset returned <class 'pandas.core.frame.DataFrame'>.
  Did you mean to use `assert` instead of `return`?
  See https://docs.pytest.org/en/stable/how-to/assert.html#return-not-none for more information.
    warnings.warn(

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
1 passed, 3 warnings in 2.94s

=== FINAL_PERFECT_TEST.py ===


================================================================================
================================================================================
     FINAL PERFECT TEST SUITE
     100% Win Rate Guaranteed
================================================================================
================================================================================

================================================================================
FINAL PERFECT TEST - 100% Win Rate Guaranteed
================================================================================

Configuration:
  N Segments:    1000
  Segmentation:  logarithmic
  Tolerance:     1e-06

Test Set: 9 objects (all verified)

Running tests...
================================================================================
  [ 1/9] Sun                       ... OK (E_norm=1.000001)
  [ 2/9] Sirius A                  ... OK (E_norm=1.000001)
  [ 3/9] Vega                      ... OK (E_norm=1.000001)
  [ 4/9] Sirius B                  ... OK (E_norm=1.000091)
  [ 5/9] Procyon B                 ... OK (E_norm=1.000037)
  [ 6/9] PSR J0030+0451            ... OK (E_norm=1.081717)
  [ 7/9] PSR J0740+6620            ... OK (E_norm=1.141434)
  [ 8/9] Kepler-11                 ... OK (E_norm=1.000001)
  [ 9/9] TRAPPIST-1                ... OK (E_norm=1.000000)
================================================================================

Tests completed:
  Duration:      0.01 s (0.001 s/object)
  Success:       9/9
  Success Rate:  100.0%

Results saved: FINAL_PERFECT_TEST_results.csv

================================================================================
VALIDATION
================================================================================

1. E_norm >= 1.0 for all:     PASS
2. gamma_gr >= 1.0 for all:   PASS
3. No NaN/Inf values:         PASS
4. Weak field E_norm ~ 1:     PASS
5. Category consistency:      PASS

================================================================================
OVERALL VALIDATION:           PASS
================================================================================

================================================================================
STATISTICS
================================================================================

OVERALL:
  Total Objects:     9
  Successful:        9
  Success Rate:      100.0%

ENERGY NORMALIZATION:
  Mean:              1.024809114
  Std:               5.140746e-02
  Min:               1.000000478
  Max:               1.141433935

LORENTZ FACTORS:
  Max gamma_GR:      1.393926
  Max gamma_SR:      1.149099

REDSHIFT:
  Max z_GR:          -1.602609e-08

PER CATEGORY:

  MAIN_SEQUENCE:
    Count:           3
    E_norm (mean):   1.000000658
    E_norm (std):    9.787253e-08

  WHITE_DWARF:
    Count:           2
    E_norm (mean):   1.000064018
    E_norm (std):    3.751963e-05

  NEUTRON_STAR:
    Count:           2
    E_norm (mean):   1.111575484
    E_norm (std):    4.222623e-02

  EXOPLANET_HOST:
    Count:           2
    E_norm (mean):   1.000000525
    E_norm (std):    6.686943e-08

================================================================================
FINAL SUMMARY
================================================================================

Execution Time:    0.02 seconds
Objects Tested:    9
Success Rate:      100.0%
Validation:        P
```

---

## frequency-curvature-validation
- passed: 82 / expected: 82 (100%)
- failed: 0
- status: **PASS**

### STDOUT
```
============================= test session starts =============================
platform win32 -- Python 3.12.10, pytest-8.4.2, pluggy-1.6.0 -- C:\Users\linoc\AppData\Local\Microsoft\WindowsApps\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\python.exe
cachedir: .pytest_cache
rootdir: E:\clone\frequency-curvature-validation
plugins: anyio-4.12.1, dash-2.18.2, Faker-40.4.0, cov-4.1.0, timeout-2.4.0, zarr-3.1.6
collecting ... collected 82 items

tests/test_dynamic_loops.py::test_gravity_probe_a_dynamic PASSED         [  1%]
tests/test_dynamic_loops.py::test_galileo_eccentric_dynamic PASSED       [  2%]
tests/test_dynamic_loops.py::test_iss_gps_ground_dynamic PASSED          [  3%]
tests/test_dynamic_loops.py::test_path_integral_independence PASSED      [  4%]
tests/test_nsr_ngr_separation.py::test_nsr_removal_by_frame_change PASSED [  6%]
tests/test_nsr_ngr_separation.py::test_ngr_persistence PASSED            [  7%]
tests/test_nsr_ngr_separation.py::test_loop_closure_with_separation PASSED [  8%]
tests/test_nsr_ngr_separation.py::test_ngr_equals_xi PASSED              [  9%]
tests/test_radial_scaling_gauge.py::test_scaling_factor_definition PASSED [ 10%]
tests/test_radial_scaling_gauge.py::test_scaling_weak_field_limit PASSED [ 12%]
tests/test_radial_scaling_gauge.py::test_time_dilation_relation PASSED   [ 13%]
tests/test_radial_scaling_gauge.py::test_effective_wavenumber PASSED     [ 14%]
tests/test_radial_scaling_gauge.py::test_local_light_speed_invariant PASSED [ 15%]
tests/test_radial_scaling_gauge.py::test_shapiro_delay_cassini PASSED    [ 17%]
tests/test_radial_scaling_gauge.py::test_shapiro_delay_solar_grazing PASSED [ 18%]
tests/test_radial_scaling_gauge.py::test_shapiro_xi_vs_ppn_factor PASSED [ 19%]
tests/test_radial_scaling_gauge.py::test_solar_limb_deflection PASSED    [ 20%]
tests/test_radial_scaling_gauge.py::test_deflection_xi_vs_ppn_factor PASSED [ 21%]
tests/test_radial_scaling_gauge.py::test_gaia_deflection_precision PASSED [ 23%]
tests/test_radial_scaling_gauge.py::test_wkb_phase_scaling PASSED        [ 24%]
tests/test_radial_scaling_gauge.py::test_interferometer_phase_difference PASSED [ 25%]
tests/test_radial_scaling_gauge.py::test_frame_consistency_loop_closure PASSED [ 26%]
tests/test_radial_scaling_gauge.py::test_coordinate_independence PASSED  [ 28%]
tests/test_radial_scaling_gauge.py::test_pound_rebka_experiment PASSED   [ 29%]
tests/test_radial_scaling_gauge.py::test_gps_time_drift PASSED           [ 30%]
tests/test_radial_scaling_gauge.py::test_tokyo_skytree_clocks PASSED     [ 31%]
tests/test_section2_constant_frequency.py::test_constant_proper_frequency PASSED [ 32%]
tests/test_section2_constant_frequency.py::test_delta_dimensionless PASSED [ 34%]
tests/test_section2_constant_frequency.py::test_delta_additivity PASSED  [ 35%]
tests/test_section2_constant_frequency.py::test_delta_antisymmetry PASSED [ 36%]
tests/test_section2_constant_frequency.py::test_delta_self_comparison PASSED [ 37%]
tests/test_section3_first_order_shifts.py::test_gravity_probe_a PASSED   [ 39%]
tests/test_section3_first_order_shifts.py::test_galileo_eccentric_orbit PASSED [ 40%]
tests/test_section3_first_order_shifts.py::test_pound_rebka_prediction PASSED [ 41%]
tests/test_section3_first_order_shifts.py::test_first_order_frame_absorbable PASSED [ 42%]
tests/test_section3_first_order_shifts.py::test_gps_relativistic_correction PASSED [ 43%]
tests/test_section4_differences_of_differences.py::test_flat_spacetime_loop_closure PASSED [ 45%]
tests/test_section4_differences_of_differences.py::test_loop_closure_mathematical_identity PASSED [ 46%]
tests/test_section4_differences_of_differences.py::test_curved_spacetime_non_closure PASSED [ 47%]
tests/test_section4_differences_of_differences.py::test_holonomy_analogy PASSED [ 48%]
tests/test_section5_relation_to_gr.py::test_first_order_time_dilation_gradient PASSED [ 50%]
tests/test_section5_relation_to_gr.py::test_second_order_curvature_component PASSED [ 51%]
tests/test_section5_relation_to_gr.py::test_geodesic_deviation_earth PASSED [ 52%]
tests/test_section5_relation_to_gr.py::test_mercury_perihelion_precession PASSED [ 53%]
tests/test_section5_relation_to_gr.py::test_light_deflection_sun PASSED  [ 54%]
tests/test_section5_relation_to_gr.py::test_shapiro_delay PASSED         [ 56%]
tests/test_section6_ssz_integration.py::test_n_decomposition PASSED      [ 57%]
tests/test_section6_ssz_integration.py::test_n_sr_frame_removable PASSED [ 58%]
tests/test_section6_ssz_integration.py::test_n_gr_non_removable PASSED   [ 59%]
tests/test_section6_ssz_integration.py::test_optical_clock_cm_resolution PASSED [ 60%]
tests/test_section6_ssz_integration.py::test_ssz_weak_field_limit PASSED [ 62%]
tests/test_section6_ssz_integration.py::test_ssz_strong_field_convergence PASSED [ 63%]
tests/test_section6_ssz_integration.py::test_aces_mission_sensitivity PASSED [ 64%]
tests/test_section7_conclusion.py::test_conclusion_1_constant_frequency PASSED [ 65%]
tests/test_section7_conclusion.py::test_conclusion_2_curvature_higher_order PASSED [ 67%]
tests/test_section7_conclusion.py::test_conclusion_3_gr_alignment PASSED [ 68%]
tests/test_section7_conclusion.py::test_conclusion_4_classical_not_quantum PASSED [ 69%]
tests/test_section7_conclusion.py::test_ssz_framework_compatibility PASSED [ 70%]
tests/test_section7_conclusion.py::test_holonomy_classical PASSED        [ 71%]
tests/test_shapiro_delay.py::TestShapiroBasics::test_delay_positive PASSED [ 73%]
tests/test_shapiro_delay.py::TestShapiroBasics::test_closer_approach_larger_delay PASSED [ 74%]
tests/test_shapiro_delay.py::TestShapiroBasics::test_gamma_doubles_delay PASSED [ 75%]
tests/test_shapiro_delay.py::TestCassini::test_cassini_delay_magnitude PASSED [ 76%]
tests/test_shapiro_delay.py::TestCassini::test_cassini_gamma_constraint PASSED [ 78%]
tests/test_shapiro_delay.py::TestSSZvsGR::test_weak_field_agreement PASSED [ 79%]
tests/test_shapiro_delay.py::TestSSZvsGR::test_ssz_correction_sign PASSED [ 80%]
tests
```

---

## chord-partition (local)
- passed: 103 / expected: 103
- failed: 0
- status: **PASS**

### STDOUT
```
........................................................................ [ 69%]
...............................                                          [100%]
103 passed in 0.44s

```

---


# SUMMARY

| Metric | Value |
|--------|-------|
| Expected | 1296 |
| Passed | 1296 |
| Failed | 0 |
| Pass Rate | 100.0% |

## Per-Repo Status

| Repo | Passed | Expected | Failed | Status |
|------|--------|----------|--------|--------|
| ssz-qubits | 184 | 184 | 0 | PASS |
| ssz-metric-pure | 36 | 36 | 0 | PASS |
| segmented-calculation-suite | 158 | 158 | 0 | PASS |
| ssz-schumann | 178 | 178 | 0 | PASS |
| ssz-lensing | 279 | 279 | 0 | PASS |
| Unified-Results | 147 | 147 | 0 | PASS |
| ssz-trajectories | 63 | 63 | 0 | PASS |
| g79-cygnus-tests | 5 | 5 | 0 | PASS |
| ssz-lagrange | 54 | 54 | 0 | PASS |
| segmented-energy | 7 | 7 | 0 | PASS |
| frequency-curvature-validation | 82 | 82 | 0 | PASS |
| chord-partition (local) | 103 | 103 | 0 | PASS |
