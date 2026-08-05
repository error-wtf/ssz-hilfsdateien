# Old Bound Energy Files - To Backup Moved

**Datum:** 2025-11-27 02:10  
**Status:** ✅ **ALLE DEPRECATED FILES VERSCHOBEN**

---

## 🎯 **Aufräum-Aktion**

Nach dem Refactoring (Bound Energy → Redshift) waren die alten Files überflüssig.

---

## 📦 **Verschobene Files**

### **Backup Location:**
```
E:\clone\backups\Segmented-Spacetime-Mass-Projection-Unified-Results\2025-11-27_bound_energy_deprecated\
```

### **Python Scripts (DEPRECATED):**
- ❌ `bound_energy_english.py` → Ersetzt durch `redshift_segment_density.py`
- ❌ `bound_energy_plot.py` → Ersetzt durch `redshift_segment_density_plot.py`
- ❌ `bound_energy_plot_with_frequenz_shift_fix.py.DEPRECATED` → Ersetzt durch `redshift_ratio_multi_object_plot_with_deltaM.py`
- ❌ `bound_energy_plot_with_frequenz_shift_fix.py.BACKUP`

### **Old Data Files:**
- ❌ `bound_energy_results.csv.OLD`
- ❌ `bound_energy_clean_objects.csv.OLD`
- ❌ `bound_energy_with_deltaM.csv`
- ❌ `bound_energy_clean_plot.png`

---

## ✅ **Files Die BLEIBEN**

### **Aktiv Verwendet:**
- ✅ **bound_energy.py** - ECHTE Bound Energy (Paper-locked, α·m_bound)
  - Verwendet in: `run_complete_test_suite.py`, `run_all_ssz_terminal.py`, `segspace_all_in_one_extended.py`
  - **Status:** AKTIV, NICHT DEPRECATED

### **Generierte Outputs:**
- ✅ `agent_out/reports/bound_energy.txt` - Generated output
- ✅ `final_reports/agent_out/bound_energy.txt` - Generated output

---

## 🔄 **Neue Files (Ersatz)**

| Alt (DEPRECATED) | Neu (AKTIV) | Zweck |
|------------------|-------------|--------|
| bound_energy_english.py | redshift_segment_density.py | Redshift & Segmentdichte |
| bound_energy_plot.py | redshift_segment_density_plot.py | Multi-Object Redshift Plot |
| bound_energy_plot_with_frequenz_shift_fix.py | redshift_ratio_multi_object_plot_with_deltaM.py | Redshift ratio mit Δ(M) |

---

## 🔧 **Git Actions**

### **Removed from Git Index:**
```bash
git rm --cached bound_energy_english.py
git rm --cached bound_energy_plot.py
git rm --cached bound_energy_plot_with_frequenz_shift_fix.py.DEPRECATED
git rm --cached bound_energy_with_deltaM.csv
git rm --cached bound_energy_clean_plot.png
```

### **NOT Removed (Still Used):**
```bash
# bound_energy.py - KEPT (echte Bound Energy, paper-locked)
```

---

## ⚠️ **WICHTIG: bound_energy.py ≠ bound_energy_english.py**

### **bound_energy.py (AKTIV):**
```python
# ECHTE Bound Energy (Paper-konsistent)
# E_bound = α·m_bound·c²
# Verwendet in: run_complete_test_suite.py, run_all_ssz_terminal.py
# Status: ✅ AKTIV, RICHTIG BENANNT
```

### **bound_energy_english.py (DEPRECATED):**
```python
# FALSCH BENANNT - berechnet KEINE Bound Energy!
# Berechnet nur: Redshift z_gr, Segmentdichte N_seg
# Status: ❌ DEPRECATED, verschoben nach Backup
```

---

## 📊 **Vorher vs. Nachher**

### **Vorher:**
```
Root Directory:
├── bound_energy.py ✅ (echte Bound Energy)
├── bound_energy_english.py ❌ (falsch benannt)
├── bound_energy_plot.py ❌ (falsch benannt)
├── bound_energy_plot_with_frequenz_shift_fix.py.DEPRECATED ❌
├── redshift_segment_density.py ✅
├── redshift_segment_density_plot.py ✅
└── redshift_ratio_multi_object_plot_with_deltaM.py ✅
```

### **Nachher:**
```
Root Directory:
├── bound_energy.py ✅ (echte Bound Energy - KEPT)
├── redshift_segment_density.py ✅
├── redshift_segment_density_plot.py ✅
└── redshift_ratio_multi_object_plot_with_deltaM.py ✅

Backup Location:
└── E:\clone\backups\...\2025-11-27_bound_energy_deprecated\
    ├── bound_energy_english.py
    ├── bound_energy_plot.py
    ├── bound_energy_plot_with_frequenz_shift_fix.py.DEPRECATED
    ├── bound_energy_plot_with_frequenz_shift_fix.py.BACKUP
    ├── bound_energy_results.csv.OLD
    ├── bound_energy_clean_objects.csv.OLD
    ├── bound_energy_with_deltaM.csv
    └── bound_energy_clean_plot.png
```

---

## ✅ **Verification**

### **Check Removal:**
```bash
# Should NOT exist in repo anymore
ls bound_energy_english.py  # File not found
ls bound_energy_plot.py     # File not found

# Should EXIST
ls bound_energy.py           # ✅ Exists
ls redshift_segment_density.py  # ✅ Exists
```

### **Check Backup:**
```bash
ls E:\clone\backups\Segmented-Spacetime-Mass-Projection-Unified-Results\2025-11-27_bound_energy_deprecated\
# Should show all 8 moved files
```

### **Check Git Status:**
```bash
git status
# Should show removed files as deleted
```

---

## 🎉 **Status: AUFGERÄUMT**

```
╔═══════════════════════════════════════════════════════════╗
║                                                           ║
║   ✅ DEPRECATED FILES: VERSCHOBEN                        ║
║   ✅ BACKUP ERSTELLT                                     ║
║   ✅ GIT INDEX UPDATED                                   ║
║   ✅ NEUE FILES: AKTIV                                   ║
║   ✅ bound_energy.py: BEHALTEN                           ║
║                                                           ║
║   STATUS: REPO AUFGERÄUMT & SAUBER                       ║
║                                                           ║
╚═══════════════════════════════════════════════════════════╝
```

**Alle überflüssigen Files sind ins Backup verschoben - Repo ist clean!**

---

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**

**Lizenz:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4
