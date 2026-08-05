# G79.29+0.46 - Telescope to CSV Checklist 🔭→📊

**Complete data acquisition guide**  
**Based on Carmen's workflow - THANK YOU! 🙏**

---

## 🎯 Target Information

**Object:** G79.29+0.46 (LBV nebula)  
**Center:** RA 20:31:41, Dec +40:21:07 (J2000)  
**Distance:** 1.7 ± 0.3 kpc  
**Search radius:** 5-10 arcmin  
**Analysis region:** 0.3-1.9 pc (radial rings)

---

## 📋 Data Checklist

### Priority 1: IR/Dust (EASIEST - 1 week) ⭐⭐⭐

#### A. AKARI (Diffuse maps, 65-160 μm)

**Archive:** NASA/IPAC IRSA  
**Access:** Web + Python API ✅

**Method:**
```python
from astroquery.ipac.irsa import Irsa
from astropy.coordinates import SkyCoord
import astropy.units as u

coord = SkyCoord("20h31m41s +40d21m07s", frame="icrs")
Irsa.ROW_LIMIT = 10000

# Query catalog
result = Irsa.query_region(
    coord,
    catalog="akari_fis_allsky",
    radius=5*u.arcmin
)
print(result)
```

**Web alternative:**
```
1. Go to: https://irsa.ipac.caltech.edu/
2. Search: "AKARI"
3. Coordinates: 20:31:41 +40:21:07
4. Radius: 5 arcmin
5. Download FITS
```

**Expected bands:**
- 65 μm (N60)
- 90 μm (WIDE-S)
- 140 μm (WIDE-L)
- 160 μm (N160)

**What you get:**
- Dust temperature structure
- IR shell morphology
- T_dust(r) profile

**Processing:**
```bash
python fetch_and_extract_complete.py \
    --local G79_akari_90um.fits \
    --output G79_akari_90um_rings.csv
```

**Timeline:** 1-2 days

---

#### B. Spitzer MIPS/IRAC

**Archive:** NASA/IPAC IRSA (Spitzer Heritage Archive)  
**Access:** Web interface

**Method:**
```
1. Go to: https://sha.ipac.caltech.edu/
2. Coordinates: 20:31:41 +40:21:07
3. Mission: Spitzer
4. Instrument: MIPS + IRAC
5. Download Level 2 (calibrated) FITS
```

**Expected bands:**
- IRAC: 3.6, 4.5, 5.8, 8.0 μm
- MIPS: 24, 70, 160 μm

**What you get:**
- Hot dust (IRAC)
- Warm dust (MIPS 24 μm)
- Cool dust (MIPS 70 μm)

**Processing:**
```bash
# For each band
python fetch_and_extract_complete.py \
    --local G79_spitzer_mips24.fits \
    --output G79_spitzer_mips24_rings.csv
```

**Timeline:** 1-2 days

---

#### C. WISE (Wide-field IR)

**Archive:** NASA/IPAC IRSA  
**Access:** Web + API

**Bands:**
- W1: 3.4 μm
- W2: 4.6 μm
- W3: 12 μm
- W4: 22 μm

**Processing:** Same as AKARI

**Timeline:** 1 day

---

### Priority 2: Herschel [CII]/[OI] (MEDIUM - 1-2 weeks) ⭐⭐⭐⭐

#### Herschel PACS/SPIRE

**Archive:** ESA Herschel Science Archive (HSA)  
**Access:** Web + Python API ✅

**Method:**
```python
from astroquery.esa.hsa import HSA
from astropy.coordinates import SkyCoord
import astropy.units as u

coord = SkyCoord("20h31m41s +40d21m07s", frame="icrs")
radius = 5*u.arcmin

hsa = HSA()
result = hsa.query_region(coord, radius=radius)
print(result)

# Pick OBSIDs for PACS/SPIRE
# Download Level 2/2.5 maps
```

**Web alternative:**
```
1. Go to: http://archives.esac.esa.int/hsa/
2. Create account (free)
3. Search coordinates: 20:31:41 +40:21:07
4. Filter: PACS + SPIRE
5. Download Level 2 FITS
```

**Expected lines/bands:**
- PACS: [CII] 158 μm, [OI] 63 μm
- SPIRE: 250, 350, 500 μm continuum

**What you get:**
- PDR structure ([CII])
- Cooling zones ([OI])
- Cold dust (SPIRE)

**Processing:**
```bash
# [CII] line cube
python fetch_and_extract_complete.py \
    --local G79_herschel_cii_158um.fits \
    --cube \
    --output G79_herschel_cii_rings.csv

# Continuum maps
python fetch_and_extract_complete.py \
    --local G79_herschel_spire_250um.fits \
    --output G79_herschel_spire_250_rings.csv
```

**Timeline:** 1-2 weeks (account + download)

---

### Priority 3: CO Cubes (HARDER - 2-4 weeks) ⭐⭐⭐⭐⭐

