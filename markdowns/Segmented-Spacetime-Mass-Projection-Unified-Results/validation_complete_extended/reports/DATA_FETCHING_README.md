# SSZ Suite - Smart Data Fetching System

## Übersicht

Das Installation System prüft **automatisch** welche Daten fehlen und lädt **nur** die benötigten Dateien herunter.

**Wichtig:** Existierende Dateien werden **NIEMALS** überschrieben!

---

## Daten-Kategorien

### **1. Release-Daten (im Package enthalten)**

Diese Dateien sind **im Release enthalten** und müssen NICHT gedownloadet werden:

```
data/
├── real_data_full.csv          # Hauptdatensatz (~50 MB)
└── gaia/
    ├── gaia_sample_small.csv   # Kleine GAIA Samples (~1 MB)
    ├── gaia_cone_g79.csv       # G79 Region (~500 KB)
    └── gaia_cone_cygx.csv      # Cygnus X Region (~500 KB)
```

**Größe insgesamt:** ~52 MB

---

### **2. Große Daten (automatischer Fetch bei Bedarf)**

Diese Dateien sind **2 GB groß** und werden **NUR wenn fehlend** automatisch geladen:

```
data/planck/
└── COM_PowerSpect_CMB-TT-full_R3.01.txt  # Planck 2018 CMB (2 GB)
```

**Quelle:** Planck Legacy Archive (ESA)

---

### **3. Optionale Daten (manueller Fetch)**

Diese Dateien sind optional und können bei Bedarf manuell geladen werden:

```
data/gaia/
└── gaia_full_sample.csv  # Vollständiger GAIA Sample (~500 MB)
```

---

## Installation Workflow

### **Was passiert bei Installation:**

```bash
.\install.ps1  # oder ./install.sh
```

#### **[8/10] Checking data files...**

```
✓ real_data_full.csv found
✓ gaia/gaia_sample_small.csv found
✓ gaia/gaia_cone_g79.csv found
✓ gaia/gaia_cone_cygx.csv found

⚠ Planck data missing (2GB) - fetching...
  Downloading Planck CMB power spectrum...
  This may take several minutes (2GB file)...
  [████████████████████████████] 100.0% (2048.3/2048.3 MB)
✓ Planck data fetched successfully

Note: Data files were downloaded. They will NOT be overwritten on reinstall.
```

---

## Smart Fetching Logik

### **Prüfung VOR Download:**

```python
if not os.path.exists("data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt"):
    # Fetch nur wenn NICHT vorhanden!
    download_planck_data()
else:
    print("✓ Planck data found (skipping download)")
```

### **Re-Installation:**

```bash
# Erste Installation:
.\install.ps1
# → Lädt Planck Daten (2 GB)

# Zweite Installation (z.B. nach Update):
.\install.ps1
# → Erkennt existierende Daten
# → Überspringt Download!
# → Keine Überschreibung!
```

---

## Manuelle Daten-Verwaltung

### **Planck Daten manuell fetchen:**

```bash
python scripts/fetch_planck.py
```

**Ausgabe:**
```
================================================================================
PLANCK CMB POWER SPECTRUM - DATA FETCH
================================================================================

Dataset: Planck 2018 Release 3
File: COM_PowerSpect_CMB-TT-full_R3.01.txt
Size: ~2 GB
Source: Planck Legacy Archive (ESA)

This may take several minutes depending on your connection...

Attempting download from ESA Planck Legacy Archive...
Downloading from: https://pla.esac.esa.int/pla/aio/...
Saving to: data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt

[████████████████████████████░░░░] 75.3% (1536.5/2048.3 MB)
```

### **Planck Daten prüfen:**

```bash
# Windows:
dir data\planck\COM_PowerSpect_CMB-TT-full_R3.01.txt

# Linux:
ls -lh data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt
```

### **Planck Daten löschen (Re-Download):**

```bash
# Windows:
del data\planck\COM_PowerSpect_CMB-TT-full_R3.01.txt

# Linux:
rm data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt

# Dann neu fetchen:
python scripts/fetch_planck.py
```

---

## Datenquellen

### **Planck Legacy Archive (ESA)**

**Primary:**
```
https://pla.esac.esa.int/pla/aio/product-action?COSMOLOGY.FILE_ID=COM_PowerSpect_CMB-TT-full_R3.01.txt
```

**Alternative (IPAC):**
```
https://irsa.ipac.caltech.edu/data/Planck/release_3/ancillary-data/cosmoparams/COM_PowerSpect_CMB-TT-full_R3.01.txt
```

### **GAIA Data (ESA)**

```
https://gea.esac.esa.int/archive/
```

---

## Release Package Struktur

### **Was MUSS im Release sein:**

```
SSZ-suite-v1.0.tar.gz/
├── data/
│   ├── real_data_full.csv          # ✅ MUSS
│   └── gaia/
│       ├── gaia_sample_small.csv   # ✅ MUSS
│       ├── gaia_cone_g79.csv       # ✅ MUSS
│       └── gaia_cone_cygx.csv      # ✅ MUSS
├── scripts/
│   ├── fetch_planck.py             # ✅ MUSS (fetch script)
│   └── ...
└── ...
```

### **Was NICHT im Release ist:**

