# CSV SCHEMAS

**PHASE 0 Deliverable - CSV-Format-Spezifikation**  
**Quelle:** `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\data\`

---

## Schema 1: Object List (Haupt-Schema)

**Datei:** `real_data_full.csv`  
**Verwendung:** Redshift-Evaluation, Paired Tests, Batch Calculations

### Spalten-Definition

| Spalte | Typ | Unit | Required | Beschreibung |
|--------|-----|------|----------|--------------|
| `case` | str | - | ✅ | Object identifier (unique) |
| `category` | str | - | ❌ | Object category (S-stars, WD, NS, BH) |
| `M_solar` | float | M☉ | ✅ | Mass in solar masses |
| `a_m` | float | m | ❌ | Semi-major axis |
| `e` | float | - | ❌ | Eccentricity |
| `P_year` | float | yr | ❌ | Orbital period |
| `T0_year` | float | yr | ❌ | Time of periastron |
| `f_true_deg` | float | deg | ❌ | True anomaly |
| `z` | float | - | ❌ | Observed redshift |
| `f_emit_Hz` | float | Hz | ❌ | Emitted frequency |
| `f_obs_Hz` | float | Hz | ❌ | Observed frequency |
| `lambda_emit_nm` | float | nm | ❌ | Emitted wavelength |
| `lambda_obs_nm` | float | nm | ❌ | Observed wavelength |
| `v_los_mps` | float | m/s | ❌ | Line-of-sight velocity |
| `v_tot_mps` | float | m/s | ❌ | Total velocity |
| `z_geom_hint` | float | - | ❌ | Geometry hint for SSZ |
| `N0` | float | - | ❌ | Normalization factor |
| `source` | str | - | ❌ | Data source reference |
| `r_emit_m` | float | m | ✅ | Emission radius |

### Beispiel-Zeile

```csv
case,category,M_solar,r_emit_m,z,v_tot_mps,v_los_mps,source
S2_SgrA*,S-stars,4297000.0,38071497974.22,0.000667,1157727.58,0.0,GRAVITY 2018
```

### Validierungs-Regeln

```python
def validate_object_row(row: dict) -> tuple[bool, list[str]]:
    errors = []
    
    # Required fields
    if not row.get('case'):
        errors.append("Missing 'case' field")
    if not row.get('M_solar') or float(row['M_solar']) <= 0:
        errors.append("Invalid M_solar: must be > 0")
    if not row.get('r_emit_m') or float(row['r_emit_m']) <= 0:
        errors.append("Invalid r_emit_m: must be > 0")
    
    # Optional field validation
    if row.get('z') and abs(float(row['z'])) > 10:
        errors.append("Suspicious z value: |z| > 10")
    if row.get('v_tot_mps') and abs(float(row['v_tot_mps'])) > 3e8:
        errors.append("Invalid v_tot_mps: > c")
    
    return len(errors) == 0, errors
```

---

## Schema 2: Ring Data (Nebula Analysis)

**Datei:** `G79_Rizzo2014_NH3_Table1.csv`  
**Verwendung:** SegWave velocity profile, Ring analysis

### Spalten-Definition

| Spalte | Typ | Unit | Required | Beschreibung |
|--------|-----|------|----------|--------------|
| `ring` | int | - | ✅ | Ring index (0, 1, 2, ...) |
| `T` | float | K | ✅ | Temperature |
| `n` | float | cm⁻³ | ❌ | Number density |
| `v_obs` | float | km/s | ✅ | Observed velocity |
| `r_pc` | float | pc | ❌ | Radius in parsec |

### Beispiel

```csv
ring,T,n,v_obs,r_pc
0,150.0,1e5,12.5,0.1
1,120.0,8e4,11.2,0.15
2,95.0,5e4,10.1,0.2
```

### Validierungs-Regeln

```python
def validate_ring_row(row: dict) -> tuple[bool, list[str]]:
    errors = []
    
    if row.get('T') and float(row['T']) <= 0:
        errors.append("Invalid T: must be > 0")
    if row.get('n') and float(row['n']) <= 0:
        errors.append("Invalid n: must be > 0")
    
    return len(errors) == 0, errors
