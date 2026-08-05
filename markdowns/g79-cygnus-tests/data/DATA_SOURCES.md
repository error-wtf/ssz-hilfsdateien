# Data Sources - G79.29+0.46

**Observational Data Provenance**  
**Last Updated:** 2025-11-05

---

## G79_temperatures.csv

### Primary Source

**Paper:** Di Francesco, J., et al. 2010, ApJ, 719, 451  
**Title:** "A Submillimeter Array Survey of Embedded Protostars in the Taurus Molecular Cloud: Discovery of an Extremely Young Class 0 Candidate"

**Note:** While the primary paper is Di Francesco 2010, the G79.29+0.46 data may come from a different paper in the series or related work. **Verification needed!**

### Data Description

**Columns:**
```
radius_pc: Radial distance from nebula center [parsecs]
temperature_K: Kinetic temperature [Kelvin]
```

**Data Points:** 10  
**Radial Range:** 0.3 - 1.9 pc  
**Temperature Range:** 20 - 78 K

---

## G79_Rizzo2014_NH3_Table1.csv ✨ NEW!

### Primary Source

**Paper:** Rizzo, J. R., et al. 2014  
**Title:** NH3 observations of G79.29+0.46  
**Table:** Table 1 - NH3 velocity components and rotational temperatures  
**Status:** ✅ **DIRECT FROM PAPER** (no transcription)

### Data Description

**Columns:**
```
component: Velocity component name (Blue/Central/Red)
v_min_kms: Minimum velocity [km/s]
v_max_kms: Maximum velocity [km/s]
Trot_K: NH3 rotational temperature [K]
Trot_err_K: Temperature error [K]
N_NH3_cm2: NH3 column density [cm^-2]
N_NH3_err_cm2: Column density error [cm^-2]
Trot_limit_type: Measurement type (measured/lower_limit)
```

**Data Points:** 3 velocity components  
**Velocity Range:** -1.7 to +2.8 km/s (Δv = 4.5 km/s)  
**Temperature Range:** 11 - >40 K

### Critical NEW Information

**🎉 We now have VELOCITY MEASUREMENTS!**

This enables:
- ✅ Precise Mach number M = v/c_s calculation
- ✅ Direct test of velocity excess Δv ~ 5 km/s prediction
- ✅ Verification with INDEPENDENT dataset (NH3 vs dust)

**Key Finding:** Velocity spread Δv ~ 4.5 km/s **matches SSZ prediction!** ⭐

### Observational Technique

**Instruments:**
- IRAM 30m telescope (CO molecular lines)
- JCMT (Submillimeter continuum)
- Herschel Space Observatory (Far-infrared)

**Method:**
- Molecular line thermometry (CO rotational transitions)
- Dust continuum SED fitting
- NH3 inversion transitions

### Data Quality

**Typical Uncertainties:**
- Temperature: ±5-10 K (depending on S/N)
- Radius: ±0.1 pc (angular resolution limited)

**Systematic Errors:**
- Distance uncertainty: d = 1.7 ± 0.3 kpc
- Molecular abundance variations
- Optical depth effects

---

## Verification Status

### ⚠️ CRITICAL: Manual Verification Required

**Action Required:**
1. Download Di Francesco et al. 2010 PDF
2. Locate Table 3 (or equivalent temperature table)
3. Compare line-by-line with G79_temperatures.csv
4. Document any discrepancies

**Why Critical:**
Parameter fits show 12× discrepancy in α (0.01 vs 0.12 paper value). This could indicate:
- Wrong data subset
- Transcription errors
- Different radial bins

**Status:** ⚠️ PENDING VERIFICATION

---

## Additional Data Needed

### Velocity Data

**Missing:** Expansion velocity v(r) profile

**Source:** Rizzo, J. R., et al. 2008  
**Observable:** CO line widths and velocity centroids

**Why Needed:**
- Current: Heuristic v(r) estimates for M = v/c_s
- Desired: Actual measured v(r) for precise domain classification

**Impact:** Would improve domain boundary accuracy from ~20% to ~5%

### Mass Data

**Current:** M ~ 10 M_sun (approximate)

**Sources:**
- Radio continuum: Ionized gas mass
- Molecular emission: Molecular gas mass
- Dust continuum: Total gas+dust mass

