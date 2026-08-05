# SSZ Calculation Suite - Erweiterungsplan

## Aktueller Stand

### ✅ Vorhanden
| Modul | Funktion |
|-------|----------|
| `xi.py` | xi_weak, xi_strong, xi_blended, xi_auto |
| `dilation.py` | D_ssz, D_gr, D_comparison |
| `redshift.py` | z_gravitational, z_sr, z_combined, z_ssz, z_geom_hint, delta_m_correction |
| `ppn.py` | light_deflection, shapiro_delay, perihelion_precession |
| `power_law.py` | Power-law Vorhersagen |
| `core.py` | calculate_single, calculate_all, summary_statistics |

---

## 🚀 ERWEITERUNGEN (Priorität)

### 1. HOHE PRIORITÄT - Experimentelle Validierung

#### 1.1 GPS-Zeitdrift Berechnung
```python
def gps_time_drift(altitude_m: float, orbital_period_h: float = 12.0) -> Dict:
    """
    GPS Satellit Zeitdrift pro Tag.
    
    Erwartet: ~45 μs/Tag (GR: 45.9, SSZ: ~45.7)
    """
```
**Status:** In ssz-qubits vorhanden, fehlt hier

#### 1.2 Pound-Rebka Experiment
```python
def pound_rebka(height_m: float = 22.5) -> Dict:
    """
    Gravitationsrotverschiebung im Labor.
    
    Erwartet: Δf/f = 2.46×10⁻¹⁵
    """
```
**Status:** In ssz-qubits vorhanden, fehlt hier

#### 1.3 Cassini Shapiro-Delay
```python
def cassini_shapiro_test() -> Dict:
    """
    γ = 1 + (2.1±2.3)×10⁻⁵
    """
```
**Status:** Teilweise in ppn.py

---

### 2. MITTLERE PRIORITÄT - Erweiterte Physik

#### 2.1 Schwarzschild-Metrik Komponenten
```python
def ssz_metric_components(r_m: float, M_kg: float) -> Dict:
    """
    g_tt, g_rr, g_θθ, g_φφ für SSZ-Metrik.
    
    SSZ: g_tt = -D²(r) = -1/(1+Ξ)²
    """
```

#### 2.2 Geodäten-Integration
```python
def null_geodesic(M_kg: float, b_m: float, ...) -> Dict:
    """
    Lichtstrahl-Trajektorie durch SSZ-Metrik.
    """

def timelike_geodesic(M_kg: float, E: float, L: float, ...) -> Dict:
    """
    Massive Teilchen-Trajektorie.
    """
```

#### 2.3 Black Hole Shadow
```python
def black_hole_shadow_radius(M_kg: float) -> Dict:
    """
    Photon sphere Radius und Schattenwinkel.
    
    SSZ: r_ph = 3M (wie GR), aber D(r_ph) ≠ 0!
    """
```

#### 2.4 Hawking Temperatur (SSZ-modifiziert)
```python
def hawking_temperature_ssz(M_kg: float) -> Dict:
    """
    T_H = ħc³/(8πGMk_B) × D(r_s)
    
    SSZ: FINIT wegen D(r_s) = 0.555!
    """
```

---

### 3. NIEDRIGE PRIORITÄT - Quanten-Erweiterungen

#### 3.1 Qubit Dekoherenz
```python
@dataclass
class Qubit:
    x: float
    y: float
    z: float
    T2: float = 100e-6
    
def qubit_decoherence_factor(q: Qubit) -> float:
    """
    SSZ-basierte Dekoherenz-Vorhersage.
    """
```

#### 3.2 Gate-Timing Korrektur
```python
def gate_timing_correction(q1: Qubit, q2: Qubit) -> float:
    """
    Δt = t_gate × (D₁ - D₂)
    """
```

---

### 4. VALIDIERUNGS-TESTS

#### 4.1 Fehlende Tests
```python
# test_gps_validation.py
def test_gps_drift_matches_observation():
    """GPS: 45.9 μs/Tag ± 0.1"""
    
def test_pound_rebka_matches_harvard():
    """Δf/f = 2.46×10⁻¹⁵ ± 1%"""
    
def test_cassini_gamma():
    """γ = 1.000021 ± 0.000023"""
    
def test_mercury_perihelion():
    """42.98 arcsec/century ± 0.04"""
    
def test_s2_star_orbit():
    """ESO Daten: 97.9% SSZ wins"""
```

#### 4.2 Astronomische Objekte
```python
# Neue Validierungsdaten
VALIDATION_OBJECTS = {
    "GPS_satellite": {...},
    "Pound_Rebka": {...},
    "Mercury": {...},
    "Cassini": {...},
    "Sgr_A*": {...},
    "M87*": {...},
}
```

---

### 5. KOSMOLOGIE-ERWEITERUNGEN

#### 5.1 Kosmologische Rotverschiebung
```python
def z_cosmological_ssz(a: float) -> float:
    """
    z = 1/a - 1 mit SSZ-Modifikation für große Skalen.
    """
```

#### 5.2 Rotationskurven
```python
def rotation_curve_modifier(r_kpc: float, M_gal: float) -> float:
    """
    v_mod = γ^(-p) für Galaxie-Rotation.
    """
```

---

## 📊 NEUE PLOTS

| Plot | Beschreibung |
|------|--------------|
| `gps_drift_comparison.png` | GPS Drift: SSZ vs GR vs Messung |
| `pound_rebka_residuals.png` | Pound-Rebka Genauigkeit |
| `perihelion_precession.png` | Merkur Periheldrehung |
| `bh_shadow_ssz_vs_gr.png` | Black Hole Shadow Vergleich |
| `hawking_temperature.png` | T_H(M) - SSZ bleibt finit! |

---

## 🛠️ IMPLEMENTIERUNGS-REIHENFOLGE

1. **Phase 1 (1-2 Tage)**
   - [ ] GPS-Zeitdrift Funktion
   - [ ] Pound-Rebka Funktion
   - [ ] Tests für beide

2. **Phase 2 (2-3 Tage)**
   - [ ] Metrik-Komponenten Modul
   - [ ] Geodäten-Integration
   - [ ] Black Hole Shadow

3. **Phase 3 (3-5 Tage)**
   - [ ] Qubit-Modul portieren
   - [ ] Hawking Temperatur
   - [ ] Kosmologie-Erweiterungen

4. **Phase 4 (1 Tag)**
   - [ ] Alle neuen Plots
   - [ ] Dokumentation Update
   - [ ] README aktualisieren

---

## 📚 QUELLEN

| Funktion | Quelle |
|----------|--------|
| GPS/Pound-Rebka | `ssz-qubits/ssz_qubits.py` |
| Geodäten | `ssz-metric-pure/geodesics_compact.py` |
| Metrik-Tensor | `ssz-metric-pure/src/sszviz.py` |
| Kosmologie | `Unified-Results/segwave_kernel.py` |

---

*Erstellt: 2025-01-17*
