# Comprehensive Script Testing Plan
**Date:** 2025-10-28  
**Purpose:** Test every critical script individually before release  
**Status:** 🔄 IN PROGRESS

---

## 📋 TEST CATEGORIES

### Category 1: Installation & Setup Scripts (CRITICAL)
- [ ] `install.ps1` - Windows installation
- [ ] `install.sh` - Linux/macOS installation
- [ ] `smoke_test_all.py` - Quick health check

### Category 2: Main Validation Scripts (CRITICAL)
- [ ] `run_all_validations.py` - Master validation runner
- [ ] `run_ssz_validation.py` - SSZ vs GR validation
- [ ] `run_ssz_theory_validation.py` - Theory validation
- [ ] `run_ssz_unified_validation.py` - Unified ToE validation
- [ ] `run_complete_test_suite.py` - Complete test suite
- [ ] `run_full_suite.py` - Original test suite

### Category 3: Core Test Files (CRITICAL)
- [ ] `tests/test_segwave_core.py` - SegWave core tests
- [ ] `tests/cosmos/test_multi_body_sigma.py` - Cosmos tests
- [ ] `scripts/tests/test_ssz_kernel.py` - SSZ kernel tests
- [ ] `scripts/tests/test_ssz_invariants.py` - SSZ invariants tests

### Category 4: Analysis Scripts (HIGH PRIORITY)
- [ ] `perfect_paired_test.py` - ESO validation
- [ ] `generate_key_plots.py` - Plot generation
- [ ] `blackhole_animation.py` - Black hole visualization

### Category 5: Utility Scripts (MEDIUM PRIORITY)
- [ ] `scripts/fetch_planck.py` - Planck data fetcher
- [ ] `tools/print_all_md.py` - Markdown printer

---

## 🧪 TEST PROTOCOL FOR EACH SCRIPT

### Phase 1: Syntax & Import Check
```bash
python -m py_compile <script.py>
python -c "import <module>; print('OK')"
```

### Phase 2: Dry Run (if applicable)
```bash
python <script.py> --help  # Check if help works
python <script.py> --dry-run  # If supported
```

### Phase 3: Full Execution
```bash
python <script.py>  # Run with default parameters
```

### Phase 4: Output Validation
- Check if expected outputs are generated
- Verify file sizes are reasonable
- Check for error messages in output

### Phase 5: Error Handling
- Test with invalid inputs (if applicable)
- Check error messages are clear
- Verify script exits gracefully

---

## 📊 TEST RESULTS TEMPLATE

```markdown
### Script: <name>
- **Syntax Check:** ✅/❌
- **Import Check:** ✅/❌
- **Dry Run:** ✅/❌/N/A
- **Full Execution:** ✅/❌
- **Output Validation:** ✅/❌
- **Error Handling:** ✅/❌
- **Issues Found:** <list or "None">
- **Fixes Applied:** <list or "None">
- **Status:** ✅ PASS / ⚠️ NEEDS FIX / ❌ FAIL
```

---

## 🎯 TESTING SEQUENCE

### Round 1: Critical Path (MUST PASS)
1. smoke_test_all.py
2. install.ps1 / install.sh
3. run_all_validations.py

### Round 2: Validation Scripts (MUST PASS)
4. run_ssz_validation.py
5. run_ssz_theory_validation.py
6. run_ssz_unified_validation.py
7. run_full_suite.py

### Round 3: Core Tests (MUST PASS)
8. tests/test_segwave_core.py
9. tests/cosmos/test_multi_body_sigma.py
10. scripts/tests/test_ssz_kernel.py

### Round 4: Analysis Scripts (SHOULD PASS)
11. perfect_paired_test.py
12. generate_key_plots.py

### Round 5: Utilities (NICE TO PASS)
13. scripts/fetch_planck.py
14. blackhole_animation.py

---

## 🔧 FIX PROTOCOL

If a script fails:
1. Document the exact error
2. Identify root cause
3. Apply minimal fix
4. Re-test
5. Commit fix with clear message
6. Update this document

---

## 📝 NOTES

- Each test will be run in isolation
- Environment: Fresh Python 3.10+ with requirements.txt
- Working directory: Repository root
- Timeout: 5 minutes per script (except full validations)

---

**Started:** 2025-10-28 17:40 UTC+01:00  
**Expected Duration:** ~2 hours  
**Tester:** Cascade AI Assistant
