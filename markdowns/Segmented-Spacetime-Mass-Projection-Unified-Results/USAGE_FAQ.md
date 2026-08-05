# Usage Guide & FAQ - SSZ Theory

**Complete usage instructions and frequently asked questions**

Date: 2025-10-29  
Version: 1.0 Final

© 2025 Carmen Wrede & Lino Casu

---

## Table of Contents

1. [Quick Start](#quick-start)
2. [Installation](#installation)
3. [Running Validations](#running-validations)
4. [Script Usage](#script-usage)
5. [FAQ](#faq)
6. [Troubleshooting](#troubleshooting)
7. [Reproduction Guide](#reproduction-guide)

---

## Quick Start

### 5-Minute Quick Start

**1. Clone Repository:**
```bash
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

**2. Install Dependencies:**
```bash
# Windows
.\install.ps1

# Linux/macOS
./install.sh
```

**3. Run Complete Validation:**
```bash
python run_complete_validation_extended.py
```

**Expected Runtime:** ~10-15 minutes  
**Expected Result:** ALL PASS

---

## Installation

### System Requirements

**Minimum:**
- Python 3.10 or higher
- 4 GB RAM
- 2 GB free disk space

**Recommended:**
- Python 3.10+
- 8 GB RAM
- 5 GB free disk space
- SSD for better performance

### Platform-Specific Installation

#### Windows

```powershell
# 1. Open PowerShell as Administrator
# 2. Navigate to repository
cd path\to\Segmented-Spacetime-Mass-Projection-Unified-Results

# 3. Run installation script
.\install.ps1

# 4. Wait for completion (~5-10 minutes)
```

**What it does:**
- Creates Python virtual environment
- Installs all dependencies
- Fetches Planck data (2 GB) if missing
- Runs test suite
- Generates summary

#### Linux/macOS

```bash
# 1. Open terminal
# 2. Navigate to repository
cd path/to/Segmented-Spacetime-Mass-Projection-Unified-Results

# 3. Make script executable
chmod +x install.sh

# 4. Run installation
./install.sh

# 5. Wait for completion (~5-10 minutes)
```

#### Google Colab

```python
# 1. Upload SSZ_Colab_AutoRunner.ipynb to Colab
# 2. Run the "One-Click Installation" cell
# 3. Wait for completion

# Or manually:
!git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
%cd Segmented-Spacetime-Mass-Projection-Unified-Results
!pip install -r requirements.txt
!python run_full_suite.py
```

---

## Running Validations

### Master Validation Pipeline

**Extended Master Pipeline (Recommended):**
```bash
python run_complete_validation_extended.py
```

**Features:**
- Runs ALL validation steps (12 steps)
- Extended error logging
- Comprehensive reports
- Individual step logs
- Error summaries

**Output:** `validation_complete_extended/` directory

**Runtime:** ~10-15 minutes

---

**Original Master Pipeline:**
```bash
python run_complete_validation_master.py
```

**Features:**
- Runs core validation steps (7 steps)
- Basic logging
- Standard reports

**Output:** `validation_complete/` directory

**Runtime:** ~7 minutes

---

### Individual Validation Scripts

#### Formula Verification
```bash
python verify_theory_scientific.py
```

**Purpose:** Verify all SSZ formulas scientifically  
**Tests:** 6 tests (5 critical + 1 info)  
**Runtime:** ~5 seconds  
**Expected:** 5/5 PASS + 1 INFO

---

#### Test Suite
```bash
python run_full_suite.py
```

**Purpose:** Run complete test suite  
**Tests:** 22 tests (100%)  
**Runtime:** ~224 seconds  
**Expected:** 22/22 PASS

---

#### ToE Unified Validation
```bash
python run_ssz_unified_validation.py
```

**Purpose:** Theory of Everything validation (11 steps)  
**Includes:** BH bomb test (Step 3)  
**Runtime:** ~180 seconds  
**Expected:** 11/11 PASS

---

#### ToE v2 Deterministic
```bash
python run_toe_validation_v2.py
```

**Purpose:** Deterministic 6-pillar validation  
**Includes:** BH bomb test (Pillar 5)  
**Runtime:** ~2 seconds  
**Expected:** 6/6 PASS

---

#### Grid Convergence
```bash
python test_grid_convergence.py
```

**Purpose:** Numerical stability verification  
**Tests:** 4 Richardson extrapolation tests  
**Runtime:** ~1 second  
**Expected:** 4/4 PASS

---

### Individual Physics Tests

#### PPN Parameters
```bash
python test_ppn_exact.py
```
**Tests:** β, γ parameters  
**Expected:** β = γ = 1 (GR limit)

#### Velocity Duality
```bash
python test_vfall_duality.py
```
**Tests:** v_esc × v_fall = c²  
**Expected:** Error = 0.000e+00

#### Energy Conditions
```bash
python test_energy_conditions.py
```
**Tests:** WEC, DEC, SEC  
**Expected:** All satisfied for r ≥ 5r_s

---

### Analysis Scripts

#### Complete SSZ Analysis
```bash
python segspace_all_in_one_extended.py
```
**Purpose:** Full SSZ analysis  
**Output:** Analysis plots and data  
**Runtime:** ~60 seconds

#### Shadow Predictions
```bash
python shadow_predictions_exact.py
```
**Purpose:** BH shadow calculations  
**Output:** Shadow prediction data  
**Runtime:** ~30 seconds

#### Lagrangian Tests
```bash
# Different objects
python lagrangian_tests.py --object sun
python lagrangian_tests.py --object jupiter
python lagrangian_tests.py --object ns
python lagrangian_tests.py --object bh
```

---

## Script Usage

### Validation Scripts

#### run_complete_validation_extended.py

**Full Command:**
```bash
python run_complete_validation_extended.py
```

**Options:** None (runs all steps)

**Outputs:**
- `validation_complete_extended/full-output-extended.md` - Complete log
- `validation_complete_extended/COMPLETE_VALIDATION_SUMMARY_EXTENDED.md` - Summary
- `validation_complete_extended/error_log.txt` - Error log
- `validation_complete_extended/validation_results_extended.json` - JSON results
- `validation_complete_extended/plots/` - All plots
- `validation_complete_extended/reports/` - All reports
- `validation_complete_extended/data/` - All data
- `validation_complete_extended/logs/` - Individual logs

---

#### verify_theory_scientific.py

**Full Command:**
```bash
python verify_theory_scientific.py
```

**Tests:**
1. Formel-Korrektheit
2. Test-Daten-Vergleich
3. Universal Intersection
4. Causality Check
5. SSZ Asymptotic Behavior (INFO)
6. Golden Ratio Verification

**Success Criteria:**
- 5/5 critical tests PASS
- 1 INFO (expected SSZ behavior)

---

#### run_full_suite.py

**Full Command:**
```bash
python run_full_suite.py
```

**Test Categories:**
- Physics Tests (6)
- SegWave Tests (20)
- Scripts Tests (15)
- Cosmos Tests (1)

**Outputs:**
- `reports/RUN_SUMMARY.md` - Compact summary
- `reports/full-output.md` - Complete log
- `reports/summary-output.md` - Detailed summary

---

### Analysis Scripts

#### segspace_all_in_one_extended.py

**Usage:**
```bash
python segspace_all_in_one_extended.py
```

**What it does:**
- Calculates mass validation
- Plots time dilation
- Finds universal intersection
- Generates sensitivity analysis

**Outputs:**
- Multiple PNG plots
- CSV data files

---

#### shadow_predictions_exact.py

**Usage:**
```bash
python shadow_predictions_exact.py
```

**What it does:**
- Calculates BH shadow radius
- For various masses
- SSZ vs GR comparison

**Outputs:**
- Shadow prediction data
- Comparison plots

---

#### lagrangian_tests.py

**Usage:**
```bash
python lagrangian_tests.py --object <OBJECT>
```

**Objects:**
- `sun` - Solar mass
- `jupiter` - Jupiter mass
- `ns` - Neutron star
- `bh` - Black hole

**Example:**
```bash
python lagrangian_tests.py --object sun
```

**Output:**
- Lagrangian formulation validation
- Action principle verification
- Euler-Lagrange equations

---

## FAQ

### General Questions

**Q: What is SSZ?**  
A: Segmented Spacetime (SSZ) is a geometric theory of gravity based on discrete spacetime structure with exponential field saturation. It resolves singularities and provides testable predictions.

**Q: How is SSZ different from GR?**  
A: SSZ has:
- No singularities (finite curvature everywhere)
- Different asymptotic behavior (D→0.5, not D→1)
- Universal intersection point with GR
- Black hole stabilization
- φ-based geometry

**Q: Is SSZ compatible with observations?**  
A: Yes, 97.9% accuracy with ESO professional data (30,008 measurements, p < 0.01).

---

### Installation Questions

**Q: Do I need admin rights?**  
A: Not required, but recommended for system-wide installation.

**Q: Can I use an existing Python environment?**  
A: Yes, but virtual environment is recommended to avoid conflicts.

**Q: What if Planck data download fails?**  
A: Retry or manually download from ESA/IPAC. Scripts will continue without it for core tests.

**Q: How much disk space do I need?**  
A: Minimum 2 GB (for Planck data), recommended 5 GB (with outputs).

---

### Validation Questions

**Q: How long does validation take?**  
A: 
- Quick test suite: ~4 minutes
- Extended pipeline: ~10-15 minutes
- Individual tests: seconds to minutes

**Q: What if a test fails?**  
A: Check `error_log.txt` for details. Most common causes:
- Missing dependencies
- Corrupted cache (run CLEAR_CACHE)
- File permissions

**Q: Are all tests required to pass?**  
A: Critical tests must pass. Optional tests are for extended validation.

**Q: Can I run tests in parallel?**  
A: Not recommended. Tests may share resources.

---

### Script Questions

**Q: Which scripts are scientifically validated?**  
A: All validation and test scripts (see CODE_DOCUMENTATION.md).

**Q: Which scripts are excluded from tests?**  
A: Animation renderers (`ssz_bigbang_vs_ssz_anim.py`) and DALL-E tests (not scientific validation).

**Q: Can I modify the scripts?**  
A: Yes, but verify results match expected outputs.

**Q: How do I add new tests?**  
A: Follow existing test patterns, add to pipeline, update documentation.

---

### Output Questions

**Q: Where are validation outputs stored?**  
A: 
- `validation_complete/` - Original pipeline
- `validation_complete_extended/` - Extended pipeline

**Q: Can I delete old outputs?**  
A: Yes, outputs are regenerated on each run.

**Q: How do I interpret results?**  
A: Check summary files (`.md`) for human-readable results, JSON for machine-readable.

**Q: Are outputs reproducible?**  
A: Yes, with fixed seeds (PY=133742, NP=424242) in ToE v2.

---

## Troubleshooting

### Common Issues

#### Issue 1: Import Errors

**Problem:** `ModuleNotFoundError`

**Solution:**
```bash
# Clear cache
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux

# Reinstall dependencies
pip install -r requirements.txt

# Retry
python run_complete_validation_extended.py
```

---

#### Issue 2: Unicode Errors (Windows)

**Problem:** `UnicodeEncodeError`

**Solution:**
- Scripts use ASCII fallbacks automatically
- If persists, set: `set PYTHONIOENCODING=utf-8`

---

#### Issue 3: Pytest Cache Issues

**Problem:** Stale test results

**Solution:**
```bash
# Clear cache BEFORE running tests
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux

# Then run tests
python run_full_suite.py
```

---

#### Issue 4: Permission Errors

**Problem:** Cannot write to output directory

**Solution:**
- Run with appropriate permissions
- Or change OUTPUT_BASE in script
- Check disk space

---

#### Issue 5: Timeout Errors

**Problem:** Script timeout

**Solution:**
- Increase timeout in pipeline configuration
- Check system resources (CPU, RAM)
- Close other applications

---

### Getting Help

**1. Check Documentation:**
- [README.md](README.md) - Project overview
- [CODE_DOCUMENTATION.md](CODE_DOCUMENTATION.md) - Script reference
- [FULL_VALIDATION_REPORT.md](FULL_VALIDATION_REPORT.md) - Validation details

**2. Check Error Logs:**
- `error_log.txt` in output directory
- Individual logs in `logs/` directory

**3. Check GitHub Issues:**
- Search existing issues
- Create new issue with:
  - OS and Python version
  - Full error message
  - Steps to reproduce

**4. Contact Authors:**
- Carmen Wrede & Lino Casu
- Repository: github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results

---

## Reproduction Guide

### Exact Reproduction Steps

**To reproduce ALL results exactly:**

**1. Clean Environment:**
```bash
# Start fresh
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Clear any existing cache
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux
```

**2. Install Dependencies:**
```bash
# Create virtual environment
python -m venv .venv

# Activate
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # Linux

# Install exact versions
pip install -r requirements.txt
```

**3. Run Extended Pipeline:**
```bash
python run_complete_validation_extended.py
```

**4. Verify Results:**
```bash
# Check summary
cat validation_complete_extended/COMPLETE_VALIDATION_SUMMARY_EXTENDED.md

# Expected:
# - Total Steps: 12
# - Passed: 10+/12
# - Success Rate: > 80%
# - Critical Failures: 0
```

---

### Deterministic Reproduction

**For bit-exact reproducibility (ToE v2 only):**

```bash
# Run ToE v2 (deterministic)
python run_toe_validation_v2.py

# Seeds are fixed:
# PY_SEED = 133742
# NP_SEED = 424242

# Expected results:
# - All 6 pillars PASS
# - Exact same numerical values
# - Reproducible across platforms
```

---

### Reproduction Checklist

- [ ] Clean git clone
- [ ] Python 3.10+ installed
- [ ] Virtual environment created
- [ ] Dependencies installed from requirements.txt
- [ ] Cache cleared before run
- [ ] Extended pipeline executed
- [ ] Results match expected outputs
- [ ] Error log checked (should be minimal)
- [ ] All critical tests PASS

---

### Expected Results Summary

**Formula Verification:**
- ✅ 5/5 critical tests PASS
- ℹ️ 1 INFO (SSZ asymptotic behavior)

**Test Suite:**
- ✅ 22/22 tests PASS (100%)

**ToE Unified:**
- ✅ 11/11 steps PASS
- ✅ BH bomb test PASS (Gain reduction 6.55×)

**ToE v2:**
- ✅ 6/6 pillars PASS (100%)
- ✅ BH bomb test PASS (Gain reduction 6.55×)

**Grid Convergence:**
- ✅ 4/4 tests PASS
- ✅ Convergence order ≥ 1.8

**Overall:**
- ✅ 58/58 science tests PASS
- ✅ 98.8% scientific validation score
- ✅ 97.9% empirical accuracy

---

## Additional Resources

**Documentation:**
- [Complete Scientific Documentation](COMPLETE_SCIENTIFIC_DOCUMENTATION.md)
- [Code Documentation](CODE_DOCUMENTATION.md)
- [Full Validation Report](FULL_VALIDATION_REPORT.md)
- [Theory Documentation](docs/theory/INDEX.md)

**Test Status:**
- [Test Suite Status](TEST_SUITE_STATUS.md)
- [ToE Validation Status](TOE_VALIDATION_STATUS.md)
- [Scientific Verification Checklist](SCIENTIFIC_VERIFICATION_CHECKLIST.md)

**Reports:**
- [Executive Summary](SSZ_EXECUTIVE_SUMMARY.md) - 5 pages
- [Complete Report](SSZ_COMPLETE_FINAL_REPORT.md) - 60+ pages

---

**© 2025 Carmen Wrede & Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Version:** 1.0 Final  
**Date:** 2025-10-29
