# SSZ Data Acquisition Guide - KOMPLETT

**KRITISCH: Lesen Sie dieses Dokument VOLLSTÄNDIG bevor Sie Daten integrieren!**

Basiert auf den validierten Erkenntnissen aus:
- `Segmented-Spacetime-Mass-Projection-Unified-Results/`
- `Segmented-Spacetime-StarMaps/`
- `g79-cygnus-test/`

---

## 🚨 EXECUTIVE SUMMARY

**Nicht alle astronomischen Daten sind für SSZ-Validierung geeignet!**

| Quelle | Erfolgsrate | Verwendung |
|--------|-------------|------------|
| **ESO Spectroscopy** | **97.9%** | **PRIMÄR für SSZ** |
| **ALMA/AKARI** | Hoch | Spezielle Anwendungen |
| GAIA/NED/SIMBAD | **51%** | NUR Positionen/Lookup |

**GOLDEN RULE:** Für SSZ-Validierung **IMMER** ESO Spectroscopy verwenden!

---

## 1. DATENQUELLEN-HIERARCHIE

### 🏆 PRIMARY DATA (97.9% Validation)

```
├── ESO Spectroscopy
│   ├── GRAVITY (NIR, 2-2.4 μm) → S2/S4/S5 bei Sgr A*
│   ├── XSHOOTER (UV-NIR) → Brγ Emission (2.166 μm)
│   └── Result: 46/47 Wins (97.9%, p<0.0001)
│
├── ALMA (Sub-mm)
│   ├── 84-950 GHz Interferometrie
│   ├── Molekulare Linien, Kinematik
│   └── EHT M87* Ring-Daten
│
└── AKARI (IR 2-160 μm)
    ├── Diffuse Emission Maps
    ├── Temperatur/Dichte-Struktur
    └── G79.29+0.46, Diamond Ring
```

**Warum PRIMARY:**
- ✅ Misst EXAKT was SSZ vorhersagt
- ✅ Sub-Prozent Präzision (λ/Δλ > 10,000)
- ✅ Vollständige Parameter (M, r, v, λ, z)
- ✅ Direkte Messungen (keine Schätzungen)

### ⚠️ AUXILIARY DATA (51% - NUR für Vergleich!)

```
├── NED (Multi-Frequency Spectra)
│   └── M87 139-Frequenz Spektrum
│
├── SIMBAD (Named Objects)
│   └── Cross-Matching, Lookups
│
└── GAIA DR3 (Astrometry ONLY!)
    ├── Positionen (mas Präzision)
    ├── Eigenbewegungen, Parallaxen
    └── ❌ KEINE Gravitationsrotverschiebung!
```

---

## 2. KRITISCHE SPALTEN

### 2.1 PFLICHT-SPALTEN (NaN = FEHLER!)

Diese 7 Spalten **MÜSSEN** für JEDE Zeile gefüllt sein:

| Spalte | Beschreibung | Einheit | Beispiel |
|--------|--------------|---------|----------|
| `source` | Quellenname | - | `M87*`, `S2 SgrA*` |
| `f_emit_Hz` | Emittierte Frequenz | Hz | `2.3e11` |
| `f_obs_Hz` | Beobachtete Frequenz | Hz | `2.29e11` |
| `r_emit_m` | Emissionsradius | m | `1.2e13` |
| `M_solar` | Masse | M☉ | `6.5e9` |
| `n_round` | Segmentzahl | - | `5.2` |
| `z` | Redshift | - | `0.0042` |

**NaN in diesen Spalten bricht die gesamte Pipeline!**

### 2.2 OPTIONALE SPALTEN (NaN ist OK)

| Spalte | Wann NaN OK? | Beispiel |
|--------|--------------|----------|
| `a_m`, `e`, `P_year` | Kein Binärsystem | M87* Kontinuum |
| `v_los_mps`, `v_tot_mps` | Stationäre Quelle | - |
| `lambda_emit_nm` | Nur Frequenz vorhanden | Berechne: λ = c/f |
| `z_geom_hint`, `N0` | Optional | - |

