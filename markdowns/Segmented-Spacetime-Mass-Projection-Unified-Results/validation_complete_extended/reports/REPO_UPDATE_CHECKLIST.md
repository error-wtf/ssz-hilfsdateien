# SSZ Suite - Repository Update Checklist

**Date:** 2025-10-18  
**Version:** v1.1 (Test System Overhaul)

---

## Pre-Update Checklist

### 1. Clean Working Directory

```bash
# Check git status
git status

# Should show only intended changes
# No uncommitted changes from tests/builds
```

### 2. Verify .gitignore

```bash
# Check what would be committed:
git add -A --dry-run

# Verify no large files:
git ls-files | xargs ls -lh | sort -k5 -h -r | head -20
```

**Expected:** No files >50 MB (except data/real_data_full.csv)

### 3. Clean Build Artifacts

```bash
# Remove Python cache:
find . -type d -name "__pycache__" -exec rm -rf {} +
find . -type f -name "*.pyc" -delete
find . -type f -name "*.pyo" -delete

# Remove build directories:
rm -rf build/
rm -rf dist/
rm -rf *.egg-info/
rm -rf .pytest_cache/

# Remove virtual environments:
rm -rf .venv/
rm -rf venv/
```

### 4. Remove Large Data Files

```bash
# Check Planck data (should be ignored):
ls -lh data/planck/*.txt 2>/dev/null || echo "Planck data not present (good!)"

# Check large GAIA files:
ls -lh data/gaia/*_full.csv 2>/dev/null || echo "Large GAIA files not present (good!)"
```

### 5. Remove Generated Reports

```bash
# Remove large output logs:
rm -f reports/summary-output.md

# Keep RUN_SUMMARY.md (small)
```

---

## What to Include in Repo

### ✅ INCLUDE (Commit these):

**Source Code:**
```
✓ All .py files
✓ test_*.py files
✓ tests/**/*.py
✓ scripts/**/*.py
```

**Configuration:**
```
✓ requirements.txt
✓ setup.py / pyproject.toml
✓ install.ps1
✓ install.sh
✓ run_full_suite.py
✓ .gitignore
```

**Documentation:**
```
✓ README.md
✓ LICENSE
✓ All *_README.md files
✓ TESTING_COMPLETE_GUIDE.md
✓ LINUX_TEST_PLAN.md
✓ tests/README_TESTS.md
✓ scripts/tests/README_SCRIPTS_TESTS.md
```

**Papers (Both Formats):**
```
✓ papers/**/*.md
✓ papers/**/*.pdf
```

**Small Data Files (~52 MB total):**
```
✓ data/real_data_full.csv (~50 MB)
✓ data/gaia/gaia_sample_small.csv (~1 MB)
✓ data/gaia/gaia_cone_g79.csv (~500 KB)
✓ data/gaia/gaia_cone_cygx.csv (~500 KB)
```

**Scripts:**
```
✓ scripts/fetch_planck.py
✓ scripts/fetch_gaia_full.py
✓ COPY_TO_TEST_SUITES.ps1
```

---

### ❌ EXCLUDE (Do NOT commit):

**Large Data Files:**
```
✗ data/planck/*.txt (2 GB - will be auto-fetched)
✗ data/gaia/gaia_full_sample.csv (500 MB - optional)
✗ Any files >50 MB
```

**Build Artifacts:**
```
✗ __pycache__/
✗ *.pyc, *.pyo
✗ build/
✗ dist/
✗ *.egg-info/
✗ .pytest_cache/
```

**Virtual Environments:**
```
✗ .venv/
✗ venv/
✗ ENV/
```

**IDE Files:**
```
✗ .vscode/
✗ .idea/
✗ *.swp
```

**Generated Reports:**
```
✗ reports/summary-output.md (100-500 KB - regenerated)
✓ reports/RUN_SUMMARY.md (small - can be included)
```

**Temporary Files:**
```
✗ *.tmp
✗ *.log
✗ *.bak
```

**Test Copies:**
```
✗ *-TEST-SUITE-Linux/
✗ *-TEST-SUITE-Windows/
```

---

## Git Commands for Update

### Step 1: Check Status

```bash
git status
```

**Expected:** Clean working directory or only intended changes

### Step 2: Add New Files