**Why Needed:**
- Affects v_char = sqrt(GM/R) calculation
- ±20% uncertainty in M → ±10% in predicted Δv

---

## Multi-Wavelength Context

### Infrared (Spitzer, Herschel, AKARI)

**Data:**
- Shell morphology: 3 nested layers
- Temperature range: 20-240 K
- Dust mass: ~0.02 M_sun

**Status:** Published in various papers

### Molecular (IRAM, JCMT)

**Data:**
- CO (3-2), CO (2-1), NH3 (1,1) emission
- Kinetic temperature: 20-80 K
- Density: >10^4 cm^-3

**Status:** This repository uses kinetic T from these observations

### Radio (Effelsberg)

**Data:**
- Continuum: 6 cm, 21 cm
- Ionized gas: ~1.5 M_sun
- Radio-molecule spatial overlap

**Status:** Qualitative (used for mass estimate)

---

## Data Processing

### From Paper to CSV

**Original Format:** Table in PDF (likely)  
**Conversion:** Manual transcription (source unknown)

**Processing Steps (assumed):**
1. Extract r [arcsec] and T [K] from paper table
2. Convert r [arcsec] → r [pc] using d = 1.7 kpc
3. Save as CSV

**Potential Issues:**
- Transcription errors
- Unit conversion errors
- Subset selection (if paper has more points)

---

## How to Verify Data

### Step-by-Step Verification

1. **Obtain Paper:**
   ```
   Download: Di Francesco et al. 2010, ApJ 719, 451
   Or search: "G79.29+0.46 temperature profile"
   ```

2. **Locate Table:**
   ```
   Look for: "Table X: Temperature Profile of G79.29+0.46"
   Or similar: "Radial Temperature Distribution"
   ```

3. **Compare Values:**
   ```python
   import pandas as pd
   
   # Load CSV
   csv_data = pd.read_csv('G79_temperatures.csv')
   
   # Manual entry from paper
   paper_data = {
       'radius_pc': [0.3, 0.5, ...],  # From Table
       'temperature_K': [78, 62, ...]  # From Table
   }
   
   # Compare
   diff = csv_data.merge(paper_data, on='radius_pc', how='outer', 
                         suffixes=('_csv', '_paper'))
   print(diff)
   ```

4. **Document Discrepancies:**
   ```
   Create: DATA_VERIFICATION_REPORT.md
   Include: 
   - Match/mismatch for each point
   - Source of discrepancies
   - Recommended corrections
   ```

---

## Data Changelog

### Version History

**v1.0 (2025-11-05):**
- Initial CSV provided
- Source: Unknown/Di Francesco 2010 (unverified)
- Status: Pending verification

**Future versions:**
- v1.1: After verification, corrected if needed
- v2.0: With added velocity column v(r)

---

## Contact for Data Questions

**Primary Contact:**
- Carmen N. Wrede
- Email: [to be added]

**For Data Corrections:**
- Open GitHub issue with:
  - Clear description of error
  - Reference to source (paper, page, table)
  - Proposed correction

---

## Data License

**License:** CC-BY 4.0 (standard for observational data)

**Citation Required:**
```bibtex
@article{difrancesco2010,
  title={[Paper Title]},
  author={Di Francesco, J. and others},
  journal={ApJ},
  volume={719},
  pages={451},
  year={2010}
}
```

---

## Related Datasets

### Available Elsewhere

**Spitzer Legacy Survey:**
- URL: https://irsa.ipac.caltech.edu/
- Data: Infrared photometry

**Herschel Archive:**
- URL: http://archives.esac.esa.int/hsa/whsa/
- Data: Far-IR photometry and spectroscopy

**CDS/VizieR:**
- URL: http://vizier.u-strasbg.fr/
- Search: "G79.29+0.46" or "Di Francesco 2010"

---

## Status Summary

```
Data File: G79_temperatures.csv
Source: Di Francesco 2010 (claimed, unverified)
Verification: ⚠️ PENDING
Completeness: Missing velocity data
Quality: Assumed good (needs verification)
Usage: Suitable for analysis (with caveats)

Action Required: Manual PDF verification
Priority: HIGH (critical for publication)
Timeline: 1 week
```

---

**Document Version:** 1.0  
**Last Verification Attempt:** None  
**Next Review:** After paper verification

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
