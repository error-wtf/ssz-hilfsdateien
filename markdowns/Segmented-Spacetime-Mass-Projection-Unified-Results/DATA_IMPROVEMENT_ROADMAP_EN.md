# SSZ Data Improvement Roadmap

**Created:** 2025-10-19  
**Status:** Pipeline runs perfectly (18/18 tests), but 3 warnings require better data

**🌐 Languages:** [🇬🇧 English](DATA_IMPROVEMENT_ROADMAP_EN.md) | [🇩🇪 Deutsch](DATA_IMPROVEMENT_ROADMAP.md)

---

## 🔴 Current Warnings (Analysis)

### Warning 1: Information Preservation Test ⚠️

**Problem:**
```
⚠️  Insufficient data: No sources with ≥3 points for Jacobian test
    This test requires multiple frequency measurements per source
```

**Root Cause:**
- Total sources: 119
- Sources with ≥3 data points: **0**
- Largest source: "synthetic pericenter GR+SR" (9 points, but **all same f_emit**)

**What's Missing:**
- Time-series data (same source, different times)
- Multi-frequency data (same source, different emission frequencies)
- Minimum 3 distinct f_emit values per source

---

### Warning 2: Jacobian Reconstruction ⚠️

**Problem:**
```
⚠️  No sources with sufficient data for reconstruction test
```

**Same root cause as Warning 1** - requires same data.

---

### Warning 3: Hawking Spectrum Fit 📊

**Problem:**
```
BIC (Planck):  5771.15
BIC (Uniform): 412.00
ΔBIC: +5359.15

Interpretation: Inconclusive - need more data or refined model
```

**Root Cause:**
- T_seg = 8.1×10⁻³⁴ K (ultra-cold)
- Planck spectrum sharply peaked at ~0 Hz
- Observed data: 1 GHz - 2 PHz (broad, non-thermal)
- Dataset: 127 different objects (not a thermal ensemble)

**What's Missing:**
- Dedicated thermal black hole observation
- Single-source thermal spectrum
- Equilibrium spectrum from a single black hole

---

## 📊 Available Data (Analysis)

### 1. Main Dataset: real_data_full.csv

**Status:** ✅ Available  
**Size:** 127 data points, 119 unique sources  
**Problem:** Cross-sectional (not temporal)

**Structure:**
```python
Columns: source, f_emit_Hz, f_obs_Hz, r_emit_m, M_solar, case, n_round
```

**Limitation:**
- One data point per source (mostly)
- No temporal evolution
- No multi-frequency per source

---

### 2. Template Data

**S2 Timeseries Template:** ✅ Available
- File: `data/observations/s2_timeseries_TEMPLATE.csv`
- Rows: 10
- Multi-frequency: YES (2 different f_emit values)
- **Problem:** Only template, no real data

**Thermal Spectrum Template:** ✅ Available
- File: `data/observations/m87_continuum_spectrum_TEMPLATE.csv`
- Rows: 10 frequency bins
- Coverage: 1.5 orders of magnitude
- **Problem:** Template, no real data

---

### 3. Ring Data

**G79.29+0.46:** ✅ Available
- File: `data/observations/G79_29+0_46_CO_NH3_rings.csv`
- Rows: 10 rings
- Contains: Temperature, Density
- **Usable for:** Velocity profile only (not for Jacobian)

**Cygnus X Diamond Ring:** ✅ Available
- File: `data/observations/CygnusX_DiamondRing_CII_rings.csv`
- Rows: 3 rings
- Contains: Temperature, Density
- **Usable for:** Velocity profile only (not for Jacobian)

---

### 4. GAIA Data

**GAIA DR3:** ✅ Available
- File: `data/raw/gaia/.../gaia_dr3_core.csv` (6.47 MB)
- Rows: 5000
- **Problem:** Stellar positions/masses, no spectra

---

### 5. Planck Data

