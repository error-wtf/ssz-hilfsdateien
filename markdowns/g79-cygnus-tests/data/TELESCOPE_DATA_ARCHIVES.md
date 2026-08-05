# Telescope Data Archives - G79.29+0.46

**Status:** 🚀 **READY TO FETCH REAL DATA**  
**Date:** 2025-11-05 19:20

---

## 🔭 Where the REAL Data Lives

The papers (Rizzo 2008, 2014, Jiménez-Esteban 2010, etc.) show only **selected results**.

The **actual observational data** (FITS cubes, spectra, maps) are in **public archives**!

---

## 📡 Available Telescope Archives

### 1. IRAM 30m - Molecular Lines

**Observations:** CO (1-0), CO (2-1), CO (3-2)  
**Source for:** Rizzo et al. 2008 (main molecular data)

**Archive Access:**
```
Archive: IRAM Large Program Archive
URL: http://www.iram.fr/IRAMFR/GILDAS/
Tool: GILDAS (CLASS/GREG) or TAPAS
Format: FITS cubes
```

**What's available:**
- Velocity-resolved CO emission cubes
- Temperature maps (from line ratios)
- Column density maps
- Position-velocity diagrams

**For G79.29+0.46:**
- Project ID: [Look in Rizzo 2008 methods section]
- Typical format: `G79_CO21_cube.fits`
- Resolution: ~20" (0.16 pc at 1.7 kpc)

**Search Strategy:**
```
1. Go to: http://www.iram.fr/IRAMFR/GILDAS/
2. Search: "G79.29+0.46" OR "IRAS 20308+4104"
3. Look for project codes mentioned in Rizzo 2008
4. Download FITS cubes
```

---

### 2. Effelsberg 100m - NH₃ Observations

**Observations:** NH₃ (1,1) - (3,3)  
**Source for:** Rizzo et al. 2014 (rotational temperatures)

**Archive Access:**
```
Archive: MPIfR (Max-Planck-Institut für Radioastronomie)
URL: https://www.mpifr-bonn.mpg.de/2169/en
Contact: archive@mpifr-bonn.mpg.de
Format: FITS (CLASS format)
```

**What's available:**
- NH₃ rotational temperature maps
- Column density N(NH₃)
- Velocity components (blue/central/red)
- Line width maps

**For G79.29+0.46:**
- Observation dates: [From Rizzo 2014]
- Frequency: 23.69 GHz (1,1), 23.72 GHz (2,2), etc.
- Resolution: ~40" (0.33 pc at 1.7 kpc)

**How to Request:**
```
Email template:
Subject: Data request for G79.29+0.46 NH₃ observations

Dear Effelsberg Archive Team,

We are conducting an analysis of the LBV nebula G79.29+0.46 
following up on the NH₃ observations published in Rizzo et al. 
(2014, A&A). Could you please provide access to the FITS cubes 
for the NH₃ (1,1)-(3,3) observations?

Project reference: [Rizzo 2014, A&A, Table 1]
Source: G79.29+0.46 / IRAS 20308+4104

Best regards,
[Your name & institution]
```

---

### 3. AKARI - Infrared Continuum

**Observations:** 65-160 µm (diffuse shell)  
**Source for:** Shell morphology, dust temperature

**Archive Access:**
```
Archive: JAXA DARTS (Data ARchives and Transmission System)
URL: https://darts.isas.jaxa.jp/astro/akari/
Format: FITS images
Access: Public, web interface
```

**What's available:**
- Far-IR continuum maps
- Dust temperature (from SED fitting)
- Shell structure
- Photometry

**Search:**
```
1. Go to: https://darts.isas.jaxa.jp/astro/akari/
2. Search by coordinates: RA 20:32:32.9, Dec +41:19:33
3. Select bands: 65, 90, 140, 160 µm
4. Download FITS images
```

---

### 4. Spitzer - Mid-Infrared

