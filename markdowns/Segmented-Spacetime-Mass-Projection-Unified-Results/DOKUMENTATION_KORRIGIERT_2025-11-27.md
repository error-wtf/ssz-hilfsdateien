# Dokumentation korrigiert (2025-11-27)

**Datum:** 2025-11-27  
**Typ:** Wissenschaftliche Korrektur der Bound Energy Referenzen  
**Status:** ✅ Hauptdateien korrigiert

---

## ✅ **Korrigierte Dateien**

### **1. commands.md**
**Änderungen:**
- ✅ Zeile 105: NOTE hinzugefügt zur Klarstellung dass `segspace_all_in_one.py bound-energy` **echte Bound Energy** berechnet
- ✅ Zeile 547-548: NOTE hinzugefügt dass `bound_energy.txt` echte Bound Energy enthält (α·m_bound)
- ✅ Warnung vor Verwechslung mit DEPRECATED Scripts

**Diff:**
```markdown
**NOTE (2025-11-27):** Der `bound-energy` Workflow in `segspace_all_in_one.py` berechnet 
**echte Bound Energy** gemäß Paper-Herleitung (α·m_bound). Dies ist NICHT zu verwechseln 
mit den DEPRECATED Scripts `bound_energy_english.py` und `bound_energy_plot.py`, 
welche nur Redshift & Segmentdichte berechnen.
```

---

### **2. Verification Summary of Segmented Spacetime Repository.md**
**Änderungen:**
- ✅ Zeile 247-250: NOTE hinzugefügt dass `bound_energy_english.py` umbenannt wurde zu `redshift_segment_density.py`
- ✅ Zeile 518-522: Klarstellung dass das Script KEINE echte Bound Energy berechnet
- ✅ Zeile 754-758: Warnung im Referenz-Abschnitt

**Diff:**
```markdown
**NOTE (2025-11-27):** Das Script bound_energy_english.py wurde umbenannt zu 
redshift_segment_density.py, da es KEINE echte Bound Energy berechnet, sondern nur 
Redshift & Segmentdichte. Für echte Bound Energy siehe bound_energy.py (Paper-locked mode).
```

---

### **3. run_complete_test_suite.py (Pipeline)**
**Änderungen:**
- ✅ Zeile 38-40: CLI_TOOLS Liste aktualisiert
- ✅ Kommentare hinzugefügt: `bound_energy.py` = echte Bound Energy
- ✅ Neue Scripts: `redshift_segment_density.py`, `redshift_segment_density_plot.py`

---

### **4. run_all_ssz_terminal.py (Pipeline)**
**Änderungen:**
- ✅ Zeile 285: Kommentar hinzugefügt dass `bound_energy.txt` von `bound_energy.py` kommt (echte Bound Energy)
- ✅ Zeile 739: Kommentar hinzugefügt zur Paper-Herleitung

---

## 📋 **Noch zu prüfende Dateien (Low Priority)**

### **Archive-Dateien (60+ Matches):**
- `archive/v1.3.0/README_OLD_BACKUP.md`
- `temp_test_clone/`
- `validation_complete/`
- `validation_complete_extended/`
- `imports/2025-10-17_upload_missing/`

**Status:** ⚠️ Können alte Referenzen behalten (Archive)

---

### **Generated Reports:**
- `output.md`
- `output-summary.md`
- `reports/full-output.md`

**Status:** ⚠️ Werden bei nächstem Run neu generiert

---

## 🎯 **Wissenschaftlich korrekte Darstellung**

### **Das Paper (SegmentedSpacetimeBoundEnergyandtheStructuralOriginofthefine-structureconstant.md)**

**Status:** ✅ **Unverändert** – Das Paper beschreibt die ECHTE Bound Energy Theorie

**Zentrale Aussage (Zeile 40-57):**
```
"Instead of explaining the shift through Doppler effects or gravitational redshift via metric expansion, 
we show that it can be derived from the internal structure of the electron itself. In our model, 
spacetime is not continuous but discretely segmented. This segmentation limits how much of an 
electron's rest energy is electromagnetically accessible. The accessible fraction corresponds to 
the local value of the fine-structure constant α, which varies depending on the segmentation 
density of space."
```

**Formeln im Paper:**
1. `r = φ/Ne` (effektiver Radius für gebundene Elektronen)
2. `E_el = (e²·Ne)/(4πε₀·φ)` (Elektromagnetische Selbstenergie)
3. `α = (e²·Ne)/(4πε₀·φ·m_bound·c²)` (Feinstrukturkonstante)
4. `E_bound = α·m_bound·c²` (Gebundene Energie)

**Diese Formeln sind RICHTIG und werden in `bound_energy.py` korrekt implementiert!**

---

### **Was KEINE Bound Energy ist:**

**Scripts die irreführend benannt waren:**
1. `bound_energy_english.py` → Jetzt: `redshift_segment_density.py`
2. `bound_energy_plot.py` → Jetzt: `redshift_segment_density_plot.py`

