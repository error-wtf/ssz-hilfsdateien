# Quick Start Guide

**Get started with SSZ in under 5 minutes**

**Repository:** Segmented Spacetime Mass Projection Unified Results  
**Version:** v1.2.0 (2025-10-19)  
**Status:** ✅ Production-Ready | Cross-Platform

---

## ⚡ Fastest Start: Google Colab (Zero Installation)

**Click → Run → Done in 5-10 minutes:**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/SSZ_Full_Pipeline_Colab.ipynb)

**Steps:**
1. Click badge above
2. `Runtime` → `Run all` (or press `Ctrl+F9`)
3. Wait ~5-10 minutes
4. ✅ Download results ZIP

**What you get:**
- ✅ 69 tests executed (35 physics + 23 technical + 11 validation)
- ✅ Complete SSZ analysis (20+ scripts)
- ✅ All reports and plots
- ✅ Downloadable ZIP archive

**No Python installation needed!**

---

## 🚀 Local Installation (One Command)

### Windows

```powershell
# Open PowerShell in repository directory
.\install.ps1
```

**Time:** ~2 minutes  
**What it does:**
- Creates virtual environment
- Installs all dependencies
- Runs 69 tests
- Verifies installation

### Linux/WSL/macOS

```bash
# Make executable (first time only)
chmod +x install.sh

# Run installer
./install.sh
```

**Time:** ~2 minutes  
**What it does:**
- Creates virtual environment
- Installs all dependencies
- Runs 69 tests
- Verifies installation

---

## 📊 Run First Analysis

### Activate Virtual Environment

**Windows:**
```powershell
.\.venv\Scripts\activate.ps1
```

**Linux/WSL/macOS:**
```bash
source .venv/bin/activate
```

### Quick Analysis

```bash
# Complete SSZ analysis (~10 minutes)
python run_all_ssz_terminal.py

# Ring velocity analysis (G79 nebula)
SSZ-rings --csv data/observations/G79_29+0_46_CO_NH3_rings.csv --v0 12.5 --fit-alpha

# All-in-one runner
python segspace_all_in_one_extended.py all
```

**Scripts:** [`run_all_ssz_terminal.py`](run_all_ssz_terminal.py) | [`segspace_all_in_one_extended.py`](segspace_all_in_one_extended.py)

---

## 🧪 Run Tests

### Quick Tests (~30 seconds)

```bash
python run_full_suite.py --quick
```

### Full Test Suite (~2-3 minutes)

```bash
python run_full_suite.py
```

**Script:** [`run_full_suite.py`](run_full_suite.py)

### Individual Test Categories

```bash
# Physics tests (detailed output)
python test_ppn_exact.py              # PPN parameters
python test_vfall_duality.py          # Dual velocity
python test_energy_conditions.py      # Energy conditions

# Pytest tests
pytest tests/ -s -v                   # All pytest tests
pytest scripts/tests/ -s -v           # Script tests
```

---

## 📖 Next Steps

### 1. Read Documentation

**Essential:**
- [README.md](README.md) - Main overview
- [DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md) - Doc navigator
- [INSTALL_README.md](INSTALL_README.md) - Detailed installation

**Data:**
- [DATA_ACQUISITION_COMPLETE_GUIDE.md](docs/DATA_ACQUISITION_COMPLETE_GUIDE.md) - How to fetch data (ESO, NED, SIMBAD, GAIA)
- [Sources.md](Sources.md) - Data provenance
- [DATA_TYPE_USAGE_GUIDE.md](data/DATA_TYPE_USAGE_GUIDE.md) - Dataset usage

**Testing:**
- [TEST_SUITE_VERIFICATION.md](TEST_SUITE_VERIFICATION.md) - Test system
- [LOGGING_SYSTEM_README.md](LOGGING_SYSTEM_README.md) - Test logging

### 2. Explore Analysis Tools

```bash
# View all CLI tools
SSZ-rings --help
SSZ-print-md --help

# Analysis examples
python segspace_all_in_one_extended.py --help

# Pipeline options
python run_all_ssz_terminal.py --help
```

**Scripts:** [`test_ppn_exact.py`](test_ppn_exact.py) | [`test_vfall_duality.py`](test_vfall_duality.py) | [`test_energy_conditions.py`](test_energy_conditions.py) | [`segspace_all_in_one_extended.py`](segspace_all_in_one_extended.py) | [`run_all_ssz_terminal.py`](run_all_ssz_terminal.py)

### 3. Check Platform Compatibility

```bash
# Run compatibility check
python PLATFORM_COMPATIBILITY_CHECK.py
```

**Script:** [`PLATFORM_COMPATIBILITY_CHECK.py`](PLATFORM_COMPATIBILITY_CHECK.py)

**Expected output:**
```
✅ Python version compatible
✅ UTF-8 fully supported
✅ All required files present
✅ Path handling correct
🎉 PLATFORM CHECK PASSED
```

---

## 💡 Common Tasks

### Run Specific Analysis

```bash
# Redshift evaluation only
python segspace_all_in_one_extended.py eval-redshift \
       --csv ./data/real_data_emission_lines.csv \
       --mode hybrid --plots

# Mass validation
python segspace_all_in_one_extended.py validate-mass

# Bound energy analysis
python segspace_all_in_one_extended.py bound-energy --plots
```

**Script:** [`segspace_all_in_one_extended.py`](segspace_all_in_one_extended.py)

### Print All Documentation

```bash
# All Markdown files
SSZ-print-md --root . --order path

# Papers only
SSZ-print-md --root papers --order depth

# Reports only
SSZ-print-md --root reports --order path
```

