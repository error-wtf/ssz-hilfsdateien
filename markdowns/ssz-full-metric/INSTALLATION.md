# Installation Guide

Complete installation instructions for SSZ Full Metric.

## 📋 Requirements

### Python Version
- Python 3.8 or higher
- Tested on Python 3.8, 3.9, 3.10, 3.11

### Operating Systems
- ✅ Windows 10/11
- ✅ Linux (Ubuntu, Debian, Fedora, etc.)
- ✅ macOS (Intel & Apple Silicon)

---

## 🚀 Quick Install

### Method 1: Git Clone (Recommended)

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/ssz-full-metric.git
cd ssz-full-metric

# Install dependencies
pip install numpy scipy matplotlib mpmath

# Verify installation
python -c "from ssz_metric import *; print('✓ SSZ Metric installed!')"
```

### Method 2: Download ZIP

1. Download from GitHub: `Code → Download ZIP`
2. Extract to your preferred location
3. Open terminal in the extracted folder
4. Run: `pip install numpy scipy matplotlib mpmath`

---

## 📦 Dependencies

### Required Packages

```bash
numpy>=1.20.0      # Array operations & linear algebra
scipy>=1.7.0       # Scientific computing & optimization
matplotlib>=3.3.0  # Plotting
mpmath>=1.2.0      # Arbitrary precision arithmetic
```

### Install All at Once

```bash
pip install numpy scipy matplotlib mpmath
```

Or using requirements file:

```bash
pip install -r requirements.txt
```

---

## 🔧 Development Installation

For contributing to the project:

```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/ssz-full-metric.git
cd ssz-full-metric

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Install in editable mode
pip install -e .

# Install development dependencies
pip install pytest pytest-cov black flake8
```

---

## ✅ Verify Installation

### Quick Check

```bash
python -c "from ssz_metric import *; print('SSZ Metric version:', __version__)"
```

### Run Tests

```bash
# Basic tests
python tests/test_intersection.py
python tests/test_metric_properties.py

# All tests
python -m pytest tests/ -v
```

### Expected Output

```
================================================================================
INTERSECTION TEST
================================================================================

System: M = 1.988e+30 kg (Solar mass)
Schwarzschildradius: r_s = 2.953 km

Intersection Point:
  u* = 1.3865616 (canonical: 1.386562)
  Error: |u* - canonical| = 3.8e-07  ← EXTRAORDINARY!

Natural Boundary:
  r_φ = 0.825 r_s = 2.437 km
  A(r_φ) = 0.284 > 0  ← NO SINGULARITY!

================================================================================
RESULT: PASS ✓
================================================================================
```

---

## 🐍 Virtual Environment (Recommended)

### Why Use Virtual Environments?

- Isolate project dependencies
- Avoid conflicts with system packages
- Easy to reproduce environments

### Create & Use

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
pip install numpy scipy matplotlib mpmath
```

**Linux/Mac:**
```bash
python3 -m venv venv
source venv/bin/activate
pip install numpy scipy matplotlib mpmath
```

**Deactivate:**
```bash
deactivate
```

---

## 🔍 Troubleshooting

### Issue: "ModuleNotFoundError: No module named 'ssz_metric'"

**Solution 1:** Make sure you're in the correct directory
```bash
cd ssz-full-metric
python -c "import sys; print(sys.path)"
```

**Solution 2:** Add to Python path
```python
import sys
sys.path.insert(0, '/path/to/ssz-full-metric')
from ssz_metric import *
```

**Solution 3:** Install in development mode
```bash
pip install -e .
```

### Issue: "ImportError: numpy not found"

**Solution:**
```bash
pip install --upgrade pip
pip install numpy scipy matplotlib mpmath
```

### Issue: Permission denied (Linux/Mac)

**Solution:**
```bash
pip install --user numpy scipy matplotlib mpmath
```

Or use virtual environment (recommended).

### Issue: "SSL Certificate Error"

**Solution:**
```bash
pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org numpy scipy matplotlib mpmath
```

---

## 💻 IDE Setup

### Visual Studio Code

1. Install Python extension
2. Open folder: `File → Open Folder → ssz-full-metric`
3. Select interpreter: `Ctrl+Shift+P → Python: Select Interpreter`
4. Choose your venv or system Python

### PyCharm

1. Open project: `File → Open → ssz-full-metric`
2. Configure interpreter: `File → Settings → Project → Python Interpreter`
3. Add interpreter or use existing

### Jupyter Notebook

```bash
pip install jupyter
jupyter notebook
```

Then create a new notebook and import:
```python
from ssz_metric import *
```

---

## 🚀 Next Steps

After installation:

1. **Read the README**: [README.md](README.md)
2. **Try examples**: See [Usage](#usage) section
3. **Run tests**: Verify everything works
4. **Explore API**: Check [API_REFERENCE.md](API_REFERENCE.md)
5. **Read findings**: [FINDINGS_COMPREHENSIVE_FINAL.md](FINDINGS_COMPREHENSIVE_FINAL.md)

---

## 📚 Additional Resources

- **Documentation**: All `.md` files in repository
- **Examples**: `examples/` directory (if available)
- **Tests**: `tests/` directory - see how to use the package
- **Reports**: 57 comprehensive reports with all findings

---

## 🆘 Getting Help

If you encounter issues:

1. Check this installation guide
2. Search existing GitHub issues
3. Open a new issue with:
   - Your OS and Python version
   - Error message
   - Steps to reproduce
   - What you've tried

---

## ✅ Installation Checklist

- [ ] Python 3.8+ installed
- [ ] Repository cloned or downloaded
- [ ] Dependencies installed
- [ ] Import works: `from ssz_metric import *`
- [ ] Tests pass
- [ ] Examples run

**If all checked: You're ready to explore singularity-free black holes!** 🌌

---

© 2025 Carmen Wrede & Lino Casu