```bash
# Add all new/modified files (respecting .gitignore):
git add .

# Or selectively:
git add tests/README_TESTS.md
git add scripts/tests/README_SCRIPTS_TESTS.md
git add TESTING_COMPLETE_GUIDE.md
git add .gitignore
git add scripts/fetch_planck.py
# ... etc
```

### Step 3: Verify What Will Be Committed

```bash
# Show what will be committed:
git diff --cached --stat

# Show file sizes:
git diff --cached --name-only | xargs ls -lh
```

**Verify:** No files >50 MB (except data/real_data_full.csv)

### Step 4: Commit Changes

```bash
git commit -m "Complete Test System Overhaul (v1.1)

Major Updates:
- All 35 physics tests now verbose with physical interpretations
- 23 technical tests run in silent mode
- Fixed pytest crash bug (use -s instead of --disable-warnings)
- Added logging system with complete output capture
- Smart data fetching (no overwrites, auto-fetch Planck)
- Fixed test_segmenter.py import bug
- Fixed summary 'Failed: 3' bug
- Papers now available in MD + PDF
- Complete documentation suite (9 README files)
- Linux/Windows installation scripts updated

New Features:
- reports/summary-output.md - Complete test log
- scripts/fetch_planck.py - Planck data downloader
- TESTING_COMPLETE_GUIDE.md - Master test guide
- tests/README_TESTS.md - Tests documentation
- scripts/tests/README_SCRIPTS_TESTS.md - Scripts tests docs
- LINUX_TEST_PLAN.md - Linux testing procedure
- DATA_FETCHING_README.md - Data management guide

Bug Fixes:
- Pytest I/O crash (--disable-warnings → -s)
- test_segmenter.py import error
- Summary false failure count
- Cache issues documented

Performance:
- Test suite: ~2-3 minutes
- Installation: ~2-20 minutes (with/without Planck)

Copyright © 2025 Carmen Wrede, Lino Casu
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4"
```

### Step 5: Create Tag (Optional)

```bash
# Tag this version:
git tag -a v1.1 -m "Test System Overhaul Release

- 35 verbose physics tests
- 23 silent technical tests
- Logging system
- Smart data fetching
- Complete documentation"

# Push tag:
git push origin v1.1
```

### Step 6: Push to Remote

```bash
# Push to main branch:
git push origin main

# Or if using different branch:
git push origin feature/test-system-overhaul
```

---

## Post-Update Verification

### 1. Clone Fresh Copy

```bash
# Test in new location:
cd /tmp
git clone https://github.com/YourUsername/SSZ-Suite.git SSZ-test
cd SSZ-test
```

### 2. Verify Files Present

```bash
# Check key files:
ls -la install.sh
ls -la tests/README_TESTS.md
ls -la scripts/fetch_planck.py
ls -la data/real_data_full.csv
```

### 3. Verify Files Absent

```bash
# These should NOT be present:
ls data/planck/*.txt 2>/dev/null && echo "ERROR: Planck in repo!" || echo "OK: Planck not in repo"
ls -la .venv/ 2>/dev/null && echo "ERROR: venv in repo!" || echo "OK: venv not in repo"
```

### 4. Test Installation

```bash
# Linux:
chmod +x install.sh
./install.sh

# Should fetch Planck data automatically
```

### 5. Verify Repository Size

```bash
# Check repo size:
du -sh .git

# Should be reasonable (<100 MB)
```

---

## GitHub/GitLab Specific

### Create Release

**On GitHub:**
1. Go to "Releases" → "Create new release"
2. Tag: `v1.1`
3. Title: `SSZ Suite v1.1 - Test System Overhaul`
4. Description:

```markdown
# SSZ Suite v1.1 - Test System Overhaul

## Major Updates

### Test System
- ✅ 35 physics tests with detailed physical interpretations
- ✅ 23 technical tests in silent mode
- ✅ Complete logging system (captures all output)
- ✅ Smart data fetching (auto-fetch Planck 2GB)

### Bug Fixes
- Fixed pytest I/O crash (use `-s` instead of `--disable-warnings`)
- Fixed test_segmenter.py import error
- Fixed false "Failed: 3" in summary

### New Features
- Complete test output logs (reports/summary-output.md)
- Planck data auto-downloader (scripts/fetch_planck.py)
- 9 comprehensive README files
- Papers in both MD and PDF formats

### Documentation
- TESTING_COMPLETE_GUIDE.md - Master testing guide
- tests/README_TESTS.md - Tests directory docs
- scripts/tests/README_SCRIPTS_TESTS.md - Scripts tests docs
- LINUX_TEST_PLAN.md - Linux testing procedure
- And 5 more...

## Installation

### Windows
```powershell
.\install.ps1
```

### Linux/macOS
```bash
chmod +x install.sh
./install.sh
```

## Quick Start

```bash
# Run all tests:
python run_full_suite.py

