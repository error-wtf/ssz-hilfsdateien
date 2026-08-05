# Update: Bound Energy References in Dokumentation

**Datum:** 2025-11-27  
**Status:** Klarstellung der Script-Funktionen

---

## 🎯 **Ziel**

Alle Referenzen zu `bound_energy_english.py` und `bound_energy_plot.py` in der Dokumentation aktualisieren mit wissenschaftlich korrekter Beschreibung.

---

## ✅ **Wissenschaftlich korrekte Darstellung**

### **1. bound_energy.py** (unverändert)
**Status:** ✅ **Korrekt** – Berechnet echte Bound Energy gemäß Paper

**Beschreibung:**
```
bound_energy.py implementiert die vollständige Paper-Herleitung der Bound Energy:
- α·m_bound = (h·f_obs·N')/(N₀·c²)
- m_bound = (α·m_bound)/α_fs  
- α_local = E_emit/(m_bound·c²)
- f_emit rekonstruiert mit rel. Fehler < 1e-12

Dies ist die EINZIGE echte Bound-Energy-Implementierung im Repository.
```

---

### **2. bound_energy_english.py** (DEPRECATED)
**Status:** ⚠️ **Irreführend benannt** – Berechnet KEINE Bound Energy

**Was es wirklich macht:**
```
bound_energy_english.py berechnet:
- Redshift z_gr = (f_emit - f_obs)/f_obs
- Segmentdichte N_seg = f_emit/f_obs - N₀
- Energieverhältnis epsilon_local = E_gamma(f_obs)/(m_e·c²)

NICHT berechnet:
- Bound Energy im Paper-Sinn
- Lokale Feinstrukturkonstante (alpha_local ist nur epsilon_local)
- Gebundene Elektronenmasse (m_bound ist Artefakt)
```

**Ersetzt durch:** `redshift_segment_density.py`

---

### **3. bound_energy_plot.py** (DEPRECATED)
**Status:** ⚠️ **Irreführend benannt** – Berechnet KEINE Bound Energy

**Was es wirklich macht:**
```
bound_energy_plot.py berechnet:
- z_total = f_emit/f_obs - 1 (Redshift)
- N_seg (Segmentdichte)
- "Back-Calculation Check" ist Tautologie (f_obs → alpha_local → f_obs)

Der Plot zeigt NICHT den "Error" der Bound Energy,
sondern nur den Redshift z_total.
```

**Ersetzt durch:** `redshift_segment_density_plot.py`

---

### **4. bound_energy_plot_with_frequenz_shift_fix.py** (OK)
**Status:** ✅ **Korrekt** – Berechnet Δm-Korrektur (näher an Bound Energy)

**Beschreibung:**
```
bound_energy_plot_with_frequenz_shift_fix.py berechnet:
- Δm = (φ/2)·N_seg (Golden Ratio Massenkorrektur)
- φ/2-BLC (Bound Length Correction)

Dies ist näher an "Bound Energy" als die beiden anderen Scripts.
Optional umbenennen zu: delta_m_phi2_BLC.py
```

---

## 📝 **Update-Anweisungen für Dokumentation**

### **In allen MD-Dateien ersetzen:**

#### **Alt (Falsch):**
```markdown
bound_energy_english.py berechnet die Bound Energy für verschiedene Objekte...
```

#### **Neu (Korrekt):**
```markdown
redshift_segment_density.py berechnet Redshift & Segmentdichte (NICHT Bound Energy):
- z_gr = (f_emit - f_obs)/f_obs (GR-Redshift)
- N_seg = f_emit/f_obs - N₀ (Segmentdichte)
- epsilon_local = E_gamma(f_obs)/(m_e·c²) (Energieverhältnis, KEIN Alpha!)

Für echte Bound Energy siehe: bound_energy.py (Paper-locked mode)
```

---

#### **Alt (Falsch):**
```markdown
bound_energy_plot.py validiert die Bound Energy durch Back-Calculation...
```

