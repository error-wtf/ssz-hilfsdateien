# Last Working Test Files Backup

This directory contains **KNOWN-GOOD BACKUPS** of test files that repeatedly get corrupted.

## Why This Exists

The following test files get corrupted repeatedly during test runs:
- `test_segwave_core.py` - IndentationError, SyntaxError
- `test_multi_body_sigma.py` - SyntaxError: unterminated string

**Root Cause Analysis:**
1. pytest assertion rewriting modifies files during import
2. Windows encoding issues (cp1252 vs UTF-8) with Unicode characters
3. Cache corruption when tests are interrupted
4. Possible IDE/editor sync conflicts

## How It Works

`run_full_suite.py` automatically:
1. **RESTORES** these files from backup BEFORE running tests
2. **CLEARS** all pytest and Python caches
3. Then runs the test suite

## Manual Restore

If tests fail with IndentationError or SyntaxError:

```powershell
# Windows
Copy-Item tests\lastworking\test_segwave_core.py tests\test_segwave_core.py
Copy-Item tests\cosmos\lastworking\test_multi_body_sigma.py tests\cosmos\test_multi_body_sigma.py
```

```bash
# Linux/Mac
cp tests/lastworking/test_segwave_core.py tests/test_segwave_core.py
cp tests/cosmos/lastworking/test_multi_body_sigma.py tests/cosmos/test_multi_body_sigma.py
```

## Updating Backups

If you modify the test files and they work correctly:

```powershell
# Windows - Update backups
Copy-Item tests\test_segwave_core.py tests\lastworking\test_segwave_core.py
Copy-Item tests\cosmos\test_multi_body_sigma.py tests\cosmos\lastworking\test_multi_body_sigma.py
```

## Files in This Directory

- `test_segwave_core.py` - Backup of tests/test_segwave_core.py
- `README.md` - This file

## Files in tests/cosmos/lastworking/

- `test_multi_body_sigma.py` - Backup of tests/cosmos/test_multi_body_sigma.py

---

© 2025 Carmen Wrede & Lino Casu
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
