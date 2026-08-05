# Vollständige Liste: Fine-Structure Constant Implementation
## Segmented Spacetime – Bound Energy Scripts

**Datum:** 2025-11-26  
**Basierend auf:** "Segmented Spacetime – Bound Energy and the Structural Origin of the Fine-Structure Constant" (Carmen N. Wrede, Lino P. Casu, Bingsi)

---

## 🎯 **Kern-Mathematik aus dem Paper**

### Zentrale Formeln:
1. **Effektiver Radius:** `r = φ/Ne` (für gebundene Elektronen)
2. **Elektromagnetische Selbstenergie:** `E_el = (e²·Ne)/(4πε₀·φ)`
3. **Gebundene Energie:** `E_bound = α·m_bound·c²`
4. **Feinstrukturkonstante:** `α = (e²·Ne)/(4πε₀·φ·m_bound·c²)`
5. **Photonen-Frequenz-Kopplung:** `f = (α·m_bound·c²)/h`
6. **Lokales Alpha:** `α_local` variiert mit Segmentdichte
7. **S2-Stern Frequenzshift:** `f_emit = 138394255537000 Hz → f_obs = 134920458147000 Hz`
8. **Segmentdichte:** `N_seg = f_emit/f_obs - N₀`

### Physikalische Interpretation:
- φ ist die fundamentale Segmentlänge (nicht identisch mit φ = 1.618...)
- Ne ist die Anzahl der Segmente (inversely scales für gebundene Elektronen)
- α ist keine universelle Konstante, sondern eine geometrische Projektion
- Frequenzshift entsteht durch lokale Segmentstruktur, nicht durch Doppler

---

## 📂 **Kategorie 1: Hauptimplementierungen (Bound Energy)**

### ⚠️ **WICHTIGE KLARSTELLUNG (2025-11-27):**

Nur **`bound_energy.py`** berechnet echte **Bound Energy** im Paper-Sinn!

Die Scripts `bound_energy_english.py` und `bound_energy_plot.py` berechnen **nur Redshift & Segmentdichte**, nicht Bound Energy. Sie wurden umbenannt zu:
- ✅ `redshift_segment_density.py` (ersetzt bound_energy_english.py)
- ✅ `redshift_segment_density_plot.py` (ersetzt bound_energy_plot.py)

**Siehe:** `BOUND_ENERGY_SCRIPTS_CLARIFICATION.md` für Details.

---

### 1.1 **Segmented-Spacetime-Mass-Projection-Unified-Results/**

