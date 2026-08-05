# 🚀 SSZ Suite - Complete Installation Guide

**Comprehensive installation instructions for Windows, Linux, and macOS**

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## 📋 Table of Contents

1. [Quick Start](#quick-start)
2. [System Requirements](#system-requirements)
3. [Automated Installation](#automated-installation)
4. [Manual Installation](#manual-installation)
5. [Google Colab (No Installation)](#google-colab)
6. [Dependencies](#dependencies)
7. [Verification](#verification)
8. [Troubleshooting](#troubleshooting)
9. [Uninstall](#uninstall)

---

## Quick Start

**⚡ Fastest Way to Get Started:**

```bash
# Windows
.\install.ps1

# Linux/macOS
chmod +x install.sh && ./install.sh
```

**That's it!** The script handles everything automatically.

---

## System Requirements

### Minimum Requirements

- **Python**: 3.10 or higher
- **RAM**: 4 GB minimum, 8 GB recommended
- **Disk Space**: 500 MB for code + dependencies, 2 GB additional for Planck data (optional)
- **OS**: Windows 10+, Linux (any modern distro), macOS 10.15+

### Required Software

- **Python 3.10+** with pip
- **Git** (for cloning repository)
- **Virtual environment support** (venv module - included with Python)

### Optional Software

- **Jupyter** - For notebook support (installed automatically if in requirements.txt)
- **wget/curl** - For downloading Planck data (available on most systems)

---

## Automated Installation

### Windows (PowerShell)

**Step 1: Clone Repository**
```powershell
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

**Step 2: Run Install Script**
```powershell
# Standard installation
.\install.ps1

# With full test suite
.\install_and_test.ps1

# Quick tests only
.\install_and_test.ps1 -Quick

# Dry-run (see what would happen)
.\install.ps1 -DryRun
```

### Linux/macOS (Bash)

**Step 1: Clone Repository**
```bash
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

**Step 2: Make Scripts Executable**
```bash
chmod +x install.sh install_and_test.sh
```

**Step 3: Run Install Script**
```bash
# Standard installation
./install.sh

# With full test suite
./install_and_test.sh

# Quick tests only
./install_and_test.sh --quick

# Dry-run (see what would happen)
./install.sh --dry-run
```

### 🔧 What the Scripts Do

The automated install scripts perform **8 steps**:

#### Step 1: Check Python Version
- Verifies Python 3.10+ is installed
- Exits if Python is too old or not found
- Shows Python version and path

#### Step 2: Clean Old Environment
- Removes existing `.venv` directory if present
- Prevents conflicts from old installations
- Fresh start every time

#### Step 3: Create Virtual Environment
- Creates new `.venv` directory
- Isolates dependencies from system Python
- Platform-specific activation instructions

#### Step 4: Upgrade Core Tools
- Updates `pip` to latest version
- Updates `setuptools` and `wheel`
- Ensures compatibility with modern packages

#### Step 5: Install Dependencies
- **Primary**: Installs from `requirements.txt`
- **Fallback**: If requirements.txt missing, installs core packages directly:
  - numpy, scipy, pandas, matplotlib, sympy
  - astropy, astroquery (astronomy)
  - pytest, pytest-timeout, colorama (testing)
  - pyarrow (Parquet support)
  - pyyaml (configuration)

#### Step 6: Install SSZ Suite Package
- Installs package in editable mode (`-e .`)
- Allows code changes without reinstall
- Registers CLI commands (`SSZ-rings`, `SSZ-print-md`)

#### Step 7: Verify Installation
- Checks if CLI tools are accessible
- Tests `SSZ-rings --help`
- Tests `SSZ-print-md --help`
- Confirms installation succeeded

#### Step 8: Run Basic Tests
- Executes 50+ core tests
- Root-level physics tests (PPN, energy, segments)
- SegWave tests (core math, CLI)
- Scripts tests (SSZ kernel, invariants)
- Provides immediate feedback on installation quality

---

## Manual Installation

If you prefer manual control or the automated scripts don't work:

### Step-by-Step Manual Install

**1. Clone Repository:**
```bash
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

**2. Create Virtual Environment:**
```bash
python -m venv .venv
```

**3. Activate Virtual Environment:**

**Windows (PowerShell):**
```powershell
.\.venv\Scripts\Activate.ps1
```

**Windows (CMD):**
```cmd
.venv\Scripts\activate.bat
```

**Linux/macOS:**
```bash
source .venv/bin/activate
```

**4. Upgrade pip:**
```bash
python -m pip install --upgrade pip setuptools wheel
```

**5. Install Dependencies:**
```bash
pip install -r requirements.txt
```

**6. Install Package:**
```bash
pip install -e .
```

**7. Verify Installation:**
```bash
SSZ-rings --help
SSZ-print-md --help
python -c "import SSZ; print('✅ SSZ Suite installed')"
```

**8. Run Tests (Optional):**
```bash
pytest tests/ scripts/tests/ -s -v --tb=short
```

---

## Google Colab

**🌐 No installation required! Run everything in your browser.**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/SSZ_Full_Pipeline_Colab.ipynb)

**Features:**
- ✅ Automatic dependency installation
- ✅ Complete pipeline execution
- ✅ All tests (35 physics + 23 technical)
- ✅ Extended metrics & plots
- ✅ Download results as ZIP

**Perfect for:**
- Quick testing without local setup
- Running on cloud hardware
- Demonstrations and teaching
- Sharing results with collaborators

---

## Dependencies

### Core Dependencies (Required)

| Package | Version | Purpose |
|---------|---------|---------|
| numpy | ≥1.24.0 | Array operations, numerical computing |
| scipy | ≥1.10.0 | Scientific algorithms, optimization |
| pandas | ≥2.0.0 | Data manipulation, CSV handling |
| matplotlib | ≥3.7.0 | Plotting and visualization |
| sympy | ≥1.12 | Symbolic mathematics |
| astropy | ≥5.3.0 | Astronomy calculations, units |
| astroquery | ≥0.4.6 | GAIA/SDSS data fetching |
| pyyaml | ≥6.0 | YAML configuration files |

### Testing Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| pytest | ≥8.0.0 | Test runner framework |
| pytest-timeout | ≥2.1.0 | Timeout handling for tests |
| colorama | ≥0.4.6 | Colored terminal output |
| iniconfig | ≥2.0.0 | pytest configuration |

### Data Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| pyarrow | ≥14.0.0 | Parquet file support for GAIA data |
| requests | (latest) | HTTP requests for data fetching |
| tqdm | (latest) | Progress bars for downloads |

### Optional Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| plotly | ≥5.18.0 | Interactive plots |
| kaleido | ≥0.2.1 | Static image export for plotly |
| jupyter | ≥1.0.0 | Jupyter notebook support |
| ipykernel | ≥6.25.0 | IPython kernel for notebooks |
| pydantic | ≥2.0.0 | Data validation |

**See [requirements.txt](requirements.txt) for complete pinned versions.**

---

## Verification

### Test Installation Success

**Quick Verification:**
```bash
# Activate virtual environment first!
SSZ-rings --help
SSZ-print-md --help
python -c "import SSZ; print('✅ SSZ installed')"
```

**Run Core Tests:**
```bash
pytest tests/ -s -v --tb=short
```

**Expected Output:**
```
========== 50+ tests passed in X.XX seconds ==========
```

**Run Full Suite:**
```bash
python run_full_suite.py
```

**Check CLI Tools:**
```bash
# SSZ Rings Analysis
SSZ-rings --csv data/real_data_full.csv --output out/

# Print Markdown Files
SSZ-print-md --depth 2 --output reports/docs_tree.md
```

---

## Troubleshooting

### Common Issues & Solutions

#### ❌ Python Version Too Old

**Error:**
```
Python 3.9 detected. Python 3.10+ required.
```

**Solution:**
- Download Python 3.10+ from [python.org](https://www.python.org/)
- Or use `pyenv` to manage multiple versions:
  ```bash
  pyenv install 3.10
  pyenv local 3.10
  ```

#### ❌ Module Not Found: astroquery

**Error:**
```
ModuleNotFoundError: No module named 'astroquery'
```

**Solution:**
```bash
pip install astroquery
# Or reinstall all dependencies:
pip install -r requirements.txt
```

#### ❌ pytest: Unknown config option 'timeout'

**Error:**
```
PytestConfigWarning: Unknown config option: timeout
```

**Solution:**
- Install `pytest-timeout`:
  ```bash
  pip install pytest-timeout
  ```
- Or update to latest requirements:
  ```bash
  pip install -U -r requirements.txt
  ```

#### ❌ Permission Denied on Linux

**Error:**
```
bash: ./install.sh: Permission denied
```

**Solution:**
```bash
chmod +x install.sh install_and_test.sh
./install.sh
```

#### ❌ Virtual Environment Activation Fails (Windows)

**Error:**
```
Execution of scripts is disabled on this system
```

**Solution:**
```powershell
# Run as Administrator:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
# Then try again:
.\.venv\Scripts\Activate.ps1
```

#### ❌ Tests Fail: "ModuleNotFoundError: No module named 'SSZ'"

**Error:**
```
ModuleNotFoundError: No module named 'SSZ'
```

**Solution:**
- Ensure virtual environment is activated:
  ```bash
  source .venv/bin/activate  # Linux/macOS
  .\.venv\Scripts\Activate.ps1  # Windows
  ```
- Reinstall package:
  ```bash
  pip install -e .
  ```

#### ❌ Large Data Files Not Found

**Error:**
```
FileNotFoundError: data/planck/...
```

**Solution:**
- Fetch Planck data (optional, 2 GB):
  ```bash
  python scripts/fetch_planck.py
  ```
- Or skip Planck-dependent tests
- **Note:** Basic tests don't require Planck data

### 🐛 Still Having Issues?

1. **Check Python version**: `python --version` (must be 3.10+)
2. **Check virtual environment**: `which python` (should show `.venv` path)
3. **Clear Python cache**: 
   ```bash
   find . -type d -name "__pycache__" -exec rm -rf {} +  # Linux/macOS
   Get-ChildItem -Recurse -Filter "__pycache__" | Remove-Item -Recurse -Force  # Windows
   ```
4. **Fresh install**:
   ```bash
   rm -rf .venv
   ./install.sh
   ```

---

## Uninstall

### Complete Removal

**Remove Virtual Environment:**
```bash
rm -rf .venv        # Linux/macOS
Remove-Item -Recurse -Force .venv  # Windows PowerShell
```

**Remove Generated Files (Optional):**
```bash
# Reports
rm -rf reports/

# Output
rm -rf out/ agent_out/ vfall_out/

# Cache
find . -type d -name "__pycache__" -exec rm -rf {} +  # Linux/macOS
Get-ChildItem -Recurse -Filter "__pycache__" | Remove-Item -Recurse -Force  # Windows
```

**Remove Repository:**
```bash
cd ..
rm -rf Segmented-Spacetime-Mass-Projection-Unified-Results
```

---

## Next Steps

After installation:

1. **✅ Verify Installation** - Run basic tests
2. **📖 Read Documentation** - Check [README.md](README.md)
3. **🧪 Run Tests** - `pytest tests/` or `python run_full_suite.py`
4. **🚀 Run Analysis** - `python run_all_ssz_terminal.py`
5. **📊 Check Results** - Look in `reports/` directory

**Useful Links:**
- 📖 [README.md](README.md) - Project overview
- 📊 [TESTING_COMPLETE_GUIDE.md](TESTING_COMPLETE_GUIDE.md) - Testing guide
- 🧪 [DATA_FETCHING_README.md](DATA_FETCHING_README.md) - Data management
- 🌐 [Colab Notebook](SSZ_Full_Pipeline_Colab.ipynb) - Browser-based execution

---

**Happy Computing! 🚀**