**Diese Scripts berechnen:**
- ❌ **KEINE** Bound Energy im Paper-Sinn
- ✅ Redshift z_gr, z_total
- ✅ Segmentdichte N_seg
- ✅ Energieverhältnis epsilon_local (KEIN alpha_local!)

**Problem:**
```python
# Alte irreführende Berechnung:
alpha_local = (f_obs * h) / (m_e * c²)
f_emit_check = (alpha_local * m_e * c²) / h
# → f_emit_check = f_obs (Tautologie!)
```

---

## 📊 **Übersicht: Was wo steht**

| Dokument | Bound Energy Referenz | Status | Aktion |
|----------|----------------------|--------|--------|
| **Paper (.md)** | ✅ Echte Theorie beschrieben | Korrekt | Keine Änderung nötig |
| **bound_energy.py** | ✅ Paper-Implementierung | Korrekt | Kommentare verbessert |
| **commands.md** | ✅ segspace workflow | Korrekt | ✅ NOTE hinzugefügt |
| **Verification Summary** | ⚠️ Erwähnt bound_energy_english.py | Irreführend | ✅ NOTE hinzugefügt |
| **README.md** | ❌ Keine Referenzen gefunden | N/A | Nichts zu ändern |
| **Archive-Dateien** | ⚠️ Alte Referenzen | Archive | Low Priority |

---

## ✅ **Neue Dokumentation erstellt**

1. ✅ `BOUND_ENERGY_SCRIPTS_CLARIFICATION.md` (Vollständige Erklärung)
2. ✅ `SCRIPTS_USAGE_UPDATED.md` (Quick-Reference)
3. ✅ `WISSENSCHAFTLICHE_KLARSTELLUNG_BOUND_ENERGY.md` (Physikalische Interpretation)
4. ✅ `UPDATE_BOUND_ENERGY_REFERENCES.md` (Update-Anweisungen)
5. ✅ `CHANGELOG_BOUND_ENERGY_CORRECTION_2025-11-27.md` (Vollständiges Changelog)
6. ✅ `DOKUMENTATION_KORRIGIERT_2025-11-27.md` (Diese Datei)

---

## 📝 **Verwendung nach Korrektur**

### **Für echte Bound Energy (Paper-Herleitung):**
```bash
# Standalone Script
python bound_energy.py --selftest

# Oder über Pipeline
python segspace_all_in_one.py bound-energy --pairs freq_pairs.csv --out bound_energy_out
```

### **Für Redshift & Segmentdichte:**
```bash
# Neues Script (ersetzt bound_energy_english.py)
python redshift_segment_density.py

# Multi-Object Plot (ersetzt bound_energy_plot.py)
python redshift_segment_density_plot.py
```

---

## 🔬 **Wissenschaftliche Integrität gesichert**

**Vorher:**
- ❌ Scripts hießen "Bound Energy", berechneten aber nur Redshift
- ❌ "alpha_local" war nur epsilon_local (Energieverhältnis)
- ❌ "Back-Calculation" war Tautologie

**Nachher:**
- ✅ Scripts heißen "Redshift & Segment Density"
- ✅ epsilon_local klar als Energieverhältnis beschriftet
- ✅ Keine irreführenden "Back-Calculation Tests"
- ✅ **bound_energy.py bleibt als EINZIGES Script mit echter Bound Energy**

---

## 📖 **Referenzen**

### **Paper (unverändert):**
- `SegmentedSpacetimeBoundEnergyandtheStructuralOriginofthefine-structureconstant.md`
- `SegmentedSpacetimeBoundEnergyandtheStructuralOriginofthefine-structureconstant.pdf`

### **Korrigierte Dokumentation:**
- `commands.md` (Zeile 105, 547-548)
- `Verification Summary of Segmented Spacetime Repository.md` (Zeile 247-250, 518-522, 754-758)
- `run_complete_test_suite.py` (Zeile 38-40)
- `run_all_ssz_terminal.py` (Zeile 285, 739)

---

## ✅ **Validation**

**Wissenschaftliche Korrektheit:**
- ✅ Paper beschreibt echte Bound Energy → Unverändert
- ✅ bound_energy.py implementiert Paper korrekt → Kommentare verbessert
- ✅ segspace_all_in_one.py berechnet echte Bound Energy → Dokumentiert
- ✅ Irreführende Scripts umbenannt → redshift_segment_density.py
- ✅ Alle Hauptdokumente korrigiert → NOTE hinzugefügt

**Rückwärtskompatibilität:**
- ⚠️ Alte Scripts existieren noch (nicht gelöscht)
- ✅ Neue Scripts verfügbar (redshift_segment_density.py/plot.py)
- ✅ Dokumentation warnt vor Verwechslung
- ✅ Pipeline aktualisiert

---

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**

**Lizenz:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4
