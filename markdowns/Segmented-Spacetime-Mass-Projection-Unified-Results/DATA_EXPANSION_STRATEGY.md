# Data Expansion Strategy - Clean Multi-Ring Datasets

**Goal:** Fix "only 1 ring" test issues with MORE REAL DATA  
**Priority:** Avoid "Datenmischmasch" - Keep data sources clean and separated  
**Date:** 2025-10-19

---

## 🎯 PROBLEM STATEMENT

**Current Issue:**
- Tests pass without validation due to single-ring datasets
- Need multi-ring data for meaningful growth/trend tests

**Solution:**
- ✅ Add MORE real multi-ring observations
- ❌ NO mixing synthetic with real data
- ❌ NO mixing different observation types
- ✅ Clear source documentation

---

## 📊 CURRENT RING DATA INVENTORY

### ✅ Existing Multi-Ring Datasets

1. **G79.29+0.46 (Star-forming Region)**
   - File: `data/observations/G79_29+0_46_CO_NH3_rings.csv`
   - Rings: 5 rings (k=1 to k=5)
   - Source: CO + NH₃ observations
   - Quality: ✅ Excellent (peer-reviewed)
   - Papers: `Ammonia_observations_in_the_LBV_nebula_G7929046_Di.pdf.md`

2. **Cygnus X Diamond Ring**
   - File: `data/observations/CygnusX_DiamondRing_CII_rings.csv`
   - Rings: 4 rings (k=1 to k=4)
   - Source: CII observations
   - Quality: ✅ Excellent (peer-reviewed)
   - Papers: `The_Diamond_Ring_in_Cygnus_X_Advanced_stage_of_an_.pdf.md`

**Total:** 2 objects, 9 rings combined

---

## 🔍 ADDITIONAL MULTI-RING CANDIDATES

### Category A: Planetary Nebulae (Ring Structures)

**Known Multi-Ring Systems:**

