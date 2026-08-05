# SSZ Theory Predictions - Data Acquisition Plan

**Datum:** 2025-10-19  
**Status:** Fehlende Daten identifiziert  
**Priorität:** HOCH (für vollständige Test-Validierung)

---

## 🎯 Fehlende Daten - Übersicht

### **Test 2: Information Preservation** ⚠️
- **Status:** Framework funktioniert, aber keine geeigneten Daten
- **Benötigt:** Zeitserien-Daten (≥3 Beobachtungen pro Quelle)
- **Aktuelles Problem:** Alle 119 Quellen haben nur 1-2 Datenpunkte

### **Test 4a: Hawking Spectrum Fit** ⚠️
- **Status:** BIC-Test läuft, aber kein thermales Spektrum erkannt
- **Benötigt:** Thermale Einzelquelle (schwarzes Loch)
- **Aktuelles Problem:** 127 diverse Objekte → kein thermales Ensemble

---

## 📋 PRIORITY 1: Zeitserien-Daten für Information Preservation

### **Was wir brauchen:**

**Option A: S2-Stern Zeitserien (OPTIMAL)**
- **Quelle:** S2-Stern um Sgr A*
- **Beobachtungen:** Mehrere Orbit-Phasen (2000-2024)
- **Daten:** Radialgeschwindigkeit über Zeit
- **Frequenzen:** Mehrere Spektrallinien pro Beobachtung

**Beispiel-Struktur:**
```csv
source,observation_date,orbital_phase,f_emit_Hz,f_obs_Hz,r_emit_m,v_los_mps,M_solar
S2,2002-05-15,0.12,4.568e14,4.565e14,3.8e10,500000,4.15e6
S2,2004-03-20,0.24,4.568e14,4.560e14,2.1e10,1200000,4.15e6
S2,2006-01-10,0.36,4.568e14,4.555e14,1.5e10,1800000,4.15e6
S2,2008-11-05,0.48,4.568e14,4.550e14,1.2e10,2100000,4.15e6
S2,2010-09-15,0.60,4.568e14,4.548e14,1.0e10,2300000,4.15e6
...
```

**Mindestanforderungen:**
- ≥5 Beobachtungen pro Quelle
- Verschiedene Orbital-Phasen (r variiert)
- Mehrere Spektrallinien (f_emit variiert)

**Datenquellen:**
1. **ESO/VLT Archive** - https://archive.eso.org
   - GRAVITY instrument data
   - SINFONI spectroscopy
   - S2 monitoring program (2000-2024)

2. **Keck Observatory Archive** - https://koa.ipac.caltech.edu
   - Galactic Center observations
   - Radial velocity measurements

3. **Published Papers:**
   - Gillessen et al. (2009) - "Monitoring Stellar Orbits Around Sgr A*"
   - GRAVITY Collaboration (2018) - "Detection of orbital motions near Sgr A*"
   - Do et al. (2019) - "Relativistic redshift of S0-2"

---

### **Option B: Pulsar-Timing (Alternative)**
- **Quelle:** Binär-Pulsare (z.B. PSR J0737-3039)
- **Beobachtungen:** Timing-Residuen über Jahre
- **Frequenzen:** Pulsar-Frequenz-Evolution

**Beispiel-Struktur:**
```csv
source,mjd,f_emit_Hz,f_obs_Hz,r_emit_m,orbital_phase,M_solar
PSR_J0737-3039A,54000.0,1.234e9,1.233e9,8.5e8,0.0,1.34
PSR_J0737-3039A,54001.0,1.234e9,1.232e9,7.8e8,0.15,1.34
PSR_J0737-3039A,54002.0,1.234e9,1.231e9,7.2e8,0.30,1.34
...
```

**Datenquellen:**
1. **ATNF Pulsar Catalogue** - https://www.atnf.csiro.au/research/pulsar/psrcat/
2. **NANOGrav Data** - https://nanograv.org
3. **Published Timing Data:**
   - Kramer et al. (2021) - "Strong-field tests with PSR J0737-3039"

---

## 📋 PRIORITY 2: Thermale Quelle für Hawking Spektrum

### **Was wir brauchen:**

**Option A: Stellar-Mass Black Hole X-ray Spectrum**
- **Quelle:** Cyg X-1, GRS 1915+105, oder ähnlich
- **Beobachtungen:** X-ray Spektrum (thermale Disk-Komponente)
- **Frequenzen:** 10¹⁶ - 10¹⁹ Hz (X-ray)

