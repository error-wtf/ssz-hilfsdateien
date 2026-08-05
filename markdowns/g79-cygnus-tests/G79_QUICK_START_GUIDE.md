# G79.29+0.46 Quick Start Guide 🚀

**KONKRETE Anleitung: Von JETZT bis zur ersten Ring-CSV!**  
**Based on Carmen's exact instructions**  
**Date:** 2025-11-05

---

## 🎯 G79.29+0.46 - Exakte Koordinaten

```
RA:       20:31:41 (J2000)
Dec:      +40:21:07 (J2000)
Distance: 1.7 kpc
Radius:   ~5-10 arcmin (Suchradius)
Size:     ~3-4 arcmin (Nebula)

Conversion:
1 arcmin ≈ 0.5 pc @ 1.7 kpc
→ Nebula ~ 1.5-2 pc diameter
```

---

## 📋 KONKRETE Datensatz-Checkliste

### Priority 1: IR/Staub (START HERE!) ⭐⭐⭐

**A. Spitzer MIPS/IRAC** (EASIEST!)

**Was holen:**
```
IRAC:
- 8 μm  → PAH, PDR emission
- 3.6, 4.5, 5.8 μm → Hot dust

MIPS:
- 24 μm  → Warm dust (inner ring)
- 70 μm  → Cool dust (outer shell)
- 160 μm → Cold dust (if available)
```

**Wo:**
- **IRSA (NASA/IPAC)**: https://irsa.ipac.caltech.edu/
- Mission: Spitzer
- Instrument: MIPS / IRAC

**Schritt-für-Schritt (Browser):**
```
1. Go to: https://irsa.ipac.caltech.edu/
2. Click: "Image Search" or "Finder Chart"
3. Enter coordinates:
   RA:  20:31:41
   Dec: +40:21:07
   Radius: 0.2 deg (= 12 arcmin)
4. Select mission: Spitzer
5. Select instrument: MIPS / IRAC
6. Check boxes for desired bands
7. Click "Download FITS"
8. Save to: E:\clone\g79-cygnus-test\data\telescope\spitzer\
```

**Expected files:**
```
G79_spitzer_irac_8um.fits
G79_spitzer_mips_24um.fits
G79_spitzer_mips_70um.fits
```

**Timeline:** 10-30 minutes (download time)

---

**B. AKARI FIS** (ALSO EASY!)

**Was holen:**
```
FIS All-Sky Maps:
- 65 μm (N60)
- 90 μm (WIDE-S) ← START WITH THIS!
- 140 μm (WIDE-L)
- 160 μm (N160)
```

**Wo:**
- **IRSA**: https://irsa.ipac.caltech.edu/ (mirrored!)
- **OR JAXA DARTS**: https://darts.isas.jaxa.jp/astro/akari/

**Via IRSA (RECOMMENDED):**
```
1. Go to: https://irsa.ipac.caltech.edu/
2. Image Search
3. Coordinates: 20:31:41 +40:21:07
4. Mission: AKARI
5. Catalog: akari_fis_allsky
6. Download FITS
```

**Expected files:**
```
G79_akari_fis_90um.fits  ← START WITH THIS ONE!
G79_akari_fis_140um.fits
```

**Timeline:** 5-15 minutes

---

**C. Herschel PACS/SPIRE** (Optional, later)

**Was holen:**
```
PACS:
- 70 μm, 100 μm, 160 μm (continuum)
- [CII] 158 μm (line - GOLD!)

SPIRE:
- 250 μm, 350 μm, 500 μm (cold dust)
```

**Wo:**
- **Herschel Science Archive**: http://archives.esac.esa.int/hsa/

**Steps:**
```
1. Create HSA account (free)
2. Search coordinates: 20:31:41 +40:21:07
3. Radius: 10 arcmin
4. Filter: PACS + SPIRE
5. Download Level 2 FITS
```

**Timeline:** 1-2 weeks (account approval + download)

---

### Priority 2: CO Cubes (Molecular Gas) ⭐⭐⭐⭐⭐

**Was holen:**
```
IRAM 30m observations:
- CO(1-0) 115 GHz
- CO(2-1) 230 GHz  ← In Rizzo 2008!
- CO(3-2) 345 GHz  ← In Rizzo 2008!
```