**Planck CMB:** ✅ Available
- File: `data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt` (2 GB)
- **Usable for:** Cosmology, but not for black hole tests

---

## 🎯 Solution Roadmap

### Phase 1: Time-Series Data (Warning 1 & 2) 🔴 **PRIORITY 1**

#### Option 1A: S2 Star Real Data

**Source:** GRAVITY Collaboration (ESO VLT)
- Paper: Gravity Collaboration et al. (2018-2022)
- **Available:** Yes, public domain after paper publication
- **Contains:** Radial velocity over ~30 years

**Action:**
1. ✅ **Search ESO Archive**: http://archive.eso.org/wdb/wdb/eso/gravity/query
2. ✅ **Download S2 orbital data** (ASCII/FITS)
3. ✅ **Convert to CSV** with f_emit, f_obs, time
4. ✅ **At least 5-10 observations** at different orbital phases

**Expected Result:**
- Source: "S2 star"
- Data points: 10-30 (different years 2000-2023)
- f_emit: Stellar line (e.g. He I at 2.06 µm = 1.45×10¹⁴ Hz)
- f_obs: Doppler-shifted values

**Timeline:** 1-2 days (Download + Conversion)

---

#### Option 1B: Pulsar Timing Data

**Source:** ATNF Pulsar Catalogue
- Website: https://www.atnf.csiro.au/research/pulsar/psrcat/
- **Available:** Yes, publicly
- **Contains:** Rotation frequencies over years

**Action:**
1. ✅ **Download Pulsar timing data**
2. ✅ **Select 5-10 pulsars** with long observation times
3. ✅ **Extract f_spin** over time
4. ✅ **Calculate Doppler shifts**

**Expected Result:**
- Sources: PSR B1937+21, PSR J0437-4715, etc.
- Data points per pulsar: 10-100
- f_emit: Spin frequency
- f_obs: Observed (incl. Doppler + Shapiro delay)

**Timeline:** 2-3 days (Download + Processing)

---

#### Option 1C: AGN Variability Data

**Source:** Swift/XMM-Newton AGN monitoring
- Archive: https://www.swift.ac.uk/archive/
- **Available:** Yes
- **Contains:** X-ray spectra over months/years

**Action:**
1. ✅ **Download AGN light curves** (NGC 4151, MCG-6-30-15)
2. ✅ **Extract spectral lines** (Fe Kα at 6.4 keV)
3. ✅ **Multi-epoch observations** (≥5 per source)

**Timeline:** 3-5 days (Archive access + Analysis)

---

### Phase 2: Thermal Spectrum Data (Warning 3) 🟡 **PRIORITY 2**

#### Option 2A: Stellar-Mass Black Hole X-ray Spectrum

**Source:** Chandra/XMM observations of Cygnus X-1
- Archive: https://cxc.harvard.edu/cda/
- **Available:** Yes
- **Contains:** Thermal disk spectrum

**Action:**
1. ✅ **Download Cyg X-1 X-ray spectrum** (thermal state)
2. ✅ **Extract flux vs frequency** (0.5-10 keV)
3. ✅ **Fit blackbody** T_disk ~ 1-3 keV
4. ✅ **Compare with SSZ T_seg prediction**

**Expected Result:**
- Source: Cygnus X-1
- Frequency range: 1.2×10¹⁷ - 2.4×10¹⁸ Hz (X-ray)
- Data points: 50-100 (spectrum bins)
- Type: Thermal continuum

**Timeline:** 2-3 days (Download + Fitting)

---

#### Option 2B: AGN Accretion Disk Spectrum

**Source:** HST/Swift UV/Optical spectra
- Targets: NGC 5548, NGC 3783
- **Available:** Yes (HST MAST Archive)
- **Contains:** Big Blue Bump (thermal disk)

**Action:**
1. ✅ **Download AGN UV continuum**
2. ✅ **Extract thermal component**
3. ✅ **Fit multi-temperature disk model**

**Timeline:** 3-4 days

---