```
data/planck/
└── COM_PowerSpect_CMB-TT-full_R3.01.txt  # ❌ ZU GROSS! Auto-fetch!
```

---

## Installation Szenarien

### **Szenario 1: Erste Installation (mit Internet)**

```bash
.\install.ps1
```

**Ergebnis:**
- ✅ Release-Daten gefunden (52 MB)
- ⚠️ Planck fehlt → Automatischer Download (2 GB)
- ✅ Installation komplett

---

### **Szenario 2: Erste Installation (ohne Internet)**

```bash
.\install.ps1
```

**Ergebnis:**
- ✅ Release-Daten gefunden (52 MB)
- ⚠️ Planck fehlt → Download FEHLSCHLÄGT
- ⚠️ Warnung: "Planck data fetch failed - continuing anyway"
- ✅ Installation funktioniert (ohne Planck Analysen)

**Später mit Internet:**
```bash
python scripts/fetch_planck.py
```

---

### **Szenario 3: Re-Installation (Daten vorhanden)**

```bash
.\install.ps1
```

**Ergebnis:**
- ✅ Release-Daten gefunden
- ✅ Planck Daten gefunden (skip download!)
- ✅ Schnelle Re-Installation (~2 Min statt ~20 Min)

---

### **Szenario 4: Update Installation**

```bash
# Update Code:
git pull origin main

# Re-install:
.\install.ps1
```

**Ergebnis:**
- ✅ Code aktualisiert
- ✅ Dependencies aktualisiert
- ✅ **Daten NICHT überschrieben!**
- ✅ Tests laufen mit existierenden Daten

---

## Daten-Größen Übersicht

| Datei | Größe | Im Release? | Auto-Fetch? |
|-------|-------|-------------|-------------|
| real_data_full.csv | ~50 MB | ✅ Ja | ❌ Nein |
| gaia_sample_small.csv | ~1 MB | ✅ Ja | ❌ Nein |
| gaia_cone_g79.csv | ~500 KB | ✅ Ja | ❌ Nein |
| gaia_cone_cygx.csv | ~500 KB | ✅ Ja | ❌ Nein |
| COM_PowerSpect_CMB-TT-full_R3.01.txt | ~2 GB | ❌ Nein | ✅ Ja |
| gaia_full_sample.csv | ~500 MB | ❌ Nein | ⚠️ Optional |

**Release-Größe:** ~52 MB  
**Nach Installation:** ~2.05 GB (mit Planck)

---

## Troubleshooting

### **Problem: Planck Download schlägt fehl**

```
⚠ Failed to fetch Planck data - continuing anyway
```

**Lösung:**
1. Prüfe Internet-Verbindung
2. Versuche später nochmal:
   ```bash
   python scripts/fetch_planck.py
   ```
3. Oder manuell downloaden von ESA/IPAC

---

### **Problem: "File already exists" Warnung**

```
✓ Planck data found (skipping download)
```

**Das ist KEIN Problem!** Das ist gewollt:
- Existierende Daten werden geschützt
- Kein unnötiger Re-Download
- Installation läuft weiter

---

### **Problem: Daten corrupted**

```bash
# Planck Daten löschen:
rm data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt

# Neu fetchen:
python scripts/fetch_planck.py
```

---

## Datei-Integrität

### **Planck Daten prüfen:**

```bash
# Größe prüfen (sollte ~2 GB sein):
ls -lh data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt

# Erste Zeilen ansehen:
head -n 5 data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt
```

**Erwartete Ausgabe:**
```
# Planck 2018 Power Spectra
# TT Power Spectrum (Full Mission)
# l      Dl^TT    error
2      226.346   1.234
3      1256.234  2.345
...
```

---

## Best Practices

### **Für Entwickler:**

1. ✅ **NIEMALS** Planck Daten ins Git committen (zu groß!)
2. ✅ Kleine Test-Daten im Release behalten
3. ✅ `.gitignore` für große Daten:
   ```
   data/planck/*.txt
   data/gaia/gaia_full_sample.csv
   ```

### **Für Users:**

1. ✅ Erste Installation mit Internet machen
2. ✅ Planck Daten behalten (keine Re-Downloads)
3. ✅ Bei Problemen: `python scripts/fetch_planck.py`

### **Für CI/CD:**

1. ✅ Cache Planck Daten in CI Pipeline
2. ✅ Oder: Tests ohne Planck laufen lassen
3. ✅ Download-Timeout setzen (10+ Minuten)

---

## FAQ

### **Q: Warum ist Planck nicht im Release?**
**A:** 2 GB ist zu groß für GitHub Releases (~100 MB Limit). Auto-fetch ist besser!

### **Q: Was wenn ich kein Internet habe?**
**A:** Installation funktioniert ohne Planck. Analysen die Planck brauchen werden übersprungen.

### **Q: Werden meine Daten überschrieben?**
**A:** **NEIN!** Das System prüft VOR dem Download. Existierende Dateien werden NICHT überschrieben!

### **Q: Kann ich Planck manuell downloaden?**
**A:** Ja! Einfach von ESA/IPAC runterladen und nach `data/planck/` legen.

### **Q: Was wenn Planck Download abbricht?**
**A:** Einfach nochmal `python scripts/fetch_planck.py` ausführen.

---

## Copyright

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

**Smart Data Fetching = Keine unnötigen Re-Downloads!** ✅
