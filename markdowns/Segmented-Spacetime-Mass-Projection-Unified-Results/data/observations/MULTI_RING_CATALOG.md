# Multi-Ring Observation Catalog

**Purpose:** Catalog of all multi-ring astronomical objects used for SegWave testing  
**Last Updated:** 2025-10-19

---

## 📊 Summary Statistics

| Category | Objects | Total Rings | Avg Rings/Object |
|----------|---------|-------------|------------------|
| Star-forming Regions | 1 | 10 | 10.0 |
| Molecular Clouds | 1 | 3 | 3.0 |
| **TOTAL** | **2** | **13** | **6.5** |

---

## 🔭 Catalog Entries

### 1. G79.29+0.46 (LBV Nebula)

**Category:** Star-forming Region  
**Rings:** 10 (excellent for growth tests)

**Key Properties:**
- Distance: 8.5 kpc
- Temperature: 78K → 20K (strong gradient)
- Velocity: 14.5 → 1.0 km/s (expansion)
- Tracers: CO, NH3, CII, HI

**Source:**
- Paper: Di Francesco et al. (2010), ApJ 719, 451
- DOI: 10.1088/0004-637X/719/1/451
- Data: `G79_29+0_46_CO_NH3_rings.csv`
- Metadata: `G79_29+0_46_metadata.json`

**Quality:** ⭐⭐⭐⭐⭐ (Excellent)
- Peer-reviewed: ✅
- Multiple tracers: ✅
- Clear ring structure: ✅
- Good SNR: ✅

**Suitable For Tests:**
- ✅ Ring growth statistics (10 rings!)
- ✅ Temperature gradients
- ✅ Velocity profiles
- ✅ Multi-tracer consistency

---

### 2. Cygnus X Diamond Ring

**Category:** Molecular Cloud (PDR)  
**Rings:** 3 (minimum for trend analysis)

**Key Properties:**
- Distance: 1.4 kpc
- Temperature: 48K → 36K (moderate gradient)
- Velocity: 1.3 km/s (constant expansion)
- Tracers: CII, CO

**Source:**
- Paper: Schneider et al. (2016), A&A 587, A74
- DOI: 10.1051/0004-6361/201526105
- Data: `CygnusX_DiamondRing_CII_rings.csv`
- Metadata: `CygnusX_DiamondRing_metadata.json`

**Quality:** ⭐⭐⭐⭐ (Very Good)
- Peer-reviewed: ✅
- CII + CO data: ✅
- Clear ring structure: ✅
- Constant velocity: ⚠️ (physics caveat)

**Suitable For Tests:**
- ✅ Constant expansion validation
- ✅ PDR structure
- ✅ Minimum ring count tests
- ⚠️ Growth statistics (only 3 rings)

---

## 📋 Data Format Standard

All ring datasets follow this CSV format:

```csv
ring,radius_pc,T,n,v_obs,v_obs_err,tracers,notes
1,0.30,78,2.0e4,14.5,0.3,"CO(3-2), NH3(2,2)","description"
2,0.45,65,1.5e4,12.0,0.5,"CO(3-2), NH3(1,1)","description"
...
```

**Required Columns:**
- `ring`: Ring number (k)
- `T`: Temperature [K]
- `v_obs`: Observed velocity [km/s]
- `tracers`: Molecular tracers used

**Optional but Recommended:**
- `radius_pc`: Radius [parsec]
- `n`: Density [cm⁻³]
- `v_obs_err`: Velocity uncertainty [km/s]
- `notes`: Observational notes

---

## 🎯 Test Coverage Matrix

| Test Type | G79 | CygnusX | Min Rings | Status |
|-----------|-----|---------|-----------|--------|
| **Ring Growth** | ✅ (10) | ⚠️ (3) | 2 | PASS |
| **Temperature Gradient** | ✅ (10) | ✅ (3) | 2 | PASS |
| **Velocity Profile** | ✅ (10) | ✅ (3) | 3 | PASS |
| **Trend Analysis** | ✅ (10) | ✅ (3) | 3 | PASS |
| **Multi-Tracer** | ✅ (7) | ✅ (2) | 1 | PASS |

**Legend:**
- ✅ Full validation possible
- ⚠️ Minimum data (marginal)
- ❌ Insufficient data

---

## 📈 Expansion Roadmap

### Priority 1: Planetary Nebulae (PLANNED)
- NGC 6543 (Cat's Eye): ~4 rings
- NGC 7293 (Helix): ~3 rings
- **Target:** Add 7 rings, 2 objects

### Priority 2: Circumstellar Disks (PLANNED)
- HL Tauri: ~7 rings (ALMA)
- TW Hydrae: ~4 rings (ALMA)
- **Target:** Add 11 rings, 2 objects

### Priority 3: Supernova Remnants (FUTURE)
- SN 1987A: 3 rings (HST)
- **Target:** Add 3 rings, 1 object

**Future Total:** 7 objects, 34 rings

---

## 🚫 Quality Control

### Data Acceptance Criteria:
- ✅ Peer-reviewed publication
- ✅ ≥2 rings (absolute minimum)
- ✅ Temperature OR velocity data
- ✅ Clear source documentation
- ✅ Consistent format

### Rejection Criteria:
- ❌ Synthetic/simulated data
- ❌ Unpublished observations
- ❌ Single-ring systems
- ❌ Mixed categories in same file
- ❌ Unclear provenance

---

## 📚 References

### Local Papers:
- `papers/validation/Ammonia_observations_in_the_LBV_nebula_G7929046_Di.pdf.md`
- `papers/validation/The_Diamond_Ring_in_Cygnus_X_Advanced_stage_of_an_.pdf.md`

### External Archives:
- NED (NASA/IPAC Extragalactic Database)
- Simbad (CDS Strasbourg)
- ALMA Science Archive
- HST Archive (MAST)

---

© 2025 Carmen Wrede & Lino Casu | ANTI-CAPITALIST SOFTWARE LICENSE v1.4
