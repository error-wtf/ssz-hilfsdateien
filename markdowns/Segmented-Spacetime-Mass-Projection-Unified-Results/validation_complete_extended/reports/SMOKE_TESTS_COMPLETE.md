# Smoke Tests - Complete Implementation Status

**Date:** 2025-10-20  
**Purpose:** Verify all critical scripts have basic smoke tests  
**Status:** SYSTEMATICALLY REVIEWED & FIXED

---

## ✅ EXISTING SMOKE TESTS

### 1. ssz_covariant_smoketest_verbose_lino_casu.py ✅ FIXED

**Status:** EXISTS & FUNCTIONAL (UTF-8 fix applied)  
**Tests:** 
- PPN parameters (β=1, γ=1)
- Weak-field: Light bending, Shapiro delay, Mercury precession
- Strong-field: Photon sphere, ISCO, shadow
- Two test cases: Sun (weak) & Sgr A* (strong)

**Fix Applied:**
```python
# Added UTF-8 encoding for Windows compatibility
import sys
import os
if sys.platform.startswith('win'):
    os.environ['PYTHONIOENCODING'] = 'utf-8'
    sys.stdout.reconfigure(encoding='utf-8', errors='replace')
```

**Runtime:** ~1 second  
**Output:** Comprehensive metric validation

---

### 2. scripts/tests/data_smoke_fetch.py ✅ EXISTS

**Status:** EXISTS  
**Tests:** Data fetching capabilities  
**Purpose:** Smoke test for external data downloads

---

## 📋 SCRIPTS REQUIRING SMOKE TESTS

### Priority 1: CRITICAL PIPELINE SCRIPTS

**1. run_full_suite.py**
- **Current status:** NO smoke test
- **Need:** Quick validation before full run
- **Test:** Import, basic config, 1 quick test

**2. run_all_ssz_terminal.py**
- **Current status:** NO smoke test
- **Need:** Pipeline components functional
- **Test:** Core modules importable

**3. segspace_all_in_one_extended.py**
- **Current status:** NO smoke test  
- **Need:** All workflows accessible
- **Test:** Decimal precision, φ value, basic calc

**4. generate_key_plots.py**
- **Current status:** NO smoke test
- **Need:** Matplotlib functional, data accessible
- **Test:** Can create figure, save PNG

### Priority 2: CORE MODULES

**5. core/compare.py**
- **Test:** Basic comparison functions

**6. core/predict.py**
- **Test:** Prediction calculations

**7. core/inference.py**
- **Test:** Statistical functions

**8. core/stats.py**
- **Test:** Extended metrics

### Priority 3: ANALYSIS SCRIPTS

**9. bound_energy.py**
- **Test:** Alpha calculation

**10. phi_test.py / phi_bic_test.py**
- **Test:** φ-geometry calculations

---

## 🛠️ SMOKE TEST TEMPLATE

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
\"\"\"
Smoke Test for [SCRIPT_NAME]
Quick validation that script can run basic operations.
\"\"\"
import sys
import os

# UTF-8 for Windows
if sys.platform.startswith('win'):
    os.environ['PYTHONIOENCODING'] = 'utf-8'
    try:
        sys.stdout.reconfigure(encoding='utf-8', errors='replace')
    except:
        pass

def smoke_test():
    \"\"\"Run basic smoke test\"\"\"
    print("="*80)
    print(f"SMOKE TEST: [SCRIPT_NAME]")
    print("="*80)
    
    # Test 1: Imports
    try:
        # Import key modules
        print("✓ Imports successful")
    except Exception as e:
        print(f"✗ Import failed: {e}")
        return False
    
    # Test 2: Basic functionality
    try:
        # Test core function
        print("✓ Basic functionality works")
    except Exception as e:
        print(f"✗ Functionality failed: {e}")
        return False
    
    # Test 3: Output
    try:
        # Test can produce output
        print("✓ Output generation works")
    except Exception as e:
        print(f"✗ Output failed: {e}")
        return False
    
    print("="*80)
    print("✅ SMOKE TEST PASSED")
    print("="*80)
    return True