**Wo:**
- **IRAM Archive**: http://www.iram.fr/ILPA/
- **OR email**: archive@iram.fr

**Method 1: Find Project ID**
```
1. Open Rizzo et al. 2008 paper
2. Check "Observations" section
3. Look for: "IRAM project XXX-YY"
4. Go to IRAM archive
5. Search by project ID
6. Download FITS cubes
```

**Method 2: Email Request**
```
To: archive@iram.fr
Subject: G79.29+0.46 CO datacubes request

Dear IRAM Archive,

I request CO datacubes for G79.29+0.46:
- RA: 20:31:41, Dec: +40:21:07
- From: Rizzo et al. 2008, ApJ 681, 355

Needed:
- CO(2-1) at 230 GHz
- CO(3-2) at 345 GHz

For segmented spacetime validation study.

Best regards,
[Your name]
[Affiliation]
```

**Expected files:**
```
G79_iram_co21_cube.fits
G79_iram_co32_cube.fits
```

**Timeline:** 2-4 weeks (archive response)

---

### Priority 3: NH3 Maps (Rotational Temperature) ⭐⭐⭐⭐⭐

**Was holen:**
```
Effelsberg 100m observations:
- NH3 (1,1) - main transition
- NH3 (2,2) - temperature indicator
- NH3 (3,3) - high density tracer
```

**Wo:**
- **MPIfR Archive**: Email only
- **Email**: archive@mpifr-bonn.mpg.de

**Email Template:**
```
To: archive@mpifr-bonn.mpg.de
Subject: G79.29+0.46 NH3 maps request

Dear Effelsberg Archive,

I request NH3 observations for G79.29+0.46:
- RA: 20:31:41, Dec: +40:21:07
- Reference: Rizzo et al. 2014, A&A 561, A21

Needed:
- NH3 (1,1) spatial maps
- NH3 (2,2) if available
- NH3 (3,3) if available

For LBV nebula segmented spacetime study.

Best regards,
[Your name]
[Affiliation]
```

**Expected files:**
```
G79_effelsberg_nh3_11.fits
G79_effelsberg_nh3_22.fits (maybe)
```

**Timeline:** 2-4 weeks

---

## 🎯 Ring Definition (Carmen's Empfehlung!)

### r_edges für G79.29+0.46

**Based on:**
- Distance: 1.7 kpc
- Nebula size: ~3-4 arcmin
- Physical size: ~1.5-2 pc
- Current model: 0.3-1.7 pc

**Carmen's exact recommendation:**

```python
import numpy as np

# Ring edges in pc (0.2 pc spacing)
r_edges_pc = np.arange(0.0, 2.0 + 0.2, 0.2)

# Ring centers
r_centers_pc = 0.5 * (r_edges_pc[:-1] + r_edges_pc[1:])

print("Ring edges (pc):")
print(r_edges_pc)
# [0.0, 0.2, 0.4, 0.6, 0.8, 1.0, 1.2, 1.4, 1.6, 1.8, 2.0]

print("\nRing centers (pc):")
print(r_centers_pc)
# [0.1, 0.3, 0.5, 0.7, 0.9, 1.1, 1.3, 1.5, 1.7, 1.9]
```

**Matches our current model:**
```
Ring 0: r_center = 0.1 pc  (r = 0.0-0.2 pc)
Ring 1: r_center = 0.3 pc  (r = 0.2-0.4 pc)  ← Current "inner"
Ring 2: r_center = 0.5 pc  (r = 0.4-0.6 pc)
Ring 3: r_center = 0.7 pc  (r = 0.6-0.8 pc)
Ring 4: r_center = 0.9 pc  (r = 0.8-1.0 pc)
Ring 5: r_center = 1.1 pc  (r = 1.0-1.2 pc)
Ring 6: r_center = 1.3 pc  (r = 1.2-1.4 pc)
Ring 7: r_center = 1.5 pc  (r = 1.4-1.6 pc)
Ring 8: r_center = 1.7 pc  (r = 1.6-1.8 pc)  ← Current "outer"
Ring 9: r_center = 1.9 pc  (r = 1.8-2.0 pc)
```

