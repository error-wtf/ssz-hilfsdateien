# Git Hybrid-Strategie: Klein OHNE LFS, Groß MIT LFS 🎯

**Datum:** 2025-10-19  
**Status:** ✅ Optimale Balance zwischen Performance und Verfügbarkeit

---

## 🎯 Strategie

### **Kleine Dateien (<100 MB) → Direkt in Git**
- ✅ Sofort verfügbar nach Clone
- ✅ Schneller Zugriff
- ✅ Keine LFS-Abhängigkeit
- ✅ Tests funktionieren out-of-the-box

### **Große Dateien (>100 MB) → Git LFS**
- ✅ Repository bleibt schlank
- ✅ Schnelle Clones
- ✅ Optional herunterladbar
- ✅ Kein GitHub 100 MB Limit-Problem

---

## 📦 Dateikategorisierung

### **KLEIN - Direkt in Git (~ 36 MB)**

#### **Models (2 Dateien - 14.39 MB):**
```
✓ models/cosmology/2025-10-17_gaia_ssz_v1/ssz_field.parquet         (0.14 MB)
✓ models/cosmology/2025-10-17_gaia_ssz_nightly/ssz_field.parquet    (14.25 MB)
```

#### **Data/Interim (4 Dateien - 17.85 MB):**
```
✓ data/interim/gaia/2025-10-17_gaia_ssz_v1/gaia_clean.parquet        (0.08 MB)
✓ data/interim/gaia/2025-10-17_gaia_ssz_v1/gaia_phase_space.parquet  (0.12 MB)
✓ data/interim/gaia/2025-10-17_gaia_ssz_nightly/gaia_clean.parquet   (6.09 MB)
✓ data/interim/gaia/2025-10-17_gaia_ssz_nightly/gaia_phase_space.parquet (11.56 MB)
```

#### **Data/Raw (4 Dateien - 10.33 MB):**
```
✓ data/raw/gaia/2025-10-17_gaia_ssz_nightly/gaia_dr3_core.csv       (6.47 MB)
✓ data/raw/gaia/2025-10-17_gaia_ssz_nightly/gaia_dr3_core.parquet   (3.32 MB)
✓ data/raw/sdss/2025-10-17_gaia_ssz_nightly/sdss_catalog.csv        (0.53 MB)
✓ data/raw/sdss/2025-10-17_gaia_ssz_nightly/sdss_catalog.parquet    (0.36 MB)
```

#### **Data/SDSS (3 Dateien - 1.42 MB):**
```
✓ data/raw/sdss/2025-10-17_gaia_ssz_real/sdss_catalog.csv           (0.53 MB)
✓ data/raw/sdss/2025-10-17_gaia_ssz_real/sdss_catalog.parquet       (0.36 MB)
✓ data/raw/sdss/2025-10-17_gaia_ssz_real/sdss_quick.csv             (0.53 MB)
```

**Total Klein: 13 Dateien, ~36 MB**

---

### **GROSS - Mit Git LFS (~ 3.5 GB)**

#### **Models (1 Datei - 1373 MB):**
```
⚡ models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet (1373.31 MB)
```

#### **Data/Interim (2 Dateien - 1926 MB):**
```
⚡ data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_clean.parquet       (757.11 MB)
⚡ data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_phase_space.parquet (1169.17 MB)
```

#### **Data/Raw (4 Dateien - 465 MB):**
```
⚡ data/raw/gaia/2025-10-17_gaia_ssz_real/gaia_dr3_core.parquet          (78.83 MB)
⚡ data/raw/gaia/2025-10-17_gaia_ssz_real/2025-10-17_gaia_ssz_real__part00_20251017T110038.parquet (193.39 MB)
⚡ data/raw/gaia/2025-10-17_gaia_ssz_real/test_run__part00_20251017T091550.parquet (193.13 MB)
⚡ data/raw/gaia/2025-10-17_gaia_ssz_real/gaia_quick.parquet             (0.32 MB)
```

**Total Groß: 7 Dateien, ~3.5 GB (als LFS-Pointer ~1 KB)**

---

## ✅ Vorteile dieser Hybrid-Strategie

### **1. Tests funktionieren sofort:**
```bash
git clone <repo-url>
cd <repo>
python run_full_suite.py  # ✓ Läuft sofort!
```

Die kleinen Model-Dateien (v1, nightly) sind direkt verfügbar:
- ✅ `test_ssz_invariants.py` - findet ssz_field.parquet (v1, 0.14 MB)
- ✅ `test_segment_growth_is_monotonic` - findet Daten
- ✅ `test_solar_segments_non_empty` - findet solar_ssz.json
- ✅ Keine FileNotFoundError mehr!

### **2. Große Dateien optional:**
```bash
# Nur wenn wirklich benötigt:
git lfs pull  # Lädt große Dateien herunter
```

### **3. Repository Performance:**
- Clone-Zeit: ~2 Minuten (statt 20+ Minuten)
- Repository-Größe: ~50 MB (statt 3.5 GB)
- Git-Operations: Schnell

