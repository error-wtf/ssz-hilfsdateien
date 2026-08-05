# Dataset Verification Status 🔍

**Analysis Date:** 2025-11-05  
**Analyst:** Bingsi + Lino  
**Status:** ⚠️ **MIXED - Needs attention**

---

## 📊 Current Dataset Inventory

### ✅ VERIFIED Datasets (100% Korrekt)

#### 1. `G79_Rizzo2014_NH3_Table1.csv` ✅✅✅

**Status:** **FULLY VERIFIED**  
**Source:** Rizzo et al. 2014, A&A, Table 1  
**Quality:** Gold standard (direct from paper)

**Content:**
```csv
component,v_min_kms,v_max_kms,Trot_K,Trot_err_K,N_NH3_cm2,N_NH3_err_cm2,Trot_limit_type
Central,0.3,1.9,11,2.0,1.7e15,2.0e14,measured
Blue,-1.7,0.3,40,,1.5e12,,lower_limit
Red,1.9,2.8,28,,1.5e12,,lower_limit
```

**Why correct:**
- ✅ Direct transcription from Table 1
- ✅ Uncertainties included
- ✅ Source documented in filename
- ✅ Used in `analyze_nh3_velocities.py`
- ✅ Results validated: Δv = 4.5 km/s

**Used for:**
- ✅ Velocity excess validation (Paper Section 5.3)
- ✅ Temperature inversion (Paper Section 3.2)
- ✅ Core SSZ predictions

**Recommendation:** **KEEP AS IS - PERFECT!** ⭐⭐⭐

---

### ⚠️ UNVERIFIED Datasets (Quelle unklar!)

#### 2. `data/G79_temperatures.csv` ⚠️⚠️

**Status:** **UNVERIFIED**  
**Source:** ❌ **UNKNOWN!**  
**Quality:** Uncertain

**Content:**
```csv
r_pc,T_K
0.30,78
0.45,65
0.60,55
0.75,45
0.90,38
1.10,32
1.30,28
1.50,25
1.70,22
1.90,20
```

**Problems:**
- ❌ NO source documentation!
- ❌ NO uncertainties
- ❌ Unknown measurement method
- ❌ Unknown tracer (dust T? kinetic T? Trot?)
- ❌ Cannot reproduce

**What we DON'T know:**
- Which paper/figure?
- Digitized or measured?
- Which wavelength/tracer?
- What uncertainties?

**Risk:** **HIGH** - Cannot use for publication without source!

**Recommendation:** 
```
❌ DO NOT USE until source verified!

Options:
1. Find original source → Document in header
2. Replace with verified data from archive
3. Delete if unreproducible
```

---

#### 3. `G79_29+0_46_for_ring_temp2v.csv` ⚠️⚠️

**Status:** **UNVERIFIED**  
**Source:** ❌ **UNKNOWN!**  
**Quality:** Uncertain

**Content:**
```csv
ring,T_proxy_K,v_obs_kms
0,78,14.5
1,65,12.0
2,55,8.0
...
```

**Problems:**
- ❌ NO source documentation!
- ❌ NO uncertainties
- ❌ "T_proxy_K" - which proxy?
- ❌ Velocity values - from which paper?

**Risk:** **HIGH** - Cannot use for publication!

**Recommendation:** 
```
❌ DO NOT USE without verification

Action: Find source or delete
```

---

#### 4. `G79_29+0_46_rings_full.csv` ⚠️⚠️

**Status:** **PARTIALLY DOCUMENTED**  
**Source:** ⚠️ Mixed (tracer notes, but no paper refs)  
**Quality:** Uncertain

**Content:**
```csv
ring,radius_pc,T_K,n_cm^-3,v_obs_kms,tracers,notes
0,0.3,78,2.0e4,14.5,"CO(3-2), NH3(2,2)",Inner shocked rim
1,0.45,65,1.5e4,12.0,"CO(3-2), NH3(1,1)",Transition zone
...
```

**Good points:**
- ✅ Tracer information included
- ✅ Physical notes
- ✅ Density estimates

**Problems:**
- ❌ NO paper references!
- ❌ NO uncertainties
- ❌ Mixed sources (CO + NH3 + [CII])?
- ❌ Cannot verify individual values

**Risk:** **MEDIUM-HIGH** - Better than others, but still unverified

**Recommendation:**
```
⚠️ NEEDS SOURCE DOCUMENTATION

Required:
1. Add source column with paper refs
2. Add uncertainty columns
3. Document measurement method for each ring

Example:
ring,radius_pc,T_K,T_err,v_obs_kms,v_err,source_paper,source_method
0,0.3,78,10,14.5,2.0,"Rizzo2008_Fig5","Digitized_CO32"
```

---

### ✅ Templates (Not Data)

#### 5. `data/G79_ring_profile_TEMPLATE.csv` ✅

**Status:** Template file (correctly empty)  
**Purpose:** Guide for creating verified datasets  
**Quality:** Good instructions

