# SSZ Suite - Output Logs Documentation

**Date:** 2025-10-18  
**Version:** 1.0

---

## Overview

When running `python run_full_suite.py`, the test suite generates **three output files** in the `reports/` directory:

```
reports/
├── RUN_SUMMARY.md        # Compact test results summary
├── summary-output.md     # Quick pass/fail overview with statistics
└── full-output.md        # COMPLETE log with ALL test output
```

---

## File Descriptions

### 1. **RUN_SUMMARY.md** (Small, ~5-10 KB)

**Purpose:** Quick reference summary for test results

**Contents:**
- Test suite overview (number of tests, pass/fail count)
- Success rate percentage
- Execution times
- List of all test phases with status

**When to use:**
- Quick check if all tests passed
- CI/CD status reports
- Git commit messages

**Example:**
```markdown
# SSZ Suite Run Summary - Physics Tests

**Date:** 2025-10-18 17:00:16

## Overview
- **Physics Test Suites:** 16
- **Passed:** 16
- **Failed:** 0
- **Success Rate:** 100.0%
```

---

### 2. **summary-output.md** (Medium, ~10-50 KB)

**Purpose:** Compact summary with test details

**Contents:**
- All test phases listed
- Pass/fail status with icons (✅/❌)
- Execution time for each test
- Summary statistics

**When to use:**
- Detailed test review
- Identifying which specific test failed
- Performance analysis

**Example:**
```markdown
## Test Details

- ✅ **PPN Exact Tests** (0.1s)
- ✅ **Dual Velocity Tests** (0.2s)
- ❌ **Energy Conditions Tests** (0.1s)
```

---

### 3. **full-output.md** (Large, ~500 KB - 5 MB)

**Purpose:** COMPLETE detailed log with ALL test output

**Contents:**
- All test phases with full output
- Complete stdout/stderr from every test
- Detailed error messages and stack traces
- Physical interpretations from physics tests
- Mathematical formulas and results
- Validation checks
- Performance metrics

**When to use:**
- Debugging test failures
- Understanding why a test failed
- Scientific verification of results
- Reviewing physical interpretations
- Tracking down subtle bugs

**Example:**
```markdown
================================================================================
TEST: PPN Parameter Validation - β and γ
================================================================================
Configuration:
  Schwarzschild radius: 2.95 km
  Test radius: 100.00 km
  
Results:
  β_measured = 1.000000000
  γ_measured = 1.000000000
  
Physical Interpretation:
  • PPN parameters match General Relativity (GR) (GR) (β=γ=1)
  • Weak-field limit correctly reproduces Einstein gravity
  • No scalar field contributions detected
================================================================================
```

---

## Git Repository Strategy

### Files INCLUDED in Repository:

✅ **RUN_SUMMARY.md** - Always committed (small, essential)  
✅ **summary-output.md** - Always committed (medium, useful for review)  
✅ **full-output.md** - Always committed (large, but valuable for verification)

### Why Include full-output.md?

1. **Scientific Reproducibility:** Full logs prove test validity
2. **Debugging History:** Track when/why tests started failing
3. **Documentation:** Serves as comprehensive test documentation
4. **Transparency:** Shows exactly what the code does

### File Sizes:

- RUN_SUMMARY.md: ~5-10 KB
- summary-output.md: ~20-50 KB
- full-output.md: ~500 KB - 2 MB (compressed well in Git)

Total: ~2-3 MB uncompressed, ~200-400 KB compressed in Git

---

## Usage Examples

### Quick Status Check:
```bash
cat reports/RUN_SUMMARY.md
```

### Find Failed Test:
```bash
grep "❌" reports/summary-output.md
```

### Debug Specific Test:
```bash
# View full output
cat reports/full-output.md | less

# Search for specific test
grep -A 50 "PPN Exact Tests" reports/full-output.md
```

### Compare Test Runs:
```bash
# Compare pass/fail status
diff reports/summary-output.md /path/to/previous/summary-output.md

# Compare full logs
diff reports/full-output.md /path/to/previous/full-output.md
```