if __name__ == "__main__":
    success = smoke_test()
    sys.exit(0 if success else 1)
```

---

## 🎯 SMOKE TEST PRINCIPLES

### What Smoke Tests Should Do:
- ✅ Verify basic imports work
- ✅ Check core functionality accessible
- ✅ Validate minimal calculations
- ✅ Confirm output generation
- ✅ Run in <5 seconds
- ✅ Exit with clear status

### What Smoke Tests Should NOT Do:
- ❌ Full validation (that's for test suites)
- ❌ Check all edge cases
- ❌ Run expensive calculations
- ❌ Require external data (unless testing fetch)
- ❌ Take >10 seconds

---

## 📊 IMPLEMENTATION STATUS

| Script | Priority | Smoke Test | Status |
|--------|----------|------------|--------|
| **ssz_covariant_smoketest** | Critical | ✅ EXISTS | **FIXED** |
| **data_smoke_fetch.py** | Critical | ✅ EXISTS | OK |
| run_full_suite.py | P1 | ⭐ NEEDED | TODO |
| run_all_ssz_terminal.py | P1 | ⭐ NEEDED | TODO |
| segspace_all_in_one_extended.py | P1 | ⭐ NEEDED | TODO |
| generate_key_plots.py | P1 | ⭐ NEEDED | TODO |
| core/compare.py | P2 | ⭐ NEEDED | TODO |
| core/predict.py | P2 | ⭐ NEEDED | TODO |
| core/inference.py | P2 | ⭐ NEEDED | TODO |
| core/stats.py | P2 | ⭐ NEEDED | TODO |
| bound_energy.py | P3 | ⭐ NEEDED | TODO |
| phi_test.py | P3 | ⭐ NEEDED | TODO |

---

## 🚀 EXECUTION PLAN

### Phase 1: Fix Existing (DONE ✅)
- [x] Fix UTF-8 in ssz_covariant_smoketest
- [x] Verify data_smoke_fetch works
- [x] Document existing tests

### Phase 2: Implement Critical (NEXT)
- [ ] Create smoke_test_pipeline.py for pipeline scripts
- [ ] Create smoke_test_core_modules.py for core modules
- [ ] Add --smoke flag to main scripts
- [ ] Integrate into CI/CD

### Phase 3: Complete Coverage
- [ ] Implement P3 smoke tests
- [ ] Add to install scripts
- [ ] Document usage

---

## 💻 USAGE

### Run Smoke Test:
```bash
# Existing covariant smoketest
python ssz_covariant_smoketest_verbose_lino_casu.py

# Future: Run all smoke tests
python -m pytest smoke_tests/ -v

# Future: Quick pipeline check
python run_full_suite.py --smoke
```

### In CI/CD:
```yaml
# Quick smoke test before full suite
- name: Smoke Tests
  run: |
    python ssz_covariant_smoketest_verbose_lino_casu.py
    python -m pytest smoke_tests/ -v --tb=short
```

---

## 📝 RECOMMENDATIONS

### For Developers:
1. Run smoke test before committing
2. Add smoke test for new critical scripts
3. Keep smoke tests fast (<5s each)

### For CI/CD:
1. Run smoke tests first (fail fast)
2. Only run full suite if smoke passes
3. Cache smoke test results

### For Users:
1. Run smoke test after install
2. Verify environment setup
3. Quick health check

---

## ✅ CURRENT STATUS SUMMARY

**Smoke Tests:**
- Existing: 2
- Working: 2 (after UTF-8 fix)
- Needed: 10+ (priority-based)

**Next Steps:**
1. Implement P1 smoke tests (4 scripts)
2. Add --smoke flags to pipelines
3. Integrate into CI/CD

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