```

---

## Schema 3: Emission Lines (Spectroscopy)

**Datei:** `real_data_emission_lines_clean.csv`  
**Verwendung:** ESO spectroscopy validation

### Spalten-Definition

| Spalte | Typ | Unit | Required | Beschreibung |
|--------|-----|------|----------|--------------|
| `case` | str | - | ✅ | Object identifier |
| `line` | str | - | ❌ | Spectral line (Hα, Br-γ, etc.) |
| `lambda_rest_nm` | float | nm | ✅ | Rest wavelength |
| `lambda_obs_nm` | float | nm | ✅ | Observed wavelength |
| `z_obs` | float | - | ✅ | Measured redshift |
| `M_solar` | float | M☉ | ✅ | Mass |
| `r_emit_m` | float | m | ✅ | Emission radius |

---

## Schema 4: Black Holes (Comprehensive)

**Datei:** `real_data_blackholes_comprehensive.csv`  
**Verwendung:** Black hole bomb tests, stability analysis

### Spalten-Definition

| Spalte | Typ | Unit | Required | Beschreibung |
|--------|-----|------|----------|--------------|
| `name` | str | - | ✅ | BH identifier |
| `M_solar` | float | M☉ | ✅ | Mass |
| `a_spin` | float | - | ❌ | Spin parameter (0-1) |
| `r_s_m` | float | m | ✅ | Schwarzschild radius |
| `type` | str | - | ❌ | stellar, intermediate, supermassive |

---

## Schema 5: Prediction Input (User Upload)

**Verwendung:** Gradio CSV Upload für Predictions

### Minimal-Schema

| Spalte | Typ | Unit | Required |
|--------|-----|------|----------|
| `name` | str | - | ✅ |
| `M_solar` | float | M☉ | ✅ |
| `R_km` | float | km | ✅ |

### Erweitertes Schema

| Spalte | Typ | Unit | Required |
|--------|-----|------|----------|
| `name` | str | - | ✅ |
| `M_solar` | float | M☉ | ✅ |
| `R_km` | float | km | ✅ |
| `z_obs` | float | - | ❌ |
| `v_km_s` | float | km/s | ❌ |
| `type` | str | - | ❌ |

### Auto-Detection

```python
def detect_schema(df: pd.DataFrame) -> str:
    """Detect CSV schema from columns."""
    cols = set(df.columns)
    
    if 'ring' in cols and 'T' in cols:
        return 'ring_data'
    if 'lambda_rest_nm' in cols:
        return 'emission_lines'
    if 'a_spin' in cols:
        return 'black_holes'
    if 'case' in cols or 'name' in cols:
        return 'object_list'
    
    return 'unknown'
```

---

## Unit Conversions

### Masse

| Input | Konvertierung zu kg |
|-------|---------------------|
| `M_solar` | × 1.98847e30 |
| `M_kg` | × 1 |
| `M_earth` | × 5.972e24 |

### Radius

| Input | Konvertierung zu m |
|-------|-------------------|
| `R_km` | × 1000 |
| `R_m` | × 1 |
| `R_solar` | × 6.96e8 |
| `r_emit_m` | × 1 |

### Geschwindigkeit

| Input | Konvertierung zu m/s |
|-------|----------------------|
| `v_km_s` | × 1000 |
| `v_mps` | × 1 |
| `v_c` | × 299792458 |

---

## Frame-Konventionen

| Frame | Beschreibung | Verwendung |
|-------|--------------|------------|
| Barycentric | Sonnensystem-Schwerpunkt | Redshift-Vergleich |
| Heliocentric | Sonnen-zentriert | Ältere Daten |
| Galactocentric | Galaxie-zentriert | Sgr A* Sterne |
| Observer | Beobachter-Frame | Raw Messungen |

**WICHTIG:** Alle Daten im Unified Repo sind **barycentric-corrected**.

---

## Beispiel-CSVs

### `examples/sample_objects.csv`
```csv
name,M_solar,R_km,type,z_obs
Sun,1.0,696340,star,0.0000021
Sirius B,1.018,5900,white_dwarf,0.00008
PSR J0348+0432,2.01,13,neutron_star,0.14
Sgr A*,4297000,12700000,black_hole,0.0
```

### `examples/sample_rings.csv`
```csv
ring,T,n,v_obs
0,150.0,1e5,12.5
1,120.0,8e4,11.2
2,95.0,5e4,10.1
3,75.0,3e4,9.3
```

---

**Erstellt:** PHASE 0 Inventarisierung  
**Status:** ✅ CSV Schemas dokumentiert
