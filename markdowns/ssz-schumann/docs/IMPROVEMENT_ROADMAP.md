# SSZ-Schumann Experiment: Verbesserungs-Roadmap

**Version:** 1.0  
**Datum:** 2025-12-08  
**Autoren:** Carmen Wrede & Lino Casu

---

## Executive Summary

Dieses Dokument beschreibt einen umfassenden Fahrplan zur Verbesserung des SSZ-Schumann-Experiments. 
Basierend auf:
- Aktueller Analyse der synthetischen Daten
- Maxwell-Gleichungen und Schumann-Resonanz-Theorie
- SSZ (Segmented Spacetime) Theorie
- Vergleich mit etablierter Physik

---

## 1. Theoretische Grundlagen

### 1.1 Maxwell-Gleichungen und Schumann-Resonanzen

Die Schumann-Resonanzen entstehen aus den Maxwell-Gleichungen in einer sphärischen Kavität:

**Ideale Resonanzfrequenz:**
```
f_n = (c / 2πR) × √(n(n+1))
```

**Beobachtete Frequenzen (mit Dämpfung η ≈ 0.74):**
```
f_n_obs = η × (c / 2πR) × √(n(n+1))

f₁ ≈ 7.83 Hz (Fundamental)
f₂ ≈ 14.3 Hz
f₃ ≈ 20.8 Hz
f₄ ≈ 27.3 Hz
f₅ ≈ 33.8 Hz
```

**Physikalische Ursachen für η < 1:**
1. Endliche Leitfähigkeit der Ionosphäre
2. Tag-Nacht-Asymmetrie
3. Magnetfeld-Variationen
4. Ionosphärische Störungen (SIDs, PCAs)
5. Erdradius-Variation (±11 km Pol-Äquator)

### 1.2 SSZ-Theorie Anwendung

**SSZ-Hypothese für Schumann-Resonanzen:**

Die SSZ-Theorie postuliert, dass Raumzeit-Segmentierung die effektive Lichtgeschwindigkeit modifiziert:

```
c_eff = c / (1 + δ_seg)
```

Dies führt zu einer Frequenzverschiebung:

```
f_n_SSZ = f_n_classical / (1 + δ_seg)
       = f_n_classical × (1 - δ_seg + O(δ_seg²))
```

**Schlüssel-Vorhersage:**
Die relative Frequenzverschiebung Δf/f sollte für ALLE Moden gleich sein:

```
Δf_n / f_n = -δ_seg / (1 + δ_seg) ≈ -δ_seg  (für kleine δ_seg)
```

### 1.3 Verbindung zu elektromagnetischer Pseudo-Krümmung

Neuere Arbeiten (arXiv:2501.12628) zeigen, dass elektromagnetische Felder als 
Raumzeit-Pseudo-Krümmung interpretiert werden können:

- Elektrische Ladungen erzeugen "Time Fission" (ladungsabhängige Zeitdilatation)
- Dies könnte mit SSZ-Segmentierung verbunden sein
- Ionosphärische Ladungsverteilung → lokale Raumzeit-Modifikation

---

## 2. Aktuelle Analyse-Ergebnisse

### 2.1 Synthetische Daten (Baseline)

| Metrik | Wert | Interpretation |
|--------|------|----------------|
| Mean δ_seg | 0.02% | Sehr klein |
| Std δ_seg | 1.36% | Rauschen dominiert |
| Mode-Korrelation | 0.46 | Moderat |
| SSZ-Score | 0.13 | Schwach/kein SSZ |
| F10.7-Korrelation | -0.12 | Sehr schwach |
| R² (Layered) | 0.014 | Kein Zusammenhang |

### 2.2 Identifizierte Probleme

1. **Signal-zu-Rausch-Verhältnis:** δ_seg-Signal zu schwach relativ zum Rauschen
2. **Mode-Korrelation:** Nur 0.46 statt >0.7 für SSZ-Signatur
3. **Proxy-Kopplung:** F10.7/Kp erklären fast keine Varianz
4. **Sensitivität:** Pipeline kann schwache SSZ-Signale nicht zuverlässig detektieren

---

## 3. Verbesserungs-Fahrplan

### Phase 1: Theoretische Vertiefung (Woche 1-2)

#### 3.1.1 Maxwell-basierte Frequenzformel erweitern

