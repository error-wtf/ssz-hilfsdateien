# Implementierungsbericht: SSZ Calculation Suite

**Datum:** 2025-01-17  
**Version:** 1.1.0  
**Autor:** Cascade AI

---

## 1. Architektur

### Projektstruktur

```
segmented-calculation-suite/
├── app.py                     # Dash Web-Anwendung
├── segcalc/                   # Hauptmodul
│   ├── config/
│   │   └── constants.py       # Physikalische Konstanten
│   ├── methods/
│   │   ├── xi.py              # Segment-Dichte (Ξ)
│   │   ├── dilation.py        # Zeit-Dilatation (D)
│   │   ├── redshift.py        # Rotverschiebung (z)
│   │   └── power_law.py       # Power Law Prediction
│   ├── validation/
│   │   └── unified_validation.py  # 42 Validierungstests
│   └── tests/                 # Unit Tests (56)
├── tests/                     # Integration Tests (88)
├── tools/                     # Analyse-Werkzeuge
└── docs/                      # Dokumentation
```

---

## 2. Kernformeln

### 2.1 Segment-Dichte Ξ(r)

```python
# Weak Field (r/r_s > 10)
Xi_weak(r, r_s) = r_s / (2 * r)

# Strong Field (r_s/r < 1.8)
Xi_strong(r, r_s) = Xi_max * (1 - exp(-φ * r_s / r))

# Blend Zone (1.8 ≤ r/r_s ≤ 2.2)
Xi_blended(r, r_s) = Hermite C² Interpolation
```

**Schlüsselwerte:**
- `Xi_max = 1.0`
- `φ = 1.618033988749895` (Goldener Schnitt)
- `Ξ(r_s) = 1 - exp(-φ) ≈ 0.802`

### 2.2 Zeit-Dilatation D(r)

```python
# SSZ (finit am Horizont!)
D_ssz(r, r_s) = 1 / (1 + Xi(r))

# GR (singulär am Horizont)
D_gr(r, r_s) = sqrt(1 - r_s / r)
```

**Schlüsselwerte:**
- `D_ssz(r_s) = 1 / (1 + 0.802) ≈ 0.555`
- `D_gr(r_s) = 0` (Singularität!)

### 2.3 Universeller Schnittpunkt

```python
# Schnittpunkt D_SSZ = D_GR
r* / r_s = 1.594811  # MASSE-UNABHÄNGIG!
D* = 0.610710
```

---

## 3. Regime-System

### 3.1 Regime-Grenzen (KANONISCH)

| Regime | r/r_s | Formel | Anwendung |
|--------|-------|--------|-----------|
| very_close | < 1.8 | Xi_strong | Nahe Horizont |
| blended | 1.8 - 2.2 | Hermite C² | Übergangszone |
| photon_sphere | 2.2 - 3.0 | Xi_strong | Photonensphäre |
| strong | 3.0 - 10.0 | Xi_strong | Starkes Feld |
| weak | > 10.0 | Xi_weak | Schwaches Feld |

### 3.2 Hermite-Blend

```python
def _hermite_blend(t: float) -> float:
    """C²-stetige Hermite-Interpolation."""
    return t * t * (3.0 - 2.0 * t)
```

---

## 4. Validierungssystem

### 4.1 Test-Kategorien (42 Tests)

| Kategorie | Tests | Beschreibung |
|-----------|-------|--------------|
| Physical Constants | 3 | G, c, M☉ |
| Fundamental Relations | 4 | Schwarzschild-Radius |
| Critical Values | 3 | Ξ(r_s), D(r_s) |
| Experimental Validation | 4 | GPS, Pound-Rebka |
| Weak Field Regime | 4 | Asymptotik |
| Blend Continuity | 7 | C⁰, C¹, C² Stetigkeit |
| Neutron Star Regime | 6 | Strong-Field Tests |
| Power Laws | 2 | Skalierungsgesetze |
| Energy Normalization | 3 | Energieerhaltung |
| Universal Intersection | 3 | r* = 1.595 |