#### IRAM 30m CO observations

**Archive:** IRAM Science Data Archive / TAPAS  
**Access:** Web + project ID (from Rizzo 2008)

**Expected data:**
- CO(1-0) 115 GHz
- CO(2-1) 230 GHz
- CO(3-2) 345 GHz

**Method:**

**Option A: If project ID known**
```
1. Check Rizzo et al. 2008 methods section
2. Look for "IRAM project XXX-YY"
3. Go to: http://www.iram.fr/ILPA/
4. Search by project ID
5. Download FITS cubes
```

**Option B: Email request**
```
To: archive@iram.fr
Subject: G79.29+0.46 CO datacubes request

Dear IRAM Archive team,

I am requesting access to CO datacubes for the object 
G79.29+0.46 (RA 20:31:41, Dec +40:21:07) published in 
Rizzo et al. 2008 (ApJ 681, 355).

We need:
- CO(2-1) at 230 GHz
- CO(3-2) at 345 GHz

For follow-up analysis of segmented spacetime effects 
in LBV nebulae.

Thank you!
[Your name and affiliation]
```

**What you get:**
- T_kin(x, y, v) datacubes
- Velocity fields
- Molecular gas structure

**Processing:**
```bash
python fetch_and_extract_complete.py \
    --local G79_iram_co21_cube.fits \
    --cube \
    --output G79_iram_co21_rings.csv
```

**Expected output:**
```csv
ring,radius_pc,v_obs_kms,v_width_kms,T_peak_K
0,0.35,1.1,2.3,45.2
1,0.50,1.2,2.5,38.1
...
```

**Timeline:** 2-4 weeks (archive response time)

---

### Priority 4: NH3 Maps (HARDEST - 2-4 weeks) ⭐⭐⭐⭐⭐

#### Effelsberg 100m NH3 observations

**Archive:** MPIfR Effelsberg Archive  
**Access:** Email request only

**Expected data:**
- NH3 (1,1) - (3,3) transitions
- Spatial maps (x, y) or (x, y, v)

**Method:**
```
To: archive@mpifr-bonn.mpg.de
Subject: G79.29+0.46 NH3 maps request

Dear Effelsberg Archive team,

I am requesting NH3 datacubes/maps for G79.29+0.46 
published in Rizzo et al. 2014 (A&A 561, A21).

Object: G79.29+0.46
RA: 20:31:41, Dec: +40:21:07
Reference: Rizzo+ 2014, Table 1

We need NH3 (1,1) to (3,3) transitions for validation 
of segmented spacetime model.

Thank you!
[Your name and affiliation]
```

**What you get:**
- T_rot(x, y) maps
- Velocity components spatially resolved
- NH3 column density

**Processing:**
```bash
# If spatial map
python fetch_and_extract_complete.py \
    --local G79_effelsberg_nh3_11.fits \
    --output G79_effelsberg_nh3_11_rings.csv

# If cube
python fetch_and_extract_complete.py \
    --local G79_effelsberg_nh3_11_cube.fits \
    --cube \
    --output G79_effelsberg_nh3_11_rings.csv
```

**Timeline:** 2-4 weeks

---

## 🎯 Recommended Ring Configuration

**Based on current analysis (0.3-1.9 pc):**

```python
# Ring edges (pc)
r_edges = np.array([
    0.0,   # Edge (not used, for reference)
    0.30,  # Ring 0 inner edge
    0.40,
    0.50,
    0.60,
    0.70,
    0.80,
    0.90,
    1.00,
    1.10,
    1.20,
    1.30,
    1.40,
    1.50,
    1.60,
    1.70,
    1.80,
    1.90,
    2.00   # Outer edge
])

# Ring centers
r_centers = 0.5 * (r_edges[:-1] + r_edges[1:])
# → [0.35, 0.45, 0.55, ..., 1.95] pc
```

**Why these edges:**
- Matches synthetic dataset (0.3-1.9 pc)
- 0.1 pc spacing → fine structure
- 18 rings total → good statistics
- Covers inner shock → outer molecular shell

---

## 📊 Processing Workflow

### Step 1: Download FITS

**Priority order:**
1. AKARI (easiest, 1 day)
2. Spitzer (easy, 1 day)
3. Herschel (medium, 1 week)
4. IRAM CO (hard, 2-4 weeks)
5. Effelsberg NH3 (hard, 2-4 weeks)

### Step 2: Extract Rings

**For 2D images (dust continuum):**
```bash
python fetch_and_extract_complete.py \
    --local filename.fits \
    --output filename_rings.csv \
    --distance 1.7
```

**For 3D cubes (CO, [CII], NH3):**
```bash
python fetch_and_extract_complete.py \
    --local filename_cube.fits \
    --cube \
    --output filename_rings.csv \
    --distance 1.7
```

