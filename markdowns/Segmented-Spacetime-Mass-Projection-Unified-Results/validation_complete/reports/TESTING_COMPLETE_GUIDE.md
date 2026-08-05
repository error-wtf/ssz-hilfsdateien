# SSZ Suite - Complete Testing Guide

**Last Updated:** 2025-10-18  
**Complete Test System Overhaul**

---

## Quick Start

```bash
# Full test suite (recommended):
python run_full_suite.py

# Installation with tests:
.\install.ps1  # Windows
./install.sh   # Linux/macOS

# Single test:
python test_ppn_exact.py

# Pytest tests:
pytest tests/test_segwave_core.py -s -v
```

---

## Test System Overview

### Total: 58 Tests

**Physics Tests (35)** - Detailed output with physical interpretations:
- 6 Root-level tests
- 17 tests/ directory tests
- 12 scripts/tests/ tests

**Technical Tests (23)** - Silent mode (run in background):
- UTF-8 encoding
- CLI validation
- MD printing
- Data fetching
- Field checks

---

## Directory Structure

```
SSZ-Suite/
├── test_*.py                    # Root physics tests (6)
├── tests/
│   ├── README_TESTS.md         # Tests documentation
│   ├── test_segwave_core.py    # 16 physics tests
│   ├── test_segwave_cli.py     # 16 technical (silent)
│   ├── test_print_all_md.py    # 6 technical (silent)
│   └── cosmos/
│       └── test_multi_body_sigma.py  # 1 physics test
├── scripts/
│   ├── fetch_planck.py         # NEW! Planck data fetcher
│   └── tests/
│       ├── README_SCRIPTS_TESTS.md  # Scripts tests docs
│       ├── test_ssz_kernel.py       # 4 physics tests
│       ├── test_ssz_invariants.py   # 6 physics tests
│       ├── test_segmenter.py        # 2 physics tests
│       └── test_cosmo_multibody.py  # 3 physics tests
├── run_full_suite.py           # Main test runner
├── install.ps1 / install.sh    # Installation scripts
└── reports/                     # Generated outputs
    ├── RUN_SUMMARY.md
    └── summary-output.md
```

---

## 1. Physics Tests (35 Tests - Verbose)

### Root-Level Tests (6)

```bash
python test_ppn_exact.py           # PPN parameters β, γ
python test_vfall_duality.py       # v_esc × v_fall = c²
python test_energy_conditions.py   # WEC/DEC/SEC
python test_c1_segments.py         # C1 continuity
python test_c2_segments_strict.py  # C2 strict
python test_c2_curvature_proxy.py  # Curvature proxy
```

### tests/test_segwave_core.py (16)

```bash
pytest tests/test_segwave_core.py -s -v
```

**Test Classes:**
- TestQFactor (3) - Temperature, density effects
- TestVelocityProfile (5) - Shell propagation
- TestFrequencyTrack (2) - Redshift evolution
- TestResiduals (3) - Model fitting
- TestCumulativeGamma (3) - Field accumulation

### scripts/tests/ (12)

```bash
pytest scripts/tests/test_ssz_kernel.py -s -v        # 4 tests
pytest scripts/tests/test_ssz_invariants.py -s -v    # 6 tests
pytest scripts/tests/test_segmenter.py -s -v         # 2 tests
pytest scripts/tests/test_cosmo_multibody.py -s -v   # 3 tests
```

### tests/cosmos/ (1)

```bash
pytest tests/cosmos/test_multi_body_sigma.py -s -v   # 1 test
```

---

## 2. Technical Tests (23 Tests - Silent)

**Run in background, only show PASSED:**

```bash
pytest tests/test_segwave_cli.py -s -v           # 16 tests
pytest tests/test_print_all_md.py -s -v          # 6 tests
pytest scripts/tests/test_cosmo_fields.py -s -v  # 1 test
# ... and others
```

---

## 3. Complete Test Suite

### run_full_suite.py

**The recommended way to run all tests:**

```bash
python run_full_suite.py
```

**Phases:**
```
[PHASE 1] Root-Level Tests (6 physics)
[PHASE 2] SegWave Tests (20 tests)
[PHASE 3] Scripts Tests (15 tests)
[PHASE 4] Cosmos Tests (1 test)
[PHASE 5] SSZ Analysis (~60s)
[PHASE 6] Example Runs (G79, Cygnus X)
[PHASE 7] Generate Summary
[PHASE 8] MD Echo
[PHASE 9] Generate Output Log
```

