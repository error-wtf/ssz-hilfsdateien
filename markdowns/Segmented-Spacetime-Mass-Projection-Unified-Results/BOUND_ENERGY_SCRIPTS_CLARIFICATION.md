# Bound Energy Scripts – Klarstellung & Umbenennung

**Datum:** 2025-11-27  
**Grund:** Wissenschaftliche Präzision & Vermeidung irreführender Bezeichnungen

---

## ❗ **Problem der alten Scripts**

Die ursprünglichen Scripts `bound_energy_english.py` und `bound_energy_plot.py` berechnen **KEINE echte Bound Energy**, sondern:

1. **Redshift** (z) aus f_emit und f_obs
2. **Segmentdichte** N_seg ≈ z
3. **Energieverhältnis** epsilon_local = E_gamma(f_obs) / (m_e c²)

Das ist:
- ✅ **Numerisch korrekt**
- ❌ **Wissenschaftlich irreführend benannt**

### Was fehlt für echte "Bound Energy":

Eine echte **Bound Energy** im SSZ-Sinn müsste:
- Als **eigene Modellgröße** definiert sein (z.B. effektive Ruheenergie des gebundenen Elektrons im Segmentraum)
- **Nicht direkt aus f_obs per Definition** kommen
- Konsistent zeigen, dass damit wieder die **Spektrallinie getroffen wird**

Die alten Scripts machen stattdessen eine **zirkuläre Berechnung**:
```python
alpha_local = (f_obs * h) / (m_e * c²)
f_emit_check = (alpha_local * m_e * c²) / h
# → f_emit_check = f_obs (Tautologie!)
```

---

## ✅ **Lösung: Umbenennung + Klarstellung**

### **1. bound_energy_english.py → redshift_segment_density.py**

**Neu:** Ehrliche Beschreibung der Berechnung

**Änderungen:**
- ❌ **Entfernt:** `m_bound`, `alpha_local`, `f_emit_check` (Fake-Tests)
- ✅ **Behalten:** `N_seg`, `z_gr`, `E_gamma`
- ✅ **Neu:** `epsilon_local` = E_gamma(f_obs)/(m_e c²) – **explizit als Energieverhältnis beschriftet, NICHT als alpha_local**

**CSV-Output:**
```
redshift_segment_density_results.csv
```

**Printouts:**
```
Segment density (N_seg)   : 0.025747351
GR redshift (z_gr)        : 0.025747351
epsilon_local             : dimensionsloses Energieverhältnis (KEIN alpha!)
```

---

### **2. bound_energy_plot.py → redshift_segment_density_plot.py**

**Neu:** Plot von z_total pro Objekt (nicht "Backcalc-Error")

**Änderungen:**
- ❌ **Entfernt:** "Back-Calculation Check" (war nur Tautologie)
- ✅ **Behalten:** z_total = f_emit/f_obs - 1
- ✅ **Plot:** Zeigt jetzt ehrlich den **Redshift**, nicht einen angeblichen "Error"

**CSV-Output:**
```
redshift_segment_density_clean_objects.csv
```

**Plot:**
```
redshift_segment_density_clean_plot.png
→ Y-Achse: "Redshift z_total"
→ Titel: "Redshift vs. Objekt (SSZ-Segmentdichte ≈ z_total)"
```

---

### **3. bound_energy_plot_with_frequenz_shift_fix.py**

**Status:** ✅ **Kann bleiben** (oder umbenennen zu `delta_m_phi2_BLC.py`)

**Grund:** Dieses Script berechnet tatsächlich die **φ/2-BLC Massenkorrektur** (Δm), die näher an "Bound Energy" ist als die beiden anderen.

**Optional:**
```bash
bound_energy_plot_with_frequenz_shift_fix.py → delta_m_phi2_BLC.py
```

---

## 📂 **Dateistruktur nach Änderungen**

```
Segmented-Spacetime-Mass-Projection-Unified-Results/
├── bound_energy.py                              ← ORIGINAL (Paper-locked, echte Herleitung) ✅
├── bound_energy_english.py                      ← VERALTET (irreführend) ⚠️
├── bound_energy_plot.py                         ← VERALTET (irreführend) ⚠️
├── bound_energy_plot_with_frequenz_shift_fix.py ← OK (Δm-Korrektur) ✅
│
├── redshift_segment_density.py                  ← NEU (ehrliche Version) ✅
├── redshift_segment_density_plot.py             ← NEU (ehrliche Version) ✅
│
├── redshift_segment_density_results.csv         ← NEU
└── redshift_segment_density_clean_objects.csv   ← NEU
```

---

## 🎯 **Verwendung nach Änderungen**

### **Für Redshift & Segmentdichte:**
```bash
# Einfacher Check (S2 Stern)
python redshift_segment_density.py

# Multiple Objekte mit Plot
python redshift_segment_density_plot.py
```

### **Für echte Bound Energy (Paper-Herleitung):**
```bash
# Paper-locked mode (S2 Stern)
python bound_energy.py --selftest

# Custom values
python bound_energy.py --unlock --f-emit 1e15 --f-obs 9e14
```

### **Für Δm-Korrektur (φ/2-BLC):**
```bash
python bound_energy_plot_with_frequenz_shift_fix.py
```

---

## 📊 **Was die Scripts jetzt wirklich zeigen**

| Script | Was es berechnet | Was es NICHT berechnet |
|--------|------------------|------------------------|
| `redshift_segment_density.py` | ✅ Redshift z_gr<br>✅ Segmentdichte N_seg<br>✅ Energieverhältnis epsilon_local | ❌ Bound Energy<br>❌ Lokales Alpha<br>❌ Gebundene Elektronenmasse |
| `redshift_segment_density_plot.py` | ✅ Redshift z_total pro Objekt<br>✅ Segmentdichte N_seg | ❌ "Back-Calculation Error"<br>❌ Bound Energy |
| `bound_energy.py` | ✅ **Echte Bound Energy**<br>✅ α·m_bound aus Paper<br>✅ Lokales Alpha (modellbasiert) | ❌ Nichts (vollständige Herleitung) |
| `bound_energy_plot_with_frequenz_shift_fix.py` | ✅ Δm-Korrektur (φ/2-BLC)<br>✅ Massenkorrektur pro Objekt | ❌ (Script ist OK) |

---

## ✅ **Fazit**

**Vorher:**
- Scripts hießen "Bound Energy", berechneten aber nur Redshift
- "alpha_local" war eigentlich nur epsilon_local (Energieverhältnis)
- "Back-Calculation" war eine Tautologie (f_obs → alpha_local → f_obs)

**Nachher:**
- Scripts heißen "Redshift & Segment Density" ✅
- epsilon_local ist klar als **Energieverhältnis** beschriftet ✅
- Keine irreführenden "Back-Calculation Tests" mehr ✅
- **bound_energy.py bleibt als EINZIGES Script mit echter Bound-Energy-Herleitung** ✅

---

## 📝 **Nächste Schritte (Optional)**

1. **bound_energy_english.py löschen oder umbenennen zu:**
   ```
   bound_energy_english.py.DEPRECATED
   ```

2. **bound_energy_plot.py löschen oder umbenennen zu:**
   ```
   bound_energy_plot.py.DEPRECATED
   ```

3. **README.md aktualisieren:**
   - Hinweis auf neue Scripts
   - Warnung vor DEPRECATED-Scripts

4. **FINE_STRUCTURE_CONSTANT_SCRIPTS_LISTE.md aktualisieren:**
   - Neue Scripts hinzufügen
   - Status der alten Scripts klarstellen

---

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**