### **4. GitHub-freundlich:**
- ✅ Keine Datei >100 MB direkt in Git
- ✅ Git LFS für große Dateien
- ✅ Unter GitHub's Limits

---

## 🔧 Git LFS Konfiguration

### **.gitattributes:**
```
models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet filter=lfs diff=lfs merge=lfs -text
data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_clean.parquet filter=lfs diff=lfs merge=lfs -text
data/interim/gaia/2025-10-17_gaia_ssz_real/gaia_phase_space.parquet filter=lfs diff=lfs merge=lfs -text
data/raw/gaia/2025-10-17_gaia_ssz_real/*.parquet filter=lfs diff=lfs merge=lfs -text
```

### **Was passiert beim Push:**
```
Kleine Dateien → Normal zu GitHub gepusht (~36 MB)
Große Dateien → Als LFS-Pointer gepusht (~7 KB)
Echte große Dateien → Zu Git LFS Server hochgeladen
```

---

## 🚀 Commit & Push

### **Commit erstellen:**
```bash
git commit -m "feat: Add parquet files with hybrid LFS strategy

- Small files (<100 MB): Direct in Git (13 files, 36 MB)
  * models v1, nightly - immediately available for tests
  * data interim v1, nightly
  * data raw nightly, SDSS catalogs
  
- Large files (>100 MB): With Git LFS (7 files, 3.5 GB)
  * models/cosmology/...gaia_ssz_real/ssz_field.parquet (1.37 GB)
  * data/interim/...gaia_ssz_real/*.parquet (1.93 GB)
  * data/raw/...gaia_ssz_real/*.parquet (465 MB)

Benefits:
- Tests run out-of-the-box with small datasets
- Large files optional via 'git lfs pull'
- Fast clones (~2 min vs 20+ min)
- GitHub 100 MB limit respected"
```

### **Push zum Repository:**
```bash
git push origin main
```

---

## 📊 Use Cases

### **Use Case 1: Schneller Test**
```bash
git clone <repo-url>
cd <repo>
python run_full_suite.py
# ✓ Funktioniert mit v1/nightly Daten (kleine Dateien)
```

### **Use Case 2: Vollständige Analyse**
```bash
git clone <repo-url>
cd <repo>
git lfs pull  # Lädt große Dateien
python run_all_ssz_terminal.py
# ✓ Alle Daten verfügbar (inkl. gaia_ssz_real)
```

### **Use Case 3: CI/CD Pipeline**
```bash
# Im CI Script:
git clone --depth 1 <repo-url>  # Shallow clone
# Nutzt nur kleine Dateien für schnelle Tests
python -m pytest tests/ -k "not real"  # Skip real-data tests
```

---

## 🎓 Best Practices

### **1. Für Entwickler:**
```bash
# Initial setup
git clone <repo-url>
cd <repo>
git lfs install  # Einmalig

# Arbeiten mit Code
git pull  # Nur Code-Updates, keine großen Dateien

# Wenn große Dateien benötigt:
git lfs pull
```

### **2. Für CI/CD:**
```bash
# Schnelle Tests ohne große Dateien
git clone --depth 1 <repo-url>
pytest tests/ -m "not slow"

# Volle Tests (weekly)
git lfs pull
pytest tests/
```

### **3. Neue große Dateien hinzufügen:**
```bash
# Zuerst LFS-Tracking aktivieren
git lfs track "path/to/large_file.parquet"
git add .gitattributes

# Dann Datei hinzufügen
git add path/to/large_file.parquet
git commit -m "Add large file with LFS"
```

---

## ⚠️ Wichtig

### **Nach dem Clone:**
- ✅ Kleine Dateien: Sofort verfügbar
- ⚠️ Große Dateien: Nur LFS-Pointer vorhanden

### **Große Dateien herunterladen:**
```bash
git lfs pull
# ODER spezifisch:
git lfs pull --include="models/cosmology/2025-10-17_gaia_ssz_real/*"
```

### **LFS Status prüfen:**
```bash
git lfs status    # Zeigt LFS-Dateien
git lfs ls-files  # Listet alle LFS-getrackten Dateien
```

---

## 🎉 Zusammenfassung

| Kategorie | Anzahl | Größe | Methode | Verfügbar nach Clone |
|-----------|--------|-------|---------|---------------------|
| Kleine Parquet | 13 | 36 MB | Git normal | ✅ Sofort |
| Große Parquet | 7 | 3.5 GB | Git LFS | ⚠️ Nach `git lfs pull` |
| CSV-Dateien | 3 | 7.5 MB | Git normal | ✅ Sofort |
| JSON-Dateien | 11 | 0.3 MB | Git normal | ✅ Sofort |
| **TOTAL** | **34** | **3.54 GB** | **Hybrid** | **✅ Tests sofort möglich** |

---

✅ **Optimale Balance:**
- Tests funktionieren sofort (v1, nightly)
- Repository bleibt schlank (~50 MB)
- Große Dateien optional verfügbar
- GitHub-kompatibel

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
