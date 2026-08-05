# SSZ Theory Predictions - WSL Setup Guide

**Windows Subsystem for Linux (WSL) Compatibility Guide**

---

## 🐧 Quick Setup (WSL 2)

### **1. Install WSL (if not already installed)**
```powershell
# In PowerShell (Admin)
wsl --install
# Restart computer
```

### **2. Install Ubuntu (recommended)**
```powershell
wsl --install -d Ubuntu-22.04
```

### **3. Update & Install Python**
```bash
# In WSL terminal
sudo apt update
sudo apt install python3 python3-pip python3-venv git -y
```

### **4. Clone Repository**
```bash
# Option A: From Windows drive
cd /mnt/h/WINDSURF/
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Option B: Clone to WSL home
cd ~
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

### **5. Install Dependencies**
```bash
pip3 install numpy pandas scipy matplotlib
```

### **6. Run Platform Check**
```bash
python3 PLATFORM_COMPATIBILITY_CHECK.py
```

**Expected Output:**
```
🌍 Environment Detected: WSL
✅ All checks passed
🎉 FULLY COMPATIBLE WITH WSL!
```

---

## 🧪 Running Tests

### **Quick Test:**
```bash
# Data validation
python3 scripts/tests/test_data_validation.py

# Theory tests (requires data)
python3 run_all_ssz_terminal.py  # Generate data first
python3 scripts/tests/test_horizon_hawking_predictions.py
```

### **Complete Validation:**
```bash
python3 run_complete_validation.py
```

**Expected:**
```
✅ Data Validation: 11/11 PASSED
✅ Theory Predictions: 7/7 PASSED  
✅ Cross-Platform: 4/4 PASSED
🎉 FULLY VALIDATED
```

---

## 🗂️ File Access

### **Windows Drives in WSL:**
```bash
# Access Windows H: drive
cd /mnt/h/

# Access Windows C: drive
cd /mnt/c/Users/YourName/Documents/
```

### **WSL Files from Windows:**
```
# From Windows Explorer
\\wsl$\Ubuntu-22.04\home\youruser\
```

---

## ⚠️ Common Issues & Solutions

### **Issue 1: Line Endings (CRLF vs LF)**

**Problem:**
```bash
./script.py
# bash: ./script.py: /usr/bin/python3^M: bad interpreter
```

**Solution:**
```bash
# Convert CRLF → LF
dos2unix script.py

# Or install dos2unix if not present
sudo apt install dos2unix
```

**Prevention:**
```bash
# Configure git
git config --global core.autocrlf input
```

### **Issue 2: Permissions**

**Problem:**
```bash
python3 script.py
# Permission denied
```

**Solution:**
```bash
chmod +x script.py
# Now you can run:
./script.py
```

### **Issue 3: Python Not Found**

**Problem:**
```bash
python scripts/tests/test_data_validation.py
# python: command not found
```

**Solution:**
```bash
# Use python3 in WSL (not python)
python3 scripts/tests/test_data_validation.py

# Or create alias
echo "alias python=python3" >> ~/.bashrc
source ~/.bashrc
```

### **Issue 4: Missing Dependencies**

**Problem:**
```python
ImportError: No module named 'numpy'
```

**Solution:**
```bash
# Install for current user
pip3 install --user numpy pandas scipy matplotlib

# Or system-wide (requires sudo)
sudo pip3 install numpy pandas scipy matplotlib
```

---

## 🔧 WSL-Specific Features

### **Performance:**
- ✅ **Faster I/O** than Windows on Linux files
- ✅ **Native Unix tools** (grep, sed, awk)
- ✅ **Better multi-threading** for Python

### **Recommendations:**
```bash
# Keep repo in WSL filesystem for best performance
~/Segmented-Spacetime-Mass-Projection-Unified-Results/

# Not on Windows drives:
# /mnt/h/... (slower I/O)
```

---

## 📊 Benchmark (WSL vs Windows)

**Test:** `python run_all_ssz_terminal.py`

| Platform | Time | Notes |
|----------|------|-------|
| **Windows Native** | ~10 min | UTF-8 auto-config needed |
| **WSL 2** | ~8 min | Native Unix, faster I/O |
| **Linux (Native)** | ~7 min | Best performance |

---

## 🚀 Advanced: Virtual Environment

**Recommended for isolation:**

```bash
# Create venv
python3 -m venv SSZ-env

# Activate
source SSZ-env/bin/activate

# Install dependencies
pip install numpy pandas scipy matplotlib

# Run tests
python scripts/tests/test_data_validation.py

# Deactivate when done
deactivate
```

---

## ✅ Validation Checklist (WSL)

### **Before Running Tests:**
- [ ] WSL 2 installed (`wsl --status`)
- [ ] Ubuntu or compatible distro
- [ ] Python 3.8+ (`python3 --version`)
- [ ] Dependencies installed (`pip3 list`)
- [ ] Repository cloned
- [ ] File permissions correct (`chmod +x *.py` if needed)

### **Run Platform Check:**
```bash
python3 PLATFORM_COMPATIBILITY_CHECK.py
```

**Must show:**
```
🌍 Environment Detected: WSL
✅ All 9 checks PASSED
```

### **Run Complete Validation:**
```bash
python3 run_complete_validation.py
```

**Must generate:**
```
reports/VALIDATION_CERTIFICATE.md
```

---

## 🔍 Debugging

### **Check WSL Version:**
```powershell
# In PowerShell
wsl --version
# Should show: WSL version: 2.x.x
```

### **Check Linux Distribution:**
```bash
# In WSL
cat /etc/os-release
# Should show: Ubuntu 22.04 (or similar)
```

### **Check Python:**
```bash
python3 --version  # Should be 3.8+
which python3      # Should be /usr/bin/python3
```

### **Check Dependencies:**
```bash
python3 -c "import numpy, pandas, scipy, matplotlib; print('All OK')"
```

---

## 📝 Integration with Windows Tools

### **VS Code:**
```bash
# Install VS Code in Windows
# Install WSL extension in VS Code
# Open folder in WSL:
code .
```

### **Git:**
```bash
# Use WSL git (recommended)
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

### **Jupyter:**
```bash
# Install in WSL
pip3 install jupyter

# Run notebook
jupyter notebook --no-browser

# Copy URL to Windows browser
```

---

## 🎯 Quick Commands Summary

```bash
# Setup (one-time)
sudo apt update && sudo apt install python3 python3-pip git -y
pip3 install numpy pandas scipy matplotlib

# Clone & Test
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
python3 PLATFORM_COMPATIBILITY_CHECK.py

# Run Complete Validation
python3 run_complete_validation.py

# Generate Data
python3 run_all_ssz_terminal.py

# Run Theory Tests
python3 scripts/tests/test_horizon_hawking_predictions.py
```

---

## 📚 Additional Resources

**WSL Documentation:**
- https://docs.microsoft.com/en-us/windows/wsl/

**Ubuntu on WSL:**
- https://ubuntu.com/wsl

**Python in WSL:**
- https://docs.python.org/3/using/windows.html#wsl

---

## 🎉 Success Indicators

**WSL is working correctly when:**
- ✅ `python3 PLATFORM_COMPATIBILITY_CHECK.py` → All PASSED
- ✅ `python3 run_complete_validation.py` → Certificate generated
- ✅ UTF-8 characters display correctly (φβγακ ✅❌⚠️)
- ✅ No "bad interpreter" errors
- ✅ No permission denied errors
- ✅ Tests run faster than Windows

---

**© 2025 Carmen Wrede, Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Version:** 1.0.0  
**Last Updated:** 2025-10-19  
**Status:** ✅ WSL FULLY SUPPORTED
