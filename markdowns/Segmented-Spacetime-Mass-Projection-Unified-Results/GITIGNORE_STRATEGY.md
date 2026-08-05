# .gitignore Strategie - Dateien unter 125 MB behalten

**Datum:** 2025-10-19  
**Ziel:** Alle Dateien unter 125 MB im Repository, große Dateien ausschließen

---

## 🎯 Strategie

### **Prinzip:**
- ✅ **BEHALTEN:** Alle Dateien < 125 MB (GitHub-Limit)
- ❌ **AUSSCHLIESSEN:** Nur spezifische große Dateien (>125 MB)

### **Warum nicht wildcards?**
❌ **FALSCH:**
```gitignore
data/**/*.parquet  # Schließt ALLE Parquet-Dateien aus!
models/**/*.parquet  # Auch kleine Test-Fixtures!
```

✅ **RICHTIG:**
```gitignore
# Nur die spezifischen großen Dateien:
models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet  # 1373 MB
data/raw/gaia/2025-10-17_gaia_ssz_real/gaia_dr3_core.parquet  # 79 MB
data/raw/gaia/2025-10-17_gaia_ssz_real/*.parquet  # Nur dieser Ordner
```

---

## 📂 Datei-Kategorien

### **1. Models (BEHALTEN wenn <125 MB)**

#### ✅ INKLUDIERT:
```
models/cosmology/2025-10-17_gaia_ssz_v1/
├── ssz_field.parquet          # 0.14 MB ✓
├── ssz_meta.json             # 0.001 MB ✓
└── solar_manifest.json       # 0.001 MB ✓

models/cosmology/2025-10-17_gaia_ssz_nightly/
├── ssz_field.parquet          # 14.25 MB ✓
├── ssz_meta.json             # 0.001 MB ✓
└── solar_manifest.json       # 0.001 MB ✓

models/solar_system/2025-10-17_gaia_ssz_*/
└── solar_ssz.json            # 0.06-0.25 MB ✓
```

#### ❌ AUSGESCHLOSSEN:
```
models/cosmology/2025-10-17_gaia_ssz_real/
└── ssz_field.parquet          # 1373.31 MB ❌ (>125 MB)
```

---

### **2. Data (BEHALTEN wenn <125 MB)**

#### ✅ INKLUDIERT:
```
data/interim/gaia/2025-10-17_gaia_ssz_v1/
├── gaia_clean.parquet         # 0.08 MB ✓
└── gaia_phase_space.parquet   # 0.12 MB ✓

data/interim/gaia/2025-10-17_gaia_ssz_nightly/
├── gaia_clean.parquet         # 6.09 MB ✓
└── gaia_phase_space.parquet   # 11.56 MB ✓

data/raw/gaia/2025-10-17_gaia_ssz_nightly/
├── gaia_dr3_core.parquet      # 3.32 MB ✓
└── gaia_dr3_core.csv          # 6.47 MB ✓

data/raw/sdss/2025-10-17_gaia_ssz_*/
├── sdss_catalog.parquet       # 0.36 MB ✓
└── sdss_catalog.csv           # 0.53 MB ✓
```

#### ❌ AUSGESCHLOSSEN:
```
data/raw/gaia/2025-10-17_gaia_ssz_real/
├── gaia_dr3_core.parquet                                 # 78.83 MB (optional)
├── 2025-10-17_gaia_ssz_real__part00_20251017T110038.parquet  # 193.39 MB ❌
└── test_run__part00_20251017T091550.parquet              # 193.13 MB ❌

data/interim/gaia/2025-10-17_gaia_ssz_real/
├── gaia_clean.parquet         # 757.11 MB ❌
└── gaia_phase_space.parquet   # 1169.17 MB ❌
```

---

## 🔧 .gitignore Implementation

### **Aktuelle Einträge:**

```gitignore
# Models - Nur große Dateien ausschließen (>125 MB)
models/**/*.hdf5
models/**/*.h5
# Nur die große Parquet-Datei ausschließen (1373 MB):
models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet
# ALLE anderen Model-Dateien BEHALTEN (<125 MB)!

# Large GAIA parquet files (>50 MB) - nur die großen ausschließen!
data/raw/gaia/2025-10-17_gaia_ssz_real/gaia_dr3_core.parquet
data/raw/gaia/2025-10-17_gaia_ssz_real/2025-10-17_gaia_ssz_real__part00_20251017T110038.parquet
data/raw/gaia/2025-10-17_gaia_ssz_real/test_run__part00_20251017T091550.parquet
data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_clean.parquet
data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_phase_space.parquet
# Kleine Parquet-Dateien (<50 MB) BEHALTEN!
```

---

## 📊 Größen-Übersicht

### **Im Repository (✓):**
| Kategorie | Anzahl | Größe | Status |
|-----------|--------|-------|--------|
| Model Files (v1, nightly) | 11 | ~15 MB | ✓ Im Index |
| Data Files (v1, nightly) | 12 | ~30 MB | ✓ Neu hinzugefügt |
| **TOTAL** | **23** | **~45 MB** | ✓ Unter Limit |

### **Ausgeschlossen (❌):**
| Datei | Größe | Grund |
|-------|-------|-------|
| models/.../gaia_ssz_real/ssz_field.parquet | 1373 MB | >125 MB |
| data/interim/.../gaia_phase_space.parquet | 1169 MB | >125 MB |
| data/interim/.../gaia_clean.parquet | 757 MB | >125 MB |
| data/raw/.../part00_110038.parquet | 193 MB | >125 MB |
| data/raw/.../test_run_091550.parquet | 193 MB | >125 MB |
| **TOTAL** | **3685 MB** | **Zu groß für Git** |

---

## ✅ Vorteile dieser Strategie

### **1. Test-Fixtures verfügbar:**
- Alle Tests können mit v1/nightly-Daten laufen
- Keine FileNotFoundError mehr
- Pipeline funktioniert out-of-the-box

### **2. Repository-Größe optimiert:**
- Nur 45 MB zusätzlich (akzeptabel)
- Unter GitHub's 100 MB File-Limit
- Schnelle Clones

### **3. Skalierbar:**
- Neue kleine Dateien werden automatisch inkludiert
- Nur explizit gelistete große Dateien ausgeschlossen
- Klar dokumentiert

### **4. Entwickler-freundlich:**
- Keine Überraschungen (keine wildcards)
- Klare Regeln
- Leicht zu warten

---

## 🚀 Empfehlung für große Dateien

### **Option 1: Git LFS (empfohlen)**
```bash
git lfs install
git lfs track "models/cosmology/2025-10-17_gaia_ssz_real/*.parquet"
git lfs track "data/interim/gaia/2025-10-17_gaia_ssz_real/*.parquet"
```

### **Option 2: Separate Downloads**
```bash
# fetch_large_data.py
python scripts/fetch_large_models.py --dataset gaia_ssz_real
```

### **Option 3: Release Assets**
- Große Dateien als GitHub Release Assets hochladen
- Installer lädt sie bei Bedarf herunter
- Versioniert und stabil

---

## 📝 Wartung

### **Neue Dateien hinzufügen:**
1. Größe prüfen: `ls -lh datei.parquet`
2. Wenn < 125 MB: Einfach `git add` - automatisch inkludiert
3. Wenn > 125 MB: Zu `.gitignore` hinzufügen

### **Bestehende Dateien:**
- Regelmäßig prüfen: `git ls-files | xargs du -h | sort -h`
- Große Dateien identifizieren: `git ls-files | xargs du -m | awk '$1 > 100'`

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
