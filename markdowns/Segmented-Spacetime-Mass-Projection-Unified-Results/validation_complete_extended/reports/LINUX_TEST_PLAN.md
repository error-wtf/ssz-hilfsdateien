# Linux Test Suite - Complete Test Plan

**Target:** H:\WINDSURF\Segmented-Spacetime-TEST-SUITE-Linux  
**Date:** 2025-10-18

---

## Pre-Test Checklist

Before testing, verify files were copied:

```bash
cd H:/WINDSURF/Segmented-Spacetime-TEST-SUITE-Linux

# Check key files exist:
ls -la install.sh
ls -la run_full_suite.py
ls -la test_ppn_exact.py
ls -la tests/test_segwave_core.py
ls -la scripts/tests/test_ssz_kernel.py
```

---

## Test Phase 1: Installation

### Step 1.1: Make install script executable

```bash
chmod +x install.sh
```

### Step 1.2: Run installation

```bash
./install.sh
```

**Expected Output:**
```
===================================================================================================
SSZ PROJECTION SUITE - LINUX INSTALLER
===================================================================================================

[1/10] Checking Python installation...
  Found: Python 3.x.x

[2/10] Setting up virtual environment...
  Virtual environment created

[3/10] Activating virtual environment...
  Activated: .venv

[4/10] Upgrading pip, setuptools, wheel...
  Upgraded core packages

[5/10] Installing dependencies...
  Found: requirements.txt
  Installed from requirements.txt

[6/10] Installing SSZ Suite package...
  Installed package

[7/10] Running test suite...
  Running ALL tests (root + tests/ + scripts/tests/)...

Root-level SSZ tests:
  test_ppn_exact.py PASSED
  test_vfall_duality.py PASSED
  test_energy_conditions.py PASSED
  test_c1_segments.py PASSED
  test_c2_segments_strict.py PASSED
  test_c2_curvature_proxy.py PASSED
  test_utf8_encoding.py PASSED

Pytest test suites:
================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
β = 1.000000000000
γ = 1.000000000000
...
PASSED

[... ALL TESTS WITH DETAILED OUTPUT ...]

  ✓ All tests passed

[8/10] Checking data files...
  ✓ real_data_full.csv found
  ✓ gaia/gaia_sample_small.csv found
  ⚠ Planck data missing (2GB) - fetching...
  [████████████████] 100%
  ✓ Planck data fetched

[9/10] Verifying installation...
  ✓ Package installed successfully

[10/10] Installation complete!
```

**Success Criteria:**
- ✅ All 7 root tests PASS
- ✅ All pytest tests show detailed output
- ✅ No pytest crashes
- ✅ Data files found or fetched
- ✅ Package installed

---

## Test Phase 2: Individual Physics Tests

### Step 2.1: Activate environment

```bash
source .venv/bin/activate
```

### Step 2.2: Test root-level physics tests

```bash
python test_ppn_exact.py
```

**Expected:**
```
================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
β = 1.000000000000 (perfect)
γ = 1.000000000000 (perfect)

Physical Interpretation:
  • β=1 → No preferred frame
  • γ=1 → GR-like curvature
================================================================================
PASSED
```

**Run all root tests:**
```bash
python test_ppn_exact.py
python test_vfall_duality.py
python test_energy_conditions.py
python test_c1_segments.py
python test_c2_segments_strict.py
python test_c2_curvature_proxy.py
```

**Success:** All show detailed output with Physical Interpretations ✅

---

### Step 2.3: Test pytest physics tests

```bash
pytest tests/test_segwave_core.py -s -v
```

**Expected:**
```
================================================================================
Q-FACTOR: Temperature Only (β=1)
================================================================================
q_k = (T_curr/T_prev)^β = 0.800000

Physical Interpretation:
  • Basic temperature effect on q_k
================================================================================
PASSED

[... 15 more tests with detailed output ...]

======================== 16 passed in 5.6s =========================
```

**Test all physics:**
```bash
pytest tests/test_segwave_core.py -s -v
pytest scripts/tests/test_ssz_kernel.py -s -v
pytest scripts/tests/test_ssz_invariants.py -s -v
pytest scripts/tests/test_segmenter.py -s -v
pytest scripts/tests/test_cosmo_multibody.py -s -v
pytest tests/cosmos/test_multi_body_sigma.py -s -v
```

**Success:** All show detailed Physical Interpretations ✅

---

