# Complete Refactoring Plan - Bound Energy Mislabeling Fix

**Date:** 2025-11-27  
**Type:** Pure naming/documentation refactor (NO math/physics changes)  
**Status:** ✅ Already partially complete, now finishing

---

## 🎯 **Scope**

Fix mislabeling of DIAGNOSTIC scripts that compute:
- Gravitational redshift z
- Segment density N_seg
- Energy ratios (photon energy / electron rest energy)

These are NOT bound-energy solvers!

---

## ✅ **Already Completed (Previous Session)**

### **Scripts Renamed:**
1. ✅ `bound_energy_english.py` → `redshift_segment_density.py`
2. ✅ `bound_energy_plot.py` → `redshift_segment_density_plot.py`

### **Documentation Created:**
- ✅ `BOUND_ENERGY_SCRIPTS_CLARIFICATION.md`
- ✅ `WISSENSCHAFTLICHE_KLARSTELLUNG_BOUND_ENERGY.md`
- ✅ `WORKFLOW_UMBENENNUNG_2025-11-27.md`

---

## 📋 **Still To Do**

### **A. Remaining Files to Rename:**

1. **`bound_energy_plot_with_frequenz_shift_fix.py`**
   - → `redshift_ratio_multi_object_plot_with_deltaM.py`
   - This is a diagnostic script with Δ(M) correction

2. **CSV Files:**
   - `bound_energy_results.csv` → `redshift_ratio_results.csv`
   - `bound_energy_clean_objects.csv` → `redshift_ratio_clean_objects.csv`
   - `bound_energy_with_deltaM.csv` → `redshift_ratio_with_deltaM.csv`

3. **PNG Files:**
   - `bound_energy_clean_plot.png` → `redshift_ratio_clean_plot.png`

### **B. Variables/Functions to Rename in Diagnostic Scripts:**

**In `bound_energy_plot_with_frequenz_shift_fix.py` (to be renamed):**
1. `alpha_local` → `epsilon_local`
2. `compute_local_alpha` → `compute_local_energy_ratio`
3. `compute_local_alpha_from_obs` → `compute_energy_ratio_from_obs`
4. `m_bound` → `m_eff`
5. `compute_bound_mass` → `compute_effective_mass_after_emission`
6. `f_emit_check` → `f_from_epsilon`
7. `rel_error` → `rel_freq_diff`

### **C. CSV Column Names:**
- `alpha_local` → `epsilon_local`
- `m_bound_kg` → `m_eff_kg`
- `rel_error_f_emit` → `rel_freq_diff`

### **D. Print Statements/Banners:**
- "BOUND ENERGY" → "REDSHIFT RATIO & SEGMENT DENSITY"
- "local alpha" → "local energy ratio epsilon"
- "Back calculation" → "Diagnostic frequency comparison"

---

## ⚠️ **DO NOT CHANGE**

1. ✅ `bound_energy.py` (core theory script - this is correct!)
2. ✅ `bound_energy.txt` (output from core theory - correct!)
3. ✅ Mathematical formulas and constants
4. ✅ Numerical algorithms
5. ✅ Core theory implementation

---

## 🔄 **Execution Order**

1. Rename `bound_energy_plot_with_frequenz_shift_fix.py` + refactor its content
2. Rename CSV/PNG files
3. Update all references in documentation
4. Update imports/references in other scripts
5. Verify no broken references

---

**© 2025 Carmen Wrede & Lino Casu**