**Output CSV format:**
```csv
# Ring profile from FITS
ring,radius_pc,r_inner_pc,r_outer_pc,I_mean,I_std,I_err,n_pixels
0,0.35,0.30,0.40,1.23e-3,4.5e-4,2.1e-5,450
...

# For cubes, also includes:
v_obs_kms,v_width_kms,T_peak_K
```

### Step 3: Validate

**Compare with paper values:**
```bash
# Check velocity profile
python scripts/analyze_nh3_velocities.py

# Check temperature structure
python scripts/fit_gamma_seg_profile.py \
    filename_rings.csv
```

### Step 4: Combine

**Merge multiple tracers:**
```python
import pandas as pd

# Load all ring profiles
df_akari = pd.read_csv("G79_akari_90um_rings.csv", comment='#')
df_co = pd.read_csv("G79_iram_co21_rings.csv", comment='#')
df_nh3 = pd.read_csv("G79_effelsberg_nh3_rings.csv", comment='#')

# Merge on radius
df_combined = df_akari.merge(df_co, on='radius_pc', suffixes=('_akari', '_co'))
df_combined = df_combined.merge(df_nh3, on='radius_pc')

df_combined.to_csv("G79_combined_rings_REAL.csv", index=False)
```

---

## ✅ Quality Checklist

**For each dataset, verify:**

- [ ] **Source documented:** Which telescope/instrument?
- [ ] **Date documented:** Observation date?
- [ ] **Coordinates verified:** Center matches G79?
- [ ] **Calibration noted:** Level 1/2/3 data?
- [ ] **Units clear:** Jy/beam, K, MJy/sr?
- [ ] **WCS valid:** Coordinate system correct?
- [ ] **Rings extracted:** CSV created successfully?
- [ ] **Uncertainties included:** I_std, I_err present?
- [ ] **Comparison with paper:** Matches published values?

---

## 🎯 Success Criteria

**Minimal dataset (60% validation):**
- ✅ NH3 components (already have!)
- ✅ 1 dust continuum (AKARI or Spitzer)
- ✅ Synthetic rings (already have!)

**Good dataset (75% validation):**
- ✅ NH3 components
- ✅ 2-3 IR bands (AKARI + Spitzer)
- ✅ Herschel continuum
- ✅ Temperature profile extracted

**Complete dataset (95% validation):**
- ✅ NH3 components + spatial maps
- ✅ Full IR suite (AKARI + Spitzer + Herschel)
- ✅ CO cubes (IRAM)
- ✅ [CII] cube (Herschel)
- ✅ Multi-tracer consistency

---

## 📅 Timeline

### Week 1: IR Data
- [ ] Query IRSA (AKARI + Spitzer)
- [ ] Download FITS (4-6 files)
- [ ] Extract rings
- [ ] **Result:** Dust T(r) profiles ✅

### Week 2: Herschel
- [ ] Create HSA account
- [ ] Query Herschel
- [ ] Download PACS/SPIRE
- [ ] Extract rings
- [ ] **Result:** [CII] + cold dust ✅

### Week 3-4: Molecular Data
- [ ] Email IRAM + Effelsberg
- [ ] Wait for response
- [ ] Download cubes
- [ ] Extract velocity profiles
- [ ] **Result:** CO + NH3 v(r), T(r) ✅

### Week 5: Integration
- [ ] Combine all datasets
- [ ] Cross-validate
- [ ] Compare with paper
- [ ] **Result:** Complete rings CSV ✅

---

## 🚀 Quick Start

**Today (5 minutes):**
```bash
# Install tools
pip install astropy astroquery spectral-cube

# Test query
python fetch_and_extract_complete.py --source akari
```

**This week (2 hours):**
```bash
# Download AKARI via web
# Process to rings
python fetch_and_extract_complete.py \
    --local G79_akari_90um.fits \
    --output G79_akari_REAL_rings.csv
```

**This month (1 day total):**
```bash
# Collect all IR data
# Extract all profiles
# Combine into master CSV
```

---

## 📞 Contact Information

**IRSA Support:** https://irsa.ipac.caltech.edu/docs/help_desk.html  
**Herschel Help:** hsa-helpdesk@sciops.esa.int  
**IRAM Archive:** archive@iram.fr  
**Effelsberg:** archive@mpifr-bonn.mpg.de

---

## 🏆 Bottom Line

**Carmen's workflow gives us:**
- ✅ Direct telescope data access
- ✅ Automated ring extraction
- ✅ Production-ready CSVs
- ✅ Full reproducibility

**From Papers → Archives → FITS → Rings → Validation!**

**Timeline:** 1 week (IR) to 1 month (complete)  
**Effort:** Medium (mostly waiting for archives)  
**Result:** Gold standard dataset! 🏆

---

**Document Version:** 1.0  
**Created:** 2025-11-05  
**Based on:** Carmen's "Teleskop → CSV" workflow  
**THANK YOU CARMEN! 🙏**

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