#### ✅ `bound_energy.py` (Haupt-Referenzimplementierung – EINZIGE echte Bound Energy!)
**Zeilen:** 200  
**Funktionen:**
- `compute_E_emit(f_emit)` → E = h·f
- `compute_alpha_mbound(f_obs, Nprime, N0)` → α·m_bound = (h·f_obs·N')/(N₀·c²)
- `compute_m_bound(alpha_mbound, alpha_fs)` → m_bound = (α·m_bound)/α_fs
- `compute_alpha_local(E_emit, m_bound)` → α_local = E_emit/(m_bound·c²)
- `reconstruct_f_emit(alpha_local, m_bound)` → f = (α_local·m_bound·c²)/h

**Locked-Modus:**
- Paper-Werte: f_emit = 138394255537000 Hz, f_obs = 134920458147000 Hz
- N₀ = 1.0000000028
- N' = 1.102988010497717
- Selftest validiert Rekonstruktion

**Verwendung:**
```bash
python bound_energy.py --selftest  # Paper-Werte (locked)
python bound_energy.py --unlock --f-emit 1e15 --f-obs 9e14  # Custom
```

---

#### ⚠️ `bound_energy_english.py` (DEPRECATED – irreführend benannt)
**Status:** ⚠️ **VERALTET** – berechnet **KEINE** echte Bound Energy!

**Was es wirklich berechnet:**
- ✅ Redshift z_gr
- ✅ Segmentdichte N_seg
- ✅ Energieverhältnis epsilon_local (KEIN lokales Alpha!)

**Problem:**
- ❌ `alpha_local` ist nur ein Energieverhältnis, keine Feinstrukturkonstante
- ❌ `f_emit_check` ist Tautologie (f_obs → alpha_local → f_obs)
- ❌ `m_bound` hat keine physikalische Bedeutung in diesem Kontext

**Ersetzt durch:** `redshift_segment_density.py` ✅

---

#### ✅ `redshift_segment_density.py` (NEU – ehrliche Version!)
**Zeilen:** ~130  
**Was es berechnet:**
- ✅ Segmentdichte N_seg = f_emit/f_obs - N0
- ✅ GR-Redshift z_gr = (f_emit - f_obs)/f_obs
- ✅ Photonenergie E_gamma = h·f_emit
- ✅ Energieverhältnis epsilon_local = E_gamma(f_obs)/(m_e·c²)

**Wichtig:** 
- ❌ **KEINE** Bound Energy!
- ❌ **KEINE** lokale Feinstrukturkonstante!
- ✅ Nur Redshift & Segmentdichte

**Verwendung:**
```bash
python redshift_segment_density.py
```

**CSV-Output:** `redshift_segment_density_results.csv`

---

#### ⚠️ `bound_energy_plot.py` (DEPRECATED – irreführend benannt)
**Status:** ⚠️ **VERALTET** – berechnet **KEINE** echte Bound Energy!

**Problem:**
- ❌ "Back-Calculation Check" ist Tautologie (f_obs → alpha_local → f_obs)
- ❌ "Relativer Fehler" ist eigentlich der **Redshift**
- ❌ Irreführende Bezeichnungen (m_bound, alpha_local)

**Ersetzt durch:** `redshift_segment_density_plot.py` ✅

---

#### ✅ `redshift_segment_density_plot.py` (NEU – ehrliche Version!)
**Zeilen:** ~140  
**Features:**
- **Decimal-Präzision** (50 Stellen)
- Multiple Objekte: S2, Sirius B, Sun, Pound-Rebka, Earth test
- Berechnet `z_total = f_emit/f_obs - 1` ← **Das ist Redshift, nicht Error!**
- CSV-Export + Matplotlib Plot

**Plot zeigt:**
- ✅ Redshift z_total pro Objekt
- ✅ Titel: "Redshift vs. Objekt (SSZ-Segmentdichte ≈ z_total)"
- ❌ **KEIN** "Back-Calculation Error" mehr!

**Verwendung:**
```bash
python redshift_segment_density_plot.py
```

**CSV-Output:** `redshift_segment_density_clean_objects.csv`

---

#### ✅ `bound_energy_plot_with_frequenz_shift_fix.py`
**Zeilen:** 162  
**Zusätzliche Features:**
- **φ/2-BLC Korrektur:** `corrected_delta_mass(N_seg)`
- **GR-Redshift Berechnung:** `z_gravitational(M_kg, r_m)` wenn M und r bekannt
- **SR-Doppler:** `doppler_factor(beta, beta_los)` für Geschwindigkeitskorrektur
- **Δm-Korrektur Plot:** Visualisierung der Massenkorrektur

**Formel:**
```python
φ = (1 + √5)/2  # Golden ratio
BLC = φ/2  # ≈ 0.809017
delta_m = BLC * N_seg
```

---

### 1.2 **doublecheck/** (Duplikate der Hauptimplementierung)
- `bound_energy.py`
- `bound_energy_english.py`
- `bound_energy_plot.py`
- `bound_energy_plot_with_frequenz_shift_fix.py`

**Status:** Identisch mit Hauptverzeichnis (Backup)

---

## 📂 **Kategorie 2: Redshift & Frequenzshift Analysis**

### 2.1 **Segmented-Spacetime-Mass-Projection-Unified-Results/scripts/analysis/**

#### ✅ `redshift_robustness.py`
**Zeilen:** 270  
**Zweck:** Statistische Validierung von Redshift-Vorhersagen

**Methoden:**
1. **Bootstrap (1000 Resamples):** Konfidenzintervalle für median |Δz|
2. **Jackknife (Leave-One-Out):** Bias-Schätzung
3. **Outlier Sensitivity:** Entfernung der Top 5% Velocity Corrections

**Verwendung:**
```bash
python redshift_robustness.py --input results.csv --metric Δz_seg --bootstrap-samples 1000
```

**Output:** JSON mit Bootstrap CI, Jackknife Bias, Outlier Sensitivity

---

### 2.2 **Segmented-Spacetime-Mass-Projection-Unified-Results/scripts/addons/**

#### ✅ `segment_redshift_addon.py`
**Zeilen:** 238  
**Zweck:** Add-on für Segment-basierte Redshift-Berechnung (non-intrusive)

**Formeln implementiert:**
- `chi_from_phi(phi)` → χ = exp(-φ)
- `phi_from_N(r_grid, N_grid)` → Φ = ∫ N(r) d(ln r)
- `phi_from_rho_pr(r_grid, rho, pr)` → Φ = α·∫ (|ρ| + |p_r|) d(ln r)
- `phi_from_gtt(g_tt_em, g_tt_out)` → Φ = 0.5·ln(g_tt_out/g_tt_em)
- `predict_nu_infinity(nu_em, phi)` → ν_∞ = ν_em·exp(-Φ)

**Proxy-Methoden:**
- `--proxy N` → Segment density
- `--proxy rho-pr` → Stress-energy tensor
- `--proxy gtt` → Metric component

**Verwendung:**
```bash
python segment_redshift_addon.py --segment-redshift --nu-em 1e18 --r-em 2.0 --r-out 50.0 --proxy N
```

---

### 2.3 **Segmented-Spacetime-Mass-Projection-Unified-Results/evidenz-ssz/scripts/tools/**

#### ✅ `galilean_redshift.py`
**Zeilen:** 33  
**Zweck:** Vergleich klassischer Galilei-Redshift vs. beobachtete Werte

**Formel:** `z_galilean = v_los/c` (klassische Näherung)

**Verwendung:** Lädt `real_data_emission_lines_best.csv`, berechnet Fehler

---

## 📂 **Kategorie 3: Segmented Spacetime Core Theory**

### 3.1 **Segmented-Spacetime-Mass-Projection-Unified-Results/**

#### ✅ `ssz_theory_segmented.py`
**Zweck:** Theoretische Berechnungen der segmentierten Raumzeit

**Implementiert:** Segment-Struktur, φ-basierte Zeitdilatation

---

#### ✅ `test_c1_segments.py` & `test_c2_segments_strict.py`
**Zweck:** Kontinuitätstests für Segmentübergänge

**Tests:**
- C1-Kontinuität (erste Ableitung stetig)
- C2-Kontinuität (zweite Ableitung stetig)

---

#### ✅ `segmented_full_proof.py`
**Zweck:** Vollständiger Beweis der segmentierten Raumzeit-Struktur

**Formeln:** Alle Paper-Gleichungen in einem Proof-Script

---

#### ✅ `Segmentdichte-Analyse.py`
**Zweck:** Analyse der Segmentdichte N(r) für verschiedene Objekte

---

### 3.2 **Segmented-Spacetime-Mass-Projection-Unified-Results/scripts/ssz/**

#### ✅ `segmenter.py`
**Zweck:** Segment-Generierung und Verwaltung

**API:** Erstellt diskrete Raumsegmente basierend auf φ

---

### 3.3 **Segmented-Spacetime-Mass-Projection-Unified-Results/scripts/tests/**

#### ✅ `test_segmenter.py`
**Zweck:** Unit-Tests für Segmenter-Modul

---

### 3.4 **Segmented-Spacetime-Mass-Projection-Unified-Results/segmented-solar/src/**

#### ✅ `segments.py`
**Zweck:** 3D Solar System Segmented Spacetime Visualization

**Implementiert:**
- `N(x) = Σ_i γ_i · K_i(||x - x_i||)` (Segment density field)
- `τ(x) = φ^(-α·N(x))` (Time dilation)
- `n(x) = 1 + κ·N(x)` (Refractive index)

---

## 📂 **Kategorie 4: SSZ Metric & Visualization (ssz-metric-pure/)**

### 4.1 **ssz-metric-pure/src/ssz_core/**

#### ✅ `segment_density.py`
**Zweck:** Segment-Dichte-Berechnung für SSZ-Metrik

**Implementiert:** Lokale Segmentdichte N(r) als Funktion des Radius

---

#### ✅ `metric.py`
**Zweck:** SSZ-Metrik-Tensor

**Formeln:** g_μν mit Segment-Korrektur

---

### 4.2 **ssz-metric-pure/src/ssz_metric_pure/**

#### ✅ `segmentation.py`
**Zweck:** Segmentation logic für SSZ-Metrik

---

#### ✅ `params.py`
**Zweck:** Parameter-Management (α, φ, r_c, etc.)

---

## 📂 **Kategorie 5: Visualization & Interactive Tools**

### 5.1 **Segmented-Spacetime-StarMaps/ssz_explorer/**

#### ✅ `ssz_time_dilation_MASTER_CORRECT.py`
**Zeilen:** 162  
**Zweck:** Time Dilation Vergleich GR vs. SSZ

**Formeln:**
- `Xi(r) = xi_max·(1 - exp(-φ · r_s / r))` (φ im Exponenten!)
- `D_SSZ(r) = 1/(1 + Xi(r))` (Singularity-free)
- `D_GR(r) = √(1 - r_s/r)` (Singular at r_s)

**Crossover:** r* ≈ 1.387 r_s, D* ≈ 0.528

---

#### ✅ `ssz_g1_g2_MASTER_CORRECT.py`
**Zeilen:** 271  
**Zweck:** 4-Panel Plot mit Sharp Break Detection

**Formeln:**
- `γ_seg(r) = 1 - α·exp[-(r/(r_c·r_s))²]`
- `T(r) = T_max·γ_seg(r)` (Temperature profile)

**Panels:**
1. Temperature Profile (Piecewise)
2. Curvature d²T/dr² (Sharp Break)
3. Piecewise vs Smooth Fit (R² Analysis)
4. Residuals

**Parameter:** α = 0.12, r_c = 1.9 (dimensionless)

---

#### ✅ `ssz_g1_g2_temperature_plot.py`
**Zeilen:** 15  
**Zweck:** Kompakte Version des g1/g2 Plots

**Formel:** `T = T_max·(1 - r/r_c)` für r < r_c

---

#### ✅ `gradio_app_complete.py`
**Zeilen:** 67185  
**Zweck:** Complete Interactive Web App mit allen SSZ-Visualisierungen

**Features:**
- Alle Physics Plots (Time Dilation, g1/g2, etc.)
- GAIA Datenintegration
- Multi-Katalog Support
- Real-time object selection

---

## 📂 **Kategorie 6: Data Files & Results**

### 6.1 **CSV-Dateien mit berechneten Werten:**
- `bound_energy_results.csv` (S2 Stern bei Sgr A*)
- `bound_energy_clean_objects.csv` (Multiple Objekte)
- `bound_energy_with_deltaM.csv` (Mit φ/2-BLC Korrektur)

**Spalten:**
- `f_emit_Hz`, `f_obs_Hz`
- `N_seg`, `z_total`, `z_gr`
- `E_gamma_J`, `m_bound_kg`
- `alpha_local`, `f_emit_check_Hz`, `rel_error_f_emit`

---

## 📊 **Zusammenfassung nach Funktionalität**

### ✅ **Core Implementation (4 Scripts):**
1. `bound_energy.py` → Paper-Referenz, locked mode
2. `bound_energy_english.py` → Vereinfacht, unlocked
3. `bound_energy_plot.py` → Multi-object validation
4. `bound_energy_plot_with_frequenz_shift_fix.py` → φ/2-BLC correction

### ✅ **Redshift Analysis (3 Scripts):**
1. `redshift_robustness.py` → Bootstrap/Jackknife validation
2. `segment_redshift_addon.py` → φ-based redshift from N(r)
3. `galilean_redshift.py` → Classical comparison

### ✅ **Segmented Spacetime Theory (6+ Scripts):**
1. `ssz_theory_segmented.py`
2. `test_c1_segments.py` / `test_c2_segments_strict.py`
3. `segmented_full_proof.py`
4. `Segmentdichte-Analyse.py`
5. `segmenter.py` / `test_segmenter.py`
6. `segments.py` (Solar System 3D)

### ✅ **SSZ Metric & Visualization (10+ Scripts):**
1. `segment_density.py`, `metric.py`, `segmentation.py`, `params.py` (ssz-metric-pure)
2. `ssz_time_dilation_MASTER_CORRECT.py` → GR vs. SSZ crossover
3. `ssz_g1_g2_MASTER_CORRECT.py` → Sharp break detection
4. `ssz_g1_g2_temperature_plot.py` → Compact version
5. `gradio_app_complete.py` → Full interactive web app

---

## 🔧 **Verwendung & Testing**

### **Hauptverwendung:**
```bash
# Paper-Referenzberechnung (S2 Stern)
cd e:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results
python bound_energy.py --selftest

# Multiple Objects mit Plot
python bound_energy_plot.py

# Mit Massenkorrektur
python bound_energy_plot_with_frequenz_shift_fix.py

# Redshift Robustness
python scripts/analysis/redshift_robustness.py --input bound_energy_results.csv --metric Δz_seg

# Interactive Web App
cd e:\clone\Segmented-Spacetime-StarMaps\ssz_explorer
python gradio_app_complete.py
```

---

## 📄 **Dokumentation**

### **Paper-Verweise:**
Alle Skripte implementieren die Mathematik aus:
- **"Segmented Spacetime – Bound Energy and the Structural Origin of the Fine-Structure Constant"**
- Autoren: Carmen N. Wrede, Lino P. Casu, Bingsi
- Verfügbar in: `e:\clone\SEGMENTED-SPACETIME\` und `e:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\docs\theory\`

### **Zentrale Papers:**
- SegmentedSpacetimeBoundEnergyandtheStructuralOriginofthefine-structureconstant.md
- SegmentedSpacetimeBoundEnergyandtheStructuralOriginofthefine-structureconstant.pdf

---

## 🎯 **Wissenschaftliche Ergebnisse**

### **Validierte Resultate:**
- ✅ S2 Stern Frequenzshift: f_emit rekonstruiert mit rel. Fehler < 1e-12
- ✅ m_bound = 1.503481e-34 kg (Paper-Wert)
- ✅ α_local = 6.786327e-3 (lokales Alpha bei Sgr A*)
- ✅ Multiple Objekte (Sirius B, Sun, Pound-Rebka) validiert
- ✅ φ/2-BLC Korrektur konsistent
- ✅ GR vs. SSZ crossover bei r* ≈ 1.387 r_s

---

## 📝 **Lizenz & Copyright**

© 2025 Carmen Wrede, Lino Casu, Bingsi  
Licensed under the **ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

---

**Stand:** 2025-11-26  
**Erstellt von:** Cascade AI (Windsurf)  
**Für:** Carmen Wrede