## Test Phase 3: Technical Tests (Silent)

```bash
pytest tests/test_segwave_cli.py -s -v
pytest tests/test_print_all_md.py -s -v
```

**Expected:**
```
tests/test_segwave_cli.py::test_help_flag PASSED
tests/test_segwave_cli.py::test_invalid_csv_path PASSED
...
======================== 16 passed in 30s =========================
```

**Success:** Only PASSED shown (no verbose output) ✅

---

## Test Phase 4: Full Test Suite

```bash
python run_full_suite.py
```

**Expected:**
```
====================================================================================================
SSZ PROJECTION SUITE - FULL TEST & ANALYSIS WORKFLOW
====================================================================================================

PHASE 1: ROOT-LEVEL SSZ TESTS
----------------------------------------------------------------------------------------------------
[RUNNING] PPN Exact Tests
  Command: python test_ppn_exact.py

================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
...
PASSED

[OK] PPN Exact Tests (took 0.1s)

[... ALL PHASES ...]

====================================================================================================
SUMMARY REPORT
====================================================================================================

Total Physics Tests: 35
Silent Technical Tests: 23
Passed: 35/35
Failed: 0/35
Success Rate: 100.0%

====================================================================================================
GENERATING DETAILED OUTPUT LOG
====================================================================================================

✓ Detailed output log written to: reports/summary-output.md
   File size: 245.8 KB

To view the complete log:
   cat reports/summary-output.md

====================================================================================================
WORKFLOW COMPLETE
====================================================================================================

📊 Summary Files:
   • reports/RUN_SUMMARY.md
   • reports/summary-output.md

✅ ALL TESTS PASSED
```

**Success Criteria:**
- ✅ Passed: 35/35
- ✅ Failed: 0/35
- ✅ Summary files generated
- ✅ No crashes

---

## Test Phase 5: Data Fetching

### Step 5.1: Check data files

```bash
ls -lh data/real_data_full.csv
ls -lh data/gaia/gaia_sample_small.csv
ls -lh data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt
```

**Expected:**
```
-rw-r--r-- 1 user user  50M  data/real_data_full.csv
-rw-r--r-- 1 user user   1M  data/gaia/gaia_sample_small.csv
-rw-r--r-- 1 user user   2G  data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt
```

### Step 5.2: Test Planck fetch script

```bash
# If Planck data missing:
python scripts/fetch_planck.py
```

**Expected:**
```
================================================================================
PLANCK CMB POWER SPECTRUM - DATA FETCH
================================================================================

Dataset: Planck 2018 Release 3
File: COM_PowerSpect_CMB-TT-full_R3.01.txt
Size: ~2 GB

Attempting download from ESA Planck Legacy Archive...
[████████████████████████████] 100.0% (2048.3/2048.3 MB)

✓ Download complete!
```

**Success:** Planck data present and valid ✅

---

## Test Phase 6: Documentation

### Step 6.1: Check README files

```bash
cat tests/README_TESTS.md | head -20
cat scripts/tests/README_SCRIPTS_TESTS.md | head -20
cat TESTING_COMPLETE_GUIDE.md | head -20
```

**Success:** All documentation present ✅

### Step 6.2: Check papers

```bash
ls papers/*.md
ls papers/*.pdf
```

**Expected:**
```
papers/ssz_theory.md
papers/ssz_theory.pdf
papers/validation_results.md
papers/validation_results.pdf
...
```

**Success:** Both MD and PDF versions present ✅

---

## Test Phase 7: Cache & Re-Installation

### Step 7.1: Clear cache

```bash
python -c "import pathlib, shutil; [shutil.rmtree(p, ignore_errors=True) for p in pathlib.Path('.').rglob('__pycache__')]"
```

### Step 7.2: Re-run single test

```bash
python test_ppn_exact.py
```

**Expected:** Still shows detailed output ✅

### Step 7.3: Re-install (should skip data)

```bash
./install.sh
```

**Expected at Step [8/10]:**
```
[8/10] Checking data files...
  ✓ real_data_full.csv found
  ✓ gaia/gaia_sample_small.csv found
  ✓ Planck data found (skipping download)  ← IMPORTANT!
```

**Success:** No re-download of Planck! ✅

---

## Test Phase 8: Verify Generated Reports

```bash
cat reports/RUN_SUMMARY.md
```

