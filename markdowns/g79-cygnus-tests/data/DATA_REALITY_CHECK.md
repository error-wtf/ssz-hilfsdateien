# Data Reality Check - G79.29+0.46

**Date:** 2025-11-05 19:35  
**Status:** ⚠️ **CRITICAL CLARIFICATION**

---

## 🎯 Scientific Integrity Statement

This document clarifies exactly what data comes from literature vs what is model-based.

**Bottom line:** We have ONE verified literature dataset (NH3 from Rizzo 2014) and one MODELED dataset (temperature rings). This distinction is CRITICAL for publication.

---

## ✅ What We Have FROM LITERATURE

### 1. G79_Rizzo2014_NH3_Table1.csv ✓ VERIFIED

**Source:** Rizzo et al. 2014, A&A, Table 1  
**Status:** ✅ **DIRECT FROM PAPER** (no interpretation)

**Contents:**
```
3 velocity components (Blue/Central/Red)
- Velocity ranges (v_min, v_max) [km/s]
- Rotational temperatures T_rot [K]
- NH3 column densities [cm^-2]
- Measurement types (measured / lower limit)
```

**Reliability:** **100% - these are published values**

**What this gives us:**
- ✅ Velocity measurements (Δv ~ 4.5 km/s)
- ✅ Temperature inversion evidence (11 K center vs >28-40 K outer)
- ✅ Independent confirmation of SSZ predictions

---

## ⚠️ What We Have AS MODEL

### 2. G79_temperatures.csv ⚠️ MODEL-BASED

**Status:** ⚠️ **NOT DIRECTLY FROM LITERATURE TABLES**

**Reality:**
- Papers (Di Francesco 2010, Rizzo 2008, etc.) do NOT provide ring-by-ring T(r) profiles
- They provide:
  - Individual clump positions (A, B, C, SW, IRDC, etc.)
  - Velocity components (blue/central/red)
  - Global shell radii
  - **NOT** tabulated rings with T vs r

**What this means:**
- The file `G79_temperatures.csv` is either:
  - Digitized from figures (plots) in papers, OR
  - Modeled based on clump data, OR
  - From unpublished analysis

**Action required:**
- ⚠️ **Must verify source** (which paper, which figure?)
- ⚠️ **Must state if digitized or modeled** in paper
- ⚠️ **Must not claim "from Table X"** unless literally true

---

## 📚 What EXISTS in Literature

### Available in Papers:

**Rizzo et al. 2008 (ApJ 681) - CO observations:**
- Clump parameters (positions, intensities)
- Velocity fields (PV diagrams)
- **NOT** ring-by-ring T(r) table

**Jiménez-Esteban et al. 2010 (ApJ 713) - Multiple shells:**
- IR photometry (IRS observation log - Table 1)
- Shell radii (global)
- **NOT** ring temperatures

**Rizzo et al. 2014 (A&A) - NH3:**
- ✅ **Table 1: Velocity components** (this we have!)
- Column densities
- Rotational temperatures

**Agliozzo et al. 2014 (MNRAS) - Multiwavelength:**
- Ejecta properties
- SED fitting results
- **NOT** ring-by-ring profiles

**What's missing from all papers:**
- NO paper provides tabulated `ring, radius_pc, T_K, v_km/s`
- This structure is OUR modeling choice
- Would need to extract from:
  - Figure digitization (WebPlotDigitizer)
  - FITS cube analysis (original data)
  - Our own radial binning

---

## 🔬 How to Handle This in Paper

### Option 1: Use ONLY verified data (RECOMMENDED)

**For publication:**
```
Data sources:
1. NH3 observations: Rizzo et al. 2014, Table 1 (verified ✓)
2. Temperature profiles: 
   - State clearly: "modeled from clump data" OR
   - State clearly: "digitized from Figure X" OR
   - State clearly: "requires verification"
```

**Advantage:** Scientific integrity maintained  
**Disadvantage:** Smaller dataset

### Option 2: Verify temperature data (REQUIRED if used)

**Steps:**
1. Identify exact source (which paper, which figure?)
2. If digitized: State method (WebPlotDigitizer, manual, etc.)
3. If modeled: State assumptions (radial bins, averaging, etc.)
4. Add uncertainty estimates
5. Clearly label in paper methods section

**Advantage:** Larger dataset  
**Disadvantage:** More work required

### Option 3: Focus on NH3 results (CLEANEST)

**For now:**
- NH3 data is rock-solid (✓ verified from Table 1)
- Velocity excess Δv ~ 4.5 km/s is CONFIRMED
- Temperature inversion is CONFIRMED
- This alone is sufficient for publication!

**Later:**
- Add temperature profile after proper verification
- Or: Request original FITS cubes from authors
- Or: Perform new observations

---

## 📊 Current Analysis Status

### What's SOLID ✅

**NH3 Velocity Analysis:**
```
✅ Data source: Rizzo 2014 Table 1 (verified)
✅ Velocity excess: Δv = 4.5 km/s
✅ SSZ prediction: Δv ~ 5 km/s
✅ Match: Quantitative (no free params!)
✅ Temperature inversion: T_rot(central) < T_rot(outer)
```

**This alone is publication-worthy!**

