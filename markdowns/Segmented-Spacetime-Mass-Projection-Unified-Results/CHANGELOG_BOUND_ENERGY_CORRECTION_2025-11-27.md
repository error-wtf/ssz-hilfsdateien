# CHANGELOG: Bound Energy Correction (2025-11-27)

**Datum:** 2025-11-27  
**Typ:** Wissenschaftliche Korrektur + Umbenennung  
**Verantwortlich:** Carmen Wrede & Lino Casu

---

## 🎯 **Zusammenfassung**

Scripts `bound_energy_english.py` und `bound_energy_plot.py` wurden **umbenannt und wissenschaftlich korrekt dokumentiert**, da sie **keine Bound Energy** berechnen, sondern nur **Redshift & Segmentdichte**.

---

## ✅ **Neue Scripts**

### **1. redshift_segment_density.py**
- **Ersetzt:** `bound_energy_english.py`
- **Funktion:** Berechnet Redshift & Segmentdichte (KEIN Bound Energy)
- **CSV-Output:** `redshift_segment_density_results.csv`
- **Änderungen:**
  - ❌ Entfernt: `m_bound`, `alpha_local`, `f_emit_check` (waren irreführend)
  - ✅ Neu: `epsilon_local` (ehrlicher Name für Energieverhältnis)
  - ✅ Klarstellung: Keine Bound Energy, nur Redshift

### **2. redshift_segment_density_plot.py**
- **Ersetzt:** `bound_energy_plot.py`
- **Funktion:** Visualisiert Redshift für mehrere Objekte
- **CSV-Output:** `redshift_segment_density_clean_objects.csv`
- **Änderungen:**
  - ❌ Entfernt: "Back-Calculation Check" (war Tautologie)
  - ✅ Neu: Plot zeigt z_total (Redshift), nicht "Error"
  - ✅ Y-Achse: "Redshift z_total" statt "Relative Error"

---

## 📝 **Neue Dokumentation**

### **1. BOUND_ENERGY_SCRIPTS_CLARIFICATION.md**
- Vollständige Erklärung des Problems
- Migration Guide (Alt → Neu)
- Wissenschaftliche Begründung
- Dateistruktur nach Änderungen

### **2. SCRIPTS_USAGE_UPDATED.md**
- Quick-Reference für alle Scripts
- Vergleichstabelle
- "Welches Script für welchen Zweck?"
- Migration Guide

### **3. WISSENSCHAFTLICHE_KLARSTELLUNG_BOUND_ENERGY.md**
- Wissenschaftliche Definitionen
- Physikalische Interpretation
- Vergleichstabelle: Script-Funktionen
- Referenzen zum Paper

### **4. UPDATE_BOUND_ENERGY_REFERENCES.md**
- Liste aller betroffenen Dateien
- Update-Anweisungen für MD-Dateien
- Priorisierung (Hoch/Mittel/Niedrig)

---

## 🔧 **Pipeline-Updates**

### **1. run_complete_test_suite.py (Zeile 38-40)**
**Alt:**
```python
'bound_energy.py',
'bound_energy_plot.py',
```

**Neu:**
```python
'bound_energy.py',  # ← Paper-locked, echte Bound Energy (mit --selftest testbar)
'redshift_segment_density.py',  # ← Neues Script (Redshift & Segmentdichte, KEIN Bound Energy)
'redshift_segment_density_plot.py',  # ← Neues Script (Multi-Object Redshift Plot)
```

### **2. run_all_ssz_terminal.py (Zeile 285, 739)**
**Kommentare hinzugefügt:**
```python
bound_energy_txt = reports_ain1 / "bound_energy.txt"  # NOTE: bound_energy.py ist echte Bound Energy (Paper-Herleitung)

# NOTE: Dies ist echte Bound Energy aus bound_energy.py (Paper-Herleitung α·m_bound)
```

---

## 📚 **Dokumentations-Updates**

### **Aktualisiert:**
1. ✅ `FINE_STRUCTURE_CONSTANT_SCRIPTS_LISTE.md`
   - Warnung bei alten Scripts (⚠️ DEPRECATED)
   - Neue Scripts dokumentiert
   - Status klargestellt

### **Zu prüfen:**
1. ⚠️ `docs/improvement/FORMULA_CODE_MAPPING.md` (11 Matches)
2. ⚠️ `commands.md` (2 Matches)
3. ⚠️ `Verification Summary of Segmented Spacetime Repository.md` (4 Matches)

---

## 🔄 **Status: Alt vs. Neu**

| Datei/Script | Alt | Neu | Status |
|--------------|-----|-----|--------|
| **bound_energy_english.py** | ❌ Irreführend | ⚠️ DEPRECATED | Nicht löschen, aber warnen |
| **bound_energy_plot.py** | ❌ Irreführend | ⚠️ DEPRECATED | Nicht löschen, aber warnen |
| **redshift_segment_density.py** | - | ✅ Neu erstellt | Production-ready |
| **redshift_segment_density_plot.py** | - | ✅ Neu erstellt | Production-ready |
| **bound_energy.py** | ✅ Korrekt | ✅ Unverändert | Einzige echte Bound Energy |
| **bound_energy_plot_with_frequenz_shift_fix.py** | ✅ OK | ✅ Unverändert | Δm-Korrektur (OK) |