---

## Continuous Integration (CI)

### Recommended Workflow:

1. **On every push:** Generate all three files
2. **Store as artifacts:** Archive full-output.md
3. **Display:** Show RUN_SUMMARY.md in CI dashboard
4. **Alert:** Notify if summary-output.md shows failures

### GitHub Actions Example:
```yaml
- name: Run SSZ Test Suite
  run: python run_full_suite.py

- name: Upload Test Results
  uses: actions/upload-artifact@v3
  with:
    name: test-reports
    path: reports/

- name: Check Test Status
  run: |
    if grep -q "Failed: 0" reports/RUN_SUMMARY.md; then
      echo "✅ All tests passed"
    else
      echo "❌ Tests failed"
      exit 1
    fi
```

---

## Logging System Details

### How It Works:

The test runner uses a **Tee Output** system that captures ALL output:

```python
# Create buffer to capture output
output_log = io.StringIO()

# Tee stdout to both console AND buffer
class TeeOutput:
    def __init__(self, *outputs):
        self.outputs = outputs
    def write(self, text):
        for output in self.outputs:
            output.write(text)

sys.stdout = TeeOutput(sys.__stdout__, output_log)
```

### What Gets Captured:

✅ Python script output (print statements)  
✅ Pytest output (test results, assertions)  
✅ Subprocess output (external commands)  
✅ Error messages (stderr)  
✅ Stack traces  
✅ Performance metrics  

❌ Interactive prompts (if any - they're skipped)  
❌ Binary data (not applicable)  

---

## Best Practices

### For Developers:

1. **Always run full suite before commit:**
   ```bash
   python run_full_suite.py
   git add reports/
   git commit -m "Update: Test results"
   ```

2. **Review full-output.md when tests fail:**
   - Check physical interpretations
   - Verify mathematical results
   - Look for warnings/errors

3. **Keep logs in repository:**
   - Provides test history
   - Helps track regressions
   - Documents expected behavior

### For Users:

1. **Quick validation:**
   ```bash
   cat reports/RUN_SUMMARY.md
   ```

2. **Detailed review:**
   ```bash
   less reports/full-output.md
   ```

3. **Compare with official logs:**
   - Download from repository
   - Compare your results
   - Report discrepancies

---

## Troubleshooting

### Problem: full-output.md is too large (>10 MB)

**Solution:** Some tests may be producing excessive output
```bash
# Find which tests produce most output
grep -o "\[RUNNING\].*" reports/full-output.md | uniq -c | sort -rn
```

### Problem: Missing output in full-output.md

**Solution:** Check if stdout is being redirected elsewhere
```bash
# Verify TeeOutput is working
python run_full_suite.py 2>&1 | tee manual_log.txt
```

### Problem: Git complains about large files

**Solution:** All three files should be tracked normally (not LFS)
```bash
# If needed, add to LFS (optional)
git lfs track "reports/full-output.md"
```

---

## Performance Impact

### Test Execution:

- **Without logging:** ~120s
- **With full logging:** ~126s (+5%)

The logging overhead is minimal (~5-6 seconds for complete suite).

### Disk Usage:

- **Per test run:** ~2-3 MB (all three files)
- **After 100 runs:** ~200-300 MB
- **Compressed in Git:** ~20-30 MB per 100 runs

---

## Future Enhancements

### Planned Features:

1. **HTML Report Generation:**
   - Convert full-output.md to interactive HTML
   - Collapsible test sections
   - Search functionality

2. **JSON Output:**
   - Machine-readable test results
   - For automated processing

3. **Differential Logging:**
   - Only log differences from previous run
   - Reduce file sizes

4. **Performance Profiling:**
   - Add timing breakdown
   - Identify slow tests

---

## Copyright

**© 2025 Carmen Wrede und Lino Casu**  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## Contact

For questions about the logging system:
- Check `run_full_suite.py` source code
- Review test documentation
- See LOGGING_SYSTEM_README.md (if exists)