### Generate Reports

```bash
# Full test suite + reports
python run_full_suite.py

# Check generated reports
ls reports/
# - RUN_SUMMARY.md (compact overview)
# - summary-output.md (complete log)
```

---

## 🔧 Troubleshooting

### Installation Issues

**Problem:** Python not found
```bash
# Check Python version
python --version  # Should be 3.10+

# Or try python3
python3 --version
```

**Problem:** Permission denied (Linux/WSL)
```bash
# Make scripts executable
chmod +x install.sh install_and_test.sh run_full_suite.sh
```

**Problem:** UTF-8 encoding errors (Windows)
```powershell
# Already handled by install.ps1
# If issues persist, check:
$OutputEncoding = [System.Text.Encoding]::UTF8
```

### Test Failures

**Problem:** Pytest crashes
```bash
# ALWAYS use -s flag (NOT --disable-warnings)
pytest tests/ -s -v --tb=short
```

**Problem:** Missing data files
```bash
# Fetch missing data
python scripts/fetch_planck.py        # Planck CMB (~2 GB)
python scripts/fetch_gaia_full.py     # GAIA catalog
```

**Problem:** Import errors
```bash
# Ensure virtual environment is active
source .venv/bin/activate  # Linux/WSL/macOS
.\.venv\Scripts\activate.ps1  # Windows

# Reinstall dependencies
pip install -r requirements.txt
```

### Platform-Specific

**Windows:**
- Use PowerShell (not CMD)
- UTF-8 auto-configured by scripts
- Path separators handled automatically

**WSL:**
- Auto-detected by install.sh
- Behaves like Linux
- Can access Windows files via `/mnt/`

**Colab:**
- Use Colab notebooks (no installation)
- Dependencies auto-installed
- Results downloadable as ZIP

**For detailed troubleshooting:** See [INSTALL_README.md](INSTALL_README.md)

---

## 📊 Expected Results

### After Installation

```
✅ Virtual environment created (.venv/)
✅ All dependencies installed (numpy, scipy, pandas, etc.)
✅ 69 tests passing (35 physics + 23 technical + 11 validation)
✅ CLI tools available (SSZ-rings, SSZ-print-md)
✅ Platform compatibility verified
```

### After First Analysis

```
✅ Reports generated (reports/)
✅ Analysis outputs (out/)
✅ Plots created (reports/figures/)
✅ Summary files (reports/RUN_SUMMARY.md)
✅ Data validated (427 real observations)
```

### Test Results Summary

```
Total Physics Tests: 35
Silent Technical Tests: 23
Passed: 58/58
Failed: 0/58
Success Rate: 100.0%
Duration: ~2-3 minutes
```

---

## 🎯 What to Run First

### 1. Platform Check (30 seconds)
```bash
python PLATFORM_COMPATIBILITY_CHECK.py
```

### 2. Quick Tests (30 seconds)
```bash
python run_full_suite.py --quick
```

### 3. Ring Analysis (1 minute)
```bash
SSZ-rings --csv data/observations/G79_29+0_46_CO_NH3_rings.csv --v0 12.5
```

### 4. Full Analysis (10 minutes)
```bash
python run_all_ssz_terminal.py
```

---

## 📞 Get Help

**Can't get started?**

1. **Check documentation:**
   - [README.md](README.md) - Main guide
   - [INSTALL_README.md](INSTALL_README.md) - Installation details
   - [DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md) - All docs

2. **Run compatibility check:**
   ```bash
   python PLATFORM_COMPATIBILITY_CHECK.py
   ```

3. **Check platform guide:**
   - [CROSS_PLATFORM_COMPATIBILITY_ANALYSIS.md](CROSS_PLATFORM_COMPATIBILITY_ANALYSIS.md)

4. **Open an issue:**
   - https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/issues

---

## 🎓 Learning Resources

### For Beginners

1. Start with [README.md](README.md)
2. Try Google Colab (zero setup)
3. Read [Sources.md](Sources.md) for data background
4. Explore [papers/validation/](papers/validation/) papers

### For Researchers

1. Review [COMPREHENSIVE_DATA_ANALYSIS.md](COMPREHENSIVE_DATA_ANALYSIS.md)
2. Check [PAIRED_TEST_ANALYSIS_COMPLETE.md](PAIRED_TEST_ANALYSIS_COMPLETE.md)
3. Read validation papers in [papers/validation/](papers/validation/)
4. Explore [docs/theory/](docs/theory/) for theory

### For Developers

1. Study [CROSS_PLATFORM_COMPATIBILITY_ANALYSIS.md](CROSS_PLATFORM_COMPATIBILITY_ANALYSIS.md)
2. Review [LOGGING_SYSTEM_README.md](LOGGING_SYSTEM_README.md)
3. Check [TEST_SUITE_VERIFICATION.md](TEST_SUITE_VERIFICATION.md)
4. Read [SSZ_COMPLETE_PIPELINE.md](SSZ_COMPLETE_PIPELINE.md)

---

## ✅ Success Checklist

After setup, you should have:

- ✅ Virtual environment active (`.venv/`)
- ✅ All 69 tests passing
- ✅ CLI tools working (`SSZ-rings --help`)
- ✅ Data files present (427 observations)
- ✅ Reports directory created (`reports/`)
- ✅ Platform compatibility confirmed

**If all ✅ → You're ready to use SSZ!**

---

**Version:** v1.2.0 (2025-10-19)  
**Time to Start:** < 5 minutes  
**Status:** ✅ Production-Ready

© 2025 Carmen Wrede & Lino Casu | ANTI-CAPITALIST SOFTWARE LICENSE v1.4
