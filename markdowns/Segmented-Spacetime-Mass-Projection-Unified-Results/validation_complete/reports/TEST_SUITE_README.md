# Complete SSZ Test Suite

Comprehensive test runner for the entire SSZ repository.

© 2025 Carmen Wrede, Lino Casu

---

## Overview

This test suite automatically discovers and runs **ALL** tests, validations, and analysis scripts in the repository, then generates detailed summary reports.

---

## Quick Start

```bash
python run_complete_test_suite.py
```

**Duration:** ~5-10 minutes (depends on number of tests)

---

## What It Does

### 1. Test Discovery

Automatically finds all test files in:
- ✅ **Root level** - Direct Python tests
- ✅ **Scripts/** - Test scripts and utilities
- ✅ **Experiments/** - Experimental analyses
- ✅ **Validation/** - SSZ vs GR validation
- ✅ **Animations/** - Animation generators

### 2. Execution

Runs each test/script:
- ⏱️ With timeout protection (300s default)
- 📝 Captures stdout/stderr
- 🔍 Extracts scientific interpretations
- ✅ Records pass/fail status

### 3. Reports Generation

Creates 3 comprehensive reports:

**A) `complete_test_results.json`**
- Machine-readable results
- Detailed per-test data
- Execution times
- Error messages

**B) `COMPLETE_TEST_SUMMARY.md`**
- Human-readable summary
- Statistics by category
- Failed tests with errors
- Next steps recommendations

**C) `TEST_INTERPRETATIONS.md`**
- Extracted scientific interpretations
- Physical meanings
- Key findings from tests

---

## Output Example

```
================================================================================
COMPLETE SSZ TEST SUITE
================================================================================
Started: 2025-10-28 06:15:00

[1/5] Discovering all test files...
  Found 25 test/analysis files:
    - root_level: 8 files
    - scripts: 6 files
    - experiments: 3 files
    - validation: 5 files
    - animations: 3 files

[2/5] Running all tests...

--- ROOT LEVEL ---
  [root_level] Running: ssz_complete_tests.py
    ✅ PASSED (2.3s)
  ...

[3/5] Generating summary statistics...
  Total: 25
  Passed: 24
  Failed: 1
  Success Rate: 96.0%

[4/5] Saving detailed results...
  ✓ Saved: complete_test_results.json

[5/5] Generating Markdown reports...
  ✓ Saved: COMPLETE_TEST_SUMMARY.md
  ✓ Saved: TEST_INTERPRETATIONS.md (12 interpretations)

================================================================================
TEST SUITE COMPLETE
================================================================================
Status: ⚠️ SOME ISSUES
Total: 25 | Passed: 24 | Failed: 1
Success Rate: 96.0%
```

---

## Use Cases

### Daily Development
```bash
# Run full suite before committing
python run_complete_test_suite.py

# Check results
cat outputs/COMPLETE_TEST_SUMMARY.md
```

### Before Release
```bash
# Comprehensive validation
python run_complete_test_suite.py

# Ensure 100% success
# Fix any failures
# Re-run until clean
```

### Scientific Review
```bash
# Run suite
python run_complete_test_suite.py

# Review interpretations
cat outputs/TEST_INTERPRETATIONS.md
```

---

## Comparison with Other Runners

| Runner | Purpose | Scope | Duration |
|--------|---------|-------|----------|
| **`run_complete_test_suite.py`** | **Complete validation** | **All tests** | **~5-10 min** |
| `run_ssz_validation.py` | SSZ vs GR validation | Specific analysis | ~2 min |
| `ssz_complete_tests.py` | Black hole tests | Stability only | ~10 sec |

---

## Configuration

### Timeout Adjustment

Edit `run_complete_test_suite.py`:

```python
def run_script(script_path, category, timeout=300):  # Default: 300s
    ...
```

Change `timeout=300` to your desired value.

### Category Filtering

To skip certain categories, comment out in discovery section:

```python
# Skip animations
# if anim_dir.exists():
#     for f in anim_dir.glob('*.py'):
#         test_files['animations'].append(f)
```

---

## Output Files

All generated in `outputs/`:

| File | Size | Content |
|------|------|---------|
| `complete_test_results.json` | ~50 KB | Structured data |
| `COMPLETE_TEST_SUMMARY.md` | ~20 KB | Human summary |
| `TEST_INTERPRETATIONS.md` | ~10 KB | Scientific findings |

---

## Interpreting Results

### Success Rate Meanings

| Rate | Meaning | Action |
|------|---------|--------|
| **100%** | ✅ Perfect | Ready for release |
| **95-99%** | ✅ Excellent | Minor fixes needed |
| **90-94%** | ⚠️ Good | Review failures |
| **<90%** | ❌ Issues | Significant work needed |

### Common Failure Types

**FAILED:**
- Script exited with non-zero code
- Logic error in test
- Missing dependencies

**TIMEOUT:**
- Script exceeded time limit
- Infinite loop
- Very large computation

**ERROR:**
- Python exception
- File not found
- Import error

---

## Troubleshooting

### "No tests found"
- Check repository structure
- Ensure test files exist
- Verify naming conventions (`*test*.py`, `ssz_*.py`)

### "All tests timeout"
- Increase timeout value
- Check system resources
- Run individual tests manually

### "Import errors"
- Install dependencies: `pip install -r requirements.txt`
- Check Python version (3.10+)
- Verify virtual environment activated

---

## Integration with CI/CD

### GitHub Actions

```yaml
name: SSZ Test Suite

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.10'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run test suite
        run: python run_complete_test_suite.py
      - name: Upload results
        uses: actions/upload-artifact@v2
        with:
          name: test-results
          path: outputs/
```

---

## Advanced Usage

### Custom Test Selection

Create a custom runner:

```python
from run_complete_test_suite import run_script

# Run specific tests
tests = [
    'ssz_stability_three_figures.py',
    'run_ssz_validation.py'
]

for test in tests:
    result = run_script(Path(test), 'custom')
    print(result)
```

### Parallel Execution

For faster runs (advanced):

```python
from concurrent.futures import ThreadPoolExecutor

with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(run_script, f, cat) 
               for cat, files in test_files.items() 
               for f in files]
```

---

## Maintenance

### Adding New Tests

1. Create test file anywhere in repo
2. Name with `test` prefix or `ssz_` prefix
3. Ensure it exits with code 0 on success
4. Run suite - automatically discovered

### Excluding Tests

Add to `.gitignore` or move to different directory.

---

## Best Practices

1. ✅ **Run before every commit**
2. ✅ **Fix failures immediately**
3. ✅ **Keep timeout reasonable** (300s default)
4. ✅ **Review interpretations** for scientific accuracy
5. ✅ **Document new tests** in their docstrings

---

## License

ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## Contact

**Authors:** Carmen Wrede & Lino Casu  
**Repository:** https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results

---

**🚀 COMPREHENSIVE VALIDATION — ONE COMMAND — COMPLETE CONFIDENCE 🚀**