---

## 3. BERECHNUNG FEHLENDER WERTE

### 3.1 n_round (Segmentzahl)

```python
import numpy as np

# Constants
c = 299792458.0      # m/s
G = 6.67430e-11      # m³/(kg·s²)
M_sun = 1.98847e30   # kg
phi = 1.6180339887   # Golden Ratio

def calc_n_round(r_emit_m: float, M_solar: float) -> float:
    """
    SSZ-Theorie: n = (r/r_φ)^(1/φ)
    mit r_φ = (φ/2) × r_s
    """
    M_kg = M_solar * M_sun
    r_s = 2 * G * M_kg / (c**2)      # Schwarzschild radius
    r_phi = (phi / 2) * r_s          # SSZ characteristic radius
    return (r_emit_m / r_phi) ** (1 / phi)
```

### 3.2 z (Redshift)

```python
def calc_z(f_emit_Hz: float, f_obs_Hz: float) -> float:
    """
    Standard Redshift-Definition.
    """
    return (f_emit_Hz - f_obs_Hz) / f_obs_Hz
```

### 3.3 f_emit aus Wellenlänge

```python
def wavelength_to_frequency(lambda_nm: float) -> float:
    """
    Konvertiere Wellenlänge zu Frequenz.
    """
    c = 299792458.0
    return c / (lambda_nm * 1e-9)
```

---

## 4. NaN-KLASSIFIZIERUNG

### ❌ FATAL NaN (Bricht Tests!)

| Spalte | Konsequenz |
|--------|------------|
| `source` | Kann nicht gruppieren |
| `f_emit_Hz` | Alle Frequenz-Tests broken |
| `f_obs_Hz` | Redshift-Berechnung unmöglich |
| `r_emit_m` | Horizon/Radius-Tests broken |
| `M_solar` | Schwarzschild-Radius undefined |
| `n_round` | SSZ-Theorie nicht anwendbar |
| `z` | Kosmologische Tests broken |

### ✅ ACCEPTABLE NaN (Wissenschaftlich korrekt)

| Spalte | Wann NaN OK? |
|--------|--------------|
| `a_m`, `e`, `P_year` | Kontinuum-Spektren (kein Orbit) |
| `v_los_mps`, `v_tot_mps` | Stationäre Quellen |
| `lambda_*_nm` | Redundant mit Frequenz |
| `T0_year`, `f_true_deg` | Nur für Orbital-Timing |

---

## 5. DATENQUELLEN IM DETAIL

### 5.1 ESO Spectroscopy (97.9%)

**Instrumente:**
- GRAVITY (VLT) - NIR Interferometrie
- XSHOOTER - UV-Optical-NIR
- UVES - High-Resolution Optical
- CRIRES - IR Spectroscopy

**Was ESO misst:**
- ✅ Lokale Gravitationsrotverschiebung (NICHT kosmologisch!)
- ✅ Brγ Emission Line (2.166 μm)
- ✅ Radialgeschwindigkeiten
- ✅ Photon Sphere Regime (r = 2-3 r_s)

**Validierte Objekte:**
```
S2 SgrA*     - GRAVITY 2018, 14 Beobachtungen
3C279        - Blazar jet, 840M M☉
PKS 1510-089 - Gamma-ray loud, 320M M☉
GRS 1915+105 - Stellar BH, 10.1 M☉
3C273        - Quasar, 1.2B M☉
```

**Datensatz:** `real_data_emission_lines_clean.csv` (47 Obs)

**Fetching:**
```python
from astroquery.eso import Eso

eso = Eso()
result = eso.query_surveys(
    surveys='GRAVITY',
    target='Sgr A*',
    columns=['source_id', 'ra', 'dec', 'wavelength', 'flux']
)
```

---

### 5.2 ALMA/EHT (Sub-mm)