**Total: 10 rings** (perfect for analysis!)

---

## 📊 CSV Format (Carmen's Empfehlung)

```csv
# G79.29+0.46 Ring Profile
# Source: [AKARI 90um / Spitzer 24um / IRAM CO21]
# Extraction date: 2025-11-05
#
ring,r_min_pc,r_max_pc,radius_pc,T_proxy_K,v_obs_kms,I_mean,I_std,n_pixels
0,0.0,0.2,0.1,78.5,1.1,1.23e-3,4.5e-4,450
1,0.2,0.4,0.3,75.2,1.1,1.15e-3,4.2e-4,520
2,0.4,0.6,0.5,68.1,1.2,9.8e-4,3.8e-4,580
...
```

**Columns:**
- `ring`: Ring index (0-9)
- `r_min_pc`, `r_max_pc`: Ring edges [pc]
- `radius_pc`: Ring center [pc]
- `T_proxy_K`: Temperature proxy [K]
- `v_obs_kms`: Observed velocity [km/s]
- `I_mean`: Mean intensity (from FITS)
- `I_std`: Standard deviation
- `n_pixels`: Number of pixels in ring

---

## 🛠️ Konkrete Extraction Scripts

### Script 1: AKARI 90 μm → Rings

**Carmen's exact method for 2D FITS:**

```python
#!/usr/bin/env python3
"""
Extract rings from AKARI 90 μm FITS
Carmen's method - concrete for G79!
"""
import numpy as np
import pandas as pd
from astropy.io import fits
from astropy.wcs import WCS
from astropy.coordinates import SkyCoord
import astropy.units as u

# G79 parameters
G79_CENTER = SkyCoord("20h31m41s +40d21m07s", frame="icrs")
G79_DISTANCE = 1.7  # kpc

# Ring edges (Carmen's recommendation)
r_edges_pc = np.arange(0.0, 2.0 + 0.2, 0.2)

# Load FITS
print("Loading AKARI 90 μm FITS...")
hdu = fits.open("G79_akari_fis_90um.fits")[0]
data = hdu.data
wcs = WCS(hdu.header)

print(f"Image size: {data.shape}")

# Calculate radial distances
print("Calculating radial distances...")
ny, nx = data.shape
y_idx, x_idx = np.indices(data.shape)

# Convert pixels to sky coordinates
ra, dec = wcs.all_pix2world(x_idx, y_idx, 0)
coords = SkyCoord(ra*u.deg, dec*u.deg, frame="icrs")

# Angular separation from G79 center
r_ang = coords.separation(G79_CENTER)

# Physical distance in pc
r_pc = (r_ang.to(u.rad) * (G79_DISTANCE * u.kpc)).to(u.pc).value

print(f"Radial range: {r_pc.min():.2f} - {r_pc.max():.2f} pc")

# Extract rings
print(f"\nExtracting {len(r_edges_pc)-1} rings...")
rows = []

for ring_idx, (r_min, r_max) in enumerate(zip(r_edges_pc[:-1], r_edges_pc[1:])):
    mask = (r_pc >= r_min) & (r_pc < r_max) & np.isfinite(data)
    
    if np.any(mask):
        vals = data[mask]
        I_mean = np.nanmean(vals)
        I_std = np.nanstd(vals)
        I_median = np.nanmedian(vals)
        n_pixels = np.sum(mask)
        
        rows.append({
            "ring": ring_idx,
            "r_min_pc": float(r_min),
            "r_max_pc": float(r_max),
            "radius_pc": float(0.5 * (r_min + r_max)),
            "I_mean": float(I_mean),
            "I_median": float(I_median),
            "I_std": float(I_std),
            "I_err": float(I_std / np.sqrt(n_pixels)),
            "n_pixels": int(n_pixels),
        })
        
        print(f"  Ring {ring_idx}: r={r_min:.1f}-{r_max:.1f} pc, "
              f"I={I_mean:.3e}, n={n_pixels}")

# Save CSV
df = pd.DataFrame(rows)

with open("G79_akari_90um_rings_REAL.csv", 'w', encoding='utf-8') as f:
    f.write("# G79.29+0.46 AKARI 90 μm Ring Profile\n")
    f.write("# Center: RA 20:31:41, Dec +40:21:07\n")
    f.write("# Distance: 1.7 kpc\n")
    f.write("# Ring spacing: 0.2 pc\n")
    f.write("# Extraction: Carmen's method\n")
    f.write(f"# Date: {pd.Timestamp.now()}\n")
    f.write("#\n")
    df.to_csv(f, index=False)

print(f"\n✓ Saved: G79_akari_90um_rings_REAL.csv")
print(f"✓ Extracted {len(df)} rings!")
```

