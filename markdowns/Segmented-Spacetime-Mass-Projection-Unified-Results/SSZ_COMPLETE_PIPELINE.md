# SSZ Complete Analysis Pipeline

## Overview

`python run_all_ssz_terminal.py` executes the **complete SSZ analysis pipeline** with 20+ scripts organized in phases.

---

## Phase 0: All-in-One Extended Analysis

**Current main script:**
```bash
python segspace_all_in_one_extended.py all
```

**Alternative (basic version):**
```bash
python segspace_all_in_one.py all
```

**Comprehensive analysis includes:**
- Paired sign tests (SEG vs SR/GR)
- Redshift analysis
- Bound energy calculations
- Mass validation (12 orders of magnitude)
- Statistical significance tests
- φ-lattice BIC comparison
- Dual velocity invariants

---

## Phase 1: Covariant Tests & Basic Validation

**Root-level Python scripts:**
```bash
python ssz_covariant_smoketest_verbose_lino_casu.py  # Covariant formulation
python test_ppn_exact.py                              # PPN parameters β=γ=1
python test_c1_segments.py                            # C1 continuity
python test_c2_segments_strict.py                     # C2 strict continuity
python test_energy_conditions.py                      # WEC/DEC/SEC
python shadow_predictions_exact.py                    # Black hole shadows
python qnm_eikonal.py                                 # Quasi-normal modes
python test_vfall_duality.py --mass Earth --r-mults 1.1,2.0  # Dual velocity
python test_utf8_encoding.py                          # UTF-8 validation
python test_c2_curvature_proxy.py                     # C2 curvature proxy
```

**Total:** 10 root-level scripts

---

## Phase 1.5: Pytest Unit Tests (71 tests)

**Automated pytest execution:**
```bash
# SegWave tests (43 tests)
python -m pytest tests/ -v --tb=short --disable-warnings

# SSZ scripts tests (28 tests)
python -m pytest scripts/tests/ -v --tb=short --disable-warnings
```

**Test coverage:**
- `tests/test_segwave_core.py` - SegWave core functionality (20 tests)
- `tests/test_segwave_cli.py` - CLI tools (16 tests)
- `tests/test_print_all_md.py` - MD printing (6 tests)
- `tests/cosmos/test_multi_body_sigma.py` - Multi-body (1 test)
- `scripts/tests/test_ssz_kernel.py` - SSZ kernel (4 tests)
- `scripts/tests/test_ssz_invariants.py` - SSZ invariants (6 tests)
- `scripts/tests/test_cosmo_fields.py` - Cosmology fields (1 test)
- `scripts/tests/test_cosmo_multibody.py` - Multi-body cosmo (3 tests)
- `scripts/tests/test_data_fetch.py` - GAIA data (3 tests)
- `scripts/tests/test_gaia_required_columns.py` - GAIA columns (3 tests)
- `scripts/tests/test_plot_ssz_maps.py` - SSZ plotting (2 tests)
- `scripts/tests/test_segmenter.py` - Segmenter (2 tests)
- `scripts/tests/test_utf8_encoding.py` - UTF-8 (4 tests)

**Total:** 71 pytest unit tests

---

## Phase 2: φ-Lattice Tests

```bash
python phi_test.py --in real_data_full.csv --outdir out/
python phi_bic_test.py --in real_data_full.csv --outdir out/
```

**Tests:**
- Golden Ratio (φ) lattice hypothesis
- BIC (Bayesian Information Criterion) comparison
- Frequency emission/observation analysis

---

## Phase 3: Velocity from Redshift

```bash
python compute_vfall_from_z.py --in real_data_full.csv --outdir vfall_out/
```

**Computes:**
- Fall velocities from redshift data
- Dual velocity validation
- Statistical distributions

---

## Phase 4: Segspace Analysis Suite

**Note:** Most functionality is now in Phase 0's `segspace_all_in_one_extended.py all`

**Legacy scripts (still called by run_all_ssz_terminal.py):**
```bash
python segspace_final_test.py --csv real_data_30_segmodel.csv
python segspace_final_explain.py
python segspace_enhanced_test_better_final.py  # VERALTET - wird noch aufgerufen
```

