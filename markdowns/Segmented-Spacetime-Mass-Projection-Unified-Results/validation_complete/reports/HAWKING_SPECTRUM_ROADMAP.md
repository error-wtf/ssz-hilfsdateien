# SSZ Hawking Spectrum Test - Roadmap & Implementation Guide

**Status:** ⚠️ TEILWEISE IMPLEMENTIERT  
**Datum:** 2025-10-19  
**Basierend auf:** Anleitung "Nachgedacht für 19s"

---

## 🎯 Ziel

Testen ob eine **thermische (Planck-ähnliche) Spektrum** mit Temperatur `T_seg` (abgeleitet von κ_seg) besser fittet als nicht-thermische Alternativen (Power-Law etc.) für Quellen nahe dem Horizont-Bereich.

---

## ✅ Was wir BEREITS haben

### **1. Grundlegende Framework (Test 4a)**
```
scripts/tests/test_horizon_hawking_predictions.py
```

**Implementiert:**
- ✅ κ_seg Berechnung (Surface Gravity Proxy)
- ✅ T_seg Berechnung (Temperature Proxy)
- ✅ BIC-Vergleich (Planck vs Uniform)
- ✅ Report-Generierung

**Limitation:**
- ❌ Nutzt nur Einzelfrequenzen (keine kontinuierlichen Spektren)
- ❌ Histogram-basiert statt echten Spektral-Fits

### **2. Daten**
```
data/real_data_full.csv
```

**Vorhanden:**
- ✅ 127 Datenpunkte
- ✅ 119 unique Quellen
- ✅ Frequenzbereich: 1.35 GHz - 2.34 PHz (6 Größenordnungen)
- ✅ Radiusbereich: 1.09 km - 8.81×10¹⁶ m

**Limitation:**
- ❌ Meist nur 1-2 Frequenzen pro Quelle
- ❌ Keine kontinuierlichen Spektren I_ν(ν) oder F_ν(ν)
- ❌ Keine Multi-Wellenlängen SEDs

### **3. Extended Test 4b (NEU!)**
```
scripts/tests/test_hawking_spectrum_continuum.py
```

**Implementiert:**
- ✅ Planck-Spektrum Fit
- ✅ Power-Law Spektrum Fit
- ✅ ΔBIC Evaluation
- ✅ Template-Daten Support

**Limitation:**
- ⚠️  Braucht echte Kontinuums-Daten (noch nicht vorhanden)

---

## ❌ Was FEHLT (für volle Umsetzung der Anleitung)

### **1. Kontinuierliche Spektren (KRITISCH!)**

**Was wir brauchen:**
```csv
source,frequency_Hz,flux_density_Jy,flux_error_Jy,instrument
M87*,2.30e11,0.95,0.05,ALMA_Band3
M87*,3.45e11,1.02,0.06,ALMA_Band3
M87*,2.28e14,0.87,0.04,ALMA_Band6
... (100+ Frequenzpunkte pro Quelle)
```

**Wo bekommt man das:**

#### **A) Sub-mm / Radio (Horizon-Skala)**

**EHT Public Data (M87*, 2017-04-05 bis 2017-04-11):**
- URL: https://eventhorizontelescope.org/for-astronomers/data
- Format: FITS (VLBI Visibilities) + Fluxdaten
- Instrumente: ALMA, SMA, JCMT, etc.
- **Was wir brauchen:** Kalibrierte Breitband-Kontinuum Flüsse

**ALMA Science Archive:**
- URL: https://almascience.nrao.edu/aq/
- Query: `M87* AND Continuum AND (Band 3 OR Band 6 OR Band 7)`
- **Was wir brauchen:** QA2 Produkte (fertig kalibriert)

**Prozess:**
```python
# Pseudo-Code
1. Download ALMA QA2 FITS files
2. Extract continuum SPWs (mehrere Frequenzen)
3. Für jede SPW: F_ν, σ_ν extrahieren
4. Kombinieren zu Spektrum
```

#### **B) Röntgen (innerer Disk)**