**Generates:**
- `reports/RUN_SUMMARY.md` - Compact overview
- `reports/summary-output.md` - Complete detailed log (100-500 KB)

**Output Example:**
```
====================================================================================================
SUMMARY REPORT
====================================================================================================

Total Physics Tests: 35
Silent Technical Tests: 23
Passed: 35/35
Failed: 0/35
Success Rate: 100.0%
Total Test Time: 125.3s

====================================================================================================
GENERATING DETAILED OUTPUT LOG
====================================================================================================

✅ Detailed output log written to: reports\summary-output.md
   File size: 245.8 KB

To view the complete log:
   type reports\summary-output.md

====================================================================================================
WORKFLOW COMPLETE
====================================================================================================

📊 Summary Files:
   • reports\RUN_SUMMARY.md
   • reports\summary-output.md

✅ ALL TESTS PASSED
```

---

## 4. Installation Scripts

### Windows (PowerShell):

```powershell
.\install.ps1
```

### Linux/macOS:

```bash
chmod +x install.sh
./install.sh
```

**Installation Steps:**
```
[1/10] Python Check
[2/10] Virtual Environment
[3/10] Activate venv
[4/10] Upgrade pip
[5/10] Dependencies
[6/10] Package Install
[7/10] Test Suite ← Runs ALL tests!
[8/10] Check Data Files ← NEW! Smart data fetching
[9/10] Verify Installation
[10/10] Complete
```

---

## 5. Test Output Format

### Physics Tests (Verbose):

```
================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
Configuration:
  Schwarzschild radius: r_s = 2GM/c²
  Test radii: [10, 50, 100] × r_s

Results:
  β = 1.000000000000 (perfect)
  γ = 1.000000000000 (perfect)

Physical Interpretation:
  • β=1 → No preferred frame (Lorentz invariance)
  • γ=1 → Standard GR curvature response
  • Both parameters match GR in weak field limit
  • Deviation from 1 would indicate modified gravity
================================================================================
PASSED
================================================================================
```

### Technical Tests (Silent):

```
tests/test_segwave_cli.py::test_help_flag PASSED
tests/test_segwave_cli.py::test_invalid_csv_path PASSED
```

---

## 6. Data & Papers

### Data Files

**Included in Release (~52 MB):**
```
data/
├── real_data_full.csv          # Main dataset
└── gaia/
    ├── gaia_sample_small.csv
    ├── gaia_cone_g79.csv
    └── gaia_cone_cygx.csv
```

**Auto-Fetched (2 GB):**
```
data/planck/
└── COM_PowerSpect_CMB-TT-full_R3.01.txt  # Planck 2018
```

**Fetch Script:**
```bash
python scripts/fetch_planck.py
```

### Papers

**Both formats included:**
```
papers/
├── *.md   # Markdown (GitHub viewing, editing)
└── *.pdf  # PDF (offline reading, printing)
```

---

## 7. Critical Information

### ALWAYS Use `-s` Flag!

```bash
# ✅ CORRECT:
pytest tests/ -s -v --tb=short

# ❌ WRONG (causes crash):
pytest tests/ -v --tb=short --disable-warnings
```

**Reason:** `--disable-warnings` causes:
```
ValueError: I/O operation on closed file
```

**This is a known pytest bug!**

---

## 8. Recent Updates (2025-10-18)

### Major Changes:

1. **All Physics Tests Verbose**
   - 35 tests with detailed output
   - Physical interpretations for all

2. **Technical Tests Silent**
   - 23 tests run in background
   - Only show PASSED

3. **Pytest Fix**
   - Changed from `--disable-warnings` to `-s`
   - No more I/O crashes

4. **Logging System**
   - Captures all output
   - Generates summary-output.md
   - Complete test log (100-500 KB)

5. **Smart Data Fetching**
   - Checks existing files
   - Fetches only missing data
   - Never overwrites

6. **Bug Fixes**
   - test_segmenter.py import error fixed
   - Summary "Failed: 3" bug fixed
   - Cache issues documented

7. **Documentation**
   - tests/README_TESTS.md
   - scripts/tests/README_SCRIPTS_TESTS.md
   - LOGGING_SYSTEM_README.md
   - INSTALL_README.md
   - DATA_FETCHING_README.md

---

## 9. Troubleshooting

### Problem: Pytest crashes

```
ValueError: I/O operation on closed file
```