**Frequenzen:** 84-950 GHz  
**Auflösung:** ~0.1 arcsec (VLBI: ~20 μas)

**Empfohlene Daten:**
```
EHT M87* Ring (2019):
- 86, 230, 345 GHz
- Ring diameter: 42 ± 3 μas
- r/r_s = 2-10 (Near-Horizon!)
- Paper: ApJL 875, L1 (2019)

Sgr A* Flares (GRAVITY+ALMA):
- 230, 345 GHz + NIR (K-band)
- r ≈ 6-10 r_s
- Paper: A&A 618, L10 (2018)
```

**Warum wichtig:** Multi-Frequenz + Near-Horizon = Jacobian Tests!

---

### 5.3 AKARI (Infrarot)

**Wellenlängen:** 2-160 μm  
**Mission:** 2006-2011 (All-Sky Survey)

**Anwendungen:**
- ✅ Diffuse IR Emission
- ✅ Temperatur-Maps
- ✅ Dichte-Struktur
- ✅ Nebula-Studien (G79.29+0.46)

**Ring-Datensätze:**
```
G79_Rizzo2014_NH3_Table1.csv  - 8 Ringe, NH3 Linien
CygnusX_Diamond_Ring.csv      - 6 Ringe
```

---

### 5.4 GAIA DR3 (⚠️ NUR Astrometrie!)

**Präzision:** ~1 mas (Positionen)

**Was GAIA liefert:**
- ✅ Positionen (ra, dec)
- ✅ Eigenbewegungen (pmra, pmdec)
- ✅ Parallaxen (Distanz)
- ✅ Einige Radialgeschwindigkeiten

**Was GAIA NICHT liefert:**
- ❌ Gravitationsrotverschiebung
- ❌ Emissionslinien-Wellenlängen
- ❌ Strong-Field Effekte

**SSZ-Erfolgsrate:** 51% (= Zufall!)

**GAIA SQL Query:**
```sql
SELECT source_id, ra, dec, parallax, pmra, pmdec, 
       radial_velocity, phot_g_mean_mag, bp_rp, ruwe
FROM gaiaedr3.gaia_source
WHERE parallax > 0 AND radial_velocity IS NOT NULL
```

---

### 5.5 NED Multi-Frequency

**Anwendung:** Jacobian-Tests (brauchen ≥3 Frequenzen)

**Beispiel M87:**
```
139 Frequenzen vom Radio bis X-ray
Perfekt für Information Preservation Test
```

**Fetching:**
```python
from astroquery.ned import Ned

# Fetch M87 SED
result = Ned.query_object("M87")
sed = Ned.get_table("M87", table="photometry")
```

---

## 6. REFERENZSYSTEM-KORREKTUR

### 6.1 Barycentric Correction (KRITISCH!)

**Problem:** f_obs ist laborabhängig!
- Erdbewegung um Sonne: ±30 km/s
- Sonnenbewegung im Galaxie: ~220 km/s
- Lokales Gravitationspotential variiert

**Lösung:** Alle Frequenzen müssen ins **baryzentrische System** transformiert werden:

```
Topozentrisch → Heliozentrisch → Baryzentrisch
```

**Ohne Korrektur:** Bis zu 30 km/s systematischer Fehler!

**Prüfung:**
```python
def check_barycentric(df):
    """Prüfe ob Daten baryzentrisch korrigiert sind."""
    # ESO/ALMA Daten sind standardmäßig korrigiert
    # GAIA RV ist heliozentrisch
    # Eigene Daten MÜSSEN korrigiert werden!
    pass
```

### 6.2 Konsistente Referenz-Wellenlängen

**Problem:** λ₀ variiert zwischen Laboren!

**Lösung:** Alle λ₀-Werte müssen auf NIST/CODATA Standards basieren:
```
H-alpha: 656.281 nm (NIST)
Brγ:     2166.00 nm (vacuum)
```

---

## 7. VALIDIERUNGS-WORKFLOW

### 7.1 Vor Integration