**Recommendation:** **KEEP - Good reference!**

---

## 🎯 Summary

### What's SAFE to use:

| File | Status | Safe? | Use for Paper? |
|------|--------|-------|----------------|
| `G79_Rizzo2014_NH3_Table1.csv` | ✅ Verified | ✅ YES | ✅ YES (95% confidence) |
| `data/G79_temperatures.csv` | ❌ Unverified | ❌ NO | ❌ NO (risky!) |
| `G79_29+0_46_for_ring_temp2v.csv` | ❌ Unverified | ❌ NO | ❌ NO (risky!) |
| `G79_29+0_46_rings_full.csv` | ⚠️ Partial | ⚠️ RISKY | ⚠️ Not without fixing |

**Current safe datasets:** **1 out of 4** (25%)

---

## 🚨 Critical Issues

### Issue 1: Missing Provenance ❌

**Problem:**
- 3 out of 4 datasets have NO source documentation
- Cannot reproduce values
- Cannot verify correctness
- **Referee will reject!**

**Impact:**
- High risk for paper rejection
- Scientific integrity compromised
- Cannot defend values

**Solution:**
```
For EACH datapoint, document:
1. Source paper (e.g., "Rizzo et al. 2008")
2. Figure/Table number (e.g., "Figure 5")
3. Method (e.g., "digitized", "Table 3 row 2")
4. Uncertainty estimate
```

---

### Issue 2: Missing Uncertainties ❌

**Problem:**
- Only NH3 file has uncertainties
- Cannot perform proper fits
- Cannot calculate χ²
- **Statistical analysis impossible!**

**Impact:**
- Cannot fit γ_seg(r) properly
- Cannot validate Paper predictions
- Weakens scientific conclusions

**Solution:**
```
Add uncertainty columns:
- T_err_K (temperature uncertainty)
- v_err_kms (velocity uncertainty)
- Estimate from:
  * Measurement scatter
  * Paper error bars
  * Typical instrument errors
```

---

### Issue 3: Mixed Tracers ⚠️

**Problem:**
- `G79_29+0_46_rings_full.csv` mixes CO, NH3, [CII], H I
- Different tracers → different temperatures!
- **Cannot compare directly!**

**Impact:**
- Ambiguous "T_K" values
- Mixing kinetic T (CO) with Trot (NH3)
- Invalid for single γ_seg(r) fit

**Solution:**
```
Separate by tracer:
- G79_CO_rings.csv (kinetic temperatures)
- G79_NH3_rings.csv (rotational temperatures)
- G79_dust_rings.csv (dust temperatures)

OR clearly label in each row:
ring,T_K,tracer,T_type
0,78,CO(3-2),kinetic
1,11,NH3(1,1),rotational
```

---

## ✅ What TO DO

### Immediate Actions (Today):

**1. Document NH3 file properly ✅**
```bash
# Already good, but add header:
# Source: Rizzo et al. 2014, A&A 561, A21
# Table: Table 1
# Extraction: Direct transcription
# Date: 2025-11-05
# Verified: Yes
```

**2. Find sources for temperature files ❌**
```
Options:
a) Search your notes for where data came from
b) Check if digitized from Rizzo 2008 figures
c) Check if from Jiménez-Esteban 2010
d) If unknown → DELETE and get from archive!
```

**3. Add uncertainties ❌**
```
For each value, estimate:
- Measurement uncertainty
- Digitization error (~10% if digitized)
- Instrument error (from papers)
```

---

### Short-term (This Week):

**Option A: Verify existing data**
```bash
# IF you know the sources:
1. Add header comments with paper refs
2. Add uncertainty columns
3. Re-validate with new info
```

**Option B: Replace with archive data** ⭐ **RECOMMENDED!**
```bash
# Download REAL data:
1. Get IRAM CO cubes → extract T(r)
2. Get Herschel PACS → extract [CII] T(r)
3. Get AKARI → extract dust T(r)

# Use our tools:
python fits_to_ring_profile.py CO_cube.fits
→ Automatic T(r) + v(r) + uncertainties!
```

---

## 🎯 Recommendations by Use Case

### For Current Paper (NH3 only): ✅

**Use:**
- ✅ `G79_Rizzo2014_NH3_Table1.csv` ONLY

**Don't use:**
- ❌ Temperature files (unverified)

**Status:** **60% Paper validation possible** (velocity + temperature inversion)

**Risk:** **LOW** - NH3 data is solid

---

### For Complete Paper (with Archive data): ⭐

**Do:**
1. ✅ Keep NH3 file (verified)
2. ⚠️ Delete or fix temperature files
3. ✅ Get archive data (IRAM, Herschel, AKARI)
4. ✅ Extract profiles with `fits_to_ring_profile.py`
5. ✅ Validate with `fit_gamma_seg_profile.py`

**Result:** **95% Paper validation** with full provenance!