**Chandra Data Archive (CDA):**
- URL: https://cda.harvard.edu/chaser/
- Query: `M87 AND ObsType=IMAGING`
- Tools: CIAO `specextract`

**XMM-Newton Science Archive (XSA):**
- URL: http://nxsa.esac.esa.int/nxsa-web/
- Query: `M87`
- Tools: SAS `especget`

**Prozess:**
```bash
# CIAO (Chandra)
specextract src.fits[sky=circle(ra,dec,r)] mode=h

# Output: spectrum.pha, spectrum.rmf, spectrum.arf
# → Binned spectrum with Response Matrices
```

#### **C) Multi-Wellenlängen SEDs**

**EHT-MWL 2017 (M87*, koordinierte Kampagne):**
- URL: https://cds.unistra.fr/
- Referenz: EHT Collaboration et al. (2019), ApJL 875, L1-L6
- **Enthält:** Radio → mm → Optical → X-ray → γ-ray

---

### **2. Daten-Download & Processing Scripts**

#### **A) ALMA Downloader (FEHLT)**

```python
# scripts/data_acquisition/fetch_alma_continuum.py (TO BE CREATED)

def query_alma_archive(target, band, date_range):
    """
    Query ALMA archive for continuum data
    
    Uses astroquery.alma
    """
    from astroquery.alma import Alma
    
    alma = Alma()
    results = alma.query_object(target)
    # Filter for continuum, specific band, date range
    # Download QA2 products
    pass

def extract_continuum_spectrum(fits_file):
    """
    Extract continuum spectrum from ALMA FITS
    
    Returns: nu_Hz, F_Jy, sigma_Jy
    """
    pass
```

#### **B) Chandra/XMM Spectrum Extractor (FEHLT)**

```python
# scripts/data_acquisition/fetch_xray_spectrum.py (TO BE CREATED)

def download_chandra_observation(obsid):
    """Download Chandra observation from CDA"""
    pass

def run_specextract(evt_file, source_region):
    """
    Run CIAO specextract
    
    Requires: CIAO installed locally
    """
    import subprocess
    subprocess.run(['specextract', ...])
    pass

def convert_pha_to_csv(pha_file, rmf_file, arf_file):
    """
    Convert Chandra PHA spectrum to CSV
    
    Returns: DataFrame with E_keV, flux, error
    """
    pass
```

#### **C) EHT-MWL Data Loader (FEHLT)**

```python
# scripts/data_acquisition/fetch_eht_mwl_sed.py (TO BE CREATED)

def download_eht_mwl_2017(target='M87'):
    """
    Download EHT Multi-Wavelength 2017 SED from VizieR
    
    Returns: Full SED (radio → γ-ray)
    """
    from astroquery.vizier import Vizier
    # Query VizieR for EHT-MWL tables
    pass
```

---

### **3. Spektrum-Processing Pipeline**

```python
# scripts/processing/process_spectrum.py (TO BE CREATED)

def unify_spectrum(spectrum_dict):
    """
    Unify different spectral data (ALMA, Chandra, etc.)
    
    Input:
        {
            'alma': {'nu_Hz': ..., 'F_Jy': ...},
            'chandra': {'E_keV': ..., 'flux_ergcm2s': ...},
        }
    
    Output:
        {'nu_Hz': [...], 'F_nu': [...], 'sigma': [...]}
    """
    pass

def flag_rfi_flares(nu, F, method='sigma_clip'):
    """
    Remove RFI (Radio Frequency Interference)
    Remove flares
    
    Returns: cleaned nu, F, sigma
    """
    pass
```

---

## 🛠️ Wie kann man das JETZT umsetzen?

### **Option 1: Mit Template-Daten (KURZFRISTIG - FÜR TESTS)**

✅ **BEREITS ERSTELLT:**
```
data/observations/m87_continuum_spectrum_TEMPLATE.csv
scripts/tests/test_hawking_spectrum_continuum.py
```

**Vorteil:**
- ✅ Testet Framework sofort
- ✅ Zeigt wie der Test funktionieren würde
- ✅ Kein Daten-Download nötig

