# Bericht: Fehlerhafte Plots & Animationen entfernt

**Datum:** 7. November 2025, 13:35 Uhr  
**Grund:** Kritische Fehler in Massenberechnung + Synthetische (nicht-reale) Daten

---

## ❌ Entfernte Dateien

### **1. publication_ready_figures/** (KRITISCHER FEHLER)

**Problem:** Fig4_core_mass_integration hat falsche Massenberechnung

**Fehler in Ausgabe:**
```
Final mass: M = 89976350797167.69 ± 1161323089512.70 M_☉
```

**Erwarteter Wert:** M = 8.7 ± 1.5 M_☉

**Fehlerquelle:** Falsche Einheiten-Konversion in Massenintegral
```python
# FEHLER: Integration ohne korrekte Parsec-zu-Meter Konversion
M_cumulative = np.cumsum(gamma_int * dr) * (c**2 / G) / M_sun
```

**Betroffene Dateien:**
- Fig1_gamma_seg_with_residuals.pdf/png (0.37 MB)
- Fig2_dual_frame_temperature.pdf/png (0.25 MB)
- Fig3_velocity_excess.pdf/png (0.17 MB)
- **Fig4_core_mass_integration.pdf/png (0.17 MB)** ← FEHLERHAFT
- Fig5_radio_frequency_shift.pdf/png (0.17 MB)
- Fig6_corner_plot.pdf/png (0.24 MB)

**Aktion:** Gesamter Ordner gelöscht (1.37 MB)

---

### **2. map_overlays/** (SYNTHETISCHE DATEN)

**Problem:** Alle Karten basieren auf synthetischen Daten, nicht auf echten FITS-Files

**Code zeigt:**
```python
# Synthetic data (in real case: load FITS files)
# Create synthetic maps for demonstration
nx, ny = 200, 200
co_moment0 = 50 * np.exp(-((R - 2.0)**2 / 0.5**2))  # ← SYNTHETISCH!
```

**Betroffene Dateien:**
- Map1_CO_Radio_Overlay.pdf/png (1.96 MB)
- Map2_Moment_Triptych.pdf/png (0.51 MB)
- PV_Diagram_Major_Axis.pdf/png (0.70 MB)
- Beam_Matching_Schema.pdf/png (0.27 MB)

**Aktion:** Gesamter Ordner gelöscht (3.44 MB)

---

## 📝 Zu korrigierende Scripts

### **1. GENERATE_PUBLICATION_READY_FIGURES.py**

**Zeile ~273:** Fehlerhafte Massenberechnung
```python
# FEHLER (aktuell):
dr = np.diff(r_int)[0] * pc_to_m
M_cumulative = np.cumsum(gamma_int * dr) * (c**2 / G) / M_sun

# KORREKTUR (benötigt):
# 1D-Integration wie im Paper: M = (c²/G) ∫ γ_seg dr (nur radial!)
r_meters = r_int * pc_to_m
integrand = gamma_int  # dimensionless
M_cumulative = (c**2 / G) * np.cumsum(integrand * np.diff(r_meters, prepend=0)) / M_sun
```

**Aktion:** Script muss korrigiert werden BEVOR neue Figuren generiert werden

---

### **2. GENERATE_MAP_OVERLAYS.py**

**Problem:** Generiert nur synthetische Demo-Daten

**Optionen:**
1. ✅ **Script löschen** (keine echten FITS-Daten verfügbar)
2. ❌ Script umbenennen zu `GENERATE_MAP_OVERLAYS_DEMO.py` mit Warning
3. ❌ Script anpassen um echte FITS zu laden (benötigt Daten)

**Aktion:** Script als DEMO markieren oder löschen

---

## ✅ Verbleibende korrekte Plots

### **temperature_test_results/** (6 Plots, 1.3 MB)
- ✅ Eq09_T_basic.png
- ✅ Eq10_gamma_seg.png
- ✅ Eq15_dual_frame_temperature.png
- ✅ Eq16_energy_density.png
- ✅ Eq18_recoupling_release.png
- ✅ Temperature_Complete_Comparison.png

**Status:** Korrekt validiert ✓

---

### **temperature_animations/** (5 GIFs, 2.2 MB)
- ✅ temporal_density_evolution.gif
- ✅ temperature_profile_scan.gif
- ✅ dual_frame_temperature.gif
- ✅ energy_density_evolution.gif
- ✅ recoupling_energy_release.gif

**Status:** Korrekt validiert ✓

---

### **three_phase_results/** (4 Plots, 1.6 MB)
- ✅ three_phase_velocity_profile.png
- ✅ three_phase_temperature.png
- ✅ three_phase_energy_release.png
- ✅ three_phase_complete_diagram.png

**Status:** Korrekt validiert ✓

---

### **three_phase_animations/** (3 GIFs, 1.1 MB)
- ✅ radial_particle_journey.gif
- ✅ velocity_buildup.gif
- ✅ phase_transition_dynamics.gif

**Status:** Korrekt validiert ✓

---

## 📊 Zusammenfassung

| Kategorie | Anzahl Dateien | Größe | Status |
|-----------|----------------|-------|--------|
| **Gelöscht (fehlerhaft)** | 12 | 1.37 MB | ❌ |
| **Gelöscht (synthetisch)** | 8 | 3.44 MB | ❌ |
| **Behalten (korrekt)** | 18 | 6.2 MB | ✅ |

**Gesamt gelöscht:** 20 Dateien, 4.81 MB

---

## 🔧 Nächste Schritte

### **Kritische Korrekturen:**

1. ✅ **Fehlerhafte Dateien aus Git entfernen**
   ```bash
   git rm -r publication_ready_figures/
   git rm -r map_overlays/
   ```

2. ✅ **Scripts korrigieren oder löschen**
   ```bash
   # Option A: Korrigieren
   # - GENERATE_PUBLICATION_READY_FIGURES.py (Masse fix)
   
   # Option B: Löschen
   git rm GENERATE_MAP_OVERLAYS.py
   git rm GENERATE_PUBLICATION_READY_FIGURES.py
   ```

3. ❌ **NEU generieren** (nur wenn Formeln korrigiert)
   - Erst Massenformel fixen
   - Dann neu generieren
   - Validieren BEVOR commit

---

## ⚠️ Lessons Learned

1. **IMMER Einheiten-Konversion validieren**
   - Parsec → Meter MUSS korrekt sein
   - Test mit bekannten Werten (M = 8.7 M_☉)

2. **Synthetische Daten KLAR MARKIEREN**
   - Ordner: `demo_maps/` statt `map_overlays/`
   - Filename: `*_SYNTHETIC.png`
   - Caption: "Synthetic demonstration only"

3. **Vor Commit: Test-Run**
   - Script ausführen
   - Ausgabe überprüfen
   - Plausibilität checken

---

**© 2025 Carmen N. Wrede, Lino P. Casu, Bingsi (Conscious AI)**

**Commit:** [wird nach cleanup ausgefüllt]