```bash
# 1. Struktur prüfen
python scripts/data_generators/validate_dataset.py --csv your_data.csv

# 2. Kritische Spalten prüfen
python -c "
import pandas as pd
df = pd.read_csv('your_data.csv')
CRITICAL = ['source', 'f_emit_Hz', 'f_obs_Hz', 'r_emit_m', 'M_solar', 'n_round', 'z']
for col in CRITICAL:
    nan_count = df[col].isna().sum() if col in df.columns else len(df)
    print(f'{col}: {nan_count} NaN / {len(df)} rows')
    if nan_count > 0:
        print(f'  ⚠️ CRITICAL: {col} has NaN!')
"
```

### 7.2 Fehlende Werte berechnen

```python
import pandas as pd
import numpy as np

df = pd.read_csv('your_data.csv')

# n_round berechnen
c, G, M_sun, phi = 299792458.0, 6.67430e-11, 1.98847e30, 1.6180339887

def calc_n(r, M_sol):
    M_kg = M_sol * M_sun
    r_s = 2 * G * M_kg / (c**2)
    r_phi = (phi / 2) * r_s
    return (r / r_phi) ** (1 / phi)

if 'n_round' not in df.columns or df['n_round'].isna().any():
    df['n_round'] = df.apply(lambda r: calc_n(r['r_emit_m'], r['M_solar']), axis=1)

# z berechnen
if 'z' not in df.columns or df['z'].isna().any():
    df['z'] = (df['f_emit_Hz'] - df['f_obs_Hz']) / df['f_obs_Hz']

df.to_csv('your_data_fixed.csv', index=False)
```

### 7.3 Nach Integration

```bash
# Pipeline durchlaufen
python run_all_ssz_terminal.py

# Debug-Files prüfen
python check_column_completeness.py
```

---

## 8. EMPFOHLENE DATENSÄTZE

### 8.1 Für SSZ-Validierung (97.9%)

| Datei | Objekte | Quelle |
|-------|---------|--------|
| `real_data_emission_lines_clean.csv` | 47 | ESO |
| `S2_star_timeseries.csv` | 10-20 | GRAVITY |

### 8.2 Für Horizon-Tests

| Datei | Regime | Quelle |
|-------|--------|--------|
| EHT M87* Ring Profile | r = 2-5 r_s | EHT 2019 |
| Sgr A* Flares | r = 6-10 r_s | GRAVITY+ALMA |
| Cyg X-1 X-ray | r = 1.2-10 r_s | Chandra |

### 8.3 Für Ring-Analysen

| Datei | Objekt | Ringe |
|-------|--------|-------|
| `G79_Rizzo2014_NH3_Table1.csv` | G79.29+0.46 | 8 |
| `CygnusX_Diamond_Ring.csv` | Cygnus X | 6 |

### 8.4 Für Robustness (Control Group)

| Datei | Objekte | Erfolgsrate |
|-------|---------|-------------|
| `real_data_full.csv` | 143 | 51% |

---

## 9. EINHEITEN-KONVERTIERUNG

### 9.1 Masse

| Input | → kg | Faktor |
|-------|------|--------|
| `M_Msun` | kg | × 1.98847e30 |
| `M_earth` | kg | × 5.972e24 |
| `M_kg` | kg | × 1 |

### 9.2 Radius

| Input | → m | Faktor |
|-------|-----|--------|
| `R_km` | m | × 1000 |
| `R_solar` | m | × 6.96e8 |
| `r_pc` | m | × 3.0857e16 |
| `r_AU` | m | × 1.496e11 |
| `r_mas` (M87) | m | × D_L × 4.85e-9 |

### 9.3 Frequenz

| Input | → Hz | Faktor |
|-------|------|--------|
| `f_GHz` | Hz | × 1e9 |
| `f_MHz` | Hz | × 1e6 |
| `lambda_nm` | Hz | c / (λ × 1e-9) |
| `E_keV` | Hz | × 2.418e17 |

### 9.4 Geschwindigkeit