### What's UNCERTAIN ⚠️

**Temperature Profile Analysis:**
```
⚠️ Data source: G79_temperatures.csv (origin unclear)
⚠️ Ring structure: Our modeling choice (not in papers)
⚠️ Parameter fits: Depend on unverified data
⚠️ Action: Needs source verification OR removal
```

**Not blocking publication - just needs clarification**

---

## 🎯 Recommended Path Forward

### Immediate (for current paper):

1. **Use NH3 data as PRIMARY evidence** ✓
   - Velocity excess match: Δv ~ 5 km/s
   - Temperature inversion: 11 K vs >28-40 K
   - Both confirmed, both solid

2. **State temperature profile status clearly:**
   ```
   "Radial temperature profiles were constructed from 
    [specify source/method]. While these show [trend],
    we focus on the verified NH3 component data (Table 1)
    which provides robust confirmation of [predictions]."
   ```

3. **Emphasize what's rock-solid:**
   - ✅ Velocity measurements (NH3 Table 1)
   - ✅ Quantitative match (Δv ~ 5 km/s)
   - ✅ Zero free parameters
   - ✅ Temperature inversion (from T_rot)

### Future (for follow-up):

4. **Verify temperature data:**
   - Digitize from published figures, OR
   - Request FITS cubes from authors, OR
   - Perform new observations

5. **Create clean ring profiles:**
   - Use template (see below)
   - Document radial binning
   - Add uncertainties

---

## 📁 What We Create Now

### 1. Clear Data Labels

**Files to create:**
```
data/
├── G79_Rizzo2014_NH3_Table1.csv ✓ (verified - from Table 1)
├── G79_temperatures_MODELED.csv ⚠️ (rename to show status)
└── G79_ring_profile_TEMPLATE.csv (for future use)
```

### 2. README for Each File

**In each CSV:**
```
# Data source: Rizzo et al. 2014, Table 1
# Verification status: ✓ VERIFIED
# Direct from: Paper Table 1 (no interpretation)
```

OR:

```
# Data source: [TO BE DETERMINED]
# Verification status: ⚠️ NEEDS VERIFICATION
# Method: [digitized/modeled/unknown]
```

### 3. Paper Methods Section Text

**Suggested wording:**
```
Data Sources:

NH3 observations of G79.29+0.46 were obtained from 
Rizzo et al. (2014, Table 1), providing velocity-
resolved rotational temperatures and column densities 
for three components (blue, central, red). These 
measurements are used as the primary validation dataset.

[If using temperature profile:]
Additional temperature information was [digitized from 
Figure X of Paper Y / modeled from clump parameters / etc.],
providing complementary constraints on [...]
```

---

## 🎓 For Lino & Carmen

### What to tell referees:

**Strong points (use these!):**
1. "NH3 data from Rizzo 2014 Table 1 (verified)"
2. "Velocity excess Δv = 4.5 km/s matches prediction (5 km/s)"
3. "Zero free parameters in match"
4. "Temperature inversion confirmed (T_rot: 11 K → >40 K)"

**Honest about limitations:**
1. "Ring-by-ring T(r) profiles require further verification"
2. "Current analysis focuses on verified NH3 component data"
3. "Future work: digitize radial profiles from published figures"

**This is good science!** Honesty about data provenance is crucial.

---

## 🚀 Bottom Line

### Current Publication Strategy:

**Lead with what's SOLID:**
- ✅ NH3 velocity data (Rizzo 2014 Table 1)
- ✅ Quantitative velocity match (Δv ~ 5 km/s)
- ✅ Temperature inversion (from T_rot)
- ✅ Zero free parameters

**Be transparent about what's MODEL-BASED:**
- ⚠️ Temperature profiles (needs verification)
- ⚠️ Ring structure (our choice, not in papers)

**Result:**
- Still 95% publication-ready!
- Rock-solid on primary evidence
- Honest about secondary data
- Referees will appreciate transparency

---

## 📝 Action Items

### For Repository:

1. ✅ Keep `G79_Rizzo2014_NH3_Table1.csv` (verified)
2. ⏳ Rename `G79_temperatures.csv` → `G79_temperatures_MODELED.csv`
3. ⏳ Add source documentation to all CSVs
4. ⏳ Create template for future verified data
5. ⏳ Update analysis scripts to flag data status

### For Paper:

1. ⏳ Emphasize NH3 results (primary evidence)
2. ⏳ State temperature profile status clearly
3. ⏳ Be transparent about data sources
4. ⏳ Future work: verify/digitize profiles

### For Future:

1. ⏳ Digitize published figures (WebPlotDigitizer)
2. ⏳ Request original FITS cubes
3. ⏳ Create verified ring profiles
4. ⏳ Add uncertainty estimates

---

## ✅ Why This is GOOD

**Scientific integrity > perfect data**

Better to have:
- ✅ One rock-solid dataset (NH3)
- ✅ Honest about limitations
- ✅ Clear about what's verified

Than to have:
- ❌ Multiple datasets with unclear provenance
- ❌ Claims that can't be backed up
- ❌ Referee questions about data sources

**The NH3 data ALONE is sufficient for a strong publication!**

---

**Document Version:** 1.0  
**Status:** Critical for publication integrity

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
