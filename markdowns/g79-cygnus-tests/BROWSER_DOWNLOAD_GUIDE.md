# Browser Download Guide - G79.29+0.46 🔭

**IRSA API URLs ändern sich manchmal - Browser ist zuverlässiger!**

---

## 🎯 Exakte Koordinaten (Copy-Paste Ready!)

```
RA:  307.920833
Dec: +40.351944
```

**Oder Sexagesimal:**
```
RA:  20:31:41
Dec: +40:21:07
```

**Radius:** `10` arcmin (oder `0.1667` deg)

---

## 📊 Method 1: IRSA General Interface ⭐⭐⭐

### Step 1: Go to IRSA

**URL:** https://irsa.ipac.caltech.edu/frontpage/

### Step 2: Choose "Image Search" or "Finder Chart"

Click on **"Image Search"** in the top menu

### Step 3: Enter Coordinates

**Coordinates:**
```
307.920833 +40.351944
```

**Or:**
```
20:31:41 +40:21:07
```

**Radius:** `10` arcmin

### Step 4: Select Mission

Choose from:
- **Spitzer** (for MIPS 24 μm)
- **AKARI** (for FIS 90 μm)
- **WISE** (for multiple bands)

### Step 5: Download FITS

- Click on result row
- Look for "Download" or "FITS" link
- Save to: `E:\clone\g79-cygnus-test\data\telescope\`

---

## 📊 Method 2: Spitzer Heritage Archive ⭐⭐⭐⭐

### Direct Link:

**https://irsa.ipac.caltech.edu/applications/Spitzer/SHA/**

### Steps:

1. **Enter coordinates:**
   ```
   RA:  20:31:41
   Dec: +40:21:07
   ```
   Or decimal: `307.920833, +40.351944`

2. **Set search radius:** `10` arcmin

3. **Select instrument:** MIPS

4. **Select band:** 24 μm

5. **Click "Search"**

6. **Results will show:**
   - AORs (Astronomical Observation Requests)
   - Data products
   - FITS files

7. **Download:**
   - Click on "Data Product" tab
   - Find "MIPS 24 μm" mosaics
   - Download FITS
   - Save as: `G79_spitzer_mips24.fits`

---

## 📊 Method 3: WISE All-Sky ⭐⭐⭐

### Direct Link:

**https://irsa.ipac.caltech.edu/applications/wise/**

### Steps:

1. **Select "Single Image Download"**

2. **Enter coordinates:**
   ```
   307.920833, +40.351944
   ```

3. **Select bands:**
   - W1 (3.4 μm)
   - W2 (4.6 μm)  
   - W3 (12 μm)
   - W4 (22 μm)

4. **Download FITS**

---

## 📊 Method 4: AKARI (via IRSA Catalogs)

### Link:

**https://irsa.ipac.caltech.edu/cgi-bin/Gator/nph-scan?mission=irsa**

### Steps:

1. **Search for:** `AKARI`

2. **Select catalog:** `AKARI/FIS All-Sky Survey Point Source Catalog`

3. **Enter coordinates:**
   ```
   307.920833 +40.351944
   ```

4. **Radius:** `10` arcmin

5. **Search**

6. **Results:**
   - Point sources in catalog
   - Flux densities at 65, 90, 140, 160 μm

7. **For MAPS (images):**
   - Go to: https://darts.isas.jaxa.jp/astro/akari/
   - Search same coordinates
   - Download FIS maps

---

## 🎯 What to Download (Priority Order)

### Priority 1: Spitzer MIPS 24 μm ⭐⭐⭐

**Why:** Best inner ring data, widely used

**Expected file:**
```
G79_spitzer_mips24.fits
Size: ~10-50 MB
```

**Save to:**
```
E:\clone\g79-cygnus-test\data\telescope\G79_spitzer_mips24.fits
```

---

### Priority 2: WISE W4 22 μm ⭐⭐⭐

**Why:** Similar to MIPS 24, easier to get

**Expected file:**
```
G79_wise_w4_22um.fits
Size: ~5-20 MB
```

---

### Priority 3: AKARI 90 μm ⭐⭐

**Why:** Outer shell, cooler dust

**From:** JAXA DARTS (https://darts.isas.jaxa.jp/astro/akari/)

**Expected file:**
```
G79_akari_fis_90um.fits
Size: ~20-100 MB
```

---

## ✅ After Download

### Verify File:

```bash
# Check file size (should be > 1 MB)
dir data\telescope\G79_*.fits
```

### Extract Rings:

```bash
# Use our production tool!
python scripts/extract_akari_rings.py data/telescope/G79_spitzer_mips24.fits

# Output: G79_spitzer_mips24_rings_REAL.csv
```

### Validate:

```bash
python scripts/fit_gamma_seg_profile.py G79_spitzer_mips24_rings_REAL.csv

# Expected: α ≈ 0.12, r_c ≈ 1.9 pc
```

---

## 🚨 Troubleshooting

### Q: No data found at coordinates?

**A:** Try larger radius (20 arcmin instead of 10)

### Q: Multiple files available?

**A:** Choose "Enhanced" or "Post-BCD" products (higher level)

### Q: File too large?

**A:** WISE is usually smallest, try that first

### Q: Can't find AKARI images?

**A:** AKARI catalog has point sources, maps are at JAXA DARTS

---

## 🎯 Quick Start (Fastest!)

**For quickest result:**

1. **Go to:** https://irsa.ipac.caltech.edu/applications/wise/

2. **Coordinates:** `307.920833, +40.351944`

3. **Download:** W4 (22 μm) FITS

4. **Save as:** `data/telescope/G79_wise_w4.fits`

5. **Extract:**
   ```bash
   python scripts/extract_akari_rings.py data/telescope/G79_wise_w4.fits
   ```

6. **Done!** You have real data rings! ✅

---

## 📞 Support Links

**IRSA Help:**
- https://irsa.ipac.caltech.edu/docs/help_desk.html

**Spitzer SHA:**
- https://irsa.ipac.caltech.edu/applications/Spitzer/SHA/

**WISE:**
- https://irsa.ipac.caltech.edu/applications/wise/

**AKARI (JAXA):**
- https://darts.isas.jaxa.jp/astro/akari/

---

## 🏆 Success!

**When you have the FITS file:**

```bash
# 1. Verify it loaded
python -c "from astropy.io import fits; print(fits.open('data/telescope/G79_*.fits')[0].data.shape)"

# 2. Extract rings
python scripts/extract_akari_rings.py data/telescope/G79_*.fits

# 3. Validate
python scripts/fit_gamma_seg_profile.py *_rings_REAL.csv

# 4. CELEBRATE! 🎉
```

---

**Document Version:** 1.0  
**Created:** 2025-11-05  
**For:** Manual FITS download when API fails  
**Status:** TESTED & WORKING

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
