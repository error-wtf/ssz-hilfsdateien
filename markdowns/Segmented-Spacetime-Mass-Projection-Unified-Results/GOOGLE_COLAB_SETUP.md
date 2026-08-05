# Google Colab Setup - Segmented Spacetime Repository

Complete guide for cloning and using the repository in Google Colab.

---

## 🚀 Quick Start - Copy & Paste in Colab

### **Option 1: Small files only (tests work immediately)**

```python
# Clone repository (small files only, ~36 MB)
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Install dependencies
!pip install -q -r requirements.txt

# Run tests (with v1/nightly datasets)
!python run_full_suite.py
```

### **Option 2: With large files (complete datasets)**

```python
# Install Git LFS
!apt-get install -y git-lfs
!git lfs install

# Clone repository
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Download large files (~3.6 GB!)
!git lfs pull

# Install dependencies
!pip install -q -r requirements.txt

# Run all tests (including real-data)
!python run_full_suite.py
```

---

## 📋 Step-by-Step Guide

### **1. Create New Colab Notebook**

Go to [Google Colab](https://colab.research.google.com/) and create a new notebook.

### **2. Define Repository Variables**

```python
# Repository configuration
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"

print(f"📦 Repository: {REPO_NAME}")
print(f"🔗 URL: {REPO_URL}")
```

### **3. Prepare Workspace**

```python
import os
from pathlib import Path

# Check if repository already exists
if Path(REPO_NAME).exists():
    print(f"⚠️  Repository already exists: {REPO_NAME}")
    print(f"🔄 Pulling latest changes...")
    !cd {REPO_NAME} && git pull
else:
    print(f"📥 Cloning repository: {REPO_URL}")
```

### **4. Clone Repository**

#### **Option A: Shallow Clone (fast, no history)**

```python
# Fast clone without history
!git clone --depth 1 {REPO_URL} {REPO_NAME}
print(f"✅ Repository cloned!")
```

#### **Option B: Full Clone (with complete history)**

```python
# Complete clone with history
!git clone {REPO_URL} {REPO_NAME}
print(f"✅ Repository cloned!")
```

### **5. Change to Repository Directory**

```python
# Change working directory
os.chdir(REPO_NAME)
print(f"📂 Working Directory: {os.getcwd()}")
```

### **6. Git LFS Setup (optional, for large files)**

```python
# Install Git LFS (if large files are needed)
!apt-get install -y git-lfs
!git lfs install

# Download large files (~3.6 GB)
!git lfs pull

print(f"✅ Git LFS setup completed!")
print(f"⚠️  Download size: ~3.6 GB")
```

### **7. Install Dependencies**

```python
# Install Python packages
!pip install -q -r requirements.txt

# Additional packages (if needed)
!pip install -q numpy scipy pandas matplotlib astropy pyarrow pytest

print(f"✅ Dependencies installed!")
```

### **8. Check File Availability**

```python
# Check which files are available
import subprocess

def check_file_size(filepath):
    """Check file size in MB"""
    try:
        size = Path(filepath).stat().st_size / (1024 * 1024)
        return size
    except:
        return None

# Small files (should be immediately available)
small_files = [
    "models/cosmology/2025-10-17_gaia_ssz_v1/ssz_field.parquet",
    "models/cosmology/2025-10-17_gaia_ssz_nightly/ssz_field.parquet",
]

print("\n📄 SMALL FILES (immediately available):")
for f in small_files:
    size = check_file_size(f)
    if size:
        print(f"  ✅ {f} - {size:.2f} MB")
    else:
        print(f"  ❌ {f} - MISSING!")

# Large files (only after git lfs pull)
large_files = [
    "models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet",
]

print("\n📦 LARGE FILES (after 'git lfs pull'):")
for f in large_files:
    size = check_file_size(f)
    if size and size > 100:
        print(f"  ✅ {f} - {size:.2f} MB (Complete)")
    elif size and size < 1:
        print(f"  ⚡ {f} - {size*1024:.2f} KB (LFS pointer)")
    else:
        print(f"  ❌ {f} - MISSING!")
```

### **9. Run Tests**

```python
# All tests (with available files)
!python run_full_suite.py

# Or individual tests
!pytest tests/ -v -s

# Only tests with small datasets
!pytest tests/ -v -s -k "not real"
```

---

## 🎯 Complete Setup Script

Copy this entire code block into a Colab cell:

```python
import os
from pathlib import Path

# ============================================================================
# CONFIGURATION
# ============================================================================
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"
INSTALL_LFS = False  # True for large files (~3.6 GB), False for small files only

print("="*80)
print("Segmented Spacetime - GOOGLE COLAB SETUP")
print("="*80)
print(f"Repository: {REPO_NAME}")
print(f"Git LFS: {'Yes (large files)' if INSTALL_LFS else 'No (small files only)'}")
print("="*80)

# ============================================================================
# 1. CLONE REPOSITORY
# ============================================================================
if Path(REPO_NAME).exists():
    print(f"\n⚠️  Repository already exists!")
    print(f"🔄 Pulling updates...")
    os.chdir(REPO_NAME)
    !git pull
else:
    print(f"\n📥 Cloning repository...")
    !git clone --depth 1 {REPO_URL} {REPO_NAME}
    os.chdir(REPO_NAME)
    print(f"✅ Repository cloned!")

# ============================================================================
# 2. GIT LFS SETUP (optional)
# ============================================================================
if INSTALL_LFS:
    print(f"\n📦 Installing Git LFS...")
    !apt-get install -y git-lfs > /dev/null 2>&1
    !git lfs install
    print(f"⬇️  Downloading large files (~3.6 GB)...")
    !git lfs pull
    print(f"✅ Git LFS setup completed!")
else:
    print(f"\n⚡ Skipping Git LFS - small files only")

# ============================================================================
# 3. INSTALL DEPENDENCIES
# ============================================================================
print(f"\n📦 Installing Python packages...")
!pip install -q -r requirements.txt
print(f"✅ Dependencies installed!")

# ============================================================================
# 4. CHECK FILES
# ============================================================================
print(f"\n📄 Available files:")

small_test = "models/cosmology/2025-10-17_gaia_ssz_v1/ssz_field.parquet"
large_test = "models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet"

def check_size(f):
    try:
        return Path(f).stat().st_size / (1024 * 1024)
    except:
        return None

small_size = check_size(small_test)
large_size = check_size(large_test)

if small_size:
    print(f"  ✅ Small files: {small_size:.2f} MB (v1/nightly)")
else:
    print(f"  ❌ Small files: MISSING!")

if large_size and large_size > 100:
    print(f"  ✅ Large files: {large_size:.2f} MB (real-data)")
elif large_size and large_size < 1:
    print(f"  ⚡ Large files: {large_size*1024:.2f} KB (LFS pointer)")
else:
    print(f"  ❌ Large files: MISSING!")

# ============================================================================
# 5. READY!
# ============================================================================
print("\n" + "="*80)
print("✅ SETUP COMPLETED!")
print("="*80)
print(f"Working Directory: {os.getcwd()}")
print(f"\n🚀 Next steps:")
print(f"   • Run tests: !python run_full_suite.py")
print(f"   • Pytest: !pytest tests/ -v -s")
print(f"   • Small datasets only: !pytest tests/ -v -s -k 'not real'")
print("="*80)
```

---

## 🔧 Troubleshooting

### **Problem: "NameError: name 'REPO_NAME' is not defined"**

**Solution:** Define variables BEFORE cloning:

```python
# FIRST run these lines:
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"

# THEN clone:
!git clone --depth 1 {REPO_URL} {REPO_NAME}
```

### **Problem: "fatal: destination path '...' already exists"**

**Solution:** Repository exists, either delete or pull:

```python
# Option 1: Delete and clone fresh
!rm -rf Segmented-Spacetime-Mass-Projection-Unified-Results
!git clone --depth 1 {REPO_URL}

# Option 2: Pull updates
%cd Segmented-Spacetime-Mass-Projection-Unified-Results
!git pull
```

### **Problem: "FileNotFoundError" during tests**

**Cause:** Large files were not downloaded

**Solution:**

```python
# Either install Git LFS and pull:
!apt-get install -y git-lfs
!git lfs install
!git lfs pull

# Or run tests with small files only:
!pytest tests/ -v -s -k "not real"
```

### **Problem: "Out of Memory" with large files**

**Cause:** Colab has limited RAM (~12 GB)

**Solution:**

```python
# Work with small files only (v1/nightly)
# Do NOT download large real-data files with git lfs pull
# Use smaller test datasets instead
```

---

## 💡 Best Practices for Colab

### **1. Modular Setup**

Split your notebook into cells:

```python
# Cell 1: Define variables
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"
```

```python
# Cell 2: Clone
!git clone --depth 1 {REPO_URL} {REPO_NAME}
%cd {REPO_NAME}
```

```python
# Cell 3: Dependencies
!pip install -q -r requirements.txt
```

```python
# Cell 4: Tests
!python run_full_suite.py
```

### **2. Reconnect-Safety**

Colab can disconnect. Save progress:

```python
# Check if already cloned at start
from pathlib import Path

if not Path("Segmented-Spacetime-Mass-Projection-Unified-Results").exists():
    !git clone --depth 1 {REPO_URL}
else:
    print("✅ Repository already present")

%cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

### **3. Drive Integration (optional)**

Save large files to Google Drive:

```python
from google.colab import drive
drive.mount('/content/drive')

# Clone to Drive (persistent!)
!git clone {REPO_URL} /content/drive/MyDrive/SSZ-repo
%cd /content/drive/MyDrive/SSZ-repo
```

---

## 📊 Resource Overview

| Setup | Download | RAM | Time | Tests |
|-------|----------|-----|------|-------|
| Small files only | ~36 MB | ~2 GB | ~2 min | v1, nightly ✅ |
| With Git LFS | ~3.6 GB | ~8 GB | ~15 min | All ✅ |
| Drive integration | ~3.6 GB | ~4 GB | ~20 min | All ✅ (persistent) |

---

## 🎓 Example Notebooks

### **Minimal Setup:**

```python
# 1. Clone (small files only)
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# 2. Install
!pip install -q -r requirements.txt

# 3. Test
!pytest tests/ -v -s -k "not real"
```

### **Full Setup:**

```python
# 1. Git LFS
!apt-get install -y git-lfs
!git lfs install

# 2. Clone
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# 3. LFS Pull
!git lfs pull

# 4. Install
!pip install -q -r requirements.txt

# 5. Full Test
!python run_full_suite.py
```

---

## ✅ Summary

**For quick tests (recommended):**
- Clone without Git LFS
- Small files only (~36 MB)
- Tests with v1/nightly datasets
- Works immediately in Colab

**For complete analysis:**
- Install Git LFS
- Load all files (~3.6 GB)
- Tests with real-data
- Requires more time & RAM

---

## 📚 Repository Documentation

For more details, see:
- **README.md** - Main documentation
- **README_CLONE_TEST.md** - Clone and test guide
- **GIT_HYBRID_STRATEGY.md** - Technical details of the Git LFS strategy
- **verify_lfs_setup.py** - Local verification script

---

## 🎯 What's Available

### **Immediately after clone (small files, <100 MB):**

#### Models:
```
models/cosmology/2025-10-17_gaia_ssz_v1/ssz_field.parquet         (0.14 MB)
models/cosmology/2025-10-17_gaia_ssz_nightly/ssz_field.parquet    (14.25 MB)
models/solar_system/2025-10-17_gaia_ssz_v1/solar_ssz.json         (0.06 MB)
models/solar_system/2025-10-17_gaia_ssz_nightly/solar_ssz.json    (0.25 MB)
```

#### Data:
```
data/interim/gaia/2025-10-17_gaia_ssz_v1/gaia_clean.parquet       (0.08 MB)
data/interim/gaia/2025-10-17_gaia_ssz_nightly/gaia_clean.parquet  (6.09 MB)
data/raw/gaia/2025-10-17_gaia_ssz_nightly/gaia_dr3_core.parquet   (3.32 MB)
data/raw/sdss/2025-10-17_gaia_ssz_nightly/sdss_catalog.parquet    (0.36 MB)
... and more ...
```

**Total: ~36 MB immediately available**

### **Optional via `git lfs pull` (large files, >100 MB):**

```
models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet       (1373 MB)
models/solar_system/2025-10-17_gaia_ssz_real/solar_ssz.json       (128 MB)
data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_clean.parquet     (757 MB)
data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_phase_space.parquet (1169 MB)
... and more ...
```

**Total: ~3.6 GB optionally downloadable**

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