**Expected:**
```
# SSZ Suite Run Summary - Physics Tests

**Date:** 2025-10-18 ...

## Overview

- **Physics Test Suites:** 16
- **Silent Technical Tests:** 3
- **Passed:** 16
- **Failed:** 0
- **Success Rate:** 100.0%
```

```bash
ls -lh reports/summary-output.md
```

**Expected:**
```
-rw-r--r-- 1 user user 245K reports/summary-output.md
```

**Success:** Both summary files generated ✅

---

## Test Phase 9: Linux-Specific Features

### Step 9.1: Test shell permissions

```bash
ls -l install.sh
```

**Expected:**
```
-rwxr-xr-x 1 user user ... install.sh
```

### Step 9.2: Test symlinks (if any)

```bash
find . -type l
```

**Expected:** None or all valid

### Step 9.3: Test line endings

```bash
file install.sh
```

**Expected:**
```
install.sh: Bourne-Again shell script, ASCII text executable
```

**Success:** Correct Unix line endings ✅

---

## Test Phase 10: Performance Benchmark

```bash
time python run_full_suite.py
```

**Expected:**
```
real    2m30s
user    2m15s
sys     0m10s
```

**Success:** Completes in ~2-3 minutes ✅

---

## Final Verification Checklist

### Core Functionality:
- [ ] Installation completes without errors
- [ ] All 35 physics tests show detailed output
- [ ] All 23 technical tests run silently
- [ ] No pytest crashes (I/O error)
- [ ] Summary shows 35/35 passed, 0/35 failed

### Data Files:
- [ ] real_data_full.csv present (~50 MB)
- [ ] GAIA small files present (~1 MB)
- [ ] Planck data fetched or present (~2 GB)
- [ ] Re-installation skips existing data

### Documentation:
- [ ] tests/README_TESTS.md exists
- [ ] scripts/tests/README_SCRIPTS_TESTS.md exists
- [ ] TESTING_COMPLETE_GUIDE.md exists
- [ ] Papers in both MD and PDF

### Output Files:
- [ ] reports/RUN_SUMMARY.md generated
- [ ] reports/summary-output.md generated (~100-500 KB)
- [ ] Both files contain correct data

### Linux-Specific:
- [ ] install.sh has execute permissions
- [ ] Correct Unix line endings
- [ ] No Windows-specific issues
- [ ] Shell scripts work correctly

---

## Quick Test Commands

**Fast verification (5 minutes):**
```bash
# 1. Install
./install.sh

# 2. Quick test
python test_ppn_exact.py

# 3. One pytest suite
pytest tests/test_segwave_core.py -s -v

# 4. Check summary
cat reports/RUN_SUMMARY.md
```

**Full verification (15 minutes):**
```bash
# 1. Install
./install.sh

# 2. Full suite
python run_full_suite.py

# 3. Verify outputs
cat reports/RUN_SUMMARY.md
ls -lh reports/summary-output.md

# 4. Check data
ls -lh data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt
```

---

## Troubleshooting

### Problem: Permission denied
```bash
chmod +x install.sh
chmod +x scripts/*.py
```

### Problem: Python not found
```bash
# Check Python version:
python3 --version  # Should be 3.10+
```

### Problem: Pytest crash
```bash
# Ensure `-s` flag is used:
pytest tests/ -s -v --tb=short  # ✅ CORRECT
```

### Problem: Planck download fails
```bash
# Manual fetch:
python scripts/fetch_planck.py

# Or continue without (optional):
# Tests will skip Planck-dependent analyses
```

---

## Expected Results Summary

**If ALL tests pass:**

✅ **Installation:** Complete without errors  
✅ **Physics Tests:** 35/35 with detailed interpretations  
✅ **Technical Tests:** 23/23 silent (only PASSED)  
✅ **Data Files:** Present or fetched automatically  
✅ **Documentation:** Complete and accessible  
✅ **Reports:** Generated correctly  
✅ **Linux Compatibility:** Full compatibility verified  

**Total Time:** ~15-20 minutes (first run with Planck fetch)  
**Re-Install Time:** ~2-3 minutes (skips existing data)

---

## Success Criteria

**PASS:** All checkboxes checked ✅  
**FAIL:** Any checkbox unchecked ❌

**Next Step:** If Linux passes, test Windows suite!

---

## Contact

**Authors:** Carmen Wrede, Lino Casu  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4  
**Date:** 2025-10-18

---

**Ready to test Linux suite!** 🐧
