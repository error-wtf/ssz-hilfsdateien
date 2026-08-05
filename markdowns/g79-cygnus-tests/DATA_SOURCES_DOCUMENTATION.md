# G79.29+0.46 Data Sources Documentation

> **Complete overview of data sources, fetch methods, and dataset provenance for the G79 Cygnus X validation suite**

© 2025 Carmen N. Wrede, Lino P. Casu  
Repository: https://github.com/error-wtf/g79-cygnus-tests  
Last Updated: 2025-11-08

---

## Table of Contents

1. [Overview](#overview)
2. [Primary Data Sources](#primary-data-sources)
3. [Automated Data Fetching](#automated-data-fetching)
4. [Currently Used Datasets](#currently-used-datasets)
5. [Data Processing Pipeline](#data-processing-pipeline)
6. [Future Data Upgrades](#future-data-upgrades)
7. [Citation Requirements](#citation-requirements)

---

## Overview

Das G79.29+0.46 Validierungs-Repository nutzt **multi-wavelength observational data** von verschiedenen Teleskop-Archiven, um die Segmented Spacetime Theorie zu testen.

**Ziel-Objekt:**
- **Name:** G79.29+0.46 (auch IRAS 20308+4104)
- **Typ:** Luminous Blue Variable (LBV) Nebula
- **Region:** Cygnus X Komplex
- **Koordinaten:** RA 20:31:41, Dec +40:21:07 (J2000)
  - Decimal: RA 307.920833°, Dec +40.351944°
- **Entfernung:** 1.7 ± 0.3 kpc
- **Nebula-Durchmesser:** ~4.5 pc

---

## Primary Data Sources

### 1. Published Literature (Currently Used)

#### 📄 **Rizzo et al. 2014 (A&A 561, A21)**
**Title:** "Ammonia observations of the LBV nebula G79.29+0.46"

**Telescope:** Effelsberg 100m  
**Instrument:** NH₃ (1,1) - (3,3) transitions  
**Data Type:** Spectroscopy - velocity components and rotation temperatures

**Key Measurements:**
- **NH₃ Velocity Components:**
  - Central: v = 0.3-1.9 km/s, T_rot = 11 ± 2 K
  - Blue: v = -1.7-0.3 km/s, T_rot > 40 K
  - Red: v = 1.9-2.8 km/s, T_rot > 28 K

**Used in Repository:**
- File: `G79_Rizzo2014_NH3_Table1.csv`
- Scripts: `analyze_nh3_velocities.py`, `test_boundary_v_realistic.py`
- Purpose: Velocity structure validation, temporal redshift calculation

**Citation:**
```bibtex
@article{Rizzo2014,
  author = {Rizzo, J.R. and Mart{\'i}n-Pintado, J. and Desmurs, J.F.},
  title = {Ammonia observations of the LBV nebula G79.29+0.46},
  journal = {A\&A},
  year = 2014,
  volume = 561,
  pages = {A21},
  doi = {10.1051/0004-6361/201322487}
}
```

---

#### 📄 **Rizzo et al. 2008 (ApJ 681, 355)**
**Title:** "The Molecular Environments of Luminous Blue Variables: A Comparison of Different Probes"

**Telescope:** IRAM 30m  
**Instrument:** CO (2-1), CO (3-2) observations  
**Data Type:** Spectral line datacubes - kinematics and temperatures

**Key Measurements:**
- CO velocity structure
- Kinetic temperatures (T_kin) from high-J transitions
- Molecular gas distribution

**Used in Repository:**
- File: `G79_rings_synthetic_from_papers.csv` (synthesized from paper figures)
- Scripts: `energy_release_model.py`, temperature validation scripts
- Purpose: Temperature profile, kinetic vs rotational temperature comparison

**Citation:**
```bibtex
@article{Rizzo2008,
  author = {Rizzo, J.R. and Mart{\'i}n-Pintado, J. and Desmurs, J.F.},
  title = {Molecular Environments of LBVs},
  journal = {ApJ},
  year = 2008,
  volume = 681,
  pages = {355-368},
  doi = {10.1086/588455}
}
```

---

#### 📄 **Jiménez-Esteban et al. 2010 (ApJ 713, 429)**
**Title:** "The Radio Nebula of the Central Star of G79.29+0.46"

**Data Type:** Radio continuum, shell structure  
**Key Measurements:** Nebula morphology, radial extent

**Used in Repository:**
- Nebula size estimates
- Shell structure parameters
- Radial extent validation

---

#### 📄 **Agliozzo et al. 2014 (MNRAS 440, 1391)**
**Title:** "IR and radio observations of G79.29+0.46"

**Data Type:** Infrared/radio continuum  
**Key Measurements:** Dust temperature, SED

**Used in Repository:**
- IR temperature estimates
- Multi-wavelength cross-validation

---

### 2. Telescope Archives (Fetch Scripts Available)

#### 🛰️ **Spitzer Space Telescope (IRSA)**

**Archive:** Spitzer Heritage Archive (SHA)  
**URL:** https://irsa.ipac.caltech.edu/applications/Spitzer/SHA/  
**Access:** Public, no account required

**Instruments:**
- **MIPS 24 μm:** Hot dust emission (inner ring structure)
- **MIPS 70 μm:** Cool dust
- **IRS:** Infrared spectroscopy

**Fetch Script:** `fetch_telescope_data.py --source spitzer`  
**Alternative:** `fetch_g79_ir_data.py --spitzer`

**Data Format:** FITS images (Post-Basic Calibrated Data - PBCD)

**Search Parameters:**
```python
Coordinates: RA 307.920833°, Dec +40.351944°
Radius: 5-10 arcmin
Catalog: spitzer_sha
```

**Expected Output:**
- 2D FITS images at 24, 70 μm
- Radial intensity profiles
- Temperature maps (from multi-band SED fitting)

**Status:** ⚠️ Fetch script ready, data download requires web interface or manual curl

---

#### 🛰️ **Herschel Space Observatory (ESA HSA)**

**Archive:** Herschel Science Archive  
**URL:** http://archives.esac.esa.int/hsa/whsa/  
**Access:** Public, free account registration required

**Instruments:**
- **PACS:** [CII] 158 μm, [OI] 63 μm (photodissociation region tracers)
- **SPIRE:** 250, 350, 500 μm (far-IR continuum)

**Fetch Script:** `fetch_telescope_data_api.py --source herschel --query`

**Data Format:** FITS Level 2.5 (fully reduced)

**Search Parameters:**
```python
Coordinates: 20:31:41 +40:21:07
Radius: 5 arcmin
Instruments: PACS, SPIRE
```

**Expected Output:**
- [CII] spectral datacubes (PDR structure)
- Multi-band far-IR continuum
- Temperature and density maps

**Status:** ⚠️ Query script ready, download requires HSA account

---

#### 🛰️ **AKARI Infrared Satellite (JAXA/DARTS)**

**Archive:** AKARI Data Archive (DARTS)  
**URL:** https://darts.isas.jaxa.jp/astro/akari/  
**Access:** Public via IRSA

**Instrument:** FIS (Far-Infrared Surveyor)  
**Bands:** 65, 90, 140, 160 μm all-sky survey

**Fetch Script:** `fetch_g79_ir_data.py --akari`  
**IRSA Query:** `fetch_telescope_data_api.py --source akari`

**Data Format:** FITS images from all-sky survey

**Search Parameters:**
```python
Catalog: akari_fis_allsky
Coordinates: RA 307.920833°, Dec +40.351944°
Radius: 10 arcmin
```

**Expected Output:**
- 90 μm FITS image (optimal for cool dust shells)
- Radial intensity profiles
- Flux measurements in ring apertures

**Status:** ✅ Query tested via IRSA/astroquery, catalog access working

**Processing Script:** `extract_akari_rings.py`

---

#### 📡 **IRAM 30m Telescope**

**Archive:** IRAM Archive / TAPAS (TAP service)  
**URL:** http://www.iram.fr/IRAMFR/GILDAS/  
**Access:** Semi-public, contact required for datacubes

**Instrument:** 30m single-dish + NOEMA interferometer  
**Lines:** CO (2-1) 230 GHz, CO (3-2) 345 GHz

**Data Type:** Spectral datacubes (velocity, position, temperature)

**Access Method:**
```
Email: archive@iram.fr
Subject: Data request for G79.29+0.46 CO observations
Reference: Rizzo et al. 2008, ApJ 681, 355
```

**Data Format:** CLASS/GILDAS format or FITS cubes

**Expected Output:**
- 3D velocity cubes: v(x, y, v)
- Kinetic temperature maps from CO line ratios
- Spatial velocity structure

**Status:** ⚠️ Requires direct contact (template in `fetch_telescope_data.py`)

**Processing Script:** `extract_co_velocity_rings.py` (requires spectral-cube package)

---

#### 📡 **Effelsberg 100m Telescope**

**Archive:** MPIfR Effelsberg Archive  
**URL:** https://www.mpifr-bonn.mpg.de/2169/en  
**Contact:** archive@mpifr-bonn.mpg.de  
**Access:** Request required

**Instrument:** 100m single-dish  
**Lines:** NH₃ (1,1) - (6,6) inversion transitions

**Data Type:** Spectral datacubes (already published data from Rizzo 2014)

**Access Method:**
```
Email: archive@mpifr-bonn.mpg.de
Subject: Data request for G79.29+0.46 NH₃ observations
Reference: Rizzo et al. 2014, A&A 561, A21
```

**Expected Output:**
- NH₃ spectral cubes
- Rotation temperature maps
- Spatial velocity structure (central/blue/red components)

**Status:** ⚠️ Table 1 data used from paper, full datacubes require archive request

---

### 3. Online Catalogs (Programmatic Access)

#### 🌐 **IRSA (NASA/IPAC Infrared Science Archive)**

**URL:** https://irsa.ipac.caltech.edu/  
**Access:** Public API via astroquery

**Available Catalogs:**
- Spitzer Heritage Archive
- WISE All-Sky Survey
- AKARI FIS All-Sky Survey
- 2MASS Point Source Catalog

**Python Access:**
```python
from astroquery.ipac.irsa import Irsa
from astropy.coordinates import SkyCoord
import astropy.units as u

coord = SkyCoord("20h31m41s +40d21m07s", frame='icrs')
result = Irsa.query_region(coord, catalog='akari_fis_allsky', 
                           radius=10*u.arcmin)
```

**Used in:** `fetch_telescope_data_api.py`, `fetch_g79_ir_data.py`

---

#### 🌐 **VizieR (CDS Strasbourg)**

**URL:** https://vizier.u-strasbg.fr/  
**Access:** Public API via astroquery

**Relevant Catalogs:**
- J/A+A/561/A21: Rizzo 2014 NH₃ data
- J/ApJ/681/355: Rizzo 2008 CO data
- Infrared source catalogs (IRAS, MSX, WISE)

**Python Access:**
```python
from astroquery.vizier import Vizier
Vizier.query_region("G79.29+0.46", radius=5*u.arcmin)
```

---

## Automated Data Fetching

### Available Scripts

#### 1. **fetch_telescope_data.py** (Manual Instructions)

**Purpose:** Print instructions for downloading data from various archives

**Usage:**
```bash
# Show all available archives
python fetch_telescope_data.py

# Detailed instructions for specific archive
python fetch_telescope_data.py --source spitzer --info
python fetch_telescope_data.py --source herschel --info
python fetch_telescope_data.py --source iram --info
```

**Features:**
- ✅ Coordinates in multiple formats
- ✅ Direct archive URLs
- ✅ Step-by-step download instructions
- ✅ Contact templates for request-required archives

---

#### 2. **fetch_telescope_data_api.py** (Automated Queries)

**Purpose:** Automated archive queries via astroquery

**Usage:**
```bash
# Query archives (list available data)
python fetch_telescope_data_api.py --source spitzer --query
python fetch_telescope_data_api.py --source herschel --query
python fetch_telescope_data_api.py --source akari --query

# Download data (saves query results as CSV)
python fetch_telescope_data_api.py --source all --download
```

**Requirements:**
```bash
pip install astroquery astropy
```

**Features:**
- ✅ Direct API queries to IRSA, HSA
- ✅ Saves query results as CSV
- ✅ Lists observation IDs for manual download
- ⚠️ Full FITS download requires web interface (file sizes)

---

#### 3. **fetch_g79_ir_data.py** (Infrared Focus)

**Purpose:** Specialized script for IR data (AKARI, Spitzer)

**Usage:**
```bash
# Query all IR missions
python fetch_g79_ir_data.py --all

# Query specific mission
python fetch_g79_ir_data.py --spitzer
python fetch_g79_ir_data.py --akari

# Just show coordinates
python fetch_g79_ir_data.py --coords

# Show curl/wget commands
python fetch_g79_ir_data.py --curl
```

**Features:**
- ✅ Optimized for AKARI FIS 90 μm
- ✅ Spitzer MIPS 24 μm queries
- ✅ Coordinate format conversion
- ✅ curl/wget examples for manual download

**Output:**
- `data/telescope/spitzer_query_results.csv`
- `data/telescope/akari_query_results.csv`

---

#### 4. **fetch_and_extract_complete.py** (Full Pipeline)

**Purpose:** Complete pipeline from fetch to ring extraction

**Usage:**
```bash
# Query archive
python fetch_and_extract_complete.py --source akari --query

# Process local FITS to rings
python fetch_and_extract_complete.py --local G79_akari_90um.fits --extract

# Process 3D datacube
python fetch_and_extract_complete.py --local CO_cube.fits --cube --extract
```

**Features:**
- ✅ Automated ring extraction from FITS
- ✅ 2D image processing (Spitzer, AKARI, Herschel continuum)
- ✅ 3D cube processing (CO, NH₃, [CII] spectral cubes)
- ✅ WCS coordinate transformation
- ✅ Radial profile calculation
- ✅ Publication-ready CSV output

**Requirements:**
```bash
pip install astropy spectral-cube pandas matplotlib
```

---

### Data Processing Pipeline

```
┌─────────────────────────────────────────────────────────────┐
│                   DATA ACQUISITION                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. Query Archive (fetch scripts)                          │
│     ↓                                                       │
│  2. Download FITS files (web or API)                       │
│     ↓                                                       │
│  3. Store in data/telescope/                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│                   DATA PROCESSING                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  4. Extract radial profiles:                               │
│     - 2D images → extract_akari_rings.py                   │
│     - 3D cubes → extract_co_velocity_rings.py              │
│     ↓                                                       │
│  5. Generate ring CSV:                                     │
│     columns: radius_pc, T_K, v_kms, I_flux, ...           │
│     ↓                                                       │
│  6. Store in data/                                         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────────┐
│                   SCIENTIFIC ANALYSIS                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  7. Fit γ_seg(r) → fit_gamma_seg_profile.py               │
│  8. Temperature validation → verify_paper_predictions.py   │
│  9. Velocity analysis → test_boundary_v_realistic.py       │
│  10. Domain classification → two_metric_model.py           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Currently Used Datasets

### ✅ PRIMARY: Fetched IR Data (100% Real Observations)

#### 1. **G79_AKARI_RINGS.csv** ⭐⭐⭐

**Source:** IRSA AKARI FIS All-Sky Survey catalog  
**Type:** 100% FETCHED from telescope archive  
**Confidence:** HIGH ✅  
**Generated:** 2025-11-06 by `RUN_COMPLETE_IR_ANALYSIS.py`

**Instrument:** AKARI Far-Infrared Surveyor (FIS)  
**Bands:** 65 μm, 90 μm, 140 μm, 160 μm  
**Coverage:** 6 sources, 3 rings with data (r = 0.625, 1.375, 1.875 pc)

**Columns:**
- `ring`, `r_min_pc`, `r_max_pc`, `radius_pc`
- `n_sources`: Number of catalog sources per ring
- `flux65/90/140/160_mean/median/std/err/n`: Complete flux statistics per band

**Why This Matters:**
- ✅ Real IR flux measurements → Temperature derivation via SED fitting
- ✅ Multi-band coverage → Dust temperature and mass estimates
- ✅ Statistical errors included → Proper uncertainty propagation
- ✅ Radial profile → Direct γ_seg(r) fitting

**Used by:**
- Temperature profile validation
- Hot ring structure confirmation
- SSZ γ_seg(r) fitting

**This dataset REPLACED the paper-based temperature estimates that were missing error bars!**

---

#### 2. **G79_WISE_RINGS.csv** ⭐⭐⭐

**Source:** IRSA AllWISE Source Catalog  
**Type:** 100% FETCHED from telescope archive  
**Confidence:** HIGH ✅  
**Generated:** 2025-11-06 by `RUN_COMPLETE_IR_ANALYSIS.py`

**Instrument:** WISE (Wide-field Infrared Survey Explorer)  
**Bands:** W1 (3.4 μm), W2 (4.6 μm), W3 (12 μm), W4 (22 μm)  
**Coverage:** 159 sources, 8 rings with data (r = 0.125 - 1.875 pc)

**Columns:**
- `ring`, `r_min_pc`, `r_max_pc`, `radius_pc`
- `n_sources`: 1-42 sources per ring
- `w1/2/3/4mpro_mean/median/std/err/n`: Complete photometry statistics

**Why This Matters:**
- ✅ Excellent spatial coverage (159 sources vs 6 from AKARI)
- ✅ Near-IR to mid-IR → Multi-temperature components
- ✅ Inner ring resolution (0.125 pc) → Domain boundary tracing
- ✅ Full error propagation

**Used by:**
- Radial structure validation
- Inner ring (g^(2)/g^(1) boundary) identification
- Cross-validation with AKARI

---

### 📄 SECONDARY: Literature Data

#### 3. **G79_Rizzo2014_NH3_Table1.csv**

**Source:** Rizzo et al. 2014, A&A 561, A21 (Table 1)  
**Type:** Direct transcription from peer-reviewed publication  
**Confidence:** HIGH ✅

**Columns:**
- `component`: Central / Blue / Red
- `v_min_kms`, `v_max_kms`: Velocity range
- `Trot_K`, `Trot_err_K`: Rotation temperature
- `N_NH3_cm2`: Column density

**Used by:**
- `analyze_nh3_velocities.py`
- `test_boundary_v_realistic.py`
- Velocity structure validation (Δv = 5 km/s prediction)

**Provenance:** Published peer-reviewed data

---

#### 4. **G79_temperatures.csv** ⚠️

**Source:** Extracted from Rizzo 2008 figures (CO temperature estimates)  
**Type:** Paper-based, INCOMPLETE (missing error bars!)  
**Confidence:** LOW → REPLACED by AKARI/WISE ⚠️

**Problem:**
- ❌ Only 10 radial points
- ❌ No error estimates
- ❌ Derived from paper figures, not tables
- ❌ Kinetic T from CO line ratios (not directly measured)

**Status:** **SUPERSEDED** by G79_AKARI_RINGS.csv and G79_WISE_RINGS.csv

**Historical Use:** Early model validation before IR catalog fetch

---

#### 5. **G79_rings_synthetic_from_papers.csv** ⚠️

**Source:** Synthesized from Rizzo 2008, 2014 + Jiménez-Esteban 2010  
**Type:** SYNTHETIC - interpolated from published zone averages  
**Confidence:** MEDIUM ⚠️

**Purpose:**
- First-order model validation
- Trend confirmation (temperature, velocity gradients)
- Placeholder for full FITS datacubes

**Important Caveats:**
- ❌ NOT direct spatial measurements
- ❌ Zone averages, not pixel-by-pixel data
- ❌ Velocity components mapped to approximate radii
- ⚠️ Suitable for trends, NOT precise fitting

**Status:** Useful for velocity structure, but **temperature data now from AKARI/WISE**

---

### 🔧 SUPPORTING DATA

#### 6. **G79_radio_predictions.csv**

**Source:** Generated by `radio_redshift_prediction.py`  
**Type:** Model predictions (SSZ framework)  
**Purpose:** Testable radio observations predictions

---

#### 7. **G79_29+0_46_rings_full.csv**

**Source:** Unknown (likely early test data)  
**Type:** Ring structure data  
**Status:** May be superseded by fetched data

---

## Why We Fetched New IR Data (2025-11-06)

### The Problem with Paper-Based Temperatures

**Original dataset:** `G79_temperatures.csv` from Rizzo 2008 paper figures

**Critical Issues:**
1. ❌ **No error bars** - extracted from paper figures, not tables
2. ❌ **Only 10 data points** - limited radial coverage
3. ❌ **Kinetic temperature from CO** - requires line ratio assumptions
4. ❌ **Not suitable for publication** - insufficient metadata

### The Solution: IRSA Catalog Fetching

**New datasets:** `G79_AKARI_RINGS.csv` + `G79_WISE_RINGS.csv`

**Why This is Better:**
1. ✅ **Full error propagation** - mean, median, std, stderr for every measurement
2. ✅ **Multi-band coverage** - AKARI (4 bands) + WISE (4 bands) = 8 wavelengths
3. ✅ **Temperature via SED fitting** - dust temperature from flux ratios
4. ✅ **Statistical rigor** - 6-159 sources with complete photometry
5. ✅ **Automated pipeline** - reproducible, documented methodology
6. ✅ **Publication-ready** - full metadata, provenance, uncertainties

### What Changed

**Before (Paper-based):**
```csv
r_pc,T_K
0.30,78
0.45,65
...
```
→ No errors, no metadata, unclear provenance

**After (IRSA-fetched):**
```csv
ring,radius_pc,n_sources,flux65_mean,flux65_std,flux65_err,...
2,0.625,2,40.27,5.27,3.73,...
```
→ Complete statistics, multi-band, traceable source

### Impact on SSZ Validation

- **Temperature profile fitting:** NOW possible with real uncertainties
- **γ_seg(r) derivation:** Statistically robust
- **Hot ring prediction:** Can be quantitatively tested
- **Publication quality:** Ready for peer review

**Date of upgrade:** 2025-11-06  
**Script used:** `RUN_COMPLETE_IR_ANALYSIS.py`  
**Data source:** IRSA (NASA/IPAC archive)

---

## Future Data Upgrades

### Priority 1: IRAM CO Datacubes ⭐⭐⭐

**Needed:** CO (2-1), CO (3-2) FITS cubes from Rizzo 2008  
**Why:** Spatial T_kin(x,y) and v(x,y) maps  
**Impact:** Replace synthetic rings with direct spatial measurements

**Action:**
```bash
# Request from IRAM archive
python fetch_telescope_data.py --source iram --info
# Follow email template
```

**Processing:**
```bash
python extract_co_velocity_rings.py CO_21_cube.fits --extract
```

---

### Priority 2: Effelsberg NH₃ Maps ⭐⭐

**Needed:** NH₃ (1,1)-(3,3) FITS cubes from Rizzo 2014  
**Why:** Spatial T_rot(x,y) and velocity component maps  
**Impact:** Validate temporal compression predictions

**Action:**
```bash
python fetch_telescope_data.py --source effelsberg --info
# Follow email template
```

---

### Priority 3: AKARI FIS 90 μm FITS ⭐⭐

**Needed:** Full FITS image (not just catalog)  
**Why:** Radial intensity profile for γ_seg(r) fitting  
**Impact:** Independent temperature tracer

**Action:**
```bash
python fetch_g79_ir_data.py --akari
# Download FITS from DARTS/IRSA
python extract_akari_rings.py data/telescope/G79_akari_90um.fits
```

---

### Priority 4: Herschel PACS [CII] ⭐

**Needed:** [CII] 158 μm spectral cube  
**Why:** PDR structure, independent velocity tracer  
**Impact:** Cross-validation of velocity structure

**Action:**
```bash
python fetch_telescope_data_api.py --source herschel --query
# Download from HSA after account creation
```

---

## Citation Requirements

### When Using This Data

If you use data from this repository, cite both the **original papers** and the **SSZ validation framework**:

#### Original Data Sources:
```bibtex
@article{Rizzo2014,
  author = {Rizzo, J.R. and Mart{\'i}n-Pintado, J. and Desmurs, J.F.},
  title = {Ammonia observations of the LBV nebula G79.29+0.46},
  journal = {A\&A},
  year = 2014,
  volume = 561,
  pages = {A21},
  doi = {10.1051/0004-6361/201322487}
}

@article{Rizzo2008,
  author = {Rizzo, J.R. and Mart{\'i}n-Pintado, J. and Desmurs, J.F.},
  title = {The Molecular Environments of LBVs},
  journal = {ApJ},
  year = 2008,
  volume = 681,
  pages = {355-368},
  doi = {10.1086/588455}
}
```

#### SSZ Framework:
```bibtex
@software{wrede2025g79validation,
  title={G79.29+0.46 Segmented Spacetime Validation Suite},
  author={Wrede, Carmen N. and Casu, Lino P. and Bingsi},
  year={2025},
  url={https://github.com/error-wtf/g79-cygnus-tests},
  note={Temporal redshift discovery and complete validation framework}
}
```

---

## Summary

### Data Status Overview

| Data Type | Source | Status | Confidence | Used In |
|-----------|--------|--------|------------|---------|
| **AKARI FIS flux (4 bands)** | **IRSA catalog** | **✅ FETCHED** | **HIGH** | **Temperature fitting** |
| **WISE photometry (4 bands)** | **IRSA catalog** | **✅ FETCHED** | **HIGH** | **Radial structure** |
| NH₃ velocity components | Rizzo 2014 (Table 1) | ✅ Available | HIGH | Velocity validation |
| CO temperature (zone avg) | Rizzo 2008 (paper figures) | ⚠️ Superseded | LOW | Replaced by AKARI/WISE |
| NH₃ T_rot (zone avg) | Rizzo 2014 (synthesized) | ✅ Available | MEDIUM | Synthetic rings (v only) |
| CO datacubes (FITS) | IRAM (request) | ⏳ Pending | - | Future upgrade |
| NH₃ datacubes (FITS) | Effelsberg (request) | ⏳ Pending | - | Future upgrade |
| AKARI FITS images | DARTS/IRSA | ⏳ Pending | - | Future upgrade |
| Spitzer MIPS FITS | IRSA | ⏳ Pending | - | Future upgrade |
| Herschel [CII] | HSA (account req) | ⏳ Pending | - | Future upgrade |

### Key Points

1. **AKARI & WISE IR data FETCHED and ready** - 100% real telescope observations ✅
2. **Temperature data NOW from multi-band photometry** (replaced paper estimates) ✅
3. **Velocity structure from Rizzo 2014 NH₃** - publication-quality ✅
4. **Statistical errors INCLUDED** - AKARI/WISE have full error propagation ✅
5. **Current dataset is PUBLICATION-READY** for SSZ validation ✅
6. **Future upgrade path:** FITS datacubes → pixel-level analysis (optional) 🚀

---

## Contact

**Data Questions:**  
Carmen N. Wrede (Principal Investigator)  
Lino P. Casu (Co-Investigator)

**Repository:**  
https://github.com/error-wtf/g79-cygnus-tests

**Related Repositories:**  
- SSZ-Metric-Pure: https://github.com/error-wtf/ssz-metric-pure
- Unified Results: https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results

---

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
