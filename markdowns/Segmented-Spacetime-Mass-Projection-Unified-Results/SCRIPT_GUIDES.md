# Script Usage Guides - SSZ Theory

**Detailed usage instructions for all scripts**

Date: 2025-10-29  
Version: 1.0 Final

© 2025 Carmen Wrede & Lino Casu

---

## Table of Contents

1. [Validation Scripts](#validation-scripts)
2. [Test Scripts](#test-scripts)
3. [Analysis Scripts](#analysis-scripts)
4. [Utility Scripts](#utility-scripts)
5. [Reproduction Instructions](#reproduction-instructions)

---

## Validation Scripts

### run_complete_validation_extended.py

**Purpose:** Extended master validation pipeline with comprehensive error logging

**Command:**
```bash
python run_complete_validation_extended.py
```

**What it does:**
1. Runs formula verification
2. Runs complete test suite (22 tests)
3. Runs ToE unified validation (11 steps, includes BH bomb)
4. Runs ToE v2 deterministic (6 pillars, includes BH bomb)
5. Runs grid convergence tests
6. Runs proper time validation
7. Runs theory validation
8. Runs individual physics tests (PPN, energy, etc.)
9. Runs analysis scripts
10. Collects all outputs
11. Generates comprehensive reports

**Runtime:** 10-15 minutes

**Outputs:**
```
validation_complete_extended/
├── full-output-extended.md (complete log)
├── COMPLETE_VALIDATION_SUMMARY_EXTENDED.md (summary)
├── error_log.txt (detailed error log)
├── validation_results_extended.json (machine-readable)
├── plots/ (38+ PNG files)
├── reports/ (329+ MD/JSON files)
├── data/ (17+ CSV files)
└── logs/ (individual step logs)
```

**Success Criteria:**
- Critical tests: ALL PASS
- Overall success rate: > 80%
- Error log: Minimal entries
- All plots generated
- All reports created

**Reproduction:**
```bash
# 1. Clear cache
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux

# 2. Run pipeline
python run_complete_validation_extended.py

# 3. Check results
cat validation_complete_extended/COMPLETE_VALIDATION_SUMMARY_EXTENDED.md
```

---

### verify_theory_scientific.py

**Purpose:** Verify all SSZ formulas are scientifically correct

**Command:**
```bash
python verify_theory_scientific.py
```

**Tests Performed:**

**Test 1: Formel-Korrektheit**
- Validates Ξ(r) formula
- Validates D(r) formula
- Success: Values match expected

**Test 2: Test-Daten-Vergleich**
- Compares formula output with CSV test data
- Success: Difference < 1s (0.000s expected)

**Test 3: Universal Intersection**
- Calculates r* and D*
- Success: Matches published values (< 1e-5)

**Test 4: Causality Check**
- Validates 0 < D ≤ 1 everywhere
- Success: No causality violations

**Test 5: SSZ Asymptotic Behavior (INFO)**
- Checks D(r→∞) = 0.5
- Note: This is INFO, not failure
- SSZ feature: Vacuum segment density

**Test 6: Golden Ratio**
- Validates φ = (1 + √5) / 2
- Verifies φ² = φ + 1
- Success: Error < 1e-13

**Expected Result:**
```
5/6 Tests bestanden
[OK] ALL CRITICAL TESTS PASSED
INFO tests are expected SSZ behavior
Exit code: 0
```

**Reproduction:**
```bash
python verify_theory_scientific.py
# Should complete in ~5 seconds
# Exit code should be 0
```

---

### run_full_suite.py

**Purpose:** Run complete test suite with all physics tests

**Command:**
```bash
python run_full_suite.py
```

**Test Phases:**

**Phase 1: Root-Level Tests (6 tests)**
- test_ppn_exact.py
- test_vfall_duality.py
- test_energy_conditions.py
- test_c1_segments.py
- test_c2_segments_strict.py
- test_c2_curvature_proxy.py

**Phase 2: SegWave Tests (20 tests)**
- 16 physics tests (Q-Factor, velocity, frequency, γ)
- 4 technical tests (CLI, silent)

**Phase 3: Scripts Tests (15 tests)**
- 9 physics tests (kernel, invariants, etc.)
- 6 technical tests (silent)

**Phase 4: Cosmos Tests (1 test)**
- Multi-body sigma test

**Phase 5: SSZ Complete Analysis**
- Runs segspace_all_in_one_extended.py

**Phase 6: Example Runs**
- G79 region
- Cygnus X region

**Phase 7: Generate Summary**
- reports/RUN_SUMMARY.md
- reports/full-output.md

**Phase 8: Echo Summary**
- Terminal output

**Expected Result:**
```
Total Physics Tests: 35
Total Tests: 22 (counted)
Passed: 22/22
Failed: 0/22
Success Rate: 100.0%
```

**Runtime:** ~224 seconds (~4 minutes)

**Reproduction:**
```bash
# Clear cache first
.\CLEAR_CACHE.bat

# Run suite
python run_full_suite.py

# Check summary
cat reports/RUN_SUMMARY.md
```

---

### run_ssz_unified_validation.py

**Purpose:** Theory of Everything (ToE) unified validation with 11 steps

**Command:**
```bash
python run_ssz_unified_validation.py
```

**Validation Steps:**

**Step 1: Model Initialization**
- Initialize SSZ and GR models
- Validate parameters

**Step 2: Universal Intersection**
- Find r* where SSZ = GR
- Verify mass-independence
- Expected: r*/r_s ≈ 1.386562

**Step 3: Black-Hole Stability (BOMB TEST)**
- Superradiant instability test
- Calculate baseline gain
- Calculate SSZ gain
- Expected: Gain reduction ≥ 6×

**Step 4: Time Emergence**
- Validate time dilation
- Proper time calculations

**Step 5: Time Chaos Boundary**
- Check boundary conditions
- No chaos in physical regime

**Step 6: Neutron-Star Prediction**
- Calculate stability band
- Testable with SKA

**Step 7: φ Invariance**
- Verify golden ratio preserved
- φ² = φ + 1

**Step 8: Singularity Resolution**
- Check curvature at r=0
- Must be finite

**Step 9: ToE Architecture**
- Validate unification framework
- Gravity + Time + Quantum

**Step 10: Summary and Output**
- Generate plots (6 PNG files)
- Create reports

**Step 11: Optional Extensions**
- Extension framework

**Expected Result:**
```
All 11 steps PASS
BH stability: Gain reduction 6.55× (>6×)
ToE Consistency Score: 83.3%
```

**Runtime:** ~180 seconds (~3 minutes)

**Outputs:**
```
outputs/unified_validation/
├── step2_intersection.png
├── step3_bh_stability.png
├── step4_time_emergence.png
├── step5_chaos_boundary.png
├── step6_ns_prediction.png
└── step9_toe_architecture.png
```

**Reproduction:**
```bash
python run_ssz_unified_validation.py
# Check outputs/unified_validation/ for plots
```

---

### run_toe_validation_v2.py

**Purpose:** Deterministic ToE validation with 6 pillars

**Command:**
```bash
python run_toe_validation_v2.py
```

**Deterministic Setup:**
```python
PY_SEED = 133742
NP_SEED = 424242
NumPy version: 2.2.6
BLAS: Single-threaded
```

**6 Pillars:**

**Pillar 1: Universal Intersection**
- L2 norm < 0.50
- r*/r_s bracket error < 1e-4

**Pillar 2: φ-Invariance**
- |φ_meas - φ| < 5e-6

**Pillar 3: Neutron Star Signature**
- Band relative width < 0.35

**Pillar 4: Singularity Resolution**
- R_sup(r→0) < 1.05

**Pillar 5: BH Stability (BOMB TEST)**
- Gain reduction ≥ 6.0×

**Pillar 6: Cosmology Fit**
- RMSE Hubble < 0.12
- RMSE BAO < 0.12
- RMSE fσ8 < 0.10

**Expected Result:**
```
All 6 pillars PASS (100%)
ToE Score: 100%
BH stability: Gain reduction 6.55×
```

**Runtime:** ~2 seconds

**Outputs:**
```
validation_out_v2/
├── COMPLETE_VALIDATION_SUMMARY.md
├── SCIENTIFIC_INTERPRETATIONS.md
├── ToE_DASHBOARD.png
├── P1_*.json (Universal Intersection)
├── P2_*.json (φ-Invariance)
├── P3_*.json (NS Signature)
├── P4_*.json (Singularity Resolution)
├── P5_*.json (BH Stability)
└── P6_*.json (Cosmology)
```

**Reproduction:**
```bash
python run_toe_validation_v2.py
# Results are bit-exact reproducible
# Same seeds → same results
```

---

### test_grid_convergence.py

**Purpose:** Numerical grid convergence verification (F-16)

**Command:**
```bash
python test_grid_convergence.py
```

**Method:**
- Richardson extrapolation
- h-refinement: h → h/2 → h/4
- Test points: r = 1.5, 2.0, 3.0, 5.0 r_s

**Success Criteria:**
- Convergence order p ≥ 1.8
- Extrapolation error < 1%

**Expected Result:**
```
All 4 test points PASS
Convergence order: p = ∞ (analytically exact)
Extrapolation error: 0.0000%
```

**Runtime:** ~1 second

**Reproduction:**
```bash
python test_grid_convergence.py
# Should complete instantly
```

---

## Test Scripts

### test_ppn_exact.py

**Purpose:** Validate PPN (Parametrized Post-Newtonian) parameters

**Command:**
```bash
python test_ppn_exact.py
```

**Tests:**
- β parameter (Eddington-Robertson)
- γ parameter (Eddington-Robertson)

**Expected:**
```
β = 1.0 (GR limit)
γ = 1.0 (GR limit)
SSZ matches GR in weak field
```

**Physical Meaning:**
- β = 1: Correct amount of space curvature
- γ = 1: Correct amount of time dilation

**Reproduction:**
```bash
python test_ppn_exact.py
# Exit code should be 0
```

---

### test_vfall_duality.py

**Purpose:** Test dual velocity invariant

**Command:**
```bash
python test_vfall_duality.py
```

**Tests:**
- v_esc × v_fall = c²
- Fundamental invariant

**Expected:**
```
v_esc × v_fall = c²
Error: 0.000e+00 (machine precision)
```

**Physical Meaning:**
- Escape velocity times freefall velocity = c²
- Fundamental constraint of spacetime geometry

**Reproduction:**
```bash
python test_vfall_duality.py
# Should show error = 0.000e+00
```

---

### test_energy_conditions.py

**Purpose:** Validate energy conditions (WEC, DEC, SEC)

**Command:**
```bash
python test_energy_conditions.py
```

**Tests:**
- Weak Energy Condition (WEC)
- Dominant Energy Condition (DEC)
- Strong Energy Condition (SEC)

**Expected:**
```
WEC: SATISFIED for r ≥ 5r_s
DEC: SATISFIED for r ≥ 5r_s
SEC: SATISFIED for r ≥ 5r_s
```

**Physical Meaning:**
- WEC: Energy density non-negative
- DEC: Energy cannot travel faster than light
- SEC: Gravity is attractive

**Reproduction:**
```bash
python test_energy_conditions.py
# All conditions should be satisfied
```

---

## Analysis Scripts

### segspace_all_in_one_extended.py

**Purpose:** Complete SSZ analysis (all-in-one)

**Command:**
```bash
python segspace_all_in_one_extended.py
```

**Analyses:**
1. Mass validation (12 orders of magnitude)
2. Time dilation calculations
3. Universal intersection finding
4. Sensitivity analysis
5. Proper time plots
6. Redshift calculations

**Outputs:**
- Multiple PNG plots
- CSV data files
- Analysis summaries

**Runtime:** ~60 seconds

**Reproduction:**
```bash
python segspace_all_in_one_extended.py
# Check current directory for plots
```

---

### shadow_predictions_exact.py

**Purpose:** Black hole shadow predictions

**Command:**
```bash
python shadow_predictions_exact.py
```

**Calculations:**
- Shadow radius for various masses
- SSZ vs GR comparison
- Photon sphere location

**Outputs:**
- Shadow prediction data
- Comparison tables

**Runtime:** ~30 seconds

**Reproduction:**
```bash
python shadow_predictions_exact.py
# Check output for shadow radius data
```

---

### lagrangian_tests.py

**Purpose:** Lagrangian formulation tests

**Commands:**
```bash
# Sun
python lagrangian_tests.py --object sun

# Jupiter
python lagrangian_tests.py --object jupiter

# Neutron Star
python lagrangian_tests.py --object ns

# Black Hole
python lagrangian_tests.py --object bh
```

**Tests:**
- Action principle
- Euler-Lagrange equations
- Variational formulation

**Expected:**
```
Action: Extremal
Equations: Satisfied
Lagrangian: Valid
```

**Reproduction:**
```bash
for obj in sun jupiter ns bh; do
    python lagrangian_tests.py --object $obj
done
```

---

## Utility Scripts

### CLEAR_CACHE Scripts

**Windows (CLEAR_CACHE.bat):**
```batch
.\CLEAR_CACHE.bat
```

**Linux/macOS (CLEAR_CACHE.sh):**
```bash
./CLEAR_CACHE.sh
```

**What it does:**
1. Clears __pycache__ directories
2. Clears .pytest_cache directories
3. Deletes .pyc files
4. Deletes .pyo files
5. Clears Python cache

**When to use:**
- Before running tests
- After updating code
- When tests show stale results
- Before reproduction runs

---

### Installation Scripts

**Windows (install.ps1):**
```powershell
.\install.ps1
```

**Linux/macOS (install.sh):**
```bash
chmod +x install.sh
./install.sh
```

**What it does:**
1. Creates virtual environment
2. Installs dependencies
3. Checks data files
4. Fetches Planck data if missing
5. Runs test suite
6. Generates summary

**Runtime:** ~5-20 minutes (depending on download speed)

---

## Reproduction Instructions

### Complete Reproduction Protocol

**For bit-exact reproduction of ALL results:**

**Step 1: Clean Environment**
```bash
# Clone fresh
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Clear any caches
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux
```

**Step 2: Install Exact Dependencies**
```bash
# Create venv
python -m venv .venv

# Activate
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # Linux

# Install exact versions
pip install -r requirements.txt
```

**Step 3: Run Extended Pipeline**
```bash
python run_complete_validation_extended.py
```

**Step 4: Verify Results**
```bash
# Check summary
cat validation_complete_extended/COMPLETE_VALIDATION_SUMMARY_EXTENDED.md

# Check error log
cat validation_complete_extended/error_log.txt

# Expected:
# - Total steps: 12
# - Passed: 10+/12
# - Critical failures: 0
# - Error log: Minimal
```

**Step 5: Run Deterministic ToE v2**
```bash
python run_toe_validation_v2.py

# Expected (bit-exact):
# - All 6 pillars PASS
# - r*/r_s = 1.386562
# - D* = 0.528007
# - φ = 1.618034
# - BH gain reduction = 6.55×
```

---

### Individual Test Reproduction

**Formula Verification:**
```bash
python verify_theory_scientific.py
# Expected: 5/5 PASS + 1 INFO, exit 0
```

**Test Suite:**
```bash
.\CLEAR_CACHE.bat
python run_full_suite.py
# Expected: 22/22 PASS (100%)
```

**ToE Unified:**
```bash
python run_ssz_unified_validation.py
# Expected: 11/11 PASS, BH bomb 6.55×
```

**Grid Convergence:**
```bash
python test_grid_convergence.py
# Expected: 4/4 PASS, p = ∞
```

---

### Troubleshooting Reproduction

**Issue: Different numerical results**
- Cause: Random seeds not fixed
- Solution: Use run_toe_validation_v2.py (deterministic)

**Issue: Tests fail**
- Cause: Cache corruption
- Solution: Run CLEAR_CACHE before tests

**Issue: Import errors**
- Cause: Wrong Python version or missing deps
- Solution: Use Python 3.10+, reinstall from requirements.txt

**Issue: Timeout**
- Cause: System too slow
- Solution: Increase timeouts in pipeline scripts

---

## Quick Reference

### Most Common Commands

```bash
# Complete validation
python run_complete_validation_extended.py

# Quick test
python run_full_suite.py

# Formula check
python verify_theory_scientific.py

# ToE validation
python run_ssz_unified_validation.py

# Clear cache
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux
```

### Expected Runtimes

| Script | Runtime |
|--------|---------|
| verify_theory_scientific.py | ~5s |
| test_grid_convergence.py | ~1s |
| run_toe_validation_v2.py | ~2s |
| test_ppn_exact.py | ~30s |
| run_ssz_unified_validation.py | ~180s |
| run_full_suite.py | ~224s |
| run_complete_validation_extended.py | ~600-900s |

---

**© 2025 Carmen Wrede & Lino Casu**

**Version:** 1.0 Final  
**Date:** 2025-10-29