**Nachteil:**
- ❌ Nicht wissenschaftlich verwendbar (nur Platzhalter)
- ❌ Template-Daten sind "ausgedacht"

**Verwendung:**
```bash
# Test läuft mit Template
python scripts/tests/test_hawking_spectrum_continuum.py
```

---

### **Option 2: Echte Daten beschaffen (MITTELFRISTIG)**

#### **Schritt 1: Einfachster Fall - ALMA Archive**

**Was:** M87* ALMA Band 6 Kontinuum (EHT 2017 Kampagne)

**Wie:**
1. Gehe zu: https://almascience.nrao.edu/aq/
2. Query: `M87` + Filter: Date `2017-04-01` bis `2017-04-30`, Band 6
3. Download: QA2 "Continuum" Produkt (FITS)
4. Extrahiere: Frequenzen + Flüsse aus FITS → CSV konvertieren

**Tools:**
```python
from astropy.io import fits

# Read ALMA FITS
hdu = fits.open('alma_continuum.fits')
data = hdu[1].data

# Extract
nu_Hz = data['FREQUENCY']
F_Jy = data['FLUX']
sigma_Jy = data['ERROR']

# Save to CSV
pd.DataFrame({'frequency_Hz': nu_Hz, 'flux_density_Jy': F_Jy, 'flux_error_Jy': sigma_Jy}).to_csv('m87_continuum_spectrum.csv')
```

**Zeitaufwand:** ~2-3 Stunden (Download + Conversion)

---

#### **Schritt 2: Erweitert - Chandra Spektrum**

**Was:** M87* Chandra X-ray Spektrum

**Wie:**
1. Gehe zu: https://cda.harvard.edu/chaser/
2. Query: `M87` + Filter: Instrument=ACIS
3. Download: Level 2 Event File
4. **Braucht:** CIAO installiert (→ Linux/WSL)
5. Run: `specextract ...` → erzeugt `.pha`, `.rmf`, `.arf`
6. Convert to CSV

**Zeitaufwand:** ~1 Tag (Installation + Processing)

---

#### **Schritt 3: Vollständig - EHT-MWL SED**

**Was:** Komplette Multi-Wellenlängen SED (EHT 2017)

**Wie:**
1. Gehe zu: https://cds.unistra.fr/ (VizieR)
2. Search: `EHT M87 2017` oder DOI `10.3847/2041-8213/ab0ec7`
3. Download: Tables (meist ASCII oder FITS)
4. Extract + Combine

**Zeitaufwand:** ~1 Tag (Suchen + Download + Merge)

---

### **Option 3: Mock-Spektren erzeugen (MITTELFRISTIG - FÜR VALIDATION)**

Wie in der Anleitung erwähnt: **Labor-Analog / Simulation**

```python
# scripts/simulation/generate_mock_hawking_spectrum.py (TO BE CREATED)

def generate_mock_thermal_spectrum(T_seg, nu_range, noise_level):
    """
    Generate mock thermal spectrum based on T_seg
    
    Add realistic noise, instrumental response, etc.
    """
    pass

def generate_mock_powerlaw_spectrum(alpha, nu_range, noise_level):
    """
    Generate mock non-thermal spectrum
    """
    pass
```

**Verwendung:**
```python
# Generate pair: thermal + non-thermal
thermal = generate_mock_thermal_spectrum(T_seg=1e-34, nu_range=[1e9, 1e15])
powerlaw = generate_mock_powerlaw_spectrum(alpha=-0.7, nu_range=[1e9, 1e15])

# Test if framework correctly identifies thermal
results = fit_spectrum_models(thermal['nu'], thermal['F'], thermal['sigma'])
assert results['thermal']['bic'] < results['powerlaw']['bic']  # Should prefer thermal
```

**Vorteil:**
- ✅ Kein Daten-Download nötig
- ✅ Kontrolle über alle Parameter
- ✅ Ideal für Unit-Tests

**Nachteil:**
- ❌ Nicht realistisch (keine echten instrumentellen Effekte)
- ❌ Kann reale Daten nicht ersetzen

---

