# SSZ Projection Suite - Installation Guide

**Quick Install:** Use the automated install scripts for your platform.

---

## Automated Installation (Recommended)

### Windows (PowerShell)

```powershell
# Full installation
.\install.ps1

# Options
.\install.ps1 -SkipTests     # Skip test suite
.\install.ps1 -DevMode       # Editable install for development
.\install.ps1 -DryRun        # Preview without executing
```

### Linux / macOS (Bash)

```bash
# Make executable
chmod +x install.sh

# Full installation
./install.sh

# Options
./install.sh --skip-tests    # Skip test suite
./install.sh --dev-mode      # Editable install for development
./install.sh --dry-run       # Preview without executing
```

---

## What the Install Scripts Do

1. **Check Python** (≥ 3.8 required)
2. **Create virtual environment** (.venv)
3. **Activate virtual environment**
4. **Upgrade pip, setuptools, wheel**
5. **Install dependencies** (from requirements.txt or core packages)
6. **Install SSZ Suite package** (standard or editable mode)
7. **Run test suite** (optional, can skip)
8. **Verify installation** (check CLI commands)

---

## Manual Installation

If you prefer manual control or troubleshooting:

### 1. Create Virtual Environment

**Windows:**
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Linux/macOS:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Upgrade Core Tools

```bash
python -m pip install --upgrade pip setuptools wheel
```

### 3. Install Dependencies

**From requirements.txt:**
```bash
pip install -r requirements.txt
```

**Or manually (core packages):**
```bash
pip install numpy scipy pandas matplotlib astropy pyyaml pytest
```

### 4. Install Package

**Standard installation:**
```bash
pip install .
```

**Development mode (editable):**
```bash
pip install -e .
```

### 5. Verify Installation

```bash
SSZ-rings --help
SSZ-print-md --help
pytest tests/ -v
```

---

## System Requirements

### Minimum

- **Python:** 3.8 or higher
- **OS:** Windows 10+, Linux (any modern distro), macOS 10.14+
- **RAM:** 2 GB
- **Disk:** 500 MB

### Recommended

- **Python:** 3.10 or higher
- **RAM:** 8 GB (for large dataset analysis)
- **Disk:** 2 GB (with validation papers)

---

## Dependencies

### Core Scientific Stack

- **numpy** - Numerical arrays and linear algebra
- **scipy** - Scientific algorithms and optimization
- **pandas** - Data structures and analysis
- **matplotlib** - Plotting and visualization
- **astropy** - Astronomical calculations
- **pyyaml** - Configuration file parsing

### Optional

- **pytest** - Testing framework (recommended)
- **plotly** - Interactive plots (for visualization features)
- **jupyter** - Notebook environment

---

## Configuration

### Validation Papers Directory

**Windows:**
```powershell
# Set environment variable (permanent)
setx SSZ_SOURCES_DIR "H:\WINDSURF\VALIDATION_PAPER"

# Or edit config/sources.yaml directly
```

**Linux/macOS:**
```bash
# Add to ~/.bashrc or ~/.zshrc
export SSZ_SOURCES_DIR="/path/to/VALIDATION_PAPER"

# Or edit config/sources.yaml directly
```

### Configuration Files

- `config/sources.yaml` - Validation papers directory
- `pyproject.toml` - Package metadata and entry points
- `.env` (optional) - Environment-specific settings

---

## Troubleshooting

### Python Not Found

**Windows:**
- Install from [python.org](https://www.python.org/downloads/)
- Check "Add Python to PATH" during installation

**Linux:**
```bash
sudo apt install python3 python3-venv python3-pip  # Debian/Ubuntu
sudo dnf install python3 python3-venv python3-pip  # Fedora
```

**macOS:**
```bash
brew install python@3.10
```

### Permission Denied (Linux/macOS)

```bash
chmod +x install.sh
./install.sh
```

### Virtual Environment Activation Fails

**Windows (ExecutionPolicy):**
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**Linux/macOS:**
```bash
# Use full path
source $(pwd)/.venv/bin/activate
```

### pip Install Fails

```bash
# Upgrade pip first
python -m pip install --upgrade pip

# Use --user flag if venv not activated
python -m pip install --user -r requirements.txt
```

### Tests Fail

Non-fatal if you skip tests with `--skip-tests` flag. Common issues:

- **Missing test data:** Some tests require example datasets
- **Unicode errors:** Ensure UTF-8 encoding in terminal
- **Network tests:** May fail without internet connection

```bash
# Run specific test
pytest tests/test_segwave_core.py -v

# Skip failing test
pytest tests/ -v -k "not network"
```

---

## Post-Installation

### Verify Commands

```bash
# Check installed commands
SSZ-rings --help
SSZ-print-md --help

# List installed package
pip list | grep segmented
```

### Run Example

```bash
# Activate venv first
source .venv/bin/activate  # Linux/macOS
.\.venv\Scripts\Activate.ps1  # Windows

# Run G79.29+0.46 analysis
SSZ-rings --csv data/observations/G79_29+0_46_CO_NH3_rings.csv \
          --v0 12.5 \
          --fit-alpha \
          --out-table reports/g79.csv
```

### View Documentation

```bash
# Segwave guide
less docs/segwave_guide.md       # Linux/macOS
Get-Content docs\segwave_guide.md  # Windows

# API reference
python -c "import SSZ.segwave; help(SSZ.segwave)"
```

---

## Uninstallation

### Remove Package

```bash
pip uninstall segmented-spacetime-suite-extended
```

### Remove Virtual Environment

```bash
# Deactivate first
deactivate

# Remove directory
rm -rf .venv  # Linux/macOS
Remove-Item -Recurse -Force .venv  # Windows
```

---

## Development Setup

For contributors and developers:

```bash
# Install in editable mode with dev dependencies
./install.sh --dev-mode

# Or manually
pip install -e ".[dev]"

# Run tests continuously
pytest-watch tests/

# Build package
python -m build
```

---

## Support

**Documentation:**
- Main README: `README.md`
- Segwave Guide: `docs/segwave_guide.md`
- Changelog: `CHANGELOG.md`

**Issues:**
- Check existing tests: `pytest tests/ -v`
- Review error logs: `data/logs/`
- Validate config: `config/sources.yaml`

---

**Copyright © 2025 Carmen Wrede und Lino Casu**  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