**Beispiel-Struktur:**
```csv
source,frequency_Hz,flux_erg_cm2_s,temperature_K,M_solar,r_emit_m
Cyg_X-1,1.0e17,1.2e-8,3.0e7,14.8,4.4e4
Cyg_X-1,2.0e17,8.5e-9,3.0e7,14.8,4.4e4
Cyg_X-1,5.0e17,3.2e-9,3.0e7,14.8,4.4e4
Cyg_X-1,1.0e18,1.1e-9,3.0e7,14.8,4.4e4
Cyg_X-1,2.0e18,3.8e-10,3.0e7,14.8,4.4e4
...
```

**Datenquellen:**
1. **HEASARC Archive** - https://heasarc.gsfc.nasa.gov
   - XMM-Newton observations
   - Chandra HETG spectra
   - NuSTAR data

2. **Swift/BAT Catalog** - https://swift.gsfc.nasa.gov
   - X-ray transients
   - Time-averaged spectra

3. **Published Spectra:**
   - Remillard & McClintock (2006) - "X-Ray Properties of Black-Hole Binaries"
   - Shaposhnikov & Titarchuk (2009) - "Cygnus X-1 spectral evolution"

---

### **Option B: AGN Thermal Disk (Alternative)**
- **Quelle:** NGC 5548, 3C 273, oder ähnlich
- **Beobachtungen:** UV/Optical thermal emission
- **Frequenzen:** 10¹⁴ - 10¹⁶ Hz

**Datenquellen:**
1. **HST Archive** - https://archive.stsci.edu
   - UV spectroscopy
   - Multi-epoch observations

2. **SDSS Quasar Catalog** - https://www.sdss.org
   - Composite spectra
   - Individual objects

---

## 🔧 Integration in Pipeline

### **Schritt 1: Daten-Format definieren**

**Neue Datei:** `data/observations/s2_star_timeseries.csv`

**Required Columns:**
```python
{
    'source': str,              # Source identifier (same for all rows)
    'observation_date': str,    # ISO format or MJD
    'f_emit_Hz': float,         # Rest-frame frequency
    'f_obs_Hz': float,          # Observed frequency  
    'r_emit_m': float,          # Emission radius
    'v_los_mps': float,         # Line-of-sight velocity
    'M_solar': float,           # Central mass in solar masses
    'orbital_phase': float,     # Optional: 0-1
    'spectral_line': str        # Optional: H-alpha, FeII, etc.
}
```

### **Schritt 2: Loader-Funktion erstellen**

**Datei:** `scripts/data_loaders/load_timeseries.py`

```python
def load_s2_timeseries(csv_path):
    """Load S2 star time-series data for Jacobian reconstruction"""
    df = pd.read_csv(csv_path)
    
    # Validate required columns
    required = ['source', 'f_emit_Hz', 'f_obs_Hz', 'r_emit_m', 'M_solar']
    missing = set(required) - set(df.columns)
    if missing:
        raise ValueError(f"Missing columns: {missing}")
    
    # Group by source
    sources = {}
    for source, group in df.groupby('source'):
        if len(group) >= 3:  # Minimum for Jacobian
            sources[source] = group.sort_values('orbital_phase')
    
    return sources
```

### **Schritt 3: Tests aktualisieren**

**Modifikation:** `scripts/tests/test_horizon_hawking_predictions.py`

```python
def load_phi_debug_data(base_path=None, timeseries_path=None):
    """Load data with optional time-series supplement"""
    
    # Load existing data
    df_main = pd.read_csv(base_path / "phi_step_debug_full.csv")
    
    # Append time-series if available
    if timeseries_path and timeseries_path.exists():
        df_ts = pd.read_csv(timeseries_path)
        df = pd.concat([df_main, df_ts], ignore_index=True)
        print(f"✅ Loaded {len(df_ts)} time-series points")
    else:
        df = df_main
        print(f"⚠️  No time-series data, using {len(df)} main points")
    
    return df
```

---

## 📊 Daten-Beschaffungs-Workflow

### **Phase 1: S2-Stern Daten (2 Wochen)**

**Woche 1: Archive-Recherche**
- [ ] ESO Archive durchsuchen (S2 GRAVITY data)
- [ ] Keck Archive durchsuchen (S2 spectroscopy)
- [ ] Papers mit Supplementary Data finden
- [ ] Daten-Zugang beantragen (falls nötig)

**Woche 2: Daten-Extraktion**
- [ ] FITS-Dateien herunterladen
- [ ] Spektren extrahieren (f_obs)
- [ ] Radialgeschwindigkeiten berechnen
- [ ] CSV formatieren
- [ ] In Pipeline integrieren

**Erwartetes Ergebnis:**
- 10-20 S2 Beobachtungen (2002-2024)
- 3-5 Spektrallinien pro Beobachtung
- 30-100 Datenpunkte gesamt

---

### **Phase 2: X-ray Spektren (1 Woche)**

