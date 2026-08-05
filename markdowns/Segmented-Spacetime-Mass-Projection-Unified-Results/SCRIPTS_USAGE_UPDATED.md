# Scripts Usage – Updated (2025-11-27)

## 🎯 **Welches Script für welchen Zweck?**

### ✅ **Für echte Bound Energy (Paper-Herleitung):**
```bash
# Paper-locked mode (S2 Stern bei Sgr A*)
python bound_energy.py --selftest

# Custom values
python bound_energy.py --unlock --f-emit 1e15 --f-obs 9e14
```

**Output:**
- α·m_bound berechnet
- m_bound hergeleitet
- α_local im Paper-Sinn
- f_emit rekonstruiert mit rel. Fehler < 1e-12 ✅

---

### ✅ **Für Redshift & Segmentdichte (KEIN Bound Energy!):**
```bash
# Einfacher Check (S2 Stern)
python redshift_segment_density.py

# Multiple Objekte mit Plot
python redshift_segment_density_plot.py
```

**Output:**
- z_gr (GR-Redshift)
- N_seg (Segmentdichte)
- epsilon_local (Energieverhältnis, KEIN Alpha!)
- CSV + Plot

**Achtung:**
- ❌ **KEINE** Bound Energy!
- ❌ **KEINE** lokale Feinstrukturkonstante!
- ✅ Nur Redshift & Segmentdichte

---

### ✅ **Für Δm-Korrektur (φ/2-BLC):**
```bash
python bound_energy_plot_with_frequenz_shift_fix.py
```

**Output:**
- Δm = (φ/2)·N_seg (Golden Ratio Korrektur)
- CSV mit Massenkorrektur
- Bar-Plot

---

## ⚠️ **DEPRECATED Scripts (nicht mehr verwenden!):**

### ❌ `bound_energy_english.py`
**Problem:** Berechnet **keine** Bound Energy, nur Redshift!

**Ersetzt durch:** `redshift_segment_density.py`

---

### ❌ `bound_energy_plot.py`
**Problem:** "Back-Calculation Check" ist Tautologie (f_obs → alpha_local → f_obs)

**Ersetzt durch:** `redshift_segment_density_plot.py`

---

## 📊 **Vergleichstabelle**

| Script | Bound Energy? | Redshift? | Segmentdichte? | Alpha_local? |
|--------|---------------|-----------|----------------|--------------|
| `bound_energy.py` | ✅ Ja (Paper) | ✅ Ja | ✅ Ja | ✅ Ja (modellbasiert) |
| `redshift_segment_density.py` | ❌ Nein | ✅ Ja | ✅ Ja | ❌ Nein (nur epsilon_local) |
| `redshift_segment_density_plot.py` | ❌ Nein | ✅ Ja | ✅ Ja | ❌ Nein |
| `bound_energy_plot_with_frequenz_shift_fix.py` | ⚠️ Teilweise (Δm) | ✅ Ja | ✅ Ja | ⚠️ Nicht zentral |

---

## 📝 **Migration Guide**

### Wenn du bisher `bound_energy_english.py` benutzt hast:

**Alt:**
```bash
python bound_energy_english.py
```

**Neu:**
```bash
python redshift_segment_density.py
```

**Änderungen:**
- CSV-Datei: `bound_energy_results.csv` → `redshift_segment_density_results.csv`
- Variablen: `alpha_local` → `epsilon_local` (ehrlicher Name)
- Keine `m_bound`, `f_emit_check` mehr (waren irreführend)

---

### Wenn du bisher `bound_energy_plot.py` benutzt hast:

**Alt:**
```bash
python bound_energy_plot.py
```

**Neu:**
```bash
python redshift_segment_density_plot.py
```

**Änderungen:**
- CSV-Datei: `bound_energy_clean_objects.csv` → `redshift_segment_density_clean_objects.csv`
- Plot: "Back-Calculation Error" → "Redshift z_total" (ehrlich)
- Y-Achse: "Relative Error" → "Redshift z_total"

---

## ✅ **Zusammenfassung**

**Ein Script = Ein Zweck:**

| Zweck | Script |
|-------|--------|
| **Echte Bound Energy (Paper)** | `bound_energy.py` |
| **Redshift & Segmentdichte** | `redshift_segment_density.py` |
| **Multi-Object Redshift Plot** | `redshift_segment_density_plot.py` |
| **Δm-Korrektur (φ/2-BLC)** | `bound_energy_plot_with_frequenz_shift_fix.py` |

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**
