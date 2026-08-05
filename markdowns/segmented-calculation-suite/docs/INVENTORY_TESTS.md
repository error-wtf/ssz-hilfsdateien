# INVENTORY: SSZ Test Suite

**PHASE 0 Deliverable - Systematische Test-Inventarisierung**  
**Quelle:** `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\`

---

## Übersicht

| Kategorie | Tests | Status |
|-----------|-------|--------|
| Physics Tests | 35 | ✅ |
| Technical Tests | 23 | ✅ |
| Multi-Ring Validation | 11 | ✅ |
| Smoke Tests | 7 | ✅ |
| **GESAMT** | **76+** | ✅ |

---

## 1. Root-Level Physics Tests (6)

### test_ppn_exact.py
| Test | PPN Parameters β, γ Exactness |
|------|------------------------------|
| **Input** | SSZ metric functions |
| **Expected** | β = γ = 1.000000000000 |
| **Toleranz** | 1e-12 |
| **Output** | Pass/Fail + physical interpretation |

### test_vfall_duality.py
| Test | Dual Velocity Invariant |
|------|------------------------|
| **Expected** | v_esc × v_fall = c² |
| **Output** | Table with γ values |

### test_energy_conditions.py
| Test | WEC/DEC/SEC/NEC |
|------|-----------------|
| **Output** | ρ, p_r, p_t values + condition checks |

### test_c1_segments.py
| Test | C1 Continuity at Segment Joins |
|------|-------------------------------|
| **Method** | Cubic Hermite blend |

### test_c2_segments_strict.py
| Test | C2 Strict Continuity |
|------|---------------------|
| **Method** | Quintic Hermite with analytic derivatives |

### test_c2_curvature_proxy.py
| Test | C2 + Curvature Proxy Smoothness |
|------|--------------------------------|
| **Expected** | Curvature proxy ≈ 10⁻¹⁵ |

---

## 2. tests/test_segwave_core.py (16 Tests)

### TestQFactor (3 Tests)
| Test | Beschreibung | Expected |
|------|--------------|----------|
| `test_temperature_only_basic` | q_k mit T only, β=1 | q = 0.8 (T=80/100) |
| `test_temperature_with_beta` | q_k mit β=2 | q = 0.64 |
| `test_temperature_and_density` | q_k mit T und n | q = 0.8 × √0.5 |

### TestVelocityProfile (5 Tests)
| Test | Beschreibung | Expected |
|------|--------------|----------|
| `test_single_shell` | Initial condition | v[0] = v0 |
| `test_two_shells_alpha_one` | Two-shell propagation | v_k = v_{k-1} × q_k^{-0.5} |
| `test_deterministic_chain` | 5-ring chain | Deterministic evolution |
| `test_alpha_zero_constant_velocity` | Classical limit α=0 | v = const |
| `test_with_density` | T + n combined | Combined effect |

### TestFrequencyTrack (2 Tests)
| Test | Beschreibung | Expected |
|------|--------------|----------|
| `test_single_gamma` | Single γ redshift | ν_out = ν_in × γ^{-0.5} |
| `test_frequency_decreases_with_gamma` | γ sequence | Decreasing frequency |

### TestResiduals (3 Tests)
| Test | Beschreibung | Expected |
|------|--------------|----------|
| `test_perfect_match` | Zero residuals | MAE = RMSE = 0 |
| `test_systematic_bias` | Constant offset | MAE = |bias| |
| `test_mixed_residuals` | Mixed signs | Positive RMSE |

### TestCumulativeGamma (3 Tests)
| Test | Beschreibung | Expected |
|------|--------------|----------|
| `test_constant_q` | Exponential growth | γ_k = q^k |
| `test_all_ones` | Isothermal | γ_k = 1 |
| `test_increasing_sequence` | Heating trend | γ increases |

---

## 3. tests/test_segwave_cli.py (16 Tests - Silent)

### TestCLIBasic (3 Tests)
- Help argument
- Required args validation
- Invalid path handling

### TestCLIExecution (4 Tests)
- Fixed alpha mode
- Fit alpha mode
- Frequency tracking
- Exponent variations

### TestCLIValidation (2 Tests)
- Negative value rejection
- Mutually exclusive args

### TestBundledDatasets (7 Tests)
- Dataset file existence
- CSV loading
- Column validation

---

## 4. tests/test_ssz_real_data_comprehensive.py (11 Tests)

### Multi-Ring Validation
| Datensatz | Objekt | Tests |
|-----------|--------|-------|
| G79 | LBV Nebula G79.29+0.46 | 3 |
| Cygnus X | Diamond Ring | 3 |
| Generic | Sample objects | 5 |

---

## 5. scripts/tests/ (16 Tests)

### test_ssz_kernel.py (4 Tests)
| Test | Beschreibung |
|------|--------------|
| Kernel initialization | SSZ kernel setup |
| Field computation | γ-field calculation |
| Boundary conditions | Edge handling |
| Numerical stability | Overflow/underflow |

### test_ssz_invariants.py (6 Tests)
| Test | Beschreibung |
|------|--------------|
| Energy conservation | E_total constant |
| Momentum conservation | p_total constant |
| Angular momentum | L_total constant |
| Metric signature | (-,+,+,+) |
| Determinant | det(g) correct |
| Symmetry | g_μν = g_νμ |

### test_segmenter.py (2 Tests)
| Test | Beschreibung |
|------|--------------|
| Segment creation | Ring structure |
| Segment merging | Adjacent merge |

### test_cosmo_multibody.py (3 Tests)
| Test | Beschreibung |
|------|--------------|
| Two-body | Binary system |
| Three-body | Triple system |
| N-body | Cluster |

---

## 6. Validation Output Tests

### validation_complete/
| Datei | Inhalt |
|-------|--------|
| `intersection_*.csv` | GR-SSZ intersection points |
| `energy_*.csv` | Energy condition results |
| `ppn_*.json` | PPN parameter validation |

---

## 7. Test-Toleranzen

| Größe | Toleranz | Einheit |
|-------|----------|---------|
| r*/r_s | ±0.01 | - |
| D* | ±0.01 | - |
| PPN β, γ | 1e-12 | - |
| RMSE | 0.5 | km/s |
| MAE | 0.3 | km/s |
| z deviation | 1e-6 | - |

---

## 8. Test-Daten

### Haupt-Datensätze
| Datei | Objekte | Spalten |
|-------|---------|---------|
| `real_data_full.csv` | 129+ | case, M_solar, r_emit_m, v_tot_mps, z_obs |
| `real_data_emission_lines_clean.csv` | 47 | ESO spectroscopy |
| `real_data_blackholes_comprehensive.csv` | 81 | Black hole configs |

### Ring-Datensätze
| Datei | Objekt |
|-------|--------|
| `G79_Rizzo2014_NH3_Table1.csv` | G79.29+0.46 |
| `CygnusX_Diamond_Ring.csv` | Cygnus X |

---

## 9. Test-Ausführung

### Alle Tests
```bash
pytest tests/ -s -v
python run_testsuite.py --all
```

### Nur Physics Tests
```bash
pytest tests/test_segwave_core.py -s -v
python test_ppn_exact.py
```

### Nur Validation
```bash
python run_ssz_validation.py
```

---

## 10. Akzeptanzkriterien (für neue Suite)

| Kriterium | Anforderung |
|-----------|-------------|
| Legacy-Parity | 100% gleiche Pass/Fail wie Original |
| Report-Format | MD + JSON exportierbar |
| Toleranzen | Identisch wie Original |
| Determinismus | Reproduzierbare Ergebnisse |

---

**Erstellt:** PHASE 0 Inventarisierung  
**Status:** ✅ Tests inventarisiert