**Aktuelle Formel:**
```python
f_n = eta * c / (2*pi*R) * sqrt(n*(n+1))
```

**Erweiterte Formel mit physikalischen Korrekturen:**
```python
def f_n_extended(n, eta, h_iono, sigma_iono, B_field=None):
    """
    Erweiterte Schumann-Frequenz mit physikalischen Korrekturen.
    
    Args:
        n: Mode-Nummer
        eta: Basis-Dämpfungsfaktor
        h_iono: Ionosphärenhöhe (km)
        sigma_iono: Ionosphärische Leitfähigkeit (S/m)
        B_field: Erdmagnetfeld-Stärke (optional)
    
    Korrekturen:
        1. Höhenabhängigkeit: f ∝ 1/√(R + h_iono)
        2. Leitfähigkeits-Dämpfung: Q-Faktor
        3. Magnetfeld-Anisotropie (optional)
    """
    R_eff = EARTH_RADIUS + h_iono * 1e3
    
    # Basis-Frequenz
    f_base = C_LIGHT / (2 * np.pi * R_eff) * np.sqrt(n * (n + 1))
    
    # Leitfähigkeits-Korrektur (Skin-Depth)
    skin_depth = np.sqrt(2 / (MU_0 * sigma_iono * 2 * np.pi * f_base))
    eta_cond = 1 - h_iono * 1e3 / skin_depth  # Vereinfacht
    
    return eta * eta_cond * f_base
```

#### 3.1.2 SSZ-Metrik für EM-Wellen ableiten

**Neue Datei:** `ssz_schumann/models/ssz_em_metric.py`

```python
def ssz_em_metric(r, r_s, Xi_max=1.0):
    """
    SSZ-Metrik für elektromagnetische Wellen.
    
    Die effektive Lichtgeschwindigkeit in SSZ:
        c_eff(r) = c / sqrt(1 + Xi(r))
    
    wobei Xi(r) = Xi_max * (1 - exp(-phi * r_s / r))
    
    Für Schumann-Resonanzen:
        - r = Abstand vom Erdmittelpunkt
        - r_s = charakteristische Länge (Ionosphärenhöhe?)
        - Xi_max = maximale Segmentierung
    """
    phi = (1 + np.sqrt(5)) / 2  # Goldener Schnitt
    Xi = Xi_max * (1 - np.exp(-phi * r_s / r))
    c_eff = C_LIGHT / np.sqrt(1 + Xi)
    return c_eff, Xi
```

### Phase 2: Daten-Pipeline Verbesserung (Woche 2-3)

#### 3.2.1 Echte Daten-Integration

**Datenquellen:**
1. **Schumann-Daten:** Zenodo DOI 10.5281/zenodo.6348930 (Sierra Nevada, 2013-2017)
2. **F10.7:** NOAA/LASP Solar Flux
3. **Kp/Ap:** GFZ Potsdam Geomagnetic Indices
4. **Ionosphärenhöhe:** COSMIC/FORMOSAT-3 Daten
5. **Blitzaktivität:** WWLLN (World Wide Lightning Location Network)

**Neue Loader:**
```python
# ssz_schumann/data_io/ionosphere_height.py
def load_ionosphere_height(start, end, source='cosmic'):
    """Lade Ionosphärenhöhen-Daten."""
    pass

# ssz_schumann/data_io/lightning_wwlln.py  
def load_global_lightning_rate(start, end):
    """Lade globale Blitzrate von WWLLN."""
    pass
```

#### 3.2.2 Erweiterte Merge-Funktion

```python
def merge_all_extended(
    schumann_df,
    f107_df,
    kp_df,
    h_iono_df=None,
    lightning_df=None,
    time_resolution='1h',
):
    """
    Erweiterte Merge-Funktion mit allen Proxies.
    
    Neue Features:
        - Ionosphärenhöhe h_iono
        - Blitzrate lightning_rate
        - Abgeleitete Variablen:
            - d_h_iono/dt (Änderungsrate)
            - lightning_norm (normalisiert)
    """
    pass
```

### Phase 3: Modell-Erweiterungen (Woche 3-4)

#### 3.3.1 Physikalisch motiviertes SSZ-Modell

**Hypothese:** SSZ-Segmentierung ist proportional zur ionosphärischen Ladungsdichte