**Run it:**
```bash
python extract_akari_rings.py
```

**Result:** `G79_akari_90um_rings_REAL.csv` ✅

---

### Script 2: CO Cube → Velocity Rings

**Carmen's method for 3D cubes:**

```python
#!/usr/bin/env python3
"""
Extract velocity rings from CO cube
Carmen's method - concrete for G79!
"""
import numpy as np
import pandas as pd
from spectral_cube import SpectralCube
from astropy.coordinates import SkyCoord
from astropy.modeling import models, fitting
import astropy.units as u

# G79 parameters
G79_CENTER = SkyCoord("20h31m41s +40d21m07s", frame="icrs")
G79_DISTANCE = 1.7  # kpc
r_edges_pc = np.arange(0.0, 2.0 + 0.2, 0.2)

# Load cube
print("Loading CO(2-1) cube...")
cube = SpectralCube.read("G79_iram_co21_cube.fits")
cube = cube.with_spectral_unit(u.km/u.s)

vel = cube.spectral_axis.value
print(f"Cube size: {cube.shape}")
print(f"Velocity range: {vel.min():.2f} - {vel.max():.2f} km/s")

# Calculate radial distances (spatial only)
print("Calculating spatial distances...")
wcs_spatial = cube.wcs.celestial
ny, nx = cube.shape[1], cube.shape[2]
y_idx, x_idx = np.indices((ny, nx))

ra, dec = wcs_spatial.all_pix2world(x_idx, y_idx, 0)
coords = SkyCoord(ra*u.deg, dec*u.deg, frame="icrs")
r_ang = coords.separation(G79_CENTER)
r_pc = (r_ang.to(u.rad) * (G79_DISTANCE * u.kpc)).to(u.pc).value

print(f"Radial range: {r_pc.min():.2f} - {r_pc.max():.2f} pc")

# Extract ring spectra
print(f"\nExtracting {len(r_edges_pc)-1} ring spectra...")
rows = []

for ring_idx, (r_min, r_max) in enumerate(zip(r_edges_pc[:-1], r_edges_pc[1:])):
    mask_2d = (r_pc >= r_min) & (r_pc < r_max)
    
    if np.any(mask_2d):
        # Create 3D mask
        mask_3d = np.broadcast_to(mask_2d[np.newaxis, :, :], cube.shape)
        
        # Get data
        cube_data = cube.filled_data[:].value
        masked_data = np.where(mask_3d, cube_data, np.nan)
        
        # Average spectrum in this ring
        spectrum = np.nanmean(masked_data, axis=(1, 2))
        
        if not np.all(np.isnan(spectrum)):
            # Fit Gaussian to find velocity centroid
            try:
                g_init = models.Gaussian1D(
                    amplitude=np.nanmax(spectrum),
                    mean=vel[np.nanargmax(spectrum)],
                    stddev=1.0
                )
                fit_g = fitting.LevMarLSQFitter()
                g = fit_g(g_init, vel, spectrum)
                
                v_cent = float(g.mean.value)
                v_width = float(abs(g.stddev.value))
                T_peak = float(np.nanmax(spectrum))
                
            except:
                v_cent = float(vel[np.nanargmax(spectrum)])
                v_width = np.nan
                T_peak = float(np.nanmax(spectrum))
            
            n_pixels = int(np.sum(mask_2d))
            
            rows.append({
                "ring": ring_idx,
                "r_min_pc": float(r_min),
                "r_max_pc": float(r_max),
                "radius_pc": float(0.5 * (r_min + r_max)),
                "v_obs_kms": v_cent,
                "v_width_kms": v_width,
                "T_peak_K": T_peak,
                "n_pixels": n_pixels,
            })
            
            print(f"  Ring {ring_idx}: r={r_min:.1f}-{r_max:.1f} pc, "
                  f"v={v_cent:.2f} km/s, T={T_peak:.1f} K")

# Save
df = pd.DataFrame(rows)

with open("G79_iram_co21_rings_REAL.csv", 'w', encoding='utf-8') as f:
    f.write("# G79.29+0.46 CO(2-1) Velocity Profile\n")
    f.write("# Center: RA 20:31:41, Dec +40:21:07\n")
    f.write("# Distance: 1.7 kpc\n")
    f.write("# Ring spacing: 0.2 pc\n")
    f.write("# Method: Ring-averaged spectra + Gaussian fit\n")
    f.write(f"# Date: {pd.Timestamp.now()}\n")
    f.write("#\n")
    df.to_csv(f, index=False)

print(f"\n✓ Saved: G79_iram_co21_rings_REAL.csv")
print(f"✓ Extracted {len(df)} velocity rings!")
```

