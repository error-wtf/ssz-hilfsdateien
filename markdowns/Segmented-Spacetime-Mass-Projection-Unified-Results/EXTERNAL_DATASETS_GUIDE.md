# External Datasets Integration Guide

**Date:** 2025-10-19  
**Purpose:** Guide for integrating external astronomical datasets into SSZ Suite

---

## ⚠️ **CRITICAL: READ FIRST**

**Before integrating ANY external data, read:**

📖 **[EXTERNAL_DATA_INTEGRATION_CRITICAL_WARNINGS.md](EXTERNAL_DATA_INTEGRATION_CRITICAL_WARNINGS.md)**

This document contains **MANDATORY** warnings about:
- 🔴 Full pipeline integration (Level 3 - CRITICAL complexity)
- ⚠️ NaN gaps (when fatal vs acceptable)
- ✅ Validation workflow (triple-check required)
- 🛠️ Our consistency check scripts

**Integration without reading this can lead to silent failures and incorrect results.**

---

## 🎯 **Zweck dieses Guides**

Du möchtest **externe Datasets** in die SSZ-Pipeline integrieren? Dieser Guide zeigt dir:
- ✅ **Welche Spalten sind erforderlich**
- ✅ **Wie du dein Dataset validierst**
- ✅ **Wie du fehlende Spalten berechnest**
- ⚠️ **Welche Flexibilität die Pipeline bietet**

---

## 📋 **Minimum Requirements (KRITISCH)**

Dein externes Dataset **MUSS** diese Spalten haben:

| Spalte | Beschreibung | Einheit | Beispiel |
|--------|-------------|---------|----------|
| `source` | Quellenname | - | `M87`, `Sgr A*` |
| `f_emit_Hz` | Emittierte Frequenz | Hz | `2.3e11` |
| `f_obs_Hz` | Beobachtete Frequenz | Hz | `2.29e11` |
| `r_emit_m` | Emissionsradius | m | `1.2e13` |
| `M_solar` | Masse (Sonnenmassen) | M☉ | `6.5e9` |
| `n_round` | Segmentzahl | - | `5.2` |
| `z` | Rotverschiebung | - | `0.0042` |

### **Berechnung fehlender Werte:**

```python
import numpy as np

# Constants
c = 299792458.0  # m/s
G = 6.67430e-11  # m^3/(kg s^2)
M_sun = 1.98847e30  # kg
phi = 1.6180339887  # Golden Ratio

# z aus Frequenzen
z = (f_emit_Hz - f_obs_Hz) / f_obs_Hz

# n_round aus SSZ-Theorie
M_kg = M_solar * M_sun
r_s = 2 * G * M_kg / (c**2)
r_phi = (phi / 2) * r_s
n_round = (r_emit_m / r_phi) ** (1 / phi)

# f_emit aus z (wenn nur f_obs gegeben)
f_emit_Hz = f_obs_Hz * (1 + z)
```

---

## ⚠️ **Optionale Spalten (NaN ist OK!)**

Diese Spalten sind **nur** für spezielle Tests nötig. **NaN ist wissenschaftlich korrekt** wenn nicht anwendbar:

### **Orbital Parameters (nur für Binärsysteme/Orbits):**
```
a_m       - Semi-major axis (m)
e         - Exzentrizität (dimensionslos)
P_year    - Orbitalperiode (Jahre)
T0_year   - Periastron-Epoch (Jahre)
f_true_deg - Wahre Anomalie (Grad)
```

**NaN setzen wenn:**
- ✅ Quelle ist kein Binärsystem
- ✅ Kontinuumsspektrum ohne Orbitalbewegung
- ✅ Einzelstern, isolierter Pulsar

### **Geschwindigkeit (nur für Doppler/Bewegung):**
```
v_los_mps - Line-of-sight velocity (m/s)
v_tot_mps - Gesamtgeschwindigkeit (m/s)
```

**NaN setzen wenn:**
- ✅ Keine Doppler-Messung vorhanden
- ✅ Stationäre Quelle

### **Wellenlänge (redundant mit Frequenz):**
```
lambda_emit_nm - Emittierte Wellenlänge (nm)
lambda_obs_nm  - Beobachtete Wellenlänge (nm)
```

**NaN setzen wenn:**
- ✅ Nur Frequenz verfügbar (λ = c/f kann berechnet werden)

---

## 🔧 **Validierungs-Workflow**

### **Schritt 1: Validierung**

```bash
# Prüfe ob dein Dataset kompatibel ist:
python scripts/data_generators/validate_dataset.py --csv your_data.csv

# Oder strict mode (prüft auch empfohlene Spalten):
python scripts/data_generators/validate_dataset.py --csv your_data.csv --strict
```