```python
def sigma_ssz_physical(
    h_iono,
    n_e,  # Elektronendichte
    T_e,  # Elektronentemperatur
    B_field,  # Magnetfeld
):
    """
    Physikalisch motivierte SSZ-Segmentierung.
    
    Basierend auf:
        - Plasma-Frequenz: f_p = sqrt(n_e * e² / (epsilon_0 * m_e))
        - Gyro-Frequenz: f_g = e * B / (2*pi*m_e)
        - Kollisionsfrequenz: nu = f(T_e, n_neutral)
    
    SSZ-Ansatz:
        sigma_ssz = alpha * (f_p / f_schumann)² * (1 + beta * f_g/f_p)
    """
    pass
```

#### 3.3.2 Multi-Layer SSZ-Modell

```python
class MultiLayerSSZModel:
    """
    Erweitertes Schichtmodell mit physikalischen Parametern.
    
    Schichten:
        1. Troposphäre (0-12 km): sigma_tropo ≈ 0
        2. Stratosphäre (12-50 km): sigma_strato ≈ 0
        3. Mesosphäre (50-85 km): sigma_meso ~ f(T, UV)
        4. D-Schicht (60-90 km): sigma_D ~ f(X-rays, Lyman-alpha)
        5. E-Schicht (90-150 km): sigma_E ~ f(UV, particles)
        6. F-Schicht (150-500 km): sigma_F ~ f(EUV, solar wind)
    
    Jede Schicht hat:
        - Höhe h_i
        - Gewicht w_i
        - Segmentierung sigma_i(t)
        - Proxy-Abhängigkeit
    """
    
    def __init__(self):
        self.layers = [
            LayerConfig('D', h_min=60, h_max=90, weight=0.3),
            LayerConfig('E', h_min=90, h_max=150, weight=0.5),
            LayerConfig('F', h_min=150, h_max=500, weight=0.2),
        ]
    
    def compute_effective_sigma(self, proxies):
        """Berechne effektive Segmentierung aus allen Schichten."""
        pass
```

### Phase 4: Analyse-Verbesserungen (Woche 4-5)

#### 3.4.1 Erweiterte Mode-Konsistenz-Analyse

```python
def check_mode_consistency_extended(
    delta_seg_dict,
    frequencies_dict,
    proxies_df,
):
    """
    Erweiterte Mode-Konsistenz-Prüfung.
    
    Neue Metriken:
        1. Phasen-Kohärenz zwischen Moden
        2. Spektrale Kohärenz (Fourier)
        3. Wavelet-Kohärenz (zeitaufgelöst)
        4. Granger-Kausalität (Mode → Proxy)
        5. Transfer-Entropie
    
    Returns:
        - Alle bisherigen Metriken
        - phase_coherence: Phasen-Übereinstimmung
        - spectral_coherence: Frequenz-Kohärenz
        - wavelet_coherence: Zeit-Frequenz-Kohärenz
        - granger_causality: Kausalitäts-Test
    """
    pass
```

#### 3.4.2 Bayesianische Modell-Selektion

```python
def bayesian_model_comparison(
    data,
    models=['classical', 'ssz_simple', 'ssz_layered', 'ssz_physical'],
):
    """
    Bayesianischer Modellvergleich.
    
    Berechnet:
        - Bayes-Faktoren
        - Posterior Model Probabilities
        - WAIC/LOO-CV für Modellselektion
    
    Verwendet PyMC oder Stan für MCMC.
    """
    pass
```

### Phase 5: Validierung & Publikation (Woche 5-6)

#### 3.5.1 Robustheits-Tests

```python
def run_robustness_suite():
    """
    Umfassende Robustheits-Tests.
    
    Tests:
        1. Bootstrap-Konfidenzintervalle
        2. Jackknife-Schätzung
        3. Cross-Validation (zeitlich)
        4. Sensitivität auf Hyperparameter
        5. Null-Hypothesen-Tests (Permutation)
    """
    pass
```

#### 3.5.2 Vergleich mit anderen Theorien

| Theorie | Vorhersage | Testbar? |
|---------|------------|----------|
| **Klassisch (Maxwell)** | f_n = η × c/(2πR) × √(n(n+1)) | ✓ Baseline |
| **SSZ** | Δf/f mode-unabhängig | ✓ Mode-Korrelation |
| **EM-Pseudo-Krümmung** | Ladungsabhängige Zeitdilatation | ? Indirekt |
| **Kaluza-Klein** | Extra-Dimensionen | ✗ Nicht direkt |