#### **Neu (Korrekt):**
```markdown
redshift_segment_density_plot.py visualisiert den Redshift für mehrere Objekte:
- Plot: z_total = f_emit/f_obs - 1 (Redshift pro Objekt)
- KEIN "Back-Calculation Error" (war Tautologie)

Für echte Bound Energy siehe: bound_energy.py (Paper-locked mode)
```

---

## 🔍 **Betroffene Dateien (automatisch gefunden)**

### **Python-Scripts (70 Matches):**
- run_complete_test_suite.py → ✅ **AKTUALISIERT**
- run_all_ssz_terminal.py → ✅ **AKTUALISIERT** (Kommentare hinzugefügt)
- segspace_all_in_one.py
- segspace_all_in_one_extended.py
- ci/summary-all-tests.py

### **Markdown-Dateien (184 Matches):**
- ✅ BOUND_ENERGY_SCRIPTS_CLARIFICATION.md (NEU)
- ✅ SCRIPTS_USAGE_UPDATED.md (NEU)
- ✅ FINE_STRUCTURE_CONSTANT_SCRIPTS_LISTE.md (AKTUALISIERT)
- docs/improvement/FORMULA_CODE_MAPPING.md → **MANUELL PRÜFEN**
- README.md → **KEINE REFERENZEN** (bereits geprüft)
- Weitere 60+ MD-Dateien

---

## 📊 **Kategorisierung der Referenzen**

| Kategorie | Status | Aktion |
|-----------|--------|--------|
| **bound_energy.py Referenzen** | ✅ Korrekt | Kommentar hinzufügen: "echte Bound Energy" |
| **bound_energy_english.py Referenzen** | ❌ Irreführend | Ersetzen durch redshift_segment_density.py |
| **bound_energy_plot.py Referenzen** | ❌ Irreführend | Ersetzen durch redshift_segment_density_plot.py |
| **bound_energy_plot_with_frequenz_shift_fix.py** | ✅ OK | Optional umbenennen zu delta_m_phi2_BLC.py |

---

## 🎯 **Priorisierung**

### **Hohe Priorität (User-facing Docs):**
1. ✅ README.md → Keine Referenzen gefunden
2. ⚠️ FORMULA_CODE_MAPPING.md → Manuell prüfen
3. ⚠️ commands.md → Manuell prüfen
4. ⚠️ FAQ.md → Prüfen ob Referenzen existieren

### **Mittlere Priorität (Generated Reports):**
- Verification Summary of Segmented Spacetime Repository.md
- output.md, output-summary.md
- Segmentierte Raumzeit – Ein geometrisch-topologisches Modell.md

### **Niedrige Priorität (Archive/Backups):**
- archive/v1.3.0/README_OLD_BACKUP.md
- temp_test_clone/
- validation_complete/
- imports/2025-10-17_upload_missing/

---

## ✅ **Bereits durchgeführte Updates**

1. ✅ `redshift_segment_density.py` erstellt
2. ✅ `redshift_segment_density_plot.py` erstellt
3. ✅ `BOUND_ENERGY_SCRIPTS_CLARIFICATION.md` erstellt
4. ✅ `SCRIPTS_USAGE_UPDATED.md` erstellt
5. ✅ `FINE_STRUCTURE_CONSTANT_SCRIPTS_LISTE.md` aktualisiert
6. ✅ `run_complete_test_suite.py` aktualisiert
7. ✅ `run_all_ssz_terminal.py` Kommentare hinzugefügt

---

## 📝 **Nächste Schritte**

### **Manuell zu prüfen:**
1. `docs/improvement/FORMULA_CODE_MAPPING.md` → Referenzen updaten
2. `commands.md` → Prüfen ob bound_energy Commands existieren
3. `Verification Summary` Dateien → Prüfen ob Update nötig

### **Optional (Low Priority):**
- Archive-Dateien (können alte Referenzen behalten)
- temp_test_clone/ (Testverzeichnis)
- validation_complete/ (Generated reports)

---

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**
