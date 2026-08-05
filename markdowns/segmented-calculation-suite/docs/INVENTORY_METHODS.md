# INVENTORY: SSZ Calculation Methods

**PHASE 0 Deliverable - Systematische Inventarisierung**  
**Quelle:** `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\`

---

## 1. Core Physics Methods (ssz/segwave/)

### 1.1 Q-Factor Calculation
| Funktion | `compute_q_factor()` |
|----------|---------------------|
| **Datei** | `ssz/segwave/seg_wave_propagation.py` |
| **Signatur** | `compute_q_factor(T_curr, T_prev, n_curr=None, n_prev=None, beta=1.0, eta=0.0)` |
| **Inputs** | T_curr (K), T_prev (K), n_curr (cm⁻³), n_prev (cm⁻³), beta, eta |
| **Output** | float: q_k ratio |
| **Formel** | `q_k = (T_curr/T_prev)^β × (n_curr/n_prev)^η` |
| **Units** | Dimensionless |

### 1.2 Velocity Profile Prediction
| Funktion | `predict_velocity_profile()` |
|----------|------------------------------|
| **Datei** | `ssz/segwave/seg_wave_propagation.py` |
| **Signatur** | `predict_velocity_profile(rings, T, v0, alpha=1.0, n=None, beta=1.0, eta=0.0)` |
| **Inputs** | rings (array), T (K array), v0 (km/s), alpha, n (cm⁻³), beta, eta |
| **Output** | DataFrame: ring, T, n, q_k, v_pred |
| **Formel** | `v_k = v_{k-1} × q_k^{-α/2}` |
| **Units** | v in km/s |

### 1.3 Frequency Track Prediction
| Funktion | `predict_frequency_track()` |
|----------|----------------------------|
| **Datei** | `ssz/segwave/seg_wave_propagation.py` |
| **Signatur** | `predict_frequency_track(nu_in, gamma_series)` |
| **Inputs** | nu_in (Hz), gamma_series (array) |
| **Output** | Series: nu_out (Hz) |
| **Formel** | `ν_out = ν_in × γ^{-1/2}` |
| **Units** | Hz |

### 1.4 Cumulative Gamma
| Funktion | `compute_cumulative_gamma()` |
|----------|------------------------------|
| **Datei** | `ssz/segwave/seg_wave_propagation.py` |
| **Signatur** | `compute_cumulative_gamma(q_series)` |
| **Inputs** | q_series (array) |
| **Output** | array: cumulative gamma |
| **Formel** | `γ_k = ∏_{i=1}^{k} q_i` |

---

## 2. Segment Density Methods (Xi)

### 2.1 Xi Strong Field
| Funktion | `Xi()` oder `xi_strong_field()` |
|----------|--------------------------------|
| **Datei** | StarMaps: `ssz_metric.py`, Core: `ssz_core.py` |
| **Signatur** | `Xi(r, r_s)` |
| **Inputs** | r (m), r_s (m) |
| **Output** | float: Ξ ∈ [0, 1) |
| **Formel** | `Ξ(r) = 1 - exp(-φ × r_s / r)` |
| **Units** | Dimensionless |
| **φ** | (1+√5)/2 ≈ 1.618034 |

### 2.2 Xi Weak Field
| Funktion | `xi_weak_field()` |
|----------|-------------------|
| **Formel** | `Ξ(r) = r_s/(2r)` |
| **Regime** | r/r_s > 110 |

### 2.3 Xi Blended (Hermite C²)
| Funktion | `xi_blended()` |
|----------|----------------|
| **Regime** | 90 < r/r_s < 110 |
| **Methode** | Quintic Hermite interpolation |

---

## 3. Time Dilation Methods

### 3.1 SSZ Time Dilation
| Funktion | `time_dilation_ssz()` / `D_SSZ()` |
|----------|-----------------------------------|
| **Formel** | `D_SSZ = 1/(1+Ξ)` |
| **Bei r_s** | D(r_s) = 0.555 (FINIT!) |

### 3.2 GR Time Dilation
| Funktion | `time_dilation_gr()` / `D_GR()` |
|----------|--------------------------------|
| **Formel** | `D_GR = √(1 - r_s/r)` |
| **Bei r_s** | D(r_s) = 0 (Singularität) |

---

## 4. Redshift Methods

### 4.1 Gravitational Redshift (GR)
| Funktion | `z_gravitational()` |
|----------|---------------------|
| **Datei** | `segspace_all_in_one_extended.py` |
| **Formel** | `z_GR = 1/√(1 - r_s/r) - 1` |
| **Inputs** | M_kg, r_m |

### 4.2 Special Relativistic Redshift
| Funktion | `z_special_rel()` |
|----------|-------------------|
| **Formel** | `z_SR = γ(1 + β_los) - 1` |
| **Inputs** | v_tot (m/s), v_los (m/s) |

### 4.3 Combined Redshift
| Funktion | `z_combined()` |
|----------|----------------|
| **Formel** | `z = (1+z_gr)(1+z_sr) - 1` |

### 4.4 SSZ Redshift Prediction
| Funktion | `z_seg_pred()` |
|----------|----------------|
| **Modes** | hybrid, deltaM, geodesic, hint |
| **Δ(M)** | `Δ = A×exp(-α×r_s) + B` |
| **A** | 98.01 |
| **α** | 2.7177e4 |
| **B** | 1.96 |

---

## 5. Comparison & Statistics Methods (core/)

### 5.1 Model Comparison
| Funktion | `compare_models()` |
|----------|-------------------|
| **Datei** | `core/compare.py` |
| **Metrics** | RMSE, MAE, AIC, BIC, Cliff's Delta |

### 5.2 Statistical Metrics
| Datei | `tools/metrics.py` |
|-------|-------------------|
| **Funktionen** | `rmse()`, `mae()`, `mape()`, `r_squared()`, `aic()`, `bic()`, `waic()`, `cliffs_delta()`, `cohens_d()` |

### 5.3 Bootstrap Inference
| Funktion | `infer_params_bootstrap()` |
|----------|---------------------------|
| **Datei** | `core/inference.py` |
| **Output** | α, β, η posterior distributions |

---

## 6. Validation Methods

### 6.1 Universal Intersection
| Funktion | `find_intersection()` |
|----------|----------------------|
| **Target** | r*/r_s = 1.594811 (korrigiert) |
| **D*** | 0.610710 |
| **Toleranz** | 0.01 |

### 6.2 PPN Parameters
| Test | β = γ = 1 (exakt) |
|------|-------------------|
| **Toleranz** | 1e-12 |

### 6.3 Energy Conditions
| Test | WEC, DEC, SEC, NEC |
|------|-------------------|
| **Methode** | Effective stress-energy tensor |

---

## 7. Data Fetching Methods

### 7.1 Gaia DR3
| Query | `queries/gaia_dr3_core.sql` |
|-------|---------------------------|
| **Spalten** | source_id, ra, dec, parallax, pmra, pmdec, radial_velocity, phot_g_mean_mag, bp_rp, ruwe |

### 7.2 ESO Spectroscopy
| Methode | HTTP fetch + CSV parse |
|---------|------------------------|

### 7.3 SIMBAD
| Methode | astroquery.simbad |
|---------|-------------------|

---

## 8. Key Constants

| Konstante | Wert | Einheit |
|-----------|------|---------|
| G | 6.67430e-11 | m³/(kg·s²) |
| c | 299792458 | m/s |
| M_☉ | 1.98847e30 | kg |
| φ | 1.618034 | - |
| α_fs | 7.2973525693e-3 | - |

---

## 9. Abhängigkeiten

```
numpy >= 1.20
pandas >= 1.3
scipy >= 1.7
matplotlib >= 3.4
plotly >= 5.0
astropy >= 5.0
astroquery >= 0.4
gradio >= 4.0
```

---

**Erstellt:** PHASE 0 Inventarisierung  
**Status:** ✅ Methoden inventarisiert