**Solution:** Use `-s` flag instead of `--disable-warnings`

---

### Problem: Tests show only "PASSED"

**Solution:** Clear Python cache:

```bash
python -c "import pathlib, shutil; [shutil.rmtree(p, ignore_errors=True) for p in pathlib.Path('.').rglob('__pycache__')]"
```

---

### Problem: Import errors

**Solution:** Activate virtual environment:

```bash
# Windows:
.\.venv\Scripts\Activate.ps1

# Linux:
source .venv/bin/activate
```

---

### Problem: Planck data missing

**Solution:** Fetch manually:

```bash
python scripts/fetch_planck.py
```

---

## 10. Performance

**Test Times:**
- Root-Level Tests: ~1s
- SegWave Tests: ~40s
- Scripts Tests: ~20s
- Cosmos Tests: ~6s
- SSZ Analysis: ~60s
- **Total: ~2-3 minutes**

**Installation Times:**
- Without Planck: ~2 minutes
- With Planck fetch: ~20 minutes (connection dependent)
- Re-installation: ~2 minutes (skips existing data)

---

## 11. CI/CD Integration

### GitHub Actions Example:

```yaml
name: SSZ Suite Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install -e .
      
      - name: Run tests
        run: |
          pytest tests/ scripts/tests/ -s -v --tb=short
          
      - name: Run full suite
        run: python run_full_suite.py
```

---

## 12. For Developers

### Test Development Guidelines:

**Physics Tests:**
```python
def test_physical_phenomenon():
    """Test description
    
    Physical Meaning:
    Explain what this tests physically
    """
    # Setup
    config = ...
    
    # Test
    result = calculate(config)
    
    # Verbose Output
    print("\n" + "="*80)
    print("TEST TITLE")
    print("="*80)
    print(f"Configuration:")
    print(f"  param = {value}")
    print(f"\nResults:")
    print(f"  result = {result}")
    print(f"\nPhysical Interpretation:")
    print(f"  • Interpretation 1")
    print(f"  • Interpretation 2")
    print("="*80)
    
    # Assert
    assert result_is_correct
```

**Technical Tests:**
```python
def test_technical_feature():
    """Simple test, no verbose output"""
    result = function()
    assert result == expected
```

---

## 13. Complete File Listing

### Updated Files (2025-10-18):

**Test Files:**
- test_ppn_exact.py ✓
- test_vfall_duality.py ✓
- test_energy_conditions.py ✓
- test_c1_segments.py ✓
- test_c2_segments_strict.py ✓
- test_c2_curvature_proxy.py ✓
- tests/test_segwave_core.py ✓
- scripts/tests/test_ssz_kernel.py ✓
- scripts/tests/test_ssz_invariants.py ✓ (added 3 tests)
- scripts/tests/test_segmenter.py ✓ (fixed import)
- scripts/tests/test_cosmo_multibody.py ✓
- tests/cosmos/test_multi_body_sigma.py ✓

**Runner Scripts:**
- run_full_suite.py ✓ (logging system)
- install.ps1 ✓ (data fetching, pytest fix)
- install.sh ✓ (data fetching, pytest fix)

**New Scripts:**
- scripts/fetch_planck.py ✅ NEW

**Documentation:**
- tests/README_TESTS.md ✅ NEW
- scripts/tests/README_SCRIPTS_TESTS.md ✅ NEW
- TESTING_COMPLETE_GUIDE.md ✅ NEW (this file)
- LOGGING_SYSTEM_README.md ✅ NEW
- INSTALL_README.md ✅ NEW
- DATA_FETCHING_README.md ✅ NEW
- PHYSICS_TESTS_COMPLETE_LIST.md ✅ NEW
- VERIFICATION_COMPLETE.md ✅ NEW

---

## 14. Success Criteria

✅ All 35 physics tests show detailed output  
✅ All 23 technical tests run silently  
✅ No pytest crashes with `-s` flag  
✅ Summary shows only physics tests  
✅ Failed count accurate  
✅ Logging system captures all output  
✅ Data fetching is smart (no overwrites)  
✅ Install scripts work on Windows + Linux  
✅ Papers available in MD + PDF  
✅ Complete documentation  

---

## Contact

**Authors:** Carmen Wrede, Lino Casu  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4  
**Copyright:** © 2025  
**Repository:** https://github.com/CarmenWrede/SSZ-Projection-Suite

---

**Complete testing system ready for release!** ✅