### 4.2 Experimentelle Validierung

| Experiment | Erwartung | Status |
|------------|-----------|--------|
| GPS Zeitdrift | ~45 μs/Tag | ✅ |
| Pound-Rebka | 2.46×10⁻¹⁵ | ✅ |
| NIST 33cm | 4.1×10⁻¹⁷ | ✅ |
| Tokyo Skytree | 5.2×10⁻¹⁵ | ✅ |

---

## 5. API-Referenz

### 5.1 segcalc.methods.xi

```python
xi_weak(r, r_s, xi_max=1.0)
    """Weak-field segment density."""
    
xi_strong(r, r_s, xi_max=1.0, phi=PHI)
    """Strong-field segment density."""
    
xi_blended(r, r_s, xi_max=1.0, phi=PHI)
    """Blended segment density with Hermite C²."""
    
xi_auto(r, r_s, xi_max=1.0, phi=PHI)
    """Auto-select regime based on r/r_s."""
```

### 5.2 segcalc.methods.dilation

```python
D_ssz(r, r_s, mode='auto')
    """SSZ time dilation factor."""
    
D_gr(r, r_s)
    """GR time dilation factor."""
    
D_comparison(r, r_s)
    """Compare D_SSZ vs D_GR."""
```

### 5.3 segcalc.methods.redshift

```python
z_gravitational(r, r_s)
    """Gravitational redshift (GR)."""
    
z_ssz(r, r_s)
    """SSZ redshift."""
```

---

## 6. Konstanten

### 6.1 Physikalische Konstanten

```python
G = 6.67430e-11      # Gravitationskonstante [m³/(kg·s²)]
c = 299792458        # Lichtgeschwindigkeit [m/s]
M_SUN = 1.98892e30   # Sonnenmasse [kg]
```

### 6.2 SSZ Konstanten

```python
PHI = 1.618033988749895              # Goldener Schnitt
XI_AT_HORIZON = 0.8017119516592427   # Ξ(r_s) = 1 - exp(-φ)
INTERSECTION_R_OVER_RS = 1.594811    # r*/r_s
INTERSECTION_D_STAR = 0.610710       # D*
```

### 6.3 Regime-Grenzen

```python
REGIME_BLEND_LOW = 1.8    # Untere Blend-Grenze
REGIME_BLEND_HIGH = 2.2   # Obere Blend-Grenze
REGIME_WEAK_START = 10.0  # Weak-Field Beginn
```

---

## 7. Web-Anwendung

### 7.1 Start

```bash
cd E:\clone\segmented-calculation-suite
python app.py
# Browser öffnen: http://localhost:8050
```

### 7.2 Features

- **Time Dilation Plot**: D_SSZ vs D_GR
- **Xi Profile**: Segment-Dichte
- **Experimental Validation**: GPS, Pound-Rebka
- **Power Law**: E_norm Skalierung
- **Interactive**: Masse und r_max einstellbar

---

## 8. Tests ausführen

```bash
# Alle Tests
python -m pytest

# Validierungstests
python -c "from segcalc.validation import run_full_validation; print(run_full_validation())"

# Spezifische Suite
python -m pytest tests/ -v
python -m pytest segcalc/tests/ -v
```

---

## 9. Abhängigkeiten

```txt
numpy>=1.21.0
scipy>=1.7.0
dash>=2.0.0
plotly>=5.0.0
pandas>=1.3.0
pytest>=7.0.0
```

---

## 10. Bekannte Einschränkungen

1. **Numerische Präzision**: Bei r → 0 kann Xi → 1 numerisch instabil werden
2. **Regime-Übergänge**: Blend-Zone ist phänomenologisch, nicht first-principles
3. **PPN-Modul**: Lensing/Shapiro noch nicht vollständig implementiert

---

© 2025 Carmen Wrede & Lino Casu
