# Linux Test Failure Analysis - pyarrow Missing

**Date:** 2025-10-28  
**System:** Linux (Python 3.13.7)  
**Issue:** ImportError for pyarrow in test_ssz_invariants.py

---

## 🔴 PROBLEM

### Test Failures:
```
FAILED scripts/tests/test_ssz_invariants.py::test_segment_growth_is_monotonic
FAILED scripts/tests/test_ssz_invariants.py::test_natural_boundary_positive
FAILED scripts/tests/test_ssz_invariants.py::test_spiral_index_bounds
FAILED scripts/tests/test_ssz_invariants.py::test_segment_density_positive

Error: ImportError: Unable to find a usable engine; tried using: 'pyarrow', 'fastparquet'.
```

### Root Cause:
**System Python WITHOUT virtual environment!**

Evidence:
```
/usr/lib/python3/dist-packages/pandas/io/parquet.py
```
↑ This is SYSTEM Python, NOT a virtual environment

---

## ✅ SOLUTION

### Option 1: Install pyarrow System-Wide (Quick Fix)

```bash
# Using apt (Debian/Ubuntu)
sudo apt install python3-pyarrow

# OR using pip
pip install pyarrow>=10.0.0

# Then re-run tests
pytest scripts/tests/test_ssz_invariants.py -v
```

### Option 2: Use Virtual Environment (RECOMMENDED!)

```bash
# Navigate to repository
cd /home/error/Segmented-Spacetime-Mass-Projection-Unified-Results

# Create virtual environment
python3 -m venv .venv

# Activate it
source .venv/bin/activate

# Install ALL dependencies from requirements.txt
pip install -r requirements.txt

# Run tests (now with correct dependencies)
pytest scripts/tests/test_ssz_invariants.py -v
```

### Option 3: Use install.sh Script

```bash
# Run automated installation script
./install.sh

# It creates venv and installs everything
# Then activates environment and runs validation
```

---

## 📋 VERIFICATION

### After Fix, Run:

```bash
# Check pyarrow is installed
python -c "import pyarrow; print(f'pyarrow version: {pyarrow.__version__}')"

# Expected output:
# pyarrow version: 10.0.0 (or higher)

# Run full test suite
pytest scripts/tests/test_ssz_invariants.py -v

# Expected: 6 passed
```

---

## 🔍 WHY THIS HAPPENED

### requirements.txt IS CORRECT:

```txt
pandas>=2.0.0
pyarrow>=10.0.0  # Required for parquet file support
```

**pyarrow was added in Commit ee6160c (today!)**

### BUT: System Python doesn't auto-install from requirements.txt

**Two scenarios:**

1. **Old installation** - Installed before pyarrow was added
2. **System Python** - Never ran `pip install -r requirements.txt`

---

## 🎯 TEST FILES AFFECTED

**File:** `scripts/tests/test_ssz_invariants.py`

**Functions that need pyarrow:**
```python
def load_field(run_id: str) -> pd.DataFrame:
    field_path = Path("outputs") / "fields" / f"{run_id}.parquet"
    return pd.read_parquet(field_path)  # ← Needs pyarrow!
```

**4 Tests use this function:**
- test_segment_growth_is_monotonic
- test_natural_boundary_positive
- test_spiral_index_bounds
- test_segment_density_positive

**2 Tests DON'T need pyarrow:**
- test_phi_value_exact (uses direct calculation)
- test_time_dilation_at_infinity (uses direct calculation)

Result: **2 passed, 4 failed**

---

## 📊 IMPACT ANALYSIS

### On Windows (with venv):
- ✅ ALL tests pass
- ✅ requirements.txt installed correctly
- ✅ pyarrow>=10.0.0 present

### On Linux (system Python):
- ⚠️ 4 tests fail (pyarrow missing)
- ⚠️ System Python lacks pyarrow
- ⚠️ Need manual install OR venv

### On Colab:
- ✅ Works (we tested this today)
- ✅ pip install in notebook cell

---

## 🚀 PREVENTION

### Update Documentation:

Add to **TROUBLESHOOTING.md**:

```markdown
## ImportError: pyarrow missing

**Symptom:**
```
ImportError: Unable to find a usable engine; tried using: 'pyarrow', 'fastparquet'.
```

**Solution:**
```bash
pip install pyarrow>=10.0.0
```

**Better Solution (use virtual environment):**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```
```

---

## 📝 COMMITS RELATED

**Fix Added:** Commit ee6160c (2025-10-28)
```
MAJOR: Complete error documentation & fixes
- Added pyarrow>=10.0.0 to requirements.txt (fixes parquet ImportError)
```

**Documentation:** Commit 7ad4a06 (2025-10-28)
```
COMPLETE: Full repository audit & documentation review
- All 161 tests accounted for, 9/9 issues resolved
```

---

## ✅ FINAL STATUS

**Code:** ✅ CORRECT (pyarrow in requirements.txt)  
**Windows:** ✅ WORKS (venv + install.ps1)  
**Linux:** ⚠️ NEEDS MANUAL FIX (system Python missing pyarrow)  
**Colab:** ✅ WORKS (pip install in notebook)

**Action Required:**
- Run `pip install pyarrow>=10.0.0` on Linux system
- OR: Use `./install.sh` to create proper venv

---

## 🎯 QUICK REFERENCE

### For the User on Linux:

```bash
# Quickest fix (1 command):
pip install pyarrow

# Re-run tests:
pytest scripts/tests/test_ssz_invariants.py -v

# Expected: 6 passed
```

---

**© 2025 Carmen Wrede & Lino Casu**  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4  

**Status:** ✅ SOLUTION DOCUMENTED
