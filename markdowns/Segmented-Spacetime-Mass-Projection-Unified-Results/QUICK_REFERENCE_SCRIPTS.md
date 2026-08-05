# Quick Reference - Script Overview

**Datum:** 2025-11-27  
**Status:** ✅ Current & Correct

---

## 🔬 **TRUE BOUND ENERGY (Paper Theory)**

### **bound_energy.py**
```bash
python bound_energy.py --selftest
```
**Purpose:** Computes TRUE bound energy as per paper derivation  
**Formula:** E_bound = α·m_bound·c²  
**Output:** `bound_energy.txt`  
**Status:** ✅ **CORRECT - Do NOT rename!**

---

## 📊 **REDSHIFT & SEGMENT DENSITY DIAGNOSTICS**

### **1. redshift_segment_density.py**
```bash
python redshift_segment_density.py
```
**Purpose:** Single object redshift & segment density analysis  
**Old name:** ~~bound_energy_english.py~~ (DEPRECATED)  
**Computes:** z, N_seg, epsilon_local (NOT bound energy!)  
**Status:** ✅ Correctly renamed & refactored

---

### **2. redshift_segment_density_plot.py**
```bash
python redshift_segment_density_plot.py
```
**Purpose:** Multi-object redshift plot  
**Old name:** ~~bound_energy_plot.py~~ (DEPRECATED)  
**Generates:** Comparison plots, CSV outputs  
**Status:** ✅ Correctly renamed & refactored

---

### **3. redshift_ratio_multi_object_plot_with_deltaM.py**
```bash
python redshift_ratio_multi_object_plot_with_deltaM.py
```
**Purpose:** Redshift ratio with φ/2-BLC Δ(M) correction  
**Old name:** ~~bound_energy_plot_with_frequenz_shift_fix.py~~ (DEPRECATED)  
**Features:**
- Computes z_total, z_gr, z_SR decomposition
- Applies φ/2-BLC mass correction
- Generates diagnostic plots

**Output:**
- `redshift_ratio_with_deltaM.csv`
- `redshift_ratio_with_deltaM_plot.png`

**Status:** ✅ Newly refactored & renamed

---

## 🔄 **PIPELINE INTEGRATION**

### **segspace_all_in_one_extended.py**
```bash
# Run TRUE bound energy calculation:
python segspace_all_in_one_extended.py bound-energy
```
**Function:** `workflow_electron_bound_energy_alpha()`  
**Computes:** E = α·m_e·c²  
**Status:** ✅ Correctly renamed (was: workflow_bound_energy)

---

## ⚠️ **DEPRECATED (Backed up, do NOT use)**

- ❌ `bound_energy_english.py.DEPRECATED`
- ❌ `bound_energy_plot.py.DEPRECATED`
- ❌ `bound_energy_plot_with_frequenz_shift_fix.py.DEPRECATED`

**These files are preserved as backups but should NOT be used!**

---

## 📋 **Key Concepts**

### **TRUE Bound Energy:**
```
E_bound = α · m_bound · c²
```
- From paper theoretical derivation
- Implemented in: `bound_energy.py`
- Pipeline function: `workflow_electron_bound_energy_alpha()`

### **Redshift Diagnostics:**
```
z = (f_emit - f_obs) / f_obs
epsilon_local = E_photon / (m_e c²)  [energy ratio, NOT α!]
N_seg ≈ z  [segment density]
```
- Diagnostic tools, NOT bound energy calculations
- Implemented in: `redshift_segment_density*.py`
- Use for: frequency shift analysis, segment density mapping

---

## 🎯 **Which Script to Use?**

| Task | Script | Command |
|------|--------|---------|
| **TRUE Bound Energy** | bound_energy.py | `python bound_energy.py --selftest` |
| **Redshift (single object)** | redshift_segment_density.py | `python redshift_segment_density.py` |
| **Redshift (multi-object plot)** | redshift_segment_density_plot.py | `python redshift_segment_density_plot.py` |
| **Redshift with Δ(M) correction** | redshift_ratio_multi_object_plot_with_deltaM.py | `python redshift_ratio_multi_object_plot_with_deltaM.py` |
| **Pipeline Bound Energy** | segspace_all_in_one_extended.py | `python segspace_all_in_one_extended.py bound-energy` |

---

## ✅ **Validation**

All scripts:
- ✅ Scientifically correctly named
- ✅ Variables clearly labeled
- ✅ Print statements accurate
- ✅ CSV outputs unambiguous
- ✅ Integrated in pipeline
- ✅ Tests passing (23/23)

**System Status: Production Ready! 🚀**

---

**© 2025 Carmen Wrede & Lino Casu**