1. **NGC 6543 (Cat's Eye Nebula)**
   - Expected: 3-5 concentric rings
   - Source: HST/Chandra observations
   - Available: NED, Simbad
   - Data Type: Emission line velocities + temperatures

2. **NGC 7293 (Helix Nebula)**
   - Expected: 2-3 main rings + outer halo
   - Source: HST/ALMA observations
   - Available: Public archives
   - Data Type: Multi-wavelength ring structure

3. **NGC 3132 (Southern Ring Nebula)**
   - Expected: 2-4 rings (JWST revealed fine structure)
   - Source: JWST NIRCam + MIRI
   - Available: MAST archive (2022+)
   - Data Type: Temperature + velocity profiles

### Category B: Circumstellar Disks (Ringed Structures)

4. **HL Tauri**
   - Expected: 7+ concentric rings
   - Source: ALMA high-resolution
   - Available: ALMA archive
   - Data Type: Dust continuum + gas emission

5. **TW Hydrae**
   - Expected: 3-4 prominent gaps/rings
   - Source: ALMA observations
   - Available: Public
   - Data Type: CO emission, dust

6. **AS 209**
   - Expected: 4-5 rings
   - Source: DSHARP survey (ALMA)
   - Available: Public archive
   - Data Type: Continuum + line emission

### Category C: Supernova Remnants (Expanding Rings)

7. **SN 1987A**
   - Expected: 3 rings (inner + 2 outer)
   - Source: HST + Chandra long-term monitoring
   - Available: Public
   - Data Type: Expansion velocities, X-ray

---

## ✅ DATA QUALITY REQUIREMENTS

### Must Have:
- [ ] Multiple rings (≥2, preferably ≥3)
- [ ] Velocity measurements per ring
- [ ] Temperature data (T_k) OR frequency data (f_k)
- [ ] Clear ring identification (k=1, k=2, etc.)
- [ ] Peer-reviewed source paper

### Nice to Have:
- [ ] Radius measurements (r_k)
- [ ] Density profiles (n_k)
- [ ] Multiple transitions/lines
- [ ] Time-series data

### Must Avoid:
- ❌ Mixing objects from different categories
- ❌ Synthetic/simulated data mixed with real
- ❌ Unpublished/unverified observations
- ❌ Single-ring systems (defeats purpose)

---

## 🔧 IMPLEMENTATION STRATEGY

### Phase 1: Curate Existing Data (HIGH PRIORITY - 1 hour)

**Action: Create category-organized dataset structure**

```
data/observations/
├── star_forming_regions/
│   ├── G79_29+0_46_CO_NH3_rings.csv (5 rings) ✅
│   └── [add similar objects]
│
├── planetary_nebulae/
│   ├── NGC_6543_rings.csv (target: 3-5 rings)
│   ├── NGC_7293_rings.csv (target: 2-3 rings)
│   └── metadata.json
│
├── circumstellar_disks/
│   ├── HL_Tauri_rings.csv (target: 7 rings)
│   ├── TW_Hya_rings.csv (target: 3-4 rings)
│   └── metadata.json
│
├── supernova_remnants/
│   ├── SN1987A_rings.csv (3 rings)
│   └── metadata.json
│
└── molecular_clouds/
    ├── CygnusX_DiamondRing_CII_rings.csv (4 rings) ✅
    └── metadata.json
```

**Metadata Format:**
```json
{
  "object_name": "NGC 6543",
  "category": "planetary_nebula",
  "n_rings": 4,
  "source_paper": "DOI or ADS link",
  "observation_date": "2020-01-15",
  "instrument": "HST/WFC3",
  "data_type": "emission_line_velocities",
  "verified": true,
  "peer_reviewed": true
}
```

---

### Phase 2: Fetch Clean Multi-Ring Data (2 hours)

**Priority Order:**

1. **Planetary Nebulae (Easiest):**
   - NGC 6543: NED spectrum + Simbad
   - NGC 7293: Public HST data
   - Clear ring structures, well-studied

2. **Circumstellar Disks (ALMA Data):**
   - HL Tauri: ALMA Science Archive
   - TW Hya: DSHARP public data
   - High quality, many rings

3. **SNR (If needed):**
   - SN 1987A: HST archive
   - Well-documented expansion

**Data Extraction Pipeline:**
```python
# scripts/data_curation/fetch_ring_data.py

def fetch_planetary_nebula_rings(object_name):
    """
    Fetch multi-ring data from NED/Simbad for planetary nebulae.
    
    Returns clean CSV with:
    - k (ring number)
    - v_k (velocity)
    - T_k (temperature)
    - r_k (radius, if available)
    - source_reference
    """
    # Query NED
    # Parse spectral lines
    # Identify ring structures
    # Return DataFrame
    pass

def verify_data_quality(df, min_rings=2):
    """
    Verify data meets quality standards.
    
    Checks:
    - ≥ min_rings rows
    - Required columns present
    - No NaN in critical columns
    - Velocities positive
    - Monotonic radius (if present)
    """
    assert len(df) >= min_rings, f"Need ≥{min_rings} rings"
    assert 'k' in df.columns
    assert 'v_k' in df.columns or 'T_k' in df.columns
    # ... more checks
    return True
```

---

### Phase 3: Update Tests with Real Multi-Ring Data (1 hour)

**Strategy: Parametrized tests with known-good datasets**

```python
# tests/test_segwave_core.py

import pytest
from pathlib import Path

# Define all available multi-ring datasets
MULTI_RING_DATASETS = [
    ("star_forming_regions/G79_29+0_46_CO_NH3_rings.csv", 5),
    ("molecular_clouds/CygnusX_DiamondRing_CII_rings.csv", 4),
    ("planetary_nebulae/NGC_6543_rings.csv", 4),  # NEW
    ("planetary_nebulae/NGC_7293_rings.csv", 3),  # NEW
    ("circumstellar_disks/HL_Tauri_rings.csv", 7),  # NEW
]

@pytest.mark.parametrize("dataset,expected_rings", MULTI_RING_DATASETS)
def test_ring_growth_real_data(dataset, expected_rings):
    """Test ring growth with REAL multi-ring observations."""
    
    # Load data
    df = pd.read_csv(f"data/observations/{dataset}")
    
    # Verify sufficient rings
    assert len(df) >= 2, f"Dataset {dataset} needs ≥2 rings"
    assert len(df) == expected_rings, f"Expected {expected_rings} rings"
    
    # Perform REAL test with REAL data
    growth_stats = calculate_growth(df)
    
    print(f"\n{'='*80}")
    print(f"RING GROWTH: {dataset}")
    print(f"{'='*80}")
    print(f"Object: {dataset.split('/')[1].replace('_rings.csv', '')}")
    print(f"Rings: {len(df)}")
    print(f"Growth mean: {growth_stats.mean:.3f}")
    print(f"Growth range: [{growth_stats.min:.3f}, {growth_stats.max:.3f}]")
    
    # Real assertions
    assert len(growth_stats) == len(df) - 1
    assert growth_stats.mean > 0  # Expect expanding rings
    assert all(g >= 0 for g in growth_stats)  # Physical constraint
```

**Result:**
- 5 test runs (one per dataset)
- All with ≥2 rings (real validation)
- No "only 1 ring" passes
- Clear test output per object

---

## 🚫 ANTI-PATTERNS TO AVOID

### ❌ DON'T: Mix Categories
```python
# BAD - Mixing planetary nebula with disk
df = pd.concat([
    load("NGC_6543_rings.csv"),      # Planetary nebula
    load("HL_Tauri_rings.csv")       # Protoplanetary disk
])
# These have DIFFERENT physics!
```

### ❌ DON'T: Mix Real + Synthetic
```python
# BAD - Real data contaminated with synthetic
real_rings = load("G79_rings.csv")
synthetic = generate_synthetic_rings()
combined = pd.concat([real_rings, synthetic])  # ❌
```

### ❌ DON'T: Mix Different Tracers
```python
# BAD - CO velocity vs CII velocity (different physics)
df = pd.concat([
    load("object_CO_rings.csv"),
    load("object_CII_rings.csv")
])
# These trace different gas phases!
```

### ✅ DO: Keep Categories Separated
```python
# GOOD - Test each category independently
@pytest.mark.parametrize("category,datasets", [
    ("planetary_nebulae", ["NGC_6543", "NGC_7293"]),
    ("circumstellar_disks", ["HL_Tauri", "TW_Hya"]),
])
def test_by_category(category, datasets):
    """Test each astronomical category separately."""
    for obj in datasets:
        df = load(f"data/observations/{category}/{obj}_rings.csv")
        # Test with consistent physics assumptions
```

---

## 📋 DATA COLLECTION CHECKLIST

### For Each New Dataset:

- [ ] **Source Verification**
  - [ ] Peer-reviewed paper exists
  - [ ] DOI/ADS bibcode recorded
  - [ ] Observation date documented
  
- [ ] **Data Quality**
  - [ ] ≥2 rings present
  - [ ] Velocity or temperature per ring
  - [ ] No NaN in critical columns
  - [ ] Physical units documented
  
- [ ] **Metadata Documentation**
  - [ ] Object classification clear
  - [ ] Instrument/telescope recorded
  - [ ] Data processing steps noted
  - [ ] Any caveats documented
  
- [ ] **File Organization**
  - [ ] Placed in correct category folder
  - [ ] Consistent CSV format
  - [ ] metadata.json updated
  - [ ] Paper reference added to papers/

- [ ] **Test Integration**
  - [ ] Added to MULTI_RING_DATASETS list
  - [ ] Parametrized test includes it
  - [ ] Expected ring count specified
  - [ ] Test passes with real data

---

## 🎯 SUCCESS CRITERIA

### After Data Expansion:

**Quantitative:**
- [ ] ≥5 multi-ring datasets (currently 2)
- [ ] ≥20 total rings across all objects (currently 9)
- [ ] All ring datasets have ≥2 rings
- [ ] 100% of ring tests use real data
- [ ] 0 "only 1 ring" test passes

**Qualitative:**
- [ ] Each dataset category-isolated
- [ ] Clear source documentation
- [ ] Peer-reviewed sources only
- [ ] No synthetic/real mixing
- [ ] Tests clearly labeled by category

### Test Output Example (Target):

```
tests/test_segwave_core.py::test_ring_growth[G79_rings-5] PASSED
tests/test_segwave_core.py::test_ring_growth[CygnusX_rings-4] PASSED
tests/test_segwave_core.py::test_ring_growth[NGC6543_rings-4] PASSED
tests/test_segwave_core.py::test_ring_growth[NGC7293_rings-3] PASSED
tests/test_segwave_core.py::test_ring_growth[HL_Tauri_rings-7] PASSED

5 passed, 0 skipped, 0 failed
All tests validated with REAL multi-ring data ✅
```

---

## 📚 DOCUMENTATION UPDATES

After data expansion, update:

1. **DATA_COLUMNS_README.md**
   - Add new ring dataset descriptions
   - Document categories

2. **Sources.md / sources.json**
   - Add new object references
   - Include paper DOIs

3. **papers/validation/**
   - Add source papers for new objects
   - Link to data files

4. **README.md**
   - Update data statistics
   - Mention multi-ring coverage

---

## 🚀 EXECUTION PLAN

### Phase 1: TODAY (1 hour)
- [ ] Organize existing data into categories
- [ ] Create metadata.json files
- [ ] Document G79 + CygnusX properly

### Phase 2: TOMORROW (2 hours)
- [ ] Fetch NGC 6543 rings (NED/Simbad)
- [ ] Fetch NGC 7293 rings (HST archive)
- [ ] Fetch HL Tauri rings (ALMA archive)

### Phase 3: DAY 3 (1 hour)
- [ ] Update test_segwave_core.py with parametrized tests
- [ ] Run full test suite
- [ ] Verify: 0 "only 1 ring" passes

**Total Time:** 4 hours for solid, clean multi-ring coverage

---

## 💡 KEY PRINCIPLES

1. **Quality over Quantity:** 5 clean datasets > 20 mixed datasets
2. **Category Separation:** Each type tests consistent physics
3. **Source Documentation:** Always traceable to peer-reviewed paper
4. **No Mixing:** Keep synthetic, real, and different categories apart
5. **Test Clarity:** Each test should clearly state what it validates

**Result:** Robust tests with REAL multi-ring data, no "Datenmischmasch"! ✅

---

© 2025 Carmen Wrede & Lino Casu | ANTI-CAPITALIST SOFTWARE LICENSE v1.4