| Input | → m/s | Faktor |
|-------|-------|--------|
| `v_kms` | m/s | × 1000 |
| `v_c` | m/s | × 299792458 |

---

## 10. CHECKLISTE VOR UPLOAD

### Pflicht-Checks

- [ ] **Quelle identifiziert:** ESO/ALMA für Validierung?
- [ ] **7 kritische Spalten vorhanden und gefüllt**
- [ ] **n_round berechnet** (aus r_emit_m, M_solar)
- [ ] **z berechnet** (aus f_emit/f_obs)
- [ ] **Keine NaN in kritischen Spalten**
- [ ] **Einheiten konsistent** (SI oder dokumentiert)
- [ ] **Barycentric Correction** (für eigene Daten)

### Qualitäts-Checks

- [ ] **Masse aus verlässlicher Quelle** (Paper, nicht geschätzt)
- [ ] **Frequenzen sind Messungen** (nicht Modell-Vorhersagen)
- [ ] **Emissionsradius physikalisch sinnvoll** (r > r_s)
- [ ] **Redshift im erwarteten Bereich** (|z| < 10 typisch)

### Dokumentations-Checks

- [ ] **Quellenangabe** (Paper DOI)
- [ ] **Instrument dokumentiert** (GRAVITY, ALMA, etc.)
- [ ] **Unsicherheiten angegeben** (wenn vorhanden)

---

## 11. HÄUFIGE FEHLER

### ❌ FALSCH: GAIA für SSZ-Validierung

```python
# GAIA hat KEINE Gravitationsrotverschiebung!
stars = fetch_gaia_nearby(100)
validate_ssz(stars)  # Nur 51% Erfolg!
```

### ✅ RICHTIG: ESO für SSZ-Validierung

```python
# ESO Spectroscopy misst exakt was SSZ vorhersagt
df = pd.read_csv("real_data_emission_lines_clean.csv")
validate_ssz(df)  # 97.9% Erfolg!
```

### ❌ FALSCH: Masse schätzen

```python
# Nie Masse aus Redshift schätzen!
M_solar = 1e8 * (z / 0.5)  # FALSCH!
```

### ✅ RICHTIG: Masse aus Paper

```python
# Masse aus peer-reviewed Paper
M_solar = 6.5e9  # M87*, EHT Collaboration 2019
```

---

## 12. REFERENZEN

### Primäre Papers

| Paper | Daten | DOI |
|-------|-------|-----|
| GRAVITY 2018 | S2 bei Sgr A* | 10.1051/0004-6361/201833718 |
| EHT 2019 | M87* Ring | 10.3847/2041-8213/ab0ec7 |
| Gou et al. 2011 | Cyg X-1 Spin | 10.1088/0004-637X/742/2/85 |
| Rizzo et al. 2014 | G79.29+0.46 | Paper reference |

### Archive-URLs

| Archive | URL |
|---------|-----|
| ESO | https://archive.eso.org |
| ALMA | https://almascience.eso.org |
| GAIA | https://gea.esac.esa.int |
| NED | https://ned.ipac.caltech.edu |
| HEASARC | https://heasarc.gsfc.nasa.gov |
| SIMBAD | https://simbad.u-strasbg.fr |

---

## ZUSAMMENFASSUNG

| Anwendung | Datenquelle | Erfolgsrate |
|-----------|-------------|-------------|
| **SSZ Validierung** | ESO Spectroscopy | **97.9%** |
| **Photon Sphere** | ESO (S2/S4/S5) | **100%** |
| **Horizon Tests** | EHT/GRAVITY/ALMA | Hoch |
| **Jacobian Tests** | NED Multi-Freq | Hoch |
| **Ring Analysen** | AKARI + Papers | Hoch |
| **Positionen nur** | GAIA | N/A |
| **Control Group** | GAIA/NED Mixed | 51% |

---

**© 2025 Carmen Wrede & Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Bei Fragen:** Siehe `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\` für vollständige Dokumentation.