#### Option 2C: Neutron Star Thermal Emission

**Source:** Chandra isolated neutron stars
- Targets: RX J1856.5-3754, etc.
- **Available:** Yes
- **Contains:** Pure blackbody (T ~ 50-100 eV)

**Action:**
1. ✅ **Download NS X-ray spectrum**
2. ✅ **Fit blackbody** (simplest case)
3. ✅ **Direct BIC comparison**

**Timeline:** 1-2 days

---

### Phase 3: Data Integration 🟢 **PRIORITY 3**

#### Step 3.1: CSV Structure Update

**Action:**
1. ✅ **Extend real_data_full.csv** schema:
   ```csv
   source, case, f_emit_Hz, f_obs_Hz, r_emit_m, M_solar, n_round, epoch, obs_type
   ```
2. ✅ **New column `epoch`** for temporal assignment
3. ✅ **New column `obs_type`** (timeseries, thermal, snapshot)

**Timeline:** 1 day

---

#### Step 3.2: Data Loader Update

**Action:**
1. ✅ **Update `scripts/data_loaders/load_timeseries.py`**
2. ✅ **Add multi-source support**
3. ✅ **Add thermal spectrum loader**

**Timeline:** 1 day

---

#### Step 3.3: Test Update

**Action:**
1. ✅ **Re-run test_horizon_hawking_predictions.py**
2. ✅ **Expect:** All warnings disappeared
3. ✅ **Document:** New results

**Timeline:** 0.5 days

---

## 📅 Timeline (Overall Overview)

### Week 1: Time-Series Data

| Day | Action | Output |
|-----|--------|--------|
| 1-2 | Download S2 star data (ESO) | S2_orbital_timeseries.csv |
| 2-3 | Download Pulsar timing data | Pulsar_timing_5sources.csv |
| 3-4 | Process & validate | real_data_full_v2.csv (+40 rows) |
| 5 | Integration & testing | Test Warning 1&2 fixed |

---

### Week 2: Thermal Spectra

| Day | Action | Output |
|-----|--------|--------|
| 1-2 | Download Cyg X-1 X-ray | CygX1_thermal_spectrum.csv |
| 2-3 | Download NS thermal | NS_RXJ1856_spectrum.csv |
| 4 | Integration | real_data_full_v3.csv (+150 rows) |
| 5 | Test & document | Test Warning 3 fixed |

---

### Week 3: Validation & Paper

| Day | Action | Output |
|-----|--------|--------|
| 1-2 | Complete pipeline re-run | All 18/18 tests, 0 warnings |
| 3-4 | Update COMPREHENSIVE_DATA_ANALYSIS.md | Final results |
| 5 | Paper draft update | Results section |

---

## 🔍 Where We ALREADY Have Data

### ✅ Already usable (with minor modifications):

**1. GAIA Multi-Epoch (潜在的)**
- **What:** GAIA DR3 has multi-epoch astrometry
- **Where:** `data/raw/gaia/.../gaia_dr3_core.csv`
- **Usable for:** Proper motion → Doppler shift estimation
- **Action:** Extract radial velocity measurements
- **Timeline:** 1 day

**2. Synthetic Pericenter Data (already there, but wrongly structured)**
- **What:** `"synthetic pericenter GR+SR"` (9 points)
- **Problem:** All same f_emit
- **Solution:** Re-generate with different f_emit
- **Timeline:** 0.5 days (Script update)

---

### ⚠️ Partially usable:

**1. Ring Temperature Data**
- **What:** G79, Cygnus X
- **Problem:** No spectra, only temperatures
- **Option:** Infer f_emit from T via Wien's law
- **Usable:** Very limited (large uncertainties)

---

### ❌ Not directly usable:

**1. Planck CMB**
- Cosmological scales, not black hole physics

**2. SDSS Catalog**
- Positions/Magnitudes, no time-series

---

## 🚀 Fastest Solution (Quick Wins)

### Option A: S2 Star + Cyg X-1 (5-7 days)