**Beispiel-Output:**
```
================================================================================
SSZ DATASET VALIDATION
================================================================================

File: external_data.csv
Strict mode: False

✓ Loaded successfully
  Rows: 50
  Columns: 12

================================================================================
1. CRITICAL COLUMNS (MUST exist and be filled)
================================================================================
✓ source: 50/50 filled (100%)
✓ f_emit_Hz: 50/50 filled (100%)
✓ f_obs_Hz: 50/50 filled (100%)
✓ r_emit_m: 50/50 filled (100%)
✓ M_solar: 50/50 filled (100%)
✗ n_round: 25/50 NaN (50%)        ← FEHLER!
✓ z: 50/50 filled (100%)

================================================================================
VALIDATION SUMMARY
================================================================================

✗ DATASET INVALID!
   1 errors found

Errors:
  - Critical column n_round has 25 NaN values

✗ Cannot be used in SSZ pipeline until fixed
```

### **Schritt 2: Fehlende Werte berechnen**

```python
import pandas as pd
import numpy as np

# Load
df = pd.read_csv('your_data.csv')

# Calculate n_round if missing
if 'n_round' not in df.columns or df['n_round'].isna().any():
    print("Calculating n_round...")
    
    c = 299792458.0
    G = 6.67430e-11
    M_sun = 1.98847e30
    phi = 1.6180339887
    
    def calc_n_round(r_m, M_solar):
        M_kg = M_solar * M_sun
        r_s = 2 * G * M_kg / (c**2)
        r_phi = (phi / 2) * r_s
        return (r_m / r_phi) ** (1 / phi)
    
    df['n_round'] = df.apply(
        lambda row: calc_n_round(row['r_emit_m'], row['M_solar']),
        axis=1
    )

# Calculate z if missing
if 'z' not in df.columns or df['z'].isna().any():
    print("Calculating z...")
    df['z'] = (df['f_emit_Hz'] - df['f_obs_Hz']) / df['f_obs_Hz']

# Save
df.to_csv('your_data_fixed.csv', index=False)
print("✓ Fixed! Re-run validation.")
```

### **Schritt 3: Re-validieren**

```bash
python scripts/data_generators/validate_dataset.py --csv your_data_fixed.csv
```

```
✅ DATASET VALID!
   All critical requirements met
   Ready for SSZ pipeline
```

---

## 🔄 **Integration in real_data_full.csv**

### **Option A: Manuelle Integration (sicher)**

```python
import pandas as pd

# Load both datasets
df_existing = pd.read_csv('real_data_full.csv')
df_external = pd.read_csv('your_data_fixed.csv')

# Ensure column compatibility
# Add missing optional columns with NaN
for col in df_existing.columns:
    if col not in df_external.columns:
        df_external[col] = np.nan

# Match column order
df_external = df_external[df_existing.columns]

# Concatenate
df_combined = pd.concat([df_existing, df_external], ignore_index=True)

# Verify critical columns still complete
critical = ['source', 'f_emit_Hz', 'f_obs_Hz', 'r_emit_m', 'M_solar', 'n_round', 'z']
assert df_combined[critical].notna().all().all(), "Critical columns have NaN!"

# Save
df_combined.to_csv('real_data_full.csv', index=False)
print(f"✓ Integrated! Total rows: {len(df_combined)}")
```

### **Option B: Script-basiert (automatisiert)**

```bash
# Use existing integration script
python scripts/data_generators/integrate_external_data.py \
    --external your_data_fixed.csv \
    --existing real_data_full.csv \
    --output real_data_full.csv
```

---

## ⚙️ **Test-Kompatibilität**

### **Wie Tests mit NaN umgehen:**

**Unsere Tests sind bereits flexibel!** Sie filtern automatisch:

```python
# Orbital parameters test
def test_orbital():
    df = pd.read_csv('real_data_full.csv')
    
    # Filter NUR Quellen mit Orbitalparametern
    orbital = df[df['a_m'].notna() & df['e'].notna()]
    
    # Test NUR auf orbital sources
    assert len(orbital) > 0
    assert (orbital['e'] >= 0).all()
```

**Dein externes Dataset kann also:**
- ✅ Nur kritische Spalten haben → Tests filtern fehlende optionale
- ✅ NaN in optionalen Spalten haben → Tests ignorieren NaN automatisch
- ✅ Zusätzliche Spalten haben → Werden ignoriert

---

## 🚨 **Häufige Probleme**

### **Problem 1: "Critical column has NaN"**
```
✗ n_round: 10/50 NaN (20%)
```

**Lösung:** Berechne n_round aus r_emit_m und M_solar (siehe Schritt 2)

### **Problem 2: "f_obs_Hz contains non-positive values"**
```
✗ f_obs_Hz: has non-positive values
```

**Lösung:** Prüfe ob Frequenzen in Hz (nicht GHz!) und positiv sind