**Optional demos:**
```bash
python final_test.py
python segmented_full_proof.py
python segmented_full_calc_proof.py
python segmented_full_compare_proof.py
```

**Important:** 
- `segspace_all_in_one_extended.py` (Phase 0) is the current main script
- Phase 4 scripts are legacy but still executed for compatibility
- No script called `segspace_all_in_one_enhanced.py` exists!

---

## Phase 5: Advanced Analysis

### 5.6 Lagrangian Geodesic Tests

```bash
python lagrangian_tests.py --object sun
python lagrangian_tests.py --object sgrA
python lagrangian_tests.py --mass 8.544456e36 --label "Sgr A*" --eps3 -4.8
```

**Tests:**
- Geodesic equations
- Effective potentials
- ISCO calculations
- Orbital stability

### 5.7 Effective Stress-Energy Tensor

```bash
python derive_effective_stress_energy.py --M 1.98847e30 --eps3 -4.8 --r-mults 1.2,2,3,5,10
python derive_effective_stress_energy.py --M 8.544456e36 --eps3 -4.8 --r-mults 1.2,2,3,5 --latex reports/ssz_sources_latex.txt
```

**Derives:**
- T_μν components
- Energy density ρ
- Pressure components (p_r, p_t)
- LaTeX output for papers

### 5.8 Theory Calculations (Action-Based Scalar)

```bash
python ssz_theory_segmented.py \
    --M 1.98847e30 \
    --mode exterior \
    --coord lnr \
    --rmin-mult 1.05 \
    --rmax-mult 12 \
    --grid 200 \
    --phi0 1e-4 --phip0 0 \
    --pr0 0 --rho0 0 --cs2 0.30 \
    --mphi 1e-7 --lam 1e-6 \
    --Z0 1.0 --alpha 3e-3 --beta=-8e-3 \
    --Zmin 1e-8 --Zmax 1e8 \
    --phi-cap 5e-3 --phip-cap 1e-3 \
    --max-step-rs 0.02 \
    --export out_theory_exterior.csv
```

**Computes:**
- Scalar field evolution
- Action-based formulation
- Exterior spacetime
- Full numerical integration

---

## Phase 6: EHT Shadow Comparison & Ring Analysis

**NEW: Now automatically executed in run_all_ssz_terminal.py!**

### 6.1 EHT Shadow Comparison Matrix

```bash
python scripts/analysis/eht_shadow_comparison.py
```

**Compares:**
- SSZ shadow predictions vs EHT observations
- M87* shadow radius (M87*)
- Sgr A* shadow predictions  
- Comparison matrix with GR
- Statistical significance
- Output: comparison tables and plots

### 6.2 SSZ Rings Analysis

**Automated for example datasets:**
```bash
# G79.29+0.46 (multi-shell LBV nebula)
python scripts/ring_temperature_to_velocity.py --csv data/observations/G79_29+0_46_CO_NH3_rings.csv

# Cygnus X Diamond Ring
python scripts/ring_temperature_to_velocity.py --csv data/observations/CygnusX_DiamondRing_CII_rings.csv
```

**Analysis:**
- Temperature-velocity conversion for expanding rings
- NH3/CO line analysis
- Shock front kinematics
- Radial velocity profiles
- Comparison with SSZ predictions

### 6.3 Redshift Robustness

```bash
python scripts/analysis/redshift_robustness.py
```

**Tests:**
- Redshift measurement robustness
- Bootstrap analysis
- Confidence intervals
- Outlier detection

---

## Phase 7: Test Summary & Visualization

### 7.1 Complete Test Summary

```bash
python ci/summary-all-tests.py
```

**Generates:**
- Complete test results summary
- Pass/fail statistics
- Performance metrics
- HTML report

### 7.2 Summary Visualization

```bash
python ci/summary_visualize.py
```

**Creates:**
- Visual test result dashboard
- Performance plots
- Coverage analysis
- Trend visualization

---