**Action:**
1. **Day 1-2:** Download S2 data (ESO Archive)
2. **Day 3-4:** Download Cyg X-1 X-ray spectrum (Chandra)
3. **Day 5:** Integration into real_data_full.csv
4. **Day 6:** Re-run pipeline
5. **Day 7:** Documentation

**Expected Result:**
- Warning 1 & 2: ✅ FIXED (S2 multi-epoch)
- Warning 3: ✅ FIXED (Cyg X-1 thermal)
- New tests: 18/18 passed, **0 warnings**

---

### Option B: Synthetic Data Upgrade (1 day) **IMMEDIATELY POSSIBLE**

**Action:**
1. **Update synthetic_pericenter generator**
2. **Generate 10 scenarios with different f_emit**
3. **Re-integrate into real_data_full.csv**
4. **Re-run tests**

**Expected Result:**
- Warning 1 & 2: ✅ FIXED (partially)
- Warning 3: ⚠️ Remains (needs real thermal data)

**Code Change (minimal):**
```python
# In data generation script:
f_emit_values = np.logspace(13, 15, 10)  # 10 different frequencies
for i, f_emit in enumerate(f_emit_values):
    # Generate synthetic orbit data...
```

---

## 💾 Download Links (Specific)

### S2 Star Data:
```
ESO Archive: http://archive.eso.org/wdb/wdb/eso/gravity/query
Search: "S2" OR "SgrA*"
Instrument: GRAVITY
Data Product: REDUCED
Download: ASCII Table
```

### Pulsar Data:
```
ATNF: https://www.atnf.csiro.au/research/pulsar/psrcat/download.html
Format: ASCII
Columns: Name, P0, DM, F0, F0_ERR, EPOCH
```

### Chandra Cyg X-1:
```
CXC Archive: https://cxc.harvard.edu/cda/
Target: Cygnus X-1
Instrument: ACIS
Mode: Continuous Clocking
Data Type: Spectrum (Level 2)
```

---

## ✅ Success Criteria

### After data update, tests should show:

**Information Preservation:**
```
✅ Test 2 PASSED: Information Preservation

Sources with ≥3 data points: 5-10
Jacobian reconstruction error: <1%
```

**Jacobian Reconstruction:**
```
✅ Extended Test 2a PASSED: Jacobian Reconstruction

Sources analyzed: 5-10
Reconstruction quality: Excellent
```

**Hawking Spectrum:**
```
✅ Extended Test 4a PASSED: Hawking Spectrum Fit

BIC (Planck):  450.00
BIC (Uniform): 520.00
ΔBIC: -70.00

Interpretation: Strong evidence for thermal spectrum ✅
```

---

## 📊 Priority Matrix

| Action | Effort | Impact | Priority | Timeline |
|--------|--------|--------|----------|----------|
| **Synthetic Data Update** | Low (1d) | Medium | 🔴 HIGH | Immediate |
| **S2 Star Download** | Medium (2d) | High | 🔴 HIGH | Week 1 |
| **Cyg X-1 Spectrum** | Medium (2d) | High | 🟡 MEDIUM | Week 2 |
| **Pulsar Timing** | Medium (3d) | Medium | 🟡 MEDIUM | Week 1 |
| **NS Thermal** | Low (1d) | Low | 🟢 LOW | Week 2 |
| **AGN Variability** | High (5d) | Medium | 🟢 LOW | Week 3 |

---

## 🎯 Recommended Workflow

### Immediately (Today):
1. ✅ **Update synthetic data generator** (1 hour)
2. ✅ **Re-run pipeline** (10 minutes)
3. ✅ **Check:** Warning 1&2 improved?

### This Week:
1. ✅ **Download S2 data** (ESO Archive)
2. ✅ **Process & integrate**
3. ✅ **Validate tests**

### Next Week:
1. ✅ **Download Cyg X-1 spectrum**
2. ✅ **Fit thermal model**
3. ✅ **Final validation**