## 📋 Roadmap / Priorisierung

### **Phase 1: Template & Framework (JETZT - FERTIG!)**
- [x] Template-Daten erstellen (`m87_continuum_spectrum_TEMPLATE.csv`)
- [x] Extended Test 4b Script (`test_hawking_spectrum_continuum.py`)
- [x] Dokumentation (`HAWKING_SPECTRUM_ROADMAP.md`)

### **Phase 2: Mock-Spektren (NÄCHSTE WOCHE)**
- [ ] Mock spectrum generator
- [ ] Validation Tests (thermal vs non-thermal identification)
- [ ] Parameter sensitivity analysis

### **Phase 3: Echte Daten - Einfach (1-2 WOCHEN)**
- [ ] ALMA Archive Downloader (`fetch_alma_continuum.py`)
- [ ] M87* ALMA Band 6 Daten beschaffen
- [ ] FITS → CSV Converter
- [ ] Integration in Test 4b

### **Phase 4: Echte Daten - Erweitert (1-2 MONATE)**
- [ ] Chandra/XMM Downloader + Processor
- [ ] CIAO/SAS Integration (benötigt Linux/WSL)
- [ ] EHT-MWL SED Loader
- [ ] Multi-Wellenlängen Kombination

### **Phase 5: Produktion (3+ MONATE)**
- [ ] Automatisierte Pipeline (Download → Process → Fit → Report)
- [ ] Multiple Quellen (M87*, Sgr A*, Cyg X-1, etc.)
- [ ] Epochen-Vergleiche
- [ ] Publikations-Quality Plots

---

## 🎯 Empfehlung: Was JETZT tun?

### **Für sofortiges Testen:**
```bash
# 1. Test mit Template-Daten
python scripts/tests/test_hawking_spectrum_continuum.py

# 2. In Complete Validation integrieren
# (später commit wenn zufrieden)
```

### **Für nächsten Schritt:**

**Option A (Schnell - Mock Daten):**
```python
# Erstelle Mock-Spektren Generator
# → Validiere dass Framework korrekt unterscheidet
# → Schreibe Unit-Tests
```

**Option B (Echt - ALMA Daten):**
```python
# Gehe zu ALMA Archive
# → Download M87* Band 6 (2017-04)
# → Konvertiere zu CSV
# → Ersetze TEMPLATE mit echten Daten
```

---

## 📊 Was ist der Stand JETZT?

```
═══════════════════════════════════════════════════════════════════════════════
                    HAWKING SPECTRUM TEST - STATUS
═══════════════════════════════════════════════════════════════════════════════

✅ IMPLEMENTIERT:
   - Basic Framework (Test 4a) - histogram-based BIC
   - Extended Framework (Test 4b) - spectral fitting
   - Template Data (M87* continuum - 10 points)
   - Documentation (diese Datei)

⚠️  TEILWEISE:
   - Spectrum Fitting (vorhanden, aber mit Template)
   - BIC Evaluation (funktioniert, braucht echte Daten)

❌ FEHLT:
   - Kontinuierliche Spektren (echte Daten)
   - ALMA/Chandra Download Scripts
   - Spektrum-Processing Pipeline
   - Multi-Source Analysis

STATUS: Framework bereit, warten auf echte Daten
NÄCHSTER SCHRITT: Mock-Spektren ODER ALMA Download
═══════════════════════════════════════════════════════════════════════════════
```

---

## 📞 Fragen?

**Für Implementation-Hilfe:**
- Siehe: `scripts/tests/test_hawking_spectrum_continuum.py`
- Siehe: `data/observations/m87_continuum_spectrum_TEMPLATE.csv`

**Für Daten-Beschaffung:**
- ALMA: https://almascience.nrao.edu/aq/
- Chandra: https://cda.harvard.edu/chaser/
- EHT: https://eventhorizontelescope.org/for-astronomers/data

---

**© 2025 Carmen Wrede, Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Version:** 1.0.0  
**Last Updated:** 2025-10-19  
**Status:** ⚠️ FRAMEWORK READY, AWAITING REAL DATA