## Phase 8: Final Interpretation & Summary

**Generates:**
- `full_pipeline/reports/summary_full_terminal_v4.json`
- Dual velocity blocks with invariants
- Quality assessment
- Statistical significance summary
- ASCII-safe interpretation (Windows compatible)

---

## Complete Output

**Analysis Reports:**
- `agent_out/reports/redshift_paired_stats.json`
- `agent_out/reports/redshift_medians.json`
- `agent_out/reports/bound_energy.txt`
- `agent_out/reports/segmented_spacetime_mass_validation.csv`
- `full_pipeline/reports/summary_full_terminal_v4.json`

**Data Files:**
- `out_theory_exterior.csv`
- `vfall_out/*.csv`
- Various validation CSVs

**Visualizations:**
- Shadow predictions
- QNM calculations
- Lagrangian effective potentials
- Bound energy plots

---

## Execution Time

**Total: ~10-15 minutes**

Breakdown:
- Phase 0: ~3-4 min (All-in-one)
- Phase 1: ~2-3 min (Covariant tests)
- Phase 2: ~1 min (φ-tests)
- Phase 3: ~1 min (v_fall)
- Phase 4: ~2-3 min (Segspace suite)
- Phase 5: ~2-3 min (Advanced analysis)
- Phase 6: <1 min (Summary)

---

## Scientific Results

Expected validation:
- ✅ PPN: β = γ = 1 (GR match in weak field)
- ✅ Mass roundtrip: error < 1e-42
- ✅ Dual velocity invariant: v_esc × v_fall = c²
- ✅ Energy conditions: WEC/DEC/SEC hold for r ≥ 5r_s
- ✅ Paired sign test: p < 1e-18
- ✅ φ-lattice: ΔBIC > +100
- ✅ Shadow predictions: Finite photon sphere
- ✅ QNM: Stable quasi-normal modes

---

## Production-Ready Analysis Scripts (NEW - Oct 2025)

**Three powerful standalone tools for advanced analysis:**

### 1. Rapidity-Based Equilibrium Analysis
```bash
python perfect_equilibrium_analysis.py
```

**Features:**
- Eliminates 0/0 singularities at equilibrium points
- Rapidity formulation: χ = arctanh(v/c)
- Angular bisector for natural coordinate origin
- Expected impact: 0% → 35-50% at r < 2 r_s

**Documentation:** [RAPIDITY_IMPLEMENTATION.md](RAPIDITY_IMPLEMENTATION.md)

### 2. Standalone Interactive Analysis
```bash
# Interactive mode
python perfect_seg_analysis.py --interactive

# Single observation
python perfect_seg_analysis.py --mass 1.0 --radius 10000 --redshift 0.001

# CSV batch
python perfect_seg_analysis.py --csv data.csv --output results.csv
```

**Features:**
- 3 usage modes (Interactive/Single/CSV)
- Flexible CSV column detection
- Regime classification
- Rapidity-based (NO 0/0!)

**Documentation:** [PERFECT_SEG_ANALYSIS_GUIDE.md](PERFECT_SEG_ANALYSIS_GUIDE.md)

### 3. Perfect Paired Test Framework
```bash
python perfect_paired_test.py --csv data/real_data_full.csv --output results.csv
```

**Features:**
- Incorporates ALL findings (φ-geometry + Rapidity + Stratification)
- Regime-specific statistics (Photon Sphere: 82%, High v: 86%)
- Complete binomial tests and p-values
- Framework ready for full SEG integration

**Documentation:** [PERFECT_PAIRED_TEST_GUIDE.md](PERFECT_PAIRED_TEST_GUIDE.md)

**Key Scientific Advances (Oct 2025):**
- ✅ **Equilibrium solution:** Rapidity formulation eliminates 0/0
- ✅ **φ-geometry validated:** FUNDAMENTAL basis (not fitting)
- ✅ **Regime understanding:** Know exactly where SEG excels
- ✅ **Statistical significance achievable:** p<0.05 possible after integration

---

## Copyright

© 2025 Carmen Wrede und Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
