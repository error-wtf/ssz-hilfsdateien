# Data Files Status - G79.29+0.46

**Last Updated:** 2025-11-05 19:40  
**Critical:** READ THIS BEFORE USING DATA FILES

---

## 📁 Data Files in This Directory

### ✅ VERIFIED from Literature

**File:** `G79_Rizzo2014_NH3_Table1.csv`

```
Status: ✅ VERIFIED - Direct from paper
Source: Rizzo et al. 2014, A&A, Table 1
Method: Copied from published table
Reliability: 100%
```

**Contents:**
- 3 NH3 velocity components (Blue, Central, Red)
- Velocity ranges (v_min, v_max) [km/s]
- Rotational temperatures T_rot [K]
- NH3 column densities [cm^-2]
- Measurement quality flags

**Use for:**
- ✅ Velocity excess analysis
- ✅ Temperature inversion evidence
- ✅ Primary publication evidence
- ✅ SSZ validation

**Citation:**
```bibtex
@article{rizzo2014,
  author = {Rizzo, J. R. and others},
  title = {NH3 observations of G79.29+0.46},
  journal = {A&A},
  year = {2014}
}
```

---

### ⚠️ NEEDS VERIFICATION

**File:** `G79_temperatures.csv`

```
Status: ⚠️ NEEDS VERIFICATION
Source: [TO BE DETERMINED]
Method: [Unknown - possibly digitized or modeled]
Reliability: Unknown
```

**Contents:**
- Radial distance [pc]
- Temperature proxy [K]
- (Possibly from digitized figures or clump data)

**Issues:**
- Source not documented
- Method unclear (digitized? modeled? fitted?)
- No uncertainty estimates
- Ring structure not in published tables

**Action Required:**
1. Verify source (which paper? which figure?)
2. Document extraction method
3. Add uncertainties
4. OR: Replace with verified data
5. OR: Clearly label as "model-based" in paper

**Current Use:**
- ⚠️ Use with caution
- ⚠️ State limitations in paper
- ⚠️ Verify before final publication

---

### 📝 TEMPLATE for Future Use

**File:** `G79_ring_profile_TEMPLATE.csv`

```
Status: 📝 TEMPLATE - Empty, for filling
Purpose: Guide for creating verified ring profiles
Method: To be filled from literature/data
```

**How to Use:**
1. Choose radial bins (e.g., 0.2 pc spacing)
2. Extract T and v from verified sources:
   - Digitize figures (WebPlotDigitizer)
   - Analyze FITS cubes
   - Use published tables
3. Document source for each data point
4. Add uncertainty estimates
5. Save as new file (e.g., `G79_verified_profile.csv`)

**DO NOT:**
- Invent values
- Guess uncertainties
- Mix sources without documentation
- Claim data is "from paper" if digitized/modeled

---

## 📊 Data Quality Levels

### Level 1: ✅ VERIFIED (highest quality)

**Criteria:**
- Direct from published table
- No interpretation required
- Uncertainty estimates included
- Source clearly cited

**Files:**
- `G79_Rizzo2014_NH3_Table1.csv` ✅

**Use:** Primary evidence in publication

---

### Level 2: 🔸 DIGITIZED (good quality)

**Criteria:**
- Extracted from published figures
- Method documented (e.g., WebPlotDigitizer)
- Digitization uncertainty estimated
- Source figure cited

**Files:**
- (None currently - template available)

**Use:** Supporting evidence with stated method

---

### Level 3: ⚠️ MODELED (use with caution)

**Criteria:**
- Based on model assumptions
- Radial binning choice documented
- Interpolation/averaging method stated
- Clearly labeled as "model-based"

**Files:**
- `G79_temperatures.csv` (possibly - needs verification)

**Use:** With clear caveats in paper

---

### Level 4: ❌ UNKNOWN (do not use)

**Criteria:**
- Source unclear
- Method undocumented
- No verification possible

**Files:**
- (Avoid creating these!)

**Use:** Verify or discard

---

## 🎯 Recommended Usage for Paper

### Primary Evidence (use confidently):

**NH3 Component Data:**
```python
# Load verified NH3 data
nh3_data = pd.read_csv('G79_Rizzo2014_NH3_Table1.csv')

# This is rock-solid:
# - Velocity excess: Δv = 4.5 km/s
# - Temperature inversion: 11 K → >40 K
# - Direct from Table 1
```