---

## 📊 **Statistische Übersicht**

### **Gefundene Referenzen:**
- **Python-Scripts:** 70 Matches in 29 Dateien
- **Markdown-Dateien:** 184 Matches in 65+ Dateien

### **Updates durchgeführt:**
- ✅ 2 neue Python-Scripts erstellt
- ✅ 4 neue MD-Dokumente erstellt
- ✅ 2 Pipeline-Scripts aktualisiert
- ✅ 1 MD-Dokument aktualisiert (FINE_STRUCTURE_CONSTANT_SCRIPTS_LISTE.md)

### **Verbleibende Aufgaben:**
- ⚠️ ~60 MD-Dateien manuell prüfen (Low Priority: Archive, Generated Reports)
- ⚠️ FORMULA_CODE_MAPPING.md updaten
- ⚠️ commands.md prüfen

---

## 🎓 **Wissenschaftliche Klarstellung**

### **Was ist Bound Energy?**

**Aus dem Paper:**
```
E_bound = α·m_bound·c²

Wobei:
- α wird berechnet aus Segmentdichte Ne
- m_bound wird hergeleitet (NICHT definiert)
- α_local ist modellbasiert (NICHT aus f_obs per Definition)
```

**Implementiert in:** `bound_energy.py` (locked mode)

---

### **Was ist NICHT Bound Energy?**

**Redshift & Segmentdichte:**
```
z_gr = (f_emit - f_obs)/f_obs
N_seg = f_emit/f_obs - N₀
epsilon_local = E_gamma(f_obs)/(m_e·c²)
```

**Implementiert in:** `redshift_segment_density.py`, `redshift_segment_density_plot.py`

---

## ✅ **Validation**

### **Alte Scripts (DEPRECATED):**
- ❌ bound_energy_english.py: "Back-Calculation" war Tautologie (f_obs → alpha_local → f_obs)
- ❌ bound_energy_plot.py: "Error" war eigentlich z_total (Redshift)

### **Neue Scripts:**
- ✅ redshift_segment_density.py: Berechnet ehrlich z_gr, N_seg, epsilon_local
- ✅ redshift_segment_density_plot.py: Zeigt z_total (Redshift), nicht "Error"

### **Unverändert:**
- ✅ bound_energy.py: Rekonstruiert f_emit mit rel. Fehler < 1e-12 (KEINE Tautologie!)

---

## 📖 **Migration Guide**

### **Für User die bound_energy_english.py benutzt haben:**

**Alt:**
```bash
python bound_energy_english.py
# Output: bound_energy_results.csv
```

**Neu:**
```bash
python redshift_segment_density.py
# Output: redshift_segment_density_results.csv
```

**Änderungen:**
- CSV-Spalten: `m_bound_kg`, `alpha_local`, `f_emit_check_Hz` entfernt
- Neu: `epsilon_local` (ehrlicher Name)
- Klarstellung: KEINE Bound Energy!

---

### **Für User die bound_energy_plot.py benutzt haben:**

**Alt:**
```bash
python bound_energy_plot.py
# Output: bound_energy_clean_objects.csv
# Plot: "Back-Calculation Check"
```

**Neu:**
```bash
python redshift_segment_density_plot.py
# Output: redshift_segment_density_clean_objects.csv
# Plot: "Redshift z_total"
```

**Änderungen:**
- Plot: Y-Achse "Relative Error" → "Redshift z_total"
- Titel: "Back-Calculation Check" → "Redshift vs. Objekt"
- CSV-Spalten: Keine m_bound, alpha_local mehr

---

## 🔗 **Referenzen**

### **Paper:**
- "Segmented Spacetime – Bound Energy and the Structural Origin of the Fine-Structure Constant"
- Carmen N. Wrede, Lino P. Casu, Bingsi

### **Neue Dokumentation:**
- BOUND_ENERGY_SCRIPTS_CLARIFICATION.md
- SCRIPTS_USAGE_UPDATED.md
- WISSENSCHAFTLICHE_KLARSTELLUNG_BOUND_ENERGY.md
- UPDATE_BOUND_ENERGY_REFERENCES.md

---

## 📅 **Timeline**

**2025-11-27 00:13 UTC+1:**
- ✅ Problem identifiziert (bound_energy_english.py/plot.py irreführend)
- ✅ Neue Scripts erstellt (redshift_segment_density.py/plot.py)
- ✅ Dokumentation erstellt (4 neue MD-Dateien)
- ✅ Pipeline-Updates (run_complete_test_suite.py, run_all_ssz_terminal.py)
- ✅ FINE_STRUCTURE_CONSTANT_SCRIPTS_LISTE.md aktualisiert

**Nächste Schritte:**
- ⚠️ MD-Dateien manuell prüfen (60+ Dateien)
- ⚠️ FORMULA_CODE_MAPPING.md updaten
- ⚠️ Optional: Alte Scripts zu .DEPRECATED umbenennen

---

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**

**Lizenz:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4