---

## 4. Konkrete Implementierungs-Aufgaben

### 4.1 Iteration 2 - Entkopplung η₀ & δ_seg (ABGESCHLOSSEN)

- [x] **T1:** Zentrale Konfiguration mit ClassicalParams und SSZParams
- [x] **T2:** Zwei-Stufen-Kalibrierung (eta_mode: full_fit, quiet_interval, fixed)
- [x] **T3:** Joint-Fit Modell (eta_0 + delta_seg Parameter)
- [x] **T4:** T_SSZ Test-Statistik mit klarer Definition
- [x] **T5:** Null-Hypothesen-Ensemble (shuffle, phase_randomize, noise)
- [x] **T6:** P-Wert-Berechnung und Signifikanz-Test
- [x] **T7:** Reconstruction Method Comparison Report
- [x] **T8:** Hauptanalyse-Script mit CLI (run_analysis.py)
- [x] **T9:** SSZ_FORMULAS.md mit T_SSZ und Kalibrierungsmethoden

### 4.2 Kurzfristig (Diese Woche) - ABGESCHLOSSEN

- [x] **T10:** Echte Space Weather Daten (F10.7, Kp) herunterladen
- [x] **T11:** Realistische Schumann-Daten generieren
- [x] **T12:** Sensitivitätskurven mit P-Werten (`scripts/run_sensitivity_analysis.py`)
- [x] **T13:** Detektionsschwelle bestimmen (1% bei 1% Rauschen)

### 4.3 Mittelfristig (2 Wochen) - ABGESCHLOSSEN

- [ ] **T14:** Echte Schumann-Daten von Zenodo laden (ausstehend: 26.5 GB Download)
- [x] **T15:** Multi-Layer SSZ-Modell (`ssz_schumann/models/multi_layer_ssz.py`)
- [x] **T16:** Bayesianische Modellselektion (`ssz_schumann/analysis/bayesian_selection.py`)
- [x] **T17:** Spektrale Kohärenz-Analyse (`ssz_schumann/analysis/spectral_coherence.py`)
- [x] **T18:** Granger-Kausalitäts-Tests (in `spectral_coherence.py`)

### 4.3.1 Progress 2025-12-08 - T1-T4 Implementation

**Implemented Tasks:**

- [x] **T1:** Extended classical frequency formula (geometry-aware)
  - `f_n_classical_extended()`: Explicit ionospheric height parameter
  - `f_n_classical_with_latitude()`: Latitude-dependent ionosphere
  - `f_n_classical_diurnal()`: Day/night variation model
  - Backward compatible with original `f_n_classical()`

- [x] **T2:** Standardized data structure and pipeline
  - `ssz_schumann/data_io/data_loader.py`: Unified data loader
  - `SchumannDataSchema`: Data contract validation
  - `load_schumann_timeseries()`: Single entry point for all data
  - `ssz_schumann/analysis/pipeline.py`: Unified analysis pipeline
  - `run_full_pipeline()`: Complete analysis in one call
  - `PipelineConfig` and `PipelineResult` dataclasses

- [x] **T3:** Real data hooks
  - `load_real_schumann_data()`: Placeholder with clear error message
  - CSV format documented in QUICKSTART.md
  - `--dataset` CLI option prepared

- [x] **T4:** SSZ signature diagnostics
  - `ssz_schumann/analysis/ssz_diagnostics.py`: New module
  - `compute_relative_shifts()`: Mode-wise relative shifts
  - `check_mode_independence()`: SSZ signature test
  - `compute_delta_seg_with_confidence()`: Confidence bands
  - `detect_dispersion_pattern()`: Classical vs SSZ discrimination
  - `generate_diagnostic_report()`: Comprehensive report

**Tests Added:**
- `tests/test_t1_t4_implementation.py`: 22 new tests
- All 157 tests passing (135 existing + 22 new)

**Remaining Limitations:**
- Real data loading requires manual CSV preparation
- Zenodo download (26.5 GB) not automated
- T14 (real Schumann data) still pending

### 4.4 Langfristig (1 Monat)

