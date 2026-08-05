# Quick Reference: Fine-Structure Constant Scripts

## 📋 **Alle Skripte mit Hauptformeln**

| # | Datei | Pfad | Hauptformel | Zeilen |
|---|-------|------|-------------|--------|
| **KATEGORIE 1: BOUND ENERGY CORE** |
| 1 | `bound_energy.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | `α = (e²Ne)/(4πε₀φm_bound c²)` | 200 |
| 2 | `bound_energy_english.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | `m_bound = m_e - E_γ/c²` | 109 |
| 3 | `bound_energy_plot.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | `f = (α_local·m_bound·c²)/h` | 144 |
| 4 | `bound_energy_plot_with_frequenz_shift_fix.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | `Δm = (φ/2)·N_seg` (BLC) | 162 |
| **KATEGORIE 2: REDSHIFT & FREQUENCY SHIFT** |
| 5 | `redshift_robustness.py` | `scripts/analysis/` | Bootstrap/Jackknife für `Δz` | 270 |
| 6 | `segment_redshift_addon.py` | `scripts/addons/` | `ν_∞ = ν_em·exp(-Φ)` | 238 |
| 7 | `galilean_redshift.py` | `evidenz-ssz/scripts/tools/` | `z = v_los/c` (klassisch) | 33 |
| **KATEGORIE 3: SEGMENT THEORY** |
| 8 | `ssz_theory_segmented.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | Segment-Theorie | ~500 |
| 9 | `test_c1_segments.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | C1-Kontinuität | ~150 |
| 10 | `test_c2_segments_strict.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | C2-Kontinuität | ~180 |
| 11 | `segmented_full_proof.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | Vollständiger Proof | ~800 |
| 12 | `Segmentdichte-Analyse.py` | `Segmented-Spacetime-Mass-Projection-Unified-Results/` | N(r) Analyse | ~300 |
| 13 | `segmenter.py` | `scripts/ssz/` | Segment-Generator | ~400 |
| 14 | `segments.py` | `segmented-solar/src/` | `N(x) = Σγ_i·K_i` (3D) | ~600 |
| **KATEGORIE 4: SSZ METRIC** |
| 15 | `segment_density.py` | `ssz-metric-pure/src/ssz_core/` | N(r) für Metrik | ~200 |
| 16 | `metric.py` | `ssz-metric-pure/src/ssz_core/` | g_μν mit Segmenten | ~300 |
| 17 | `segmentation.py` | `ssz-metric-pure/src/ssz_metric_pure/` | Segmentation Logic | ~250 |
| 18 | `params.py` | `ssz-metric-pure/src/ssz_metric_pure/` | α, φ, r_c Parameter | ~150 |
| **KATEGORIE 5: VISUALIZATION** |
| 19 | `ssz_time_dilation_MASTER_CORRECT.py` | `ssz_explorer/` | `D_SSZ = 1/(1+Xi)` | 162 |
| 20 | `ssz_g1_g2_MASTER_CORRECT.py` | `ssz_explorer/` | `γ_seg = 1-α·exp[-(r/r_c·r_s)²]` | 271 |
| 21 | `ssz_g1_g2_temperature_plot.py` | `ssz_explorer/` | `T = T_max·(1-r/r_c)` | 15 |
| 22 | `gradio_app_complete.py` | `ssz_explorer/` | Full Interactive Web App | 67185 |

---

## 🔑 **Schlüsselformeln**

### **1. Feinstrukturkonstante**
```
α = (e²·Ne) / (4πε₀·φ·m_bound·c²)
```

### **2. Gebundene Energie**
```
E_bound = α·m_bound·c²
```

### **3. Photonen-Frequenz**
```
f = (α·m_bound·c²) / h
```

### **4. Segmentdichte**
```
N_seg = f_emit/f_obs - N₀
```

### **5. Lokales Alpha**
```
α_local = E_emit / (m_bound·c²)
```

### **6. SSZ Time Dilation**
```
D_SSZ(r) = 1 / (1 + Xi(r))
Xi(r) = xi_max·(1 - exp(-φ · r_s / r))
```

---

## 🎯 **Verwendungsbeispiele**

### **Paper-Referenz (S2 Stern)**
```bash
cd e:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results
python bound_energy.py --selftest
```

### **Multiple Objects**
```bash
python bound_energy_plot.py
```

### **Redshift Analysis**
```bash
python scripts/analysis/redshift_robustness.py --input bound_energy_results.csv
```

### **Interactive Web App**
```bash
cd e:\clone\Segmented-Spacetime-StarMaps\ssz_explorer
python gradio_app_complete.py
```

---

## 📊 **Validierte Werte (S2 Stern)**

| Parameter | Wert | Einheit |
|-----------|------|---------|
| `f_emit` | 138394255537000 | Hz |
| `f_obs` | 134920458147000 | Hz |
| `m_bound` | 1.503481e-34 | kg |
| `α_local` | 6.786327e-3 | dimensionless |

---

**© 2025 Carmen Wrede, Lino Casu, Bingsi**
