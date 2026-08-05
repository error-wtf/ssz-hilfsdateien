# Virtual Environment Usage

## ⚠️ Important: Always Activate the Virtual Environment

After running `install.sh` or `install.ps1`, all Python packages (including `pyarrow`, `pytest`, etc.) are installed **inside the virtual environment** (`.venv/`).

If you run tests or scripts **without activating** the virtual environment, you'll get errors like:

```
ImportError: No module named 'pyarrow'
ImportError: Unable to find a usable engine for parquet support
```

---

## 🐧 Linux / WSL / macOS

### Activate the virtual environment:
```bash
source .venv/bin/activate
```

### Check if venv is active:
```bash
source check_venv.sh
# or check manually:
echo $VIRTUAL_ENV
```

### Run tests (with venv active):
```bash
pytest scripts/tests/test_ssz_invariants.py -v
python test_ppn_exact.py
```

### Deactivate when done:
```bash
deactivate
```

---

## 🪟 Windows (PowerShell)

### Activate the virtual environment:
```powershell
.\.venv\Scripts\Activate.ps1
```

### Check if venv is active:
```powershell
.\check_venv.ps1
# or check manually:
$env:VIRTUAL_ENV
```

### Run tests (with venv active):
```powershell
pytest scripts/tests/test_ssz_invariants.py -v
python test_ppn_exact.py
```

### Deactivate when done:
```powershell
deactivate
```

---

## 🔍 How to Tell if venv is Active

### Visual indicators:
- **Prompt changes:** `(.venv) user@host:~/project$`
- **Environment variable:** `$VIRTUAL_ENV` or `$env:VIRTUAL_ENV` is set
- **Python location:** `which python` points to `.venv/bin/python`

### Using check scripts:
```bash
# Linux/WSL/macOS
source check_venv.sh

# Windows
.\check_venv.ps1
```

---

## ❌ Common Mistakes

### Running tests without venv:
```bash
# ❌ WRONG - system Python, no packages
python test_ppn_exact.py

# ✅ CORRECT - activate first
source .venv/bin/activate
python test_ppn_exact.py
```

### Using system pytest:
```bash
# ❌ WRONG - /usr/bin/pytest (system)
pytest scripts/tests/test_ssz_invariants.py

# ✅ CORRECT - .venv/bin/pytest
source .venv/bin/activate
pytest scripts/tests/test_ssz_invariants.py
```

---

## 📦 What's Installed in the venv?

All packages from `requirements.txt`:
- **Core:** numpy, scipy, pandas, matplotlib
- **Astronomy:** astropy, astroquery
- **Data:** pyarrow (for Parquet files)
- **Testing:** pytest, pytest-timeout
- **Visualization:** plotly, kaleido
- **Config:** pyyaml

---

## 🚀 Quick Reference

| Task | Linux/WSL/macOS | Windows |
|------|-----------------|---------|
| **Activate** | `source .venv/bin/activate` | `.\.venv\Scripts\Activate.ps1` |
| **Check** | `source check_venv.sh` | `.\check_venv.ps1` |
| **Deactivate** | `deactivate` | `deactivate` |

---

## 💡 Tips

1. **Always activate before running tests**
2. **Your terminal prompt will show `(.venv)` when active**
3. **Use the check scripts if unsure**
4. **Reactivate after opening a new terminal**

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