### **Problem 3: "Missing critical column: z"**
```
✗ z: MISSING
```

**Lösung:** 
- Wenn f_emit und f_obs vorhanden: `z = (f_emit - f_obs) / f_obs`
- Wenn bekannte Quelle: Nutze kosmologisches z aus Literatur

### **Problem 4: "Eccentricity outside [0, 1)"**
```
⚠ e: has values outside [0, 1)
```

**Lösung:** 
- Für Ellipsen: 0 ≤ e < 1
- e=0: Kreis, e→1: Parabel
- Wenn e≥1: Entweder Fehler oder hyperbolic orbit (dann NaN setzen)

---

## 📊 **Beispiel: GAIA Data Integration**

### **Original GAIA format:**
```csv
source_id,ra,dec,parallax,pmra,pmdec,radial_velocity,phot_g_mean_mag
12345,10.5,45.2,5.3,10.2,-5.1,25.3,12.5
```

### **Konvertiert für SSZ:**
```python
import pandas as pd
import numpy as np

# Load GAIA
gaia = pd.read_csv('gaia_sample.csv')

# Convert to SSZ format
SSZ = pd.DataFrame()
SSZ['source'] = 'GAIA_' + gaia['source_id'].astype(str)
SSZ['case'] = 'GAIA DR3'

# Frequency from G-band magnitude (proxy)
# G-band central wavelength ~ 550 nm
c = 3e8
lambda_nm = 550
SSZ['f_obs_Hz'] = c / (lambda_nm * 1e-9)
SSZ['f_emit_Hz'] = SSZ['f_obs_Hz']  # No significant redshift

# Estimate radius from magnitude (stellar models)
SSZ['r_emit_m'] = 1e9  # ~Solar radius (crude estimate)

# Mass from stellar models (very crude!)
SSZ['M_solar'] = 1.0  # Assume solar mass

# Calculate derived
# z from parallax (distance) - negligible for Milky Way
SSZ['z'] = 0.0

# n_round from theory
phi = 1.6180339887
G = 6.67430e-11
M_sun = 1.98847e30
c = 299792458.0

def calc_n(r, M_sol):
    M_kg = M_sol * M_sun
    r_s = 2 * G * M_kg / (c**2)
    r_phi = (phi / 2) * r_s
    return (r / r_phi) ** (1 / phi)

SSZ['n_round'] = SSZ.apply(lambda r: calc_n(r['r_emit_m'], r['M_solar']), axis=1)

# Optional: velocity from proper motion
if 'radial_velocity' in gaia.columns:
    SSZ['v_los_mps'] = gaia['radial_velocity'] * 1000  # km/s to m/s
else:
    SSZ['v_los_mps'] = np.nan

# Save
SSZ.to_csv('gaia_for_ssz.csv', index=False)
```

### **Validieren:**
```bash
python scripts/data_generators/validate_dataset.py --csv gaia_for_ssz.csv

✅ DATASET VALID!
   All critical requirements met
   Ready for SSZ pipeline
```

---

## ✅ **Checkliste für Integration**

- [ ] Externe Daten haben alle 7 kritischen Spalten
- [ ] Validierungs-Script läuft durch (exit code 0)
- [ ] Fehlende n_round/z berechnet aus verfügbaren Daten
- [ ] Optionale Spalten auf NaN wenn nicht anwendbar
- [ ] Spalten-Reihenfolge matched existing dataset
- [ ] Backup von real_data_full.csv erstellt
- [ ] Integration durchgeführt
- [ ] Tests laufen durch: `python run_all_ssz_terminal.py`
- [ ] Commit mit Message: "Add X external data points from Y"

---

## 🎯 **Best Practices**

### **DO:**
- ✅ Validiere IMMER mit validation script vor Integration
- ✅ Berechne n_round und z wenn möglich (nicht raten!)
- ✅ Setze NaN für nicht-anwendbare optionale Spalten
- ✅ Dokumentiere Datenquelle in commit message
- ✅ Erstelle Backup vor Integration

### **DON'T:**
- ❌ Kritische Spalten mit NaN lassen
- ❌ Optionale Spalten mit Platzhaltern füllen (0, -999, etc.)
- ❌ Spalten weglassen die in existing dataset sind
- ❌ Integration ohne Validation
- ❌ Verschiedene Einheiten verwenden (Hz nicht GHz!)

---

## 📚 **Referenzen**

**Validation Script:**
```bash
scripts/data_generators/validate_dataset.py
```

**Column Documentation:**
```
DATA_COLUMNS_README.md
```

**Integration Example:**
```bash
scripts/data_generators/integrate_ned_spectrum.py
```

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Version:** 1.0.0  
**Last Updated:** 2025-10-19  
**Contact:** See README.md for contribution guidelines
