# Sources.md - Astronomical Data Provenance

## Purpose

This document describes the origin of **ALL astronomical data** used in this repository, including:
- **M87*** (ALMA + Chandra multi-frequency observations)
- **Cygnus X-1** (Chandra thermal X-ray spectrum)
- **S2 star** (VLT/GRAVITY orbital timeseries)

All data refers to primary literature, public archives, and programmatic interfaces.

## Data Provenance

All observational data used in `real_data_full.csv` originates from **peer-reviewed published observations** or **public observatory archives**. The scripts process published values and store them locally. For reproducibility, all source references are listed below.

**Acknowledgments:** 
- ALMA Partnership / Event Horizon Telescope (EHT) (EHT) (EHT) Collaboration
- Chandra X-ray Observatory / NASA
- GRAVITY Collaboration (ESO VLT)
- Keck Observatory Archive
- NIST Atomic Spectra Database
- CDS services (SIMBAD/VizieR)

---

## 1. M87* Multi-Frequency Spectrum (ALMA + Chandra)

### Primary Literature

**EHT Collaboration (2019)** - M87* Event Horizon Telescope (EHT) (EHT) Observations:
* [First M87 Event Horizon Telescope (EHT) (EHT) Results. I. The Shadow of the Supermassive Black Hole](https://iopscience.iop.org/article/10.3847/2041-8213/ab0ec7)
* [EHT Collaboration et al., ApJL 875, L1 (2019)](https://arxiv.org/abs/1906.11238)

**ALMA Observations:**
* ALMA Band 3: 230 GHz, 345 GHz (1.3 mm)
* ALMA Band 6: 228 GHz (1.3 mm)
* ALMA Band 7: 340 GHz (0.87 mm)
* [ALMA Archive](https://almascience.eso.org/alma-data/archive)

**Chandra X-ray Observations:**
* Energy range: 0.5-10 keV (1.2×10¹⁷ - 2.4×10¹⁸ Hz)
* ObsID: 352 (M87 nucleus)
* [Chandra Data Archive](https://cxc.harvard.edu/cda/)
* [Di Matteo et al., ApJ 582, 133 (2003)](https://iopscience.iop.org/article/10.1086/344504)

### Data Access

**ALMA Science Archive:**
* [https://almascience.eso.org/alma-data/archive](https://almascience.eso.org/alma-data/archive)
* [https://almascience.eso.org/asax/](https://almascience.eso.org/asax/)
* Project Code: 2017.1.00841.V (EHT)

**Chandra Archive:**
* [https://cxc.harvard.edu/cda/](https://cxc.harvard.edu/cda/)
* [https://cda.harvard.edu/cscsearch/](https://cda.harvard.edu/cscsearch/)
* Target: M87*, ObsID: 352, 2707, 3717, etc.

---

## 2. Cygnus X-1 Thermal X-ray Spectrum (Chandra)

### Primary Literature

**Thermal Disk State Observations:**
* [Gou et al., ApJ 701, 1076 (2009)](https://iopscience.iop.org/article/10.1088/0004-637X/701/2/1076)
* ["The Extreme Spin of the Black Hole in Cygnus X-1"](https://arxiv.org/abs/1106.3690)
* [Miller et al., ApJ 775, L45 (2013)](https://iopscience.iop.org/article/10.1088/2041-8205/775/2/L45)

**Chandra Observations:**
* Instrument: ACIS-S (Advanced CCD Imaging Spectrometer)
* Energy: 0.5-10 keV → Frequency: 1.2×10¹⁷ - 2.4×10¹⁸ Hz
* Temperature: T_disk ~ 3×10⁷ K (30 MK)
* ObsID: 107, 1511, 3815, etc.

### Data Access

**Chandra Data Archive:**
* [https://cxc.harvard.edu/cda/](https://cxc.harvard.edu/cda/)
* Search: "Cygnus X-1", Instrument: ACIS
* [Python access: cxotime, ciao](https://cxc.harvard.edu/ciao/)

**HEASARC (High Energy Astrophysics Archive):**
* [https://heasarc.gsfc.nasa.gov/](https://heasarc.gsfc.nasa.gov/)
* [Browse Interface](https://heasarc.gsfc.nasa.gov/db-perl/W3Browse/w3browse.pl)

---

## 3. S2 Star Orbital Timeseries (VLT/GRAVITY)

* [https://www.aanda.org/articles/aa/full\_html/2018/07/aa33718-18/aa33718-18.html](https://www.aanda.org/articles/aa/full_html/2018/07/aa33718-18/aa33718-18.html)
* [https://www.aanda.org/articles/aa/pdf/2018/07/aa33718-18.pdf](https://www.aanda.org/articles/aa/pdf/2018/07/aa33718-18.pdf)
* [https://arxiv.org/abs/1807.09409](https://arxiv.org/abs/1807.09409)
* [https://www.science.org/doi/10.1126/science.aav8137](https://www.science.org/doi/10.1126/science.aav8137)
* [https://www.science.org/cms/asset/9b318de9-5652-4b20-9eab-f6eadab49e35/pap.pdf](https://www.science.org/cms/asset/9b318de9-5652-4b20-9eab-f6eadab49e35/pap.pdf)
* [https://arxiv.org/abs/1907.10731](https://arxiv.org/abs/1907.10731)
* (Program IDs & observation nights) [https://cds.cern.ch/record/2806198/files/2112.07478.pdf](https://cds.cern.ch/record/2806198/files/2112.07478.pdf)

### Primary Literature (S2/S0-2, Redshift)

* [https://physics.nist.gov/PhysRefData/ASD/lines\_form.html](https://physics.nist.gov/PhysRefData/ASD/lines_form.html)
* [https://www.nist.gov/pml/atomic-spectra-database](https://www.nist.gov/pml/atomic-spectra-database)
* [https://www.gemini.edu/observing/resources/near-ir-resources/spectroscopy/hydrogen-recombination-lines](https://www.gemini.edu/observing/resources/near-ir-resources/spectroscopy/hydrogen-recombination-lines)

## ESO Archive & Programmatic Access

* [https://archive.eso.org/](https://archive.eso.org/)
* [https://archive.eso.org/scienceportal/](https://archive.eso.org/scienceportal/)
* [https://archive.eso.org/cms/eso-data/programmatic-access.html](https://archive.eso.org/cms/eso-data/programmatic-access.html)
* [https://archive.eso.org/tap\_obs/examples/](https://archive.eso.org/tap_obs/examples/)
* [http://archive.eso.org/tap\_obs](http://archive.eso.org/tap_obs)
* [http://archive.eso.org/tap\_cat](http://archive.eso.org/tap_cat)
* [https://archive.eso.org/cms/eso-data/eso-programme-identification-code.html](https://archive.eso.org/cms/eso-data/eso-programme-identification-code.html)
* [https://www.eso.org/sci/facilities/paranal/instruments/gravity.html](https://www.eso.org/sci/facilities/paranal/instruments/gravity.html)

## CDS / SIMBAD / VizieR

* [https://simbad.u-strasbg.fr/simbad/sim-fbasic](https://simbad.u-strasbg.fr/simbad/sim-fbasic)
* [https://simbad.unistra.fr/simbad/sim-tap](https://simbad.unistra.fr/simbad/sim-tap)
* [https://tapvizier.u-strasbg.fr/adql/](https://tapvizier.u-strasbg.fr/adql/)

## Keck Observatory Archive (KOA)

* [https://vmkoaweb.ipac.caltech.edu/UserGuide/index.html](https://vmkoaweb.ipac.caltech.edu/UserGuide/index.html)
* [https://www.ipac.caltech.edu/project/keck-archive](https://www.ipac.caltech.edu/project/keck-archive)
* [https://github.com/KeckObservatoryArchive/PyKOA/](https://github.com/KeckObservatoryArchive/PyKOA/)

## Project Repository

* [https://github.com/LinoCasu/Segmented-Spacetime-Mass-Projection-Unified-Results](https://github.com/LinoCasu/Segmented-Spacetime-Mass-Projection-Unified-Results)

---

---

## 4. Supporting Data Sources

### Line Physics (Brackett-γ, H-alpha)

* [https://physics.nist.gov/PhysRefData/ASD/lines_form.html](https://physics.nist.gov/PhysRefData/ASD/lines_form.html)
* [https://www.nist.gov/pml/atomic-spectra-database](https://www.nist.gov/pml/atomic-spectra-database)
* [https://www.gemini.edu/observing/resources/near-ir-resources/spectroscopy/hydrogen-recombination-lines](https://www.gemini.edu/observing/resources/near-ir-resources/spectroscopy/hydrogen-recombination-lines)

### Mass Measurements

**M87* Black Hole Mass:**
* M = 6.5×10⁹ M☉
* [EHT Collaboration, ApJL 875, L1 (2019)](https://iopscience.iop.org/article/10.3847/2041-8213/ab0ec7)

**Cygnus X-1 Black Hole Mass:**
* M = 14.8 M☉
* [Miller-Jones et al., Science 371, 1046 (2021)](https://www.science.org/doi/10.1126/science.abb3363)

**Sgr A* Black Hole Mass:**
* M = 4.15×10⁶ M☉
* [GRAVITY Collaboration, A&A 615, L15 (2018)](https://www.aanda.org/articles/aa/full_html/2018/07/aa33718-18/aa33718-18.html)

---

## Reproducibility Procedures

### General Workflow

1. **Identify published observations** from primary literature
2. **Access public archives** (ALMA, Chandra, ESO)
3. **Extract spectral/timing data** from tables or FITS files
4. **Convert to SSZ format** (f_emit_Hz, f_obs_Hz, r_emit_m, M_solar)
5. **Store in CSV** (`real_data_full.csv`)
6. **Run pipeline** (`python run_all_ssz_terminal.py`)

### M87* Spectrum Reproduction

1. **Access ALMA Archive** → Project 2017.1.00841.V
2. **Download measurement sets** or published flux tables
3. **Extract frequencies and flux densities**
   - ALMA Band 3: 230 GHz, 345 GHz
   - ALMA Band 6/7: 228 GHz, 340 GHz
4. **Access Chandra Archive** → M87* ObsID 352, 2707
5. **Extract X-ray spectrum** (0.5-10 keV)
6. **Combine radio + X-ray** → Multi-frequency spectrum
7. **Store in** `data/observations/m87_continuum_spectrum_TEMPLATE.csv`

### Cygnus X-1 Thermal Spectrum Reproduction

1. **Access Chandra Archive** → Cyg X-1, thermal state
2. **Download ACIS spectra** (ObsID 107, 1511, 3815)
3. **Extract energy spectrum** (0.5-10 keV)
4. **Convert E(keV) → ν(Hz)**: ν = E × 2.418×10¹⁷ Hz/keV
5. **Fit thermal disk model** → T_disk ~ 3×10⁷ K
6. **Store in** `data/observations/cyg_x1_thermal_spectrum_TEMPLATE.csv`

### S2 Star Timeseries Reproduction

1. **Set reference lines:**
   - Brackett-γ: λ₀ = 2.1661 µm → f_emit = 1.38×10¹⁴ Hz
   - H-alpha: λ₀ = 656.3 nm → f_emit = 4.57×10¹⁴ Hz

2. **Obtain timeseries:**
   - **Option A:** Extract from GRAVITY Collaboration papers (Tables 1-3)
   - **Option B:** Query ESO Archive for GRAVITY/SINFONI spectra
     - Program IDs: 60.A-9102, 099.B-0640, etc.
     - Download reduced spectra (FITS)

3. **Extract line centers:**
   - Measure Doppler-shifted line centers → f_obs
   - Multiple epochs (2002-2018+)
   - Multiple orbital phases

4. **Calculate redshift:**
   - z = (f_emit - f_obs) / f_obs
   - Or: z = v_radial / c (from papers)

5. **Store in** `data/observations/s2_star_timeseries_TEMPLATE.csv`

## Notes

* Use vacuum wavelengths; differences from air wavelengths here are on the order of \~O(10^-3).
* For automated pipelines, `astroquery` (ESO/CDS) and `PyKOA` (Keck) are suitable. A later switch from “CSV-only” to “API fetch + caching” is planned.

---
Note on ALMA data access: Accessing ALMA data requires an authentication token, which means you must register an account. As of July 15, 2025, the access method has been switched from simple GET requests to a PROOF-based authentication system.

---

## Programmatic Access Tools

### Python Libraries

**ALMA:**
```python
from astroquery.alma import Alma
alma = Alma()
results = alma.query_object('M87', public=True)
```

**Chandra:**
```python
from astroquery.heasarc import Heasarc
heasarc = Heasarc()
table = heasarc.query_object('Cyg X-1', mission='CHANDRA')
```

**ESO (VLT/GRAVITY):**
```python
from astroquery.eso import Eso
eso = Eso()
eso.login('username')
table = eso.query_instrument('GRAVITY', target='S2')
```

### Archive URLs (Direct Access)

* **ALMA:** [https://almascience.eso.org/asax/](https://almascience.eso.org/asax/)
* **Chandra:** [https://cxc.harvard.edu/cda/](https://cxc.harvard.edu/cda/)
* **ESO:** [https://archive.eso.org/](https://archive.eso.org/)
* **HEASARC:** [https://heasarc.gsfc.nasa.gov/](https://heasarc.gsfc.nasa.gov/)

---

## Data Quality & Validation

### Current Dataset Statistics (2025-10-19)

**Total Data Points:** 167  
**Unique Sources:** 123  
**Real Observations:** 30 (M87*, Cyg X-1, S2)  

**Frequency Coverage:**
- Radio: 2.3×10¹¹ Hz (ALMA Band 3)
- Sub-mm: 3.4×10¹⁴ Hz (ALMA Band 7)
- Optical: 4.6×10¹⁴ Hz (VLT Br-gamma, H-alpha)
- X-ray: 1.0×10¹⁷ - 3.0×10¹⁸ Hz (Chandra)

**Total Range:** 6+ orders of magnitude (Radio → X-ray)

### Validation Status

- All data cross-checked with published values  
Multi-frequency sources: 5 (M87: 278 obs, Cyg X-1: 10, M87*: 10, S2: 10, Sgr A*: 6)  
- Thermal sources: 1 (Cyg X-1, T = 3×10⁷ K)  
 Multi-epoch sources: 2 (S2, PSR B1937+21)  

---

## Notes on Data Access

* **ALMA:** Requires account registration. As of 2024, uses OAuth2 authentication.
* **Chandra:** Public data freely accessible via CXC Archive.
* **ESO/VLT:** Public data available; proprietary period = 1 year after observation.
* **Vacuum wavelengths:** Always use vacuum values; air corrections ~ O(10⁻³).

### Future Enhancements

- [ ] Automated API fetch with caching (astroquery)
- [ ] Real-time ALMA/Chandra queries
- [ ] Integration with VO (Virtual Observatory) protocols
- [ ] Automated pipeline from archive → SSZ analysis

---

## Citation

If you use this data in publications, please cite:

1. **This repository:**
   - Wrede, C. & Casu, L. (2025). Segmented Spacetime Mass Projection - Unified Results.
   - https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results

2. **Original observations:**
   - M87*: EHT Collaboration et al., ApJL 875, L1 (2019)
   - Cyg X-1: Gou et al., ApJ 701, 1076 (2009)
   - S2: GRAVITY Collaboration, A&A 615, L15 (2018)

---

** 2025 Carmen Wrede & Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Last Updated:** 2025-10-19  
**Status:** Production-ready with real observational data
