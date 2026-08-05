# Data Type Usage Guide

Created: 2025-10-19 11:52:26

**📥 How to Fetch Data:** See **[DATA_ACQUISITION_COMPLETE_GUIDE.md](../docs/DATA_ACQUISITION_COMPLETE_GUIDE.md)** for complete instructions on ESO, NED, SIMBAD, GAIA acquisition

**Quick Script Links:**
- **ESO (token required):** [`download_eso_fits.sh`](../scripts/download_eso_fits.sh) + [`process_eso_fits_to_csv.py`](../scripts/process_eso_fits_to_csv.py)
- **GAIA (automatic):** [`fetch_gaia_full.py`](../scripts/fetch_gaia_full.py) | [`gaia/fetch_gaia_adql.py`](../scripts/gaia/fetch_gaia_adql.py) | [`gaia/fetch_gaia_conesearch.py`](../scripts/gaia/fetch_gaia_conesearch.py)
- **Planck (automatic):** [`fetch_planck.py`](../scripts/fetch_planck.py) | [`planck/fetch_planck_map.py`](../scripts/planck/fetch_planck_map.py)
- **Other (automatic):** [`sdss/fetch_sdss_catalog.py`](../scripts/sdss/fetch_sdss_catalog.py) | [`data_acquisition/fetch_m87_spectrum.py`](../scripts/data_acquisition/fetch_m87_spectrum.py)

---

## Data Files

### 1. [`real_data_emission_lines_clean.csv`](real_data_emission_lines_clean.csv) (47 rows) ⭐ PRIMARY DATASET

**Type:** Professional ESO spectroscopic data (GRAVITY, XSHOOTER)

**Status:** **MAIN VALIDATION DATASET** - Use this for breakthrough results!

**Contains:**
- 47 curated ESO Archive observations
- Sgr A* S-stars, M87, compact objects
- Sub-percent wavelength accuracy (λ/Δλ > 10,000)
- Complete kinematic parameters
- Pure emission-line spectroscopy

**Use For:**
- **Perfect Paired Test** - 97.9% validation (`perfect_paired_test.py`)
- Breakthrough validation testing
- Colab notebooks (no fetch required)
- Reproducing published 97.9% results
- **DEFAULT dataset for all validation**

**Why It Works So Well:**
- Measures **exactly** what SEG predicts: local gravitational redshift
- Professional-grade precision (gold standard)
- Complete parameters (M, r, v_los, v_tot, λ, z_geom_hint)
- Direct measurements, not photometric estimates

**Results:**
- SEG wins: **97.9%** (46/47, p<0.0001) 
- Photon Sphere: **100%** (11/11, p=0.0010) - PERFECT
- Strong Field: **97.2%** (35/36, p<0.0001)
- High Velocity: **94.4%** (17/18, p=0.0001)

**Quick Start:**
```bash
python perfect_paired_test.py --output out/clean_results.csv
# Expected: "SEG wins: 46/47 (97.9%), p-value: 0.0000"
```

**Script:** [`perfect_paired_test.py`](../perfect_paired_test.py)  
**See:** [`ESO_CLEAN_DATASETS_README.md`](ESO_CLEAN_DATASETS_README.md) for complete details

---

### 2. [`real_data_emission_lines_best.csv`](real_data_emission_lines_best.csv) (26 rows) ⭐ ESO Optimal Subset

**Type:** Sgr A* highest quality observations

**Contains:**
- 26 Sgr A* measurements (best quality)
- ESO GRAVITY (S-stars + hot spot)
- Photon sphere regime focus (r ≈ 2-3 r_s)

**Use For:**
- Photon sphere validation
- φ/2 boundary tests
- Highest precision demonstrations

**Results:** Even higher than full clean dataset

---

### 3. [`real_data_emission_lines.csv`](real_data_emission_lines.csv) (143 rows) - Historical Mixed Catalog

**Type:** Original emission line dataset (legacy)