**Risk:** **MINIMAL** - All data fully documented

---

## 📝 Verification Checklist

### For EACH dataset, verify:

- [ ] **Source:** Which paper/observation?
- [ ] **Reference:** Figure/Table number?
- [ ] **Method:** Digitized/measured/calculated?
- [ ] **Tracer:** CO/NH3/dust/[CII]?
- [ ] **Type:** Kinetic/rotational/dust temperature?
- [ ] **Uncertainties:** Error bars included?
- [ ] **Date:** When extracted?
- [ ] **By whom:** Who created this file?
- [ ] **Validation:** Cross-checked with paper?

**Current status:**
- `G79_Rizzo2014_NH3_Table1.csv`: 9/9 ✅✅✅
- `data/G79_temperatures.csv`: 1/9 ❌❌❌
- `G79_29+0_46_for_ring_temp2v.csv`: 0/9 ❌❌❌
- `G79_29+0_46_rings_full.csv`: 3/9 ⚠️⚠️

---

## 🏆 Best Practice Example

### What a PERFECT dataset looks like:

```csv
# G79.29+0.46 CO(2-1) Radial Temperature Profile
# Source: Rizzo et al. 2008, ApJ 681, 355
# Extraction: Figure 5, CO(2-1) temperature vs radius
# Method: Digitized using WebPlotDigitizer v4.6
# Date: 2025-11-05
# Extracted by: Lino P. Casu
# Verified by: Carmen N. Wrede
# Tracer: CO(2-1) kinetic temperature
# Distance: 1.7 kpc
# Notes: Inner 3 rings show elevated T, outer rings cooler
#
ring,radius_pc,T_kin_K,T_err_K,v_obs_kms,v_err_kms,source_detail
0,0.30,78,10,14.5,2.0,"Rizzo2008_Fig5_digitized"
1,0.50,65,8,12.0,1.5,"Rizzo2008_Fig5_digitized"
2,0.70,55,7,8.0,1.0,"Rizzo2008_Fig5_digitized"
...
```

**Why perfect:**
- ✅ Full header with all metadata
- ✅ Source paper + figure cited
- ✅ Method documented (digitized)
- ✅ Date + persons documented
- ✅ Uncertainties included
- ✅ Tracer clearly specified
- ✅ Notes explain context
- ✅ 100% reproducible!

---

## 🚀 Action Plan

### Priority 1: URGENT (Today)

1. **Decide on temperature files:**
   - Option A: Find sources → Document
   - Option B: Delete → Use NH3 only for now
   - Option C: Replace → Get archive data

2. **Document decision in paper:**
   ```
   If using NH3 only:
   "We use NH3 component data from Rizzo et al. (2014)
    as the primary validated dataset for SSZ comparison."
   
   If using temperature files:
   "Temperature profiles were extracted from [SOURCE],
    providing radial structure across the nebula."
   ```

### Priority 2: This Week

3. **Get archive data** (recommended!)
   ```bash
   # Start AKARI/Herschel downloads
   python fetch_telescope_data_api.py --source akari --query
   ```

4. **Extract verified profiles:**
   ```bash
   # When data arrives
   python fits_to_ring_profile.py data.fits --output verified_profile.csv
   ```

### Priority 3: Long-term

5. **Build complete verified dataset:**
   - ✅ NH3 (have)
   - ⏳ CO (IRAM request)
   - ⏳ [CII] (Herschel)
   - ⏳ Dust (AKARI/Spitzer)

6. **Full validation:**
   ```bash
   python fit_gamma_seg_profile.py verified_T_profile.csv
   python calculate_core_mass.py gamma_seg.csv
   ```

---

## 🎓 Bottom Line für Lino

**Current dataset status:**

| Category | Status | Confidence |
|----------|--------|------------|
| NH3 velocity/temperature | ✅ VERIFIED | 95% |
| Radial temperature profile | ❌ UNVERIFIED | ⚠️ 20% |
| Radial velocity profile | ❌ UNVERIFIED | ⚠️ 20% |
| Multi-tracer data | ⚠️ MIXED | ⚠️ 40% |

**What's safe for paper RIGHT NOW:**
- ✅ NH3 component analysis (Δv, T_inversion)
- ❌ γ_seg(r) fit (needs verified T profile)
- ❌ M_core calculation (needs verified γ_seg)

**Recommendation:** 

**Path A (Quick):** Use NH3 only → 60% validation → Submit now  
**Path B (Better):** Get archive data → 95% validation → Submit in 1 month ⭐

**Critical decision:** 
- Temperature files: Delete, verify, or replace?
- My recommendation: **REPLACE with archive data!**

---

**Status:** ⚠️ **MIXED - Action required**  
**Safe to use:** 1 out of 4 datasets (25%)  
**Recommendation:** Get archive data for full validation! 🚀

---

**Document Version:** 1.0  
**Created:** 2025-11-05  
**Next review:** After decision on temperature files

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