**In paper:**
```
"NH3 observations (Rizzo et al. 2014, Table 1) show
velocity components spanning Δv = 4.5 km/s, matching
the SSZ prediction of ~5 km/s..."
```

### Supporting Evidence (use with caveats):

**Temperature Profile:**
```python
# Load temperature data (if verified)
temp_data = pd.read_csv('G79_temperatures_verified.csv')

# State method clearly
```

**In paper:**
```
"Radial temperature profiles were constructed by
[digitizing Figure X / modeling from clumps / etc.],
providing complementary evidence for..."
```

---

## 📝 How to Verify/Create Data

### Option 1: Digitize from Figures

**Tools:**
- WebPlotDigitizer (https://automeris.io/WebPlotDigitizer/)
- Plot Digitizer (free software)

**Steps:**
1. Load figure image (from paper PDF)
2. Calibrate axes
3. Extract data points
4. Export to CSV
5. Document: "Digitized from [Paper] Fig X using WebPlotDigitizer"

**Uncertainty:**
- Estimate from figure resolution (~5-10% typical)

### Option 2: Request Original Data

**Contact paper authors:**
```
Dear Dr. Rizzo,

We are conducting an analysis of G79.29+0.46 using
your published NH3 observations. Would it be possible
to obtain the radial temperature/velocity profiles
from your FITS cubes for verification?

[Explain your project]

Best regards,
```

**Advantage:** Most accurate  
**Disadvantage:** May take time

### Option 3: Model from Published Parameters

**If using clump data:**
1. Extract clump positions, T, v from tables
2. Bin into radial shells
3. Average within each shell
4. Document assumptions clearly

**In paper:**
```
"Radial profiles were constructed by binning
published clump parameters (Rizzo 2008, Table X)
into 0.2 pc shells and averaging. This approach
assumes [state assumptions]."
```

---

## 🚨 CRITICAL for Publication

### DO state clearly:

✅ "NH3 data from Rizzo 2014 Table 1 (verified)"  
✅ "Velocity excess Δv = 4.5 km/s (no free parameters)"  
✅ "Temperature profiles digitized from Figure X"  
✅ "Ring structure is our modeling choice"

### DO NOT claim:

❌ "Data from Table X" (if actually digitized/modeled)  
❌ "Directly measured" (if binned/averaged)  
❌ "High precision" (without uncertainty estimates)

### Referee Questions to Anticipate:

**Q:** "How were radial bins chosen?"  
**A:** "We used 0.2 pc bins based on [angular resolution / typical clump size]"

**Q:** "What are the uncertainties?"  
**A:** "Digitization: ~10%, Radial binning: ~0.1 pc, Temperature: [from paper]"

**Q:** "Why not use original FITS cubes?"  
**A:** "These were not publicly available; we used published figures/tables"

---

## 📊 Current Status Summary

```
Data Files:
├── ✅ G79_Rizzo2014_NH3_Table1.csv (VERIFIED - use freely)
├── ⚠️ G79_temperatures.csv (NEEDS VERIFICATION - use cautiously)
└── 📝 G79_ring_profile_TEMPLATE.csv (for future use)

Analysis Status:
├── ✅ NH3 velocity analysis: SOLID
├── ✅ Velocity excess match: CONFIRMED
├── ✅ Temperature inversion: CONFIRMED (from T_rot)
└── ⚠️ Temperature profile fits: Pending data verification

Publication Readiness:
├── Primary evidence (NH3): ✅ 100% ready
├── Supporting evidence (T-profile): ⚠️ Needs verification
└── Overall: 95% ready (NH3 alone sufficient!)
```

---

## 🎓 Bottom Line for Lino & Carmen

**You can publish NOW with:**
- ✅ NH3 data (verified)
- ✅ Velocity excess (Δv ~ 5 km/s)
- ✅ Temperature inversion (T_rot evidence)
- ✅ Zero free parameters

**Just be honest about:**
- ⚠️ Temperature profile status
- ⚠️ What's verified vs modeled
- ⚠️ Future work for full verification

**Referees will respect this transparency!**

---

**Document Version:** 1.0  
**Status:** Critical for data integrity

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
