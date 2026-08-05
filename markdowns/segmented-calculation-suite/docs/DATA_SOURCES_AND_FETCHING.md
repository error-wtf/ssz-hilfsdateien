# DATA SOURCES AND FETCHING

**PHASE 0 Deliverable - Datenquellen-Inventarisierung**  
**Quelle:** `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\`

---

## 1. Bundled Datasets (Lokal)

### 1.1 Haupt-Datensätze

| Datei | Pfad | Objekte | Beschreibung |
|-------|------|---------|--------------|
| `real_data_full.csv` | `data/` | 129+ | Master dataset |
| `real_data_emission_lines_clean.csv` | `data/` | 47 | ESO spectroscopy (clean) |
| `real_data_blackholes_comprehensive.csv` | Root | 81 | Black hole configurations |
| `real_data_full_typed.csv` | `data/` | 129+ | With type annotations |

### 1.2 Ring-Datensätze (Nebulae)

| Datei | Objekt | Ringe | Quelle |
|-------|--------|-------|--------|
| `G79_Rizzo2014_NH3_Table1.csv` | G79.29+0.46 | 8 | Rizzo et al. 2014 |
| `CygnusX_Diamond_Ring.csv` | Cygnus X | 6 | Diamond Ring |

### 1.3 Backup-Datensätze

| Datei | Datum | Zweck |
|-------|-------|-------|
| `real_data_full_backup.csv` | 2025-10-19 | Pre-merge backup |
| `real_data_full_cleaned.csv` | 2025-10-19 | Cleaned version |
| `real_data_full_expanded.csv` | 2025-10-19 | Expanded |

---

## 2. Online-Datenquellen

### 2.1 Gaia DR3

| Parameter | Wert |
|-----------|------|
| **Endpoint** | Gaia Archive TAP |
| **Query** | `queries/gaia_dr3_core.sql` |
| **Rate Limit** | ~1000 objects/query |
| **Caching** | Disk cache empfohlen |

**SQL Query:**
```sql
SELECT
  source_id, ra, ra_error, dec, dec_error,
  parallax, parallax_error,
  pmra, pmra_error, pmdec, pmdec_error,
  radial_velocity, radial_velocity_error,
  phot_g_mean_mag, bp_rp, ruwe
FROM gaiaedr3.gaia_source
```

**Pflicht-Spalten:**
- `source_id` - Unique identifier
- `ra`, `dec` - Position (deg)
- `parallax` - Distanz-Proxy (mas)
- `radial_velocity` - RV (km/s)

### 2.2 ESO Science Archive

| Parameter | Wert |
|-----------|------|
| **Endpoint** | ESO Archive Portal |
| **Methode** | HTTP GET + CSV parse |
| **Rate Limit** | ~100 requests/hour |
| **Auth** | None (public data) |

**Fetching:**
```python
import httpx
url = "https://archive.eso.org/..."
response = httpx.get(url)
df = pd.read_csv(io.StringIO(response.text))
```

### 2.3 SIMBAD

| Parameter | Wert |
|-----------|------|
| **Library** | `astroquery.simbad` |
| **Rate Limit** | ~50 queries/minute |
| **Caching** | Built-in |

**Fetching:**
```python
from astroquery.simbad import Simbad
result = Simbad.query_object("Sirius")
```

### 2.4 VizieR

| Parameter | Wert |
|-----------|------|
| **Library** | `astroquery.vizier` |
| **Kataloge** | B/eso, I/355, II/246 |

---

## 3. Fetching-Mechanismen (Unified Repo)

### 3.1 Bestehende Fetcher

| Datei | Funktion | Quelle |
|-------|----------|--------|
| `fetch_real_astronomical_data.py` | General astronomical data | Multiple |
| `fetch_eso_br_gamma.py` | ESO Br-γ spectra | ESO Archive |
| `fetch_blackholes_comprehensive.py` | Black hole catalog | Multiple |
| `fetch_robust_5000.py` | Large-scale fetch | Gaia |
| `fetch_ligo.py` | LIGO GW data | LIGO |

### 3.2 Fetcher-Struktur

```python
def fetch_dataset(source: str, limit: int = 100, cache: bool = True):
    """
    Generic fetcher interface.
    
    Args:
        source: "gaia", "eso", "simbad", "sample"
        limit: Max objects
        cache: Use disk cache
    
    Returns:
        pd.DataFrame with standardized columns
    """
```

---

## 4. Caching-Strategie

### 4.1 Disk Cache

| Pfad | Inhalt | TTL |
|------|--------|-----|
| `cache/gaia/` | Gaia query results | 7 days |
| `cache/eso/` | ESO spectra | 30 days |
| `cache/simbad/` | SIMBAD lookups | 1 day |

### 4.2 Cache-Format

```
cache/
├── gaia/
│   ├── query_<hash>.csv
│   └── meta_<hash>.json
├── eso/
│   └── spectrum_<id>.csv
└── simbad/
    └── object_<name>.json
```

---

## 5. Daten-Validierung

### 5.1 Pflicht-Felder

| Feld | Typ | Unit | Required |
|------|-----|------|----------|
| `name` / `case` | str | - | ✅ |
| `M_solar` | float | M☉ | ✅ |
| `r_emit_m` | float | m | ✅ |
| `z_obs` | float | - | ❌ |
| `v_tot_mps` | float | m/s | ❌ |
| `v_los_mps` | float | m/s | ❌ |

### 5.2 Validierungs-Regeln

```python
def validate_row(row: dict) -> bool:
    """
    Validate a data row.
    
    Rules:
    - M_solar > 0
    - r_emit_m > 0
    - |z_obs| < 10 (sanity check)
    - |v_tot_mps| < c
    """
```

---

## 6. Fallback-Strategie

| Priorität | Aktion |
|-----------|--------|
| 1 | Cache prüfen |
| 2 | Online fetch |
| 3 | Bundled data |
| 4 | Sample objects |

---

## 7. Rate Limits & Best Practices

| Quelle | Limit | Empfehlung |
|--------|-------|------------|
| Gaia | 1000/query | Batch queries |
| ESO | 100/hour | Cache aggressiv |
| SIMBAD | 50/min | Sleep 1.5s |
| VizieR | 100/min | Sleep 1s |

---

## 8. Beispiel: Kompletter Fetch-Workflow

```python
# 1. Check cache
if cache_exists(source, query_hash):
    return load_cache(source, query_hash)

# 2. Online fetch
try:
    df = fetch_online(source, query)
    save_cache(source, query_hash, df)
    return df
except RateLimitError:
    time.sleep(60)
    return fetch_online(source, query)
except ConnectionError:
    # 3. Fallback to bundled
    return load_bundled(source)
```

---

**Erstellt:** PHASE 0 Inventarisierung  
**Status:** ✅ Datenquellen inventarisiert