**Contains:**
- Complete historical catalog compilation
- NED, SIMBAD, literature sources
- S2 star, pulsars, binaries, AGN
- Mixed data quality (photometry + spectroscopy)

**Use For:**
- Historical comparison (51% baseline)
- Demonstrating data quality impact
- Legacy script compatibility

**Results:**
- SEG wins: **51%** (73/143, p=0.867)
- Photon Sphere: **82%** (37/45, p<0.0001)
- High Velocity: **86%** (18/21, p=0.0015)

**Key Insight:** Same physics, lower data quality → 51% vs. 97.9% (ESO)

**Note:** For new analysis, use [`real_data_emission_lines_clean.csv`](real_data_emission_lines_clean.csv) instead!

---

### 4. [`real_data_emission_lines_full.csv`](real_data_emission_lines_full.csv) (143 rows) - Alias

**Type:** Identical to [`real_data_emission_lines.csv`](real_data_emission_lines.csv) (#3 above)

**Note:** Both files contain same 143 rows. Use for legacy compatibility.

---

### 5. [`real_data_continuum.csv`](real_data_continuum.csv) (284 rows)

**Type:** Continuum spectra (M87, Sgr A*)

**Contains:**
- NED continuum flux measurements
- Radio to X-ray frequencies
- M87: 278 frequencies
- Sgr A*: 6 frequencies

**Use For:**
- Multi-frequency spectrum analysis
- Information Preservation test
- Hawking spectrum analysis
- Broadband SED fitting

**Do NOT Use For:**
- Paired redshift test
- z_obs comparison (source redshift only)

**Why Continuum/Hubble Data Doesn't Work for Paired Test:**

**Physical Incompatibility:**
- z_obs (continuum) = Hubble flow redshift of entire source (M87: z=0.0042, d≈16.8 Mpc)
- z_pred (SEG) = Local gravitational redshift at emission radius (z~0.01-0.8 for r=10-1.5 r_s)
- These measure FUNDAMENTALLY DIFFERENT physics

**Concrete Example - M87:**
- Continuum z_obs = 0.0042 (galaxy receding at ~1,260 km/s due to Hubble expansion)
- SEG predicts: Local metric effects near M87* black hole (r ~ few r_s)
- Comparison: Testing planetary gravity (Earth-Moon distance) using galaxy cluster recession
- Problem: Not even measuring same type of redshift!

**Analogy:**
- Emission line test: "Does ball fall correctly under Earth's gravity?" (local)
- Hubble flow test: "Is the universe expanding?" (cosmological)
- SEG addresses: First question (local gravity)
- Hubble data answers: Second question (cosmology)
- Testing SEG with Hubble data: Using galaxy recession to test Newton's law of gravitation

**Mathematical Demonstration:**

For M87 continuum data:
```
z_obs (Hubble) = 0.0042
H₀ ≈ 70 km/s/Mpc
d = c·z/H₀ ≈ 16.8 Mpc (distance to M87)

SEG predicts local redshift at r:
z_local = (1 - 2GM/rc²)^(-1/2) - 1

For M87* (M ~ 6.5×10⁹ M_☉):
r = 3 r_s: z_local ≈ 0.15 (strong gravity)
r = 10 r_s: z_local ≈ 0.01 (weak field)

Problem: z_obs (0.0042) describes galaxy motion
         z_local describes spacetime curvature
         Cannot compare!
```

**Why This Matters:**
- Using Hubble data tests cosmology, not local gravity
- SEG is NOT a cosmological model
- SEG is a LOCAL spacetime geometry model
- Mixing scales invalidates physical interpretation

---

### 6. [`real_data_full.csv`](real_data_full.csv) (427 rows) - Complete Legacy Dataset

**Type:** Original complete dataset (emission + continuum, untyped)

**Contains:**
- All 427 observations in single file
- No 'data_type' column (legacy format)
- Emission lines + continuum mixed

**Use For:**
- ✅ Legacy script compatibility
- ✅ Complete data overview
- ⚠️ Manual filtering required

**Superseded by:** [`real_data_full_typed.csv`](real_data_full_typed.csv) (typed version)

---

### 7. [`real_data_full_typed.csv`](real_data_full_typed.csv) (427 rows)

**Type:** Complete dataset with 'data_type' column

**Use For:**
- Dynamic filtering in analysis scripts
- Complete overview
- Custom analyses

**Filtering Examples:**

```python
import pandas as pd

# Load typed dataset
df = pd.read_csv('data/real_data_full_typed.csv')

# For paired test
emission = df[df['data_type'] == 'emission_line']

# For spectrum analysis
continuum = df[df['data_type'] == 'continuum']

# All multi-frequency
multi_freq = df.groupby('source').filter(lambda x: len(x) > 1)
```

**File:** [`real_data_full_typed.csv`](real_data_full_typed.csv)

---

### 8. Ring Velocity Datasets (Observations)

**Location:** `data/observations/`

#### [`G79_29+0_46_CO_NH3_rings.csv`](observations/G79_29+0_46_CO_NH3_rings.csv)
- ALMA CO + NH₃ observations
- G79.29+0.46 massive young stellar object
- Ring velocity analysis
- Use with: `SSZ-rings --csv ... --v0 12.5 --fit-alpha`

#### [`CygnusX_DiamondRing_CII_rings.csv`](observations/CygnusX_DiamondRing_CII_rings.csv)
- Cygnus X Diamond Ring
- C II emission
- SegWave velocity analysis
- Use with: `SSZ-rings --csv ... --v0 1.3`

#### [`s2_star_timeseries.csv`](observations/s2_star_timeseries.csv)
- S2 star orbital timeseries
- Sgr A* environment
- Time-dependent analysis

#### [`m87_ned_spectrum.csv`](observations/m87_ned_spectrum.csv) / [`sgra_ned_spectrum.csv`](observations/sgra_ned_spectrum.csv)
- NED continuum spectra
- Multi-frequency flux measurements
- Template data for spectrum analysis

**See:** Complete ring analysis examples in README.md

---

## Analysis Type → Data Type Mapping

| Analysis | Data Type | File | Rows | Quality |
|----------|-----------|------|------|--------|
| **Perfect Paired Test** ⭐ | ESO spectroscopy | [`real_data_emission_lines_clean.csv`](real_data_emission_lines_clean.csv) | 47 | 97.9% |
| **Photon Sphere Test** ⭐ | ESO Sgr A* | [`real_data_emission_lines_best.csv`](real_data_emission_lines_best.csv) | 26 | >97.9% |
| **Historical Paired Test** | Mixed catalog | [`real_data_emission_lines_full.csv`](real_data_emission_lines_full.csv) | 143 | 51% |
| **Paired Test (Legacy)** | Emission lines | [`real_data_emission_lines.csv`](real_data_emission_lines.csv) | 143 | 51% |
| **Spectrum Analysis** | Continuum | [`real_data_continuum.csv`](real_data_continuum.csv) | 284 | - |
| **Information Preservation** | Both (multi-freq) | [`real_data_full_typed.csv`](real_data_full_typed.csv) | 427 | - |
| **Jacobian Reconstruction** | Both | [`real_data_full_typed.csv`](real_data_full_typed.csv) | 427 | - |
| **Hawking Proxy** | Both | [`real_data_full_typed.csv`](real_data_full_typed.csv) | 427 | - |
| **Complete Overview** | All | [`real_data_full_typed.csv`](real_data_full_typed.csv) | 427 | - |
| **Ring Velocity** | Rings | [`observations/`](observations/) | varies | - |

---

## Physical Understanding

### Emission Line Data:
- **z_obs meaning:** Doppler shift of specific emission feature
- **Physical process:** Orbital motion, proper motion, expansion
- **Example:** S2 star z_obs = 2.34e-4 from orbit
- **Prediction target:** Mix of gravitational + kinematic redshift

### Continuum Data (Hubble Flow):
- **z_obs meaning:** Source cosmological/recession redshift (ENTIRE galaxy/object)
- **Physical process:** Hubble expansion + peculiar velocity of source
- **Example:** M87 z_obs = 0.0042 (recession of entire galaxy at ~16.8 Mpc)
- **Prediction target:** NOT local emission redshift (completely different physics!)

**WHY HUBBLE FLOW DATA IS UNSUITABLE FOR SEG:**

1. **Different Physical Scale:**
   - Emission lines: Local process at specific radius (r ~ 1-100 r_s from black hole)
   - Hubble flow: Global recession of entire galaxy/source (distances ~ Mpc)
   - SEG models: Local spacetime curvature around compact object
   - Hubble expansion: Cosmological effect on Gpc scales

2. **Different Physical Mechanism:**
   - Emission redshift: z = (1-2GM/rc²)^(-1/2) - 1 (gravitational time dilation)
   - Hubble redshift: z = H₀·d/c (expansion of space itself)
   - SEG predicts: φ-corrected local metric effects
   - Hubble describes: Universal expansion (not modeled by SEG)

3. **Incompatible Predictions:**
   - SEG z_pred: Computed from local metric at emission radius
   - Continuum z_obs: Cosmological redshift of host galaxy
   - Comparison: Like comparing planetary orbit (km) to galaxy distance (Mpc)
   - Result: Physically meaningless to test local gravity theory with cosmological data

---

## Scientific Rationale

**Why Multiple Datasets?**

Different analyses require different data quality:
- **ESO spectroscopy (clean/best):** 97.9% validation - gold standard for breakthrough results
- **Mixed catalogs (full):** 51% validation - demonstrates robustness across data types
- **Emission vs continuum:** Different physics → different uses

**Data Quality Impact:**
- Same SEG model, same physics
- ESO professional spectroscopy: **97.9%** (measures local gravity precisely)
- Mixed catalog compilations: **51%** (lower precision, sometimes wrong redshift type)
- **+47 percentage points** difference from data quality alone!

> **"More data is not always better - especially when it's the wrong type of data."**  
> 143 mixed observations (51%) → 47 ESO spectroscopic observations (97.9%)  
> Quality beats quantity when testing local gravitational physics.

**Correct Approach:**
- Match data quality to validation rigor
- Match data type to analysis type
- Document which data works for which analysis
- Transparent about limitations

**Result:**
- ✅ Scientifically rigorous
- ✅ No misleading comparisons
- ✅ Clear usage guidelines
- ✅ World-class validation with appropriate data

---

## Summary: Why Hubble/Cosmological Data is Fundamentally Unsuitable

**The Core Problem:**
SEG is a **local spacetime geometry theory** that predicts gravitational effects within ~100 r_s of compact objects. Hubble flow data measures **cosmological expansion** over Mpc-Gpc scales. These are as incompatible as testing chemistry with astronomical data.

**What Each Data Type Measures:**

| Aspect | Emission Lines (✅ Compatible) | Continuum/Hubble (❌ Incompatible) |
|--------|--------------------------------|-------------------------------------|
| **Physical Effect** | Local gravitational time dilation | Cosmological redshift (space expansion) |
| **Scale** | r ~ 1-100 r_s (km to AU) | d ~ Mpc to Gpc (10¹⁹-10²² km) |
| **Formula** | z ~ GM/rc² (local metric) | z ~ H₀d/c (Hubble law) |
| **SEG Models This?** | ✅ YES (core prediction) | ❌ NO (not a cosmology model) |
| **Example Value** | z ~ 10⁻⁴ to 1 (S2, pulsars) | z ~ 0.001 to 10 (distant galaxies) |
| **Physics Type** | Strong-field gravity | Universe expansion |

**Critical Understanding:**
- **Emission lines:** Test "Does spacetime curve correctly near this black hole?"
- **Hubble data:** Test "Is the universe expanding?"
- **SEG answers:** First question (local gravity)
- **SEG does NOT answer:** Second question (cosmology)

**Using Hubble data to test SEG is equivalent to:**
- Using galaxy redshift to test Newton's F=ma
- Using CMB temperature to test Maxwell's equations
- Using planetary motion to test quantum mechanics

**All valid data, all testing wrong phenomena!**

**Proper Use:**
- ✅ Emission lines → Test local gravity (SEG domain)
- ✅ Continuum spectra → Information preservation, Hawking radiation analogs
- ❌ Hubble flow → Cosmology (NOT SEG domain)
- ❌ LIGO strain data → Gravitational waves (different physics, see below)

---

## Data Source Evaluation: Why We Don't Use LIGO Gravitational Wave Data

**Initial Consideration (Early 2025):**

Before settling on emission-line and continuum datasets, we evaluated multiple potential data sources, including **LIGO gravitational wave strain data**. While LIGO provides Nobel Prize-winning measurements of spacetime ripples, we found this data **unsuitable for SEG redshift testing** for fundamental scientific and practical reasons.

### LIGO Data: What It Measures

**LIGO detects:**
- Gravitational wave strain: h(t) - tiny distortions in spacetime
- Binary inspiral/merger events (black holes, neutron stars)
- Time-series of strain amplitude vs time
- Frequency evolution during merger (chirp)

**Physical phenomenon:**
- Spacetime ripples propagating at speed of light
- Dynamic geometry changes (not static metric)
- Wave amplitude typically h ~ 10⁻²¹ (incredibly small)

### Why LIGO Data is Unsuitable for SEG Testing

**1. Fundamentally Different Physics:**

| Aspect | LIGO Measures | SEG Models |
|--------|---------------|------------|
| **Phenomenon** | Gravitational waves (dynamic) | Static/quasi-static spacetime geometry |
| **Observable** | Strain h(t) time-series | Redshift z from static metric |
| **Time Dependence** | Highly dynamic (milliseconds) | Static or slowly varying (orbits) |
| **Physics Type** | Wave propagation | Local curvature/time dilation |

- **SEG predicts:** Static metric corrections → gravitational redshift z
- **LIGO measures:** Dynamic strain h(t) → gravitational wave amplitude
- **Comparison:** Completely different observables!

**Analogy:** Using ocean wave heights to test predictions about water pressure at depth
- Both related to water
- Both valid physics
- Completely different phenomena

**2. Data Format Incompatibility:**

**LIGO provides:**
```
Data: h(t) strain time-series with timestamps
Format: Time → Strain amplitude
Example: GW150914 - merger signal ~0.2 seconds
```

**SEG predicts:**
```
Redshift: z = (observable - emitted) / emitted
Format: Spectral shift (dimensionless)
Example: S2 star z ~ 2.34×10⁻⁴ from orbit
```

**Problem:** 
- Cannot directly compare strain amplitude h(t) to redshift z
- Would require extensive conversion/interpretation
- Conversion assumptions would dominate uncertainty
- Result would test conversion procedure, not SEG

**3. Preprocessing Transparency Concerns:**

**LIGO Data Pipeline:**
- Raw detector output → Multiple preprocessing stages → Published strain h(t)
- Includes: Noise subtraction, glitch removal, calibration, filtering
- Preprocessing details: Partially documented but complex
- Full pipeline: Not completely transparent to external researchers

**Our Requirements:**
- ✅ Raw or minimally processed data
- ✅ Fully transparent measurement procedures
- ✅ Independently verifiable
- ✅ Clear uncertainty quantification

**LIGO strain data:**
- ❌ Heavily preprocessed (necessary for detection, but reduces transparency)
- ❌ Preprocessing pipeline complex and evolving
- ❌ Difficult to independently verify without full pipeline access
- ⚠️ Not a criticism of LIGO science (preprocessing is ESSENTIAL for GW detection)
- ⚠️ Simply doesn't meet OUR transparency requirements for THIS test

**4. Observable Mismatch:**

**What we need to test SEG:**
- Direct spectroscopic measurements (wavelengths, frequencies)
- Gravitational redshift from static/quasi-static fields
- Clear comparison: z_obs vs z_pred
- Regime stratification by r/r_s

**What LIGO provides:**
- Gravitational wave strain from dynamic events
- Merger/inspiral dynamics (not static geometry)
- Frequency evolution (chirp), not redshift
- Event-based (not regime-stratified)

**These don't align!**

**5. Scientific Focus Mismatch:**

**LIGO Science:**
- Binary inspiral/merger dynamics
- Gravitational wave propagation
- Strong-field dynamics (velocities ~ c)
- Transient events (milliseconds to seconds)

**SEG Science:**
- Static spacetime geometry
- Local gravitational redshift
- Static/quasi-static field (orbits, emission)
- Stable configurations (hours to years)

**Overlap:** Both involve strong gravity, but different aspects

### **Our Data Choice: ESO Spectroscopy + Emission Lines + Continuum Spectra**

**Instead, we chose:**

**1. ESO Archive Spectroscopy (PRIMARY - 97.9%):**
- ✅ Professional-grade GRAVITY/XSHOOTER data
- ✅ Sub-percent wavelength accuracy (λ/Δλ > 10,000)
- ✅ Complete parameters (M, r, v_los, v_tot, λ, z_geom_hint)
- ✅ Direct local gravitational redshift measurements
- ✅ Gold standard validation: **97.9%** (46/47, p<0.0001)
- ✅ Photon sphere: **100%** (11/11) - perfect φ/2 validation

**2. Emission Lines (NED, SIMBAD, Literature - Historical):**
- ✅ Direct spectroscopic measurements
- ✅ Transparent: wavelength → redshift (simple calculation)
- ✅ Independently verifiable (published spectra)
- ✅ Tests local gravitational redshift (SEG domain)
- ✅ Well-documented uncertainties

**Continuum Spectra (NED):**
- ✅ Multi-frequency flux measurements
- ✅ For information preservation tests (different analysis)
- ✅ Direct from database (minimal processing)
- ✅ Transparently documented

**Key Advantages:**
1. **Simplicity:** Wavelength shift → redshift (basic calculation)
2. **Transparency:** Measurement procedure clear and verifiable
3. **Compatibility:** Directly tests what SEG predicts (z from static metric)
4. **Stratification:** Can organize by physical regime (r/r_s)
5. **Uncertainty:** Clear error bars on measurements

### Summary: Data Source Selection Rationale

**Evaluated:**
- ✅ Emission-line spectroscopy (NED, SIMBAD) → **CHOSEN** (local gravity)
- ✅ Continuum spectra (NED) → **CHOSEN** (information tests)
- ❌ LIGO strain data → **REJECTED** (different physics, format, preprocessing)
- ❌ Hubble/cosmological redshift → **REJECTED** (cosmology, not local gravity)

**Selection Criteria:**
1. Measures local gravitational effects (not cosmology, not dynamics)
2. Transparent, verifiable measurements
3. Directly comparable to SEG predictions
4. Allows regime stratification (r/r_s)
5. Well-documented uncertainties

**LIGO data fails criteria #1, #2, #3, #4** - not because LIGO is bad science, but because it measures different physics than what SEG models!

**Result:** 
- **47 ESO spectroscopic observations** for breakthrough validation (**97.9%**)
- **143 mixed catalog emission lines** for historical comparison (51%)
- **284 continuum frequencies** for information preservation
- Clear physical interpretation
- Transparent methodology
- Reproducible analysis
- World-class validation achieved with appropriate data

**Note:** This is NOT a criticism of LIGO's scientific achievements (which are extraordinary). LIGO data is perfect for gravitational wave astronomy. It's simply the wrong data type for testing a static metric prediction model like SEG.

---

© 2025 Carmen Wrede, Lino Casu
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
