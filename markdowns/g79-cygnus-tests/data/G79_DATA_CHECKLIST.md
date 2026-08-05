# G79.29+0.46 Data Acquisition Checklist

**Complete guide: From telescope to ring CSV**  
**Date:** 2025-11-05

---

## 🎯 Target Information

### G79.29+0.46 (IRAS 20308+4104)

**Coordinates (J2000):**
```
RA  = 20:31:41  (20h 31m 41s)
Dec = +40:21:07  (+40° 21' 07")

Decimal: RA = 307.920833°, Dec = 40.351944°
```

**Physical Parameters:**
- Distance: d = 1.7 ± 0.3 kpc
- Systemic velocity: v_LSR ~ +5 km/s
- Type: LBV candidate nebula
- Size: ~2 pc diameter

**Search Radius:** 5-10 arcmin (recommended: 5')

---

## 📊 Required Datasets

### Priority 1: IR Continuum (Easy to get!)

#### 1.1 AKARI Far-IR
**Why:** Dust temperature, shell structure  
**Bands:** 65, 90, 140, 160 µm

**How to get:**
```python
from astroquery.ipac.irsa import Irsa
from astropy.coordinates import SkyCoord
import astropy.units as u

coord = SkyCoord("20h31m41s +40d21m07s", frame="icrs")
akari = Irsa.query_region(
    coord,
    catalog="akari_fis_allsky",
    radius=5*u.arcmin
)
```

**Web download:**
- URL: https://darts.isas.jaxa.jp/astro/akari/
- Search: RA 307.921, Dec 40.352
- Download: FITS images for all 4 bands
- Save to: `data/telescope/akari/`

**Expected files:**
```
G79_akari_65um.fits
G79_akari_90um.fits
G79_akari_140um.fits
G79_akari_160um.fits
```

**Timeline:** 1-2 hours

---

#### 1.2 Spitzer MIPS
**Why:** Mid-IR dust temperature  
**Bands:** 24, 70 µm

**How to get:**
- URL: https://irsa.ipac.caltech.edu/applications/Spitzer/SHA/
- Search: RA 20:31:41, Dec +40:21:07
- Instrument: MIPS
- Download: PBCD (Post-Basic Calibrated Data)
- Save to: `data/telescope/spitzer/`

**Expected files:**
```
G79_spitzer_mips24.fits
G79_spitzer_mips70.fits
```

**Timeline:** 1-2 hours

---

#### 1.3 Herschel PACS/SPIRE
**Why:** Far-IR continuum + [CII], [OI] lines  
**Instruments:**
- PACS: [CII] 158 µm, [OI] 63 µm
- SPIRE: 250, 350, 500 µm

**How to get (ADQL):**
```python
from astroquery.esa.hsa import HSA

hsa = HSA()

query = f"""
SELECT 
    observation_id, instrument, obs_mode,
    wavelength, ra, dec
FROM herschel.observation
WHERE 
    CONTAINS(POINT('ICRS', ra, dec),
             CIRCLE('ICRS', 307.921, 40.352, 0.083)) = 1
ORDER BY start_time
"""

result = hsa.query_tap(query)
```

**Web download:**
- URL: http://archives.esac.esa.int/hsa/whsa/
- Create free account
- Search: G79.29+0.46 or coordinates
- Download: Level 2.5 (fully reduced)
- Save to: `data/telescope/herschel/`

**Expected files:**
```
G79_herschel_pacs_CII_158um.fits
G79_herschel_pacs_OI_63um.fits
G79_herschel_spire_250um.fits
G79_herschel_spire_350um.fits
G79_herschel_spire_500um.fits
```

**Timeline:** 1-2 days (account setup + download)

---

### Priority 2: Molecular Lines (Critical!)

#### 2.1 IRAM 30m CO
**Why:** Main velocity + kinetic temperature data!  
**Lines:** CO (2-1) at 230 GHz, CO (3-2) at 345 GHz

**How to get:**
1. Check Rizzo et al. 2008 (ApJ 681, 355) for project ID
2. Search IRAM archive: http://www.iram.fr/IRAMFR/GILDAS/
3. Or email request:

```
To: archive@iram.fr
Subject: Data request for G79.29+0.46 CO observations

Dear IRAM Archive Team,

We are analyzing the LBV nebula G79.29+0.46 following Rizzo et al. 
(2008, ApJ 681, 355). Could you provide the CO (2-1) and (3-2) FITS 
cubes used in that study?

Target: G79.29+0.46 (IRAS 20308+4104)
Coordinates: RA 20:31:41, Dec +40:21:07 (J2000)
Project reference: Rizzo et al. 2008, ApJ 681, 355

Purpose: SSZ theoretical validation
Institution: [Your institution]

Best regards,
[Your name]
```

**Expected files:**
```
G79_iram_co21_cube.fits  (CO 2-1, 230 GHz)
G79_iram_co32_cube.fits  (CO 3-2, 345 GHz)
```

**Timeline:** 1-2 weeks (email response)

---

#### 2.2 Effelsberg NH₃
**Why:** Rotational temperatures (verify Rizzo 2014 Table 1)  
**Lines:** NH₃ (1,1), (2,2), (3,3)

**How to get:**
Email request (template):

```
To: archive@mpifr-bonn.mpg.de
Subject: Data request for G79.29+0.46 NH₃ observations

Dear Effelsberg Archive Team,

We are conducting an analysis of G79.29+0.46 following up on the NH₃ 
observations published in Rizzo et al. (2014, A&A). Could you provide 
the NH₃ (1,1)-(3,3) FITS cubes?

Target: G79.29+0.46 (IRAS 20308+4104)
Coordinates: RA 20:31:41, Dec +40:21:07 (J2000)
Reference: Rizzo et al. 2014, A&A, Table 1

Purpose: SSZ model validation
Institution: [Your institution]

Best regards,
[Your name]
```

**Expected files:**
```
G79_effelsberg_nh3_11.fits  (1,1 transition)
G79_effelsberg_nh3_22.fits  (2,2 transition)
G79_effelsberg_nh3_33.fits  (3,3 transition)
```

**Timeline:** 1-2 weeks (email response)

---

## 🔧 Processing Workflow

### Step 1: Download Data (Week 1-2)

**Day 1-2: IR Data**
- [ ] AKARI (4 bands)
- [ ] Spitzer MIPS (2 bands)
- [ ] Herschel account setup

**Day 3-7: Herschel**
- [ ] Download PACS [CII], [OI]
- [ ] Download SPIRE continuum

**Day 1: Molecular requests**
- [ ] Send IRAM email
- [ ] Send Effelsberg email

---

### Step 2: Extract Ring Profiles (Week 2-3)

**For each 2D image (AKARI, Spitzer, Herschel SPIRE):**

```bash
python scripts/fits_to_ring_profile.py \
    data/telescope/akari/G79_akari_90um.fits \
    --output G79_akari_90um_rings.csv \
    --r-min 0.3 --r-max 1.9 --r-step 0.2
```

**Ring configuration:**
```python
r_edges = [0.3, 0.5, 0.7, 0.9, 1.1, 1.3, 1.5, 1.7, 1.9]  # pc
# Matches your existing temperature data!
```

**For 3D cubes (CO, NH₃, [CII]):**

```bash
python scripts/fits_to_ring_profile.py \
    data/telescope/iram/G79_iram_co21_cube.fits \
    --cube \
    --output G79_co21_rings.csv \
    --r-min 0.3 --r-max 1.9 --r-step 0.2
```

**Output:** CSV files with:
- `ring, radius_pc, I_mean, I_std, I_sem, n_pixels` (2D)
- `ring, radius_pc, v_obs_kms, T_peak, v_width_kms` (3D)

---

### Step 3: Combine & Validate (Week 3)

**Create master CSV:**
```python
import pandas as pd

# Load all ring profiles
akari_90 = pd.read_csv('G79_akari_90um_rings.csv')
co21 = pd.read_csv('G79_co21_rings.csv')
nh3 = pd.read_csv('G79_nh3_rings.csv')

# Merge on ring/radius
master = akari_90.merge(co21, on='radius_pc', suffixes=('_akari', '_co'))
master = master.merge(nh3, on='radius_pc')

# Now you have: radius_pc, T_dust, v_obs, T_rot, etc.
master.to_csv('G79_master_profile.csv', index=False)
```

**Validate against papers:**
- Compare with Rizzo 2008 velocity ranges
- Check Rizzo 2014 NH₃ temperatures
- Verify radial ranges match

---

## 📋 Expected Final Datasets

### After full processing:

```
data/telescope/
├── akari/
│   ├── G79_akari_65um.fits
│   ├── G79_akari_90um.fits
│   ├── G79_akari_140um.fits
│   └── G79_akari_160um.fits
│
├── spitzer/
│   ├── G79_spitzer_mips24.fits
│   └── G79_spitzer_mips70.fits
│
├── herschel/
│   ├── G79_herschel_pacs_CII_158um.fits
│   ├── G79_herschel_pacs_OI_63um.fits
│   ├── G79_herschel_spire_250um.fits
│   ├── G79_herschel_spire_350um.fits
│   └── G79_herschel_spire_500um.fits
│
├── iram/
│   ├── G79_iram_co21_cube.fits
│   └── G79_iram_co32_cube.fits
│
└── effelsberg/
    ├── G79_effelsberg_nh3_11.fits
    ├── G79_effelsberg_nh3_22.fits
    └── G79_effelsberg_nh3_33.fits

data/rings/
├── G79_akari_90um_rings.csv
├── G79_spitzer_mips24_rings.csv
├── G79_herschel_CII_rings.csv
├── G79_co21_rings.csv
├── G79_nh3_11_rings.csv
└── G79_master_profile.csv  ← FINAL!
```

---

## ✅ Checklist Summary

### Week 1: IR Data
- [ ] Install astroquery (`pip install astroquery`)
- [ ] Download AKARI (4 bands)
- [ ] Download Spitzer MIPS (2 bands)
- [ ] Create Herschel account
- [ ] Download Herschel PACS/SPIRE
- [ ] Extract ring profiles from all IR data

### Week 2: Molecular Data Requests
- [ ] Send IRAM CO request email
- [ ] Send Effelsberg NH₃ request email
- [ ] Continue processing IR data
- [ ] Create preliminary combined profiles

### Week 3: Molecular Data Processing
- [ ] Receive IRAM CO cubes
- [ ] Receive Effelsberg NH₃ cubes
- [ ] Extract velocity/temperature profiles
- [ ] Create master combined CSV

### Week 4: Validation & Integration
- [ ] Cross-validate with papers
- [ ] Compare multiple tracers
- [ ] Calculate uncertainties
- [ ] Integrate into SSZ analysis
- [ ] Update paper!

---

## 🎯 Success Criteria

**You'll know you're done when you have:**

1. ✅ Master CSV with columns:
   ```
   ring, radius_pc,
   T_dust_K, T_dust_err,
   v_obs_kms, v_obs_err,
   T_rot_K, T_rot_err,
   source_notes
   ```

2. ✅ All source FITS files archived
3. ✅ Documented provenance for each value
4. ✅ Uncertainties calculated from data
5. ✅ Validation against published results

**Publication readiness: 100%!** 🎉

---

## 💡 Pro Tips

### 1. Ring Edge Choices
Use edges that match your existing data:
```python
r_edges = np.array([0.3, 0.5, 0.7, 0.9, 1.1, 1.3, 1.5, 1.7, 1.9])
```
This gives 8 rings matching the radial range 0.3-1.9 pc.

### 2. Distance Uncertainty
G79 distance: 1.7 ± 0.3 kpc (18% uncertainty!)
- Affects r_pc calculation
- Propagate through to final uncertainties
- Document in CSV header

### 3. Coordinate Precision
Always use: RA 20:31:41, Dec +40:21:07
- NOT 20:32:32.9 (that was an error!)
- Matters for sub-arcmin astrometry

### 4. File Naming
Use consistent naming:
```
G79_[instrument]_[line/band]_[product].fits
G79_akari_90um_rings.csv
G79_co21_velocity_rings.csv
```

### 5. Metadata in CSV
Always include header comments:
```
# Source: G79_akari_90um.fits
# Center: RA 20:31:41, Dec +40:21:07
# Distance: 1.7 kpc
# Ring edges: 0.3-1.9 pc (0.2 pc steps)
# Extracted: 2025-11-05
```

---

## 🚀 Quick Start

**To get started TODAY:**

```bash
# 1. Install tools
pip install astroquery astropy pandas numpy

# 2. Test AKARI query
python -c "
from astroquery.ipac.irsa import Irsa
from astropy.coordinates import SkyCoord
import astropy.units as u

coord = SkyCoord('20h31m41s +40d21m07s', frame='icrs')
result = Irsa.query_region(coord, catalog='akari_fis_allsky', radius=5*u.arcmin)
print(f'Found {len(result)} AKARI sources')
"

# 3. Download first FITS from DARTS
# (Web interface - follow link from query)

# 4. Extract first profile!
python scripts/fits_to_ring_profile.py \
    G79_akari_90um.fits \
    --output G79_first_profile.csv
```

**Timeline to first result: 1-2 hours!** ⚡

---

**Document Version:** 1.0  
**Status:** Complete & ready to use  
**Last Updated:** 2025-11-05

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