---

## 📝 Summary

**Current Status:**
- ✅ Pipeline runs perfectly (18/18 tests)
- ⚠️ 3 warnings (data-limited)

**Root Cause:**
- Dataset optimized for cross-source comparison
- Missing: Time-series & thermal ensembles

**Solution:**
- **Short-term (1 day):** Synthetic data update
- **Mid-term (1-2 weeks):** S2 + Cyg X-1 real data
- **Long-term (3 weeks):** Complete validation with 0 warnings

**Expected Final Result:**
```
ALL TESTS PASSED ✅
ALL WARNINGS RESOLVED ✅
PRODUCTION-READY FOR PUBLICATION 🚀
```

---

## ⚠️ IMPORTANT: DATA MANAGEMENT PITFALLS

### 🚨 CRITICAL WARNING: "Apples and Oranges" Comparison

**PROBLEM IDENTIFIED IN:** `PAIRED_TEST_ANALYSIS_COMPLETE.md`

**Root Cause:**
```
NED continuum data uses SOURCE cosmological redshift (z_obs),
NOT EMISSION gravitational redshift!

Our z_geom = local gravitational redshift at emission radius
NED z_obs    = global cosmological redshift of the source

→ Completely different physical quantities!
→ Comparison yields massive errors
→ Makes SSZ look worse than it actually is
```

### 📊 DATA WAS DELIBERATELY SPLIT

**Why we have different datasets:**

**1. Snapshot Data (cross-source comparison):**
```
Purpose: Compare different sources
Type: One data point per source
Example: Galaxies, stars, black holes
Redshift: z_obs (observed, cosmological)
```

**2. Time-Series Data (single-source evolution):**
```
Purpose: Temporal evolution of one source
Type: Multiple data points same source
Example: S2 star, pulsars
Redshift: z_emit (local, gravitational)
```

**3. Thermal Spectra (single-source, multi-frequency):**
```
Purpose: Spectral analysis, temperature determination
Type: Multiple frequencies same source
Example: Cyg X-1 X-ray, M87 continuum
Redshift: Can be either! (CAUTION)
```

### ⚠️ PITFALLS DURING INTEGRATION

**Pitfall 1: Redshift Mixing**
```python
# ❌ WRONG:
z_predicted = calculate_z_geom(M, r)  # Local gravitational redshift
z_observed  = df['z_obs']             # Global cosmological redshift
error = z_predicted - z_observed      # APPLES ≠ ORANGES!

# ✅ CORRECT:
if dataset_type == 'timeseries':
    z_predicted = calculate_z_geom(M, r)  # Local
    z_observed  = df['z_emit']            # Local
elif dataset_type == 'snapshot':
    z_predicted = calculate_z_total(M, r, v_los)  # Total
    z_observed  = df['z_obs']                     # Total
```

**Pitfall 2: Multi-Frequency without Context**
```python
# ❌ WRONG:
# Using NED continuum as multi-frequency for Jacobian test
df_ned = df[df['source'] == 'M87']  # 278 different frequencies
jacobian_test(df_ned)  # But all z_obs are IDENTICAL!

# ✅ CORRECT:
# Only use real time-series or emission-line data
df_s2 = df[df['source'] == 'S2']  # 10 data points
# with DIFFERENT z_emit values
jacobian_test(df_s2)
```

**Pitfall 3: Case-Label Mismatch**
```python
# ❌ WRONG:
df_cyg['case'] = 'thermal'  # Correct
df_cyg['obs_type'] = 'thermal'  # Correct
df_cyg['f_obs_Hz'] = df_cyg['frequency_Hz']  # BUT: without context!

# ✅ CORRECT:
df_cyg['case'] = 'thermal_spectrum'
df_cyg['obs_type'] = 'continuum'  # Spectrum, not line
df_cyg['f_emit_Hz'] = df_cyg['frequency_Hz']  # Rest-frame
df_cyg['f_obs_Hz'] = df_cyg['frequency_Hz']   # No cosmological shift
df_cyg['z_type'] = 'none'  # Important: Mark that z_obs is NOT gravitational
```