**Observations:** MIPS (24, 70 µm), IRS (5-38 µm)  
**Source for:** Jiménez-Esteban 2010 (hot dust, PDR)

**Archive Access:**
```
Archive: NASA/IPAC IRSA (Infrared Science Archive)
URL: https://irsa.ipac.caltech.edu/Missions/spitzer.html
Format: FITS (enhanced products available)
Access: Public, SHA (Spitzer Heritage Archive)
```

**What's available:**
- MIPS 24 µm, 70 µm photometry
- IRS spectroscopy (PAH features, fine structure lines)
- Enhanced mosaics (post-pipeline processing)

**Search:**
```
1. Go to: https://irsa.ipac.caltech.edu/applications/Spitzer/SHA/
2. Enter: "G79.29+0.46" or coordinates
3. Select: MIPS + IRS observations
4. Download: PBCD (Post-Basic Calibrated Data)
```

**Program ID:** [Check Jiménez-Esteban 2010 acknowledgments]

---

### 5. Herschel - Far-IR Lines & Continuum

**Observations:** PACS ([C II], [O I]), SPIRE (continuum)  
**Source for:** Outer PDR structure, extended emission

**Archive Access:**
```
Archive: ESA HSA (Herschel Science Archive)
URL: http://archives.esac.esa.int/hsa/whsa/
Format: FITS (Level 2.0 or higher)
Access: Public, requires registration
```

**What's available:**
- [C II] 158 µm (PDR tracer)
- [O I] 63 µm (shock/PDR)
- SPIRE continuum (250, 350, 500 µm)
- Photometry for extended sources

**Search:**
```
1. Go to: http://archives.esac.esa.int/hsa/whsa/
2. Create account (free)
3. Search: "G79.29" or RA/Dec
4. Select: PACS + SPIRE observations
5. Download: Level 2.5 (fully reduced)
```

---

### 6. JCMT - High-J CO

**Observations:** CO (3-2), (4-3), other high-J lines  
**Source for:** Molecular ridge, cross-check with IRAM

**Archive Access:**
```
Archive: CADC (Canadian Astronomy Data Centre)
URL: https://www.cadc-ccda.hia-iha.nrc-cnrc.gc.ca/
Search: JCMT Science Archive
Format: FITS cubes
```

**Search:**
```
1. Go to: https://www.cadc-ccda.hia-iha.nrc-cnrc.gc.ca/en/jcmt/
2. Search: Target name or coordinates
3. Select: CO observations
4. Download: Reduced cubes
```

---

## 🛠️ How to Extract Radial Profiles

### Python Tools Needed

```bash
pip install astropy
pip install spectral-cube
pip install radio-beam
pip install reproject
```

### General Workflow

```python
import numpy as np
from astropy.io import fits
from astropy import units as u
from astropy.coordinates import SkyCoord
from spectral_cube import SpectralCube
import matplotlib.pyplot as plt

# 1. Load FITS cube
cube = SpectralCube.read('G79_CO21_cube.fits')

# 2. Define center (G79.29+0.46)
center = SkyCoord('20h32m32.9s', '+41d19m33s', frame='icrs')

# 3. Extract radial profile
# (Will create detailed script for this)

# 4. Bin into rings (e.g., 0.2 pc spacing)
radii_pc = np.arange(0.3, 2.0, 0.2)

# 5. For each ring:
#    - Average temperature
#    - Average velocity
#    - Calculate uncertainties

# 6. Save to CSV
# ring, radius_pc, T_K, T_err_K, v_km_s, v_err_km_s
```

---

## 📋 Data Fetching Strategy

### Phase 1: Quick Win (NH₃ from Rizzo 2014)

**Priority:** HIGH  
**Reason:** Already have Table 1 verified

**Action:**
1. Request NH₃ FITS from Effelsberg archive
2. Extract T_rot maps
3. Create spatial profiles (not just components)
4. Verify against Table 1

**Timeline:** 1-2 weeks (including archive response)

---