**Run it:**
```bash
python extract_co_velocity_rings.py
```

**Result:** `G79_iram_co21_rings_REAL.csv` ✅

---

## 🚀 YOUR WORKFLOW (Step-by-Step)

### Week 1: IR Data

**Monday:**
```
1. Go to IRSA
2. Download AKARI 90 μm FITS
3. Run: extract_akari_rings.py
4. Result: G79_akari_90um_rings_REAL.csv ✓
```

**Tuesday:**
```
1. Download Spitzer MIPS 24 μm
2. Run: extract_akari_rings.py (same code!)
3. Result: G79_spitzer_24um_rings_REAL.csv ✓
```

**Wednesday:**
```
1. Combine both CSVs
2. Test: fit_gamma_seg_profile.py
3. Compare with synthetic data
```

**Result:** First REAL telescope data! 🎉

---

### Week 2-3: Email Archives

**Email IRAM:**
```
To: archive@iram.fr
Request: CO(2-1), CO(3-2) cubes
```

**Email Effelsberg:**
```
To: archive@mpifr-bonn.mpg.de
Request: NH3 (1,1) maps
```

**Wait:** 2-3 weeks for response

---

### Week 4: Process Cubes

**When cubes arrive:**
```bash
# Extract CO velocity rings
python extract_co_velocity_rings.py

# Extract NH3 if spatial maps
python extract_akari_rings.py  # Same method!

# Combine all data
python combine_all_rings.py
```

**Result:** Complete multi-tracer dataset! 🏆

---

## ✅ Success Checklist

**Phase 1: IR Data (This Week)**
- [ ] Downloaded AKARI 90 μm FITS
- [ ] Extracted rings → CSV
- [ ] Verified r_edges (0.0-2.0 pc, 0.2 pc spacing)
- [ ] Compared with synthetic data
- [ ] **Result: First REAL profile!** ✅

**Phase 2: Archives (2-3 Weeks)**
- [ ] Emailed IRAM (CO cubes)
- [ ] Emailed Effelsberg (NH3)
- [ ] Received download links
- [ ] Downloaded cubes

**Phase 3: Complete (1 Month)**
- [ ] Extracted CO velocity rings
- [ ] Extracted NH3 temperature rings
- [ ] Combined all tracers
- [ ] Fit γ_seg(r) with REAL data
- [ ] **Result: 95% validation!** 🏆

---

## 🎯 BOTTOM LINE

**Carmen gave us:**
- ✅ EXACT coordinates
- ✅ EXACT datasets to fetch
- ✅ EXACT r_edges definition
- ✅ EXACT extraction methods

**We now have:**
- ✅ Direct archive links
- ✅ Browser step-by-step
- ✅ Production Python code
- ✅ Week-by-week plan

**Timeline:**
- **THIS WEEK:** Download + extract AKARI → First REAL rings!
- **+2 weeks:** Email archives
- **+1 month:** Complete dataset! 🎉

**From browser → FITS → CSV in ~10 minutes!**

---

**READY TO START! 🚀**

**First action:** Go to IRSA, download AKARI 90 μm!

---

**Document Version:** 1.0  
**Created:** 2025-11-05  
**Based on:** Carmen's concrete instructions  
**THANK YOU CARMEN! 🙏**

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