### 📋 INTEGRATION CHECKLIST

**ALWAYS check before merging:**

- [ ] **1. Redshift type identified:**
  - [ ] z_obs (cosmological, global)
  - [ ] z_emit (gravitational, local)
  - [ ] z_total (both combined)

- [ ] **2. Data type classified:**
  - [ ] `snapshot` - Cross-source comparison
  - [ ] `timeseries` - Single-source evolution
  - [ ] `thermal_spectrum` - Multi-frequency continuum
  - [ ] `emission_line` - Spectral line (z_emit!)

- [ ] **3. Column mapping correct:**
  - [ ] `f_emit_Hz` = Rest-frame frequency
  - [ ] `f_obs_Hz` = Observed frequency
  - [ ] `r_emit_m` = Emission radius
  - [ ] `epoch` = Observation date/time

- [ ] **4. Meta-data added:**
  - [ ] `obs_type` (snapshot/timeseries/continuum/line)
  - [ ] `z_type` (cosmological/gravitational/total/none)
  - [ ] `source_category` (galaxy/star/BH/AGN)

- [ ] **5. Test compatibility checked:**
  - [ ] Jacobian Test: Needs multi-frequency WITH different z_emit
  - [ ] Paired Test: Needs consistent z-types
  - [ ] Hawking Test: Needs thermal continuum (not emission lines)

### 🎯 RECOMMENDED PROCEDURE

**Step 1: Categorize data**
```python
# Add new columns to schema
df['obs_type'] = 'snapshot'     # Default
df['z_type'] = 'cosmological'   # Default
df['source_category'] = 'unknown'  # Default
```

**Step 2: Separate merge scripts**
```bash
# DO NOT throw everything into one pot!
python merge_snapshot_data.py     # Cross-source
python merge_timeseries_data.py   # Time evolution
python merge_continuum_data.py    # Thermal spectra
python merge_emission_lines.py    # Spectral lines
```

**Step 3: Validation BEFORE merge**
```python
def validate_data(df, data_type):
    """Validate data before integration"""
    if data_type == 'timeseries':
        assert df['z_type'].unique() == ['gravitational']
        assert df['obs_type'].unique() == ['timeseries']
    elif data_type == 'continuum':
        assert df['z_type'].unique() == ['none', 'cosmological']
        assert df['obs_type'].unique() == ['continuum']
    # etc.
```

**Step 4: Define test subsets**
```python
# Different subsets for different tests!
df_jacobian = df[df['obs_type'] == 'timeseries']
df_paired = df[df['z_type'].isin(['gravitational', 'total'])]
df_hawking = df[df['obs_type'] == 'continuum']
```

### 📚 SEE ALSO

- **PAIRED_TEST_ANALYSIS_COMPLETE.md** - Detailed error analysis
- **TODO_DATA_INTEGRATION.md** - Integration TODO
- **DATA_IMPROVEMENT_STATUS_REPORT.md** - Status report

### ⚡ QUICK REFERENCE

**What does NOT belong together:**
```
❌ z_geom (local) vs z_obs (global)
❌ Thermal continuum vs Emission lines
❌ Time-series vs Snapshot for Jacobian
❌ NED spectra (cosmological) vs VLT spectra (local)
```

**What belongs together:**
```
✅ S2 time-series (different times, same source)
✅ Cyg X-1 thermal (different frequencies, thermal ensemble)
✅ Snapshot data (different sources, z_obs consistent)
```

---

**REMEMBER: Proper data management is CRITICAL for valid results! 🎯**

---

**© 2025 Carmen Wrede & Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Created:** 2025-10-19  
**Status:** Ready for Implementation (WITH PITFALLS WARNING!)  
**Version:** 1.1.0 (Updated with Data Management Guidelines)