- [ ] **T19:** Paper-Draft für arXiv
- [ ] **T20:** Reproduzierbarkeits-Paket
- [ ] **T21:** Interaktives Dashboard (Streamlit/Dash)
- [ ] **T22:** Vergleich mit anderen Observatorien
- [ ] **T23:** Vorhersage-Modell für Schumann-Frequenzen

### 4.5 Nächste Schritte für Real-Data SSZ Limits

1. **Daten-Akquisition:** Sierra Nevada Dataset (26.5 GB) herunterladen
2. **Preprocessing:** Qualitätskontrolle, Outlier-Entfernung
3. **Kalibrierung:** eta_0 auf quiet interval kalibrieren
4. **Analyse:** T_SSZ berechnen, P-Wert bestimmen
5. **Interpretation:** Obergrenze für δ_seg bei gegebenem Konfidenzniveau

---

## 5. Erwartete Ergebnisse

### 5.1 Positive SSZ-Detektion (falls vorhanden)

Wenn SSZ-Effekte existieren, erwarten wir:
- Mode-Korrelation > 0.7
- SSZ-Score > 0.7
- Konsistente Δf/f über alle Moden
- Korrelation mit ionosphärischen Proxies

### 5.2 Null-Ergebnis (kein SSZ)

Wenn keine SSZ-Effekte:
- Mode-Korrelation < 0.5
- SSZ-Score < 0.3
- Frequenzvariationen durch klassische Effekte erklärbar
- **Wichtig:** Obere Grenze für δ_seg bestimmen

### 5.3 Wissenschaftlicher Wert

Beide Ergebnisse sind wertvoll:
- **Positiv:** Erster Nachweis von SSZ in EM-Wellen
- **Negativ:** Strenge Obergrenze für SSZ-Effekte bei ELF

---

## 6. Ressourcen & Referenzen

### 6.1 Datenquellen

| Quelle | URL | Daten |
|--------|-----|-------|
| Zenodo Schumann | doi:10.5281/zenodo.6348930 | f1, f2, f3 (2013-2017) |
| NOAA F10.7 | ftp://ftp.swpc.noaa.gov | Solar Flux |
| GFZ Kp/Ap | https://www.gfz-potsdam.de | Geomagnetik |
| WWLLN | http://wwlln.net | Blitzaktivität |
| COSMIC | https://cdaac-www.cosmic.ucar.edu | Ionosphäre |

### 6.2 Literatur

1. Schumann, W.O. (1952). "Über die strahlungslosen Eigenschwingungen einer leitenden Kugel"
2. Balser & Wagner (1960). "Observations of Earth-ionosphere cavity resonances"
3. Williams, E.R. (1992). "The Schumann Resonance: A Global Tropical Thermometer"
4. Nickolaenko & Hayakawa (2002). "Resonances in the Earth-Ionosphere Cavity"
5. arXiv:2501.12628 - "Electromagnetism as Spacetime Pseudo-Curvature"

### 6.3 Code-Referenzen

- `ssz-metric-pure`: Korrekte SSZ-Formeln
- `Segmented-Spacetime-Mass-Projection-Unified-Results`: Validierte SSZ-Implementierung
- `segmented-energy`: Energie-Framework

---

## 7. Zeitplan

```
Woche 1: Theoretische Grundlagen & Maxwell-Erweiterung
Woche 2: Echte Daten-Integration
Woche 3: Multi-Layer Modell
Woche 4: Erweiterte Analyse-Methoden
Woche 5: Validierung & Robustheits-Tests
Woche 6: Dokumentation & Paper-Draft
```

---

## 8. Erfolgs-Kriterien

| Kriterium | Minimum | Ziel | Stretch |
|-----------|---------|------|---------|
| Tests bestanden | 100% | 100% | 100% |
| Code-Coverage | 70% | 85% | 95% |
| Dokumentation | API-Ref | + Theory | + Paper |
| Echte Daten | 1 Jahr | 4 Jahre | + andere Stationen |
| SSZ-Sensitivität | 1% | 0.1% | 0.01% |

---

**Nächster Schritt:** Implementierung von Task T1 (Erweiterte Frequenzformel)

---

© 2025 Carmen Wrede & Lino Casu  
Licensed under the Anti-Capitalist Software License v1.4