### Phase 2: CO from IRAM

**Priority:** HIGH  
**Reason:** Main velocity/temperature data

**Action:**
1. Search IRAM archive for G79 project
2. Download CO (2-1) or (3-2) cube
3. Extract T_kinetic from line ratios
4. Create v(r) and T(r) profiles

**Timeline:** 1-2 weeks

---

### Phase 3: IR Continuum

**Priority:** MEDIUM  
**Reason:** Dust temperature, shell structure

**Action:**
1. Download Spitzer MIPS + Herschel PACS
2. Fit SEDs radially
3. Extract T_dust(r)
4. Compare with molecular T

**Timeline:** 2-3 weeks

---

### Phase 4: Complete Multi-wavelength

**Priority:** LOW (nice to have)  
**Reason:** Full picture, but not critical for SSZ validation

**Action:**
1. Combine all datasets
2. Multi-tracer analysis
3. Comprehensive radial profiles
4. Cross-validation

**Timeline:** 1-2 months

---

## 🎯 What This Gives Us

### Instead of:
```
⚠️ G79_temperatures.csv (source unclear)
⚠️ Modeled or digitized from figures
⚠️ Uncertainties unknown
```

### We'll have:
```
✅ G79_IRAM_CO_radial_profile.csv (from FITS cube)
✅ G79_Effelsberg_NH3_profile.csv (from archive)
✅ G79_Spitzer_dust_temp_profile.csv (from SED fits)
✅ Each with documented uncertainties
✅ Fully reproducible extraction method
✅ Python scripts for transparency
```

---

## 📝 Next Steps - Action Plan

### Immediate (This Week):

1. ✅ Create this archive documentation (DONE!)
2. ⏳ Prepare Python script template for FITS analysis
3. ⏳ Create archive request email templates
4. ⏳ Document extraction methodology

### Short-term (1-2 Weeks):

5. ⏳ Submit archive requests (IRAM, Effelsberg)
6. ⏳ Download publicly available data (Spitzer, Herschel, AKARI)
7. ⏳ Test extraction scripts on available data
8. ⏳ Create preliminary profiles

### Medium-term (1 Month):

9. ⏳ Process all received data
10. ⏳ Generate verified ring profiles
11. ⏳ Cross-validate with published results
12. ⏳ Update paper with real data

---

## 🎓 Scientific Impact

### Before (Current Status):
- ✅ NH₃ components (Table 1, verified)
- ⚠️ Temperature profiles (needs verification)
- Publication-ready: 95%

### After (With Archive Data):
- ✅ NH₃ components (Table 1, verified)
- ✅ NH₃ spatial profiles (from FITS)
- ✅ CO velocity/temperature profiles (from FITS)
- ✅ Dust temperature profiles (from IR SEDs)
- ✅ Complete multi-tracer validation
- Publication-ready: **100%!**

---

## 📚 References for Archive Access

**IRAM:**
- Manual: http://www.iram.fr/IRAMFR/GILDAS/doc/html/class-html/
- Data policy: Public after proprietary period

**Effelsberg:**
- Archive info: https://www.mpifr-bonn.mpg.de/2169/en
- Contact required for data access

**Spitzer/IRSA:**
- SHA User Guide: https://irsa.ipac.caltech.edu/data/SPITZER/docs/
- All data public

**Herschel/HSA:**
- User manual: http://archives.esac.esa.int/hsa/whsa-tap-server/
- Registration required (free)

**AKARI/DARTS:**
- Help: https://darts.isas.jaxa.jp/astro/akari/help.html
- Public access

---

## ✅ Status

**Documentation:** ✅ COMPLETE  
**Tools:** ⏳ Python scripts to be created  
**Data Requests:** ⏳ Ready to submit  
**Timeline:** 1-4 weeks for complete dataset

**This is the RIGHT way to do science!** 🔬

---

**Document Version:** 1.0  
**Created:** 2025-11-05  
**Next Update:** After first archive responses

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