**Tag 1-2: Cyg X-1 Spektrum**
- [ ] HEASARC suchen (XMM-Newton ObsID)
- [ ] Spektrum herunterladen (FITS)
- [ ] Flux vs. Energy extrahieren

**Tag 3-4: Spektrum prozessieren**
- [ ] Energy → Frequency konvertieren
- [ ] Thermale Komponente fitten
- [ ] Planck-Temperatur bestimmen

**Tag 5-7: Integration**
- [ ] CSV formatieren
- [ ] Test aktualisieren
- [ ] BIC-Vergleich durchführen

**Erwartetes Ergebnis:**
- 50-100 Frequenz-Bins (10¹⁶-10¹⁹ Hz)
- Thermale Temperatur T ~ 10⁷ K
- ΔBIC < -10 (starke Evidenz für Planck)

---

## 🚀 Quick Start (sofortige Schritte)

### **1. ESO Archive (JETZT)**

**URL:** https://archive.eso.org/wdb/wdb/adp/phase3_main/form

**Suche:**
```
Target: S2
Instrument: GRAVITY, SINFONI
Program ID: 60.A-9102, 099.B-0640
Date Range: 2002-01-01 to 2024-12-31
Data Product Type: SPECTRUM
```

**Download:** 
- FITS files mit Radialgeschwindigkeit
- Supplementary Tables (CSV)

---

### **2. Published Data (JETZT)**

**Paper 1: GRAVITY Collaboration (2018)**
- **DOI:** 10.1051/0004-6361/201833718
- **Supplementary Data:** Table 2 (Radial velocities)
- **Format:** ASCII table → CSV konvertieren

**Paper 2: Gillessen et al. (2017)**
- **DOI:** 10.3847/1538-4357/aa5c41
- **Supplementary Data:** Online Table (S2 astrometry + RV)

---

### **3. HEASARC Quick Access (JETZT)**

**URL:** https://heasarc.gsfc.nasa.gov/db-perl/W3Browse/w3table.pl?tablehead=name%3Dxmmmaster

**Suche:**
```
Target: Cyg X-1
Mission: XMM-Newton
Obs Mode: Timing/Spectroscopy
Exposure: >10 ks
```

**Download:**
- PPS (Pipeline Products) - bereits reduzierte Spektren
- Format: FITS → ASCII → CSV

---

## 📦 Dateien die wir erstellen

### **Neue Dateien:**
```
data/observations/
├── s2_star_timeseries.csv          # S2 Orbit-Daten (30-100 rows)
├── cyg_x1_thermal_spectrum.csv     # X-ray Spektrum (50-100 rows)
├── psr_j0737_timing.csv            # Pulsar (optional)
└── README_TIMESERIES.md            # Daten-Dokumentation

scripts/data_loaders/
├── load_timeseries.py              # Loader-Funktionen
└── process_xray_spectrum.py        # X-ray Prozessierung

scripts/tests/
└── test_horizon_hawking_predictions.py  # UPDATED (neue Daten)
```

### **Aktualisierte Dateien:**
```
run_all_ssz_terminal.py             # Optional: Auto-load timeseries
reports/
└── SSZ_THEORY_PREDICTIONS_REAL_DATA_SUMMARY.md  # Mit neuen Results
```

---

## ✅ Success Metrics

### **Information Preservation:**
- ✅ ≥1 Quelle mit ≥5 Beobachtungen
- ✅ Jacobian reconstruction error < 1%
- ✅ ≥50% Quellen mit stabilen Jacobianen

### **Hawking Spectrum:**
- ✅ ΔBIC < -10 (starke Evidenz für Planck)
- ✅ Temperatur-Fit: χ² < 2.0
- ✅ Thermale Komponente identifiziert

---

## 📞 Kontakte & Ressourcen

### **ESO Archive Support:**
- Email: archive@eso.org
- User Guide: https://archive.eso.org/cms/eso-archive-news/archive-user-guide.html

### **HEASARC Help Desk:**
- Email: heasarc-vo@athena.gsfc.nasa.gov
- Browse Tutorial: https://heasarc.gsfc.nasa.gov/cgi-bin/W3Browse/w3browse.pl

### **Paper Authors (für Supplementary Data):**
- GRAVITY Collaboration: gravity@mpe.mpg.de
- Gillessen et al.: gillessen@mpe.mpg.de

---

## 🎯 Timeline

**Woche 1-2:** S2 Daten beschaffen + integrieren  
**Woche 3:** X-ray Spektrum beschaffen + integrieren  
**Woche 4:** Tests finalisieren + Paper schreiben  

**Ziel:** Alle 7 Tests mit echten Daten validiert bis Ende Oktober 2025

---

**© 2025 Carmen Wrede, Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**