# Single test:
python test_ppn_exact.py

# Pytest:
pytest tests/test_segwave_core.py -s -v
```

## Data Files

**Included in release (~52 MB):**
- data/real_data_full.csv
- data/gaia/gaia_sample_small.csv
- data/gaia/gaia_cone_*.csv

**Auto-fetched (2 GB):**
- data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt

## What's Changed

See CHANGELOG.md for complete details.

## Contributors

Carmen Wrede, Lino Casu

## License

ANTI-CAPITALIST SOFTWARE LICENSE v1.4
```

5. Attach assets (if any):
   - Source code (auto-generated)
   - Binary releases (if applicable)

---

## Update README.md

Add prominent badge at top:

```markdown
# SSZ Projection Suite

![Tests](https://img.shields.io/badge/tests-58%20passing-brightgreen)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![License](https://img.shields.io/badge/license-Anti--Capitalist-red)

**Latest Release:** v1.1 (2025-10-18) - Test System Overhaul

## What's New in v1.1

✅ **35 physics tests** with detailed physical interpretations  
✅ **23 technical tests** in silent mode  
✅ **Complete logging system** capturing all test output  
✅ **Smart data fetching** (no overwrites, auto-fetch 2GB Planck)  
✅ **Bug fixes**: pytest crash, import errors, false failures  
✅ **Documentation**: 9 comprehensive README files  
✅ **Papers**: Both MD and PDF formats included  

[See full changelog →](CHANGELOG.md)
```

---

## Create CHANGELOG.md

```bash
cat > CHANGELOG.md << 'EOF'
# Changelog

All notable changes to the SSZ Projection Suite.

## [1.1] - 2025-10-18

### Added
- Complete logging system with output capture
- 9 comprehensive README documentation files
- scripts/fetch_planck.py for automatic Planck data download
- Papers in both MD and PDF formats
- Smart data fetching system (no overwrites)
- Linux test plan documentation

### Changed
- All 35 physics tests now show detailed physical interpretations
- 23 technical tests converted to silent mode
- Updated install.ps1 and install.sh with pytest fix
- Improved test output formatting
- Enhanced run_full_suite.py with logging

### Fixed
- Pytest I/O crash (changed --disable-warnings to -s flag)
- test_segmenter.py import error (removed create_segments)
- False "Failed: 3" in summary (silent tests counted as failures)
- Python cache issues

### Removed
- Verbose output from technical tests (now silent)

## [1.0] - 2025-10-15

### Added
- Initial release
- Complete SSZ physics test suite
- Installation scripts for Windows and Linux
- Basic documentation

EOF
```

---

## Final Checklist

Before pushing:

- [ ] .gitignore created and verified
- [ ] Large files removed (Planck, large GAIA)
- [ ] Build artifacts cleaned
- [ ] Virtual environments removed
- [ ] All source code added
- [ ] Documentation complete
- [ ] Small data files included
- [ ] Papers (MD + PDF) included
- [ ] Commit message descriptive
- [ ] Tag created (optional)
- [ ] README.md updated
- [ ] CHANGELOG.md created
- [ ] Fresh clone tested
- [ ] Installation works from clone

---

## Quick Commands Summary

```bash
# Clean:
find . -type d -name "__pycache__" -exec rm -rf {} +
rm -rf build/ dist/ *.egg-info/ .pytest_cache/ .venv/
rm -f reports/summary-output.md

# Add & Commit:
git add .
git status
git diff --cached --stat
git commit -m "Complete Test System Overhaul (v1.1)"

# Tag & Push:
git tag -a v1.1 -m "Test System Overhaul"
git push origin main
git push origin v1.1

# Verify:
cd /tmp && git clone <your-repo> && cd <repo-name>
./install.sh  # or install.ps1
```

---

## Contact

**Authors:** Carmen Wrede, Lino Casu  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4  
**Repository:** https://github.com/YourUsername/SSZ-Suite

---

**Ready for repository update!** ✅
