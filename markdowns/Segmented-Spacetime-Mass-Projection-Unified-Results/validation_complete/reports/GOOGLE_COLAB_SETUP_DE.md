# Google Colab Setup - Segmented Spacetime Repository

Komplette Anleitung zum Klonen und Nutzen des Repositories in Google Colab.

---

## 🚀 Quick Start - Copy & Paste in Colab

### **Option 1: Nur kleine Dateien (Tests sofort lauffähig)**

```python
# Repository klonen (NUR kleine Dateien, ~36 MB)
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Abhängigkeiten installieren
!pip install -q -r requirements.txt

# Tests ausführen (mit v1/nightly Datasets)
!python run_full_suite.py
```

### **Option 2: Mit großen Dateien (vollständige Datasets)**

```python
# Git LFS installieren
!apt-get install -y git-lfs
!git lfs install

# Repository klonen
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Große Dateien herunterladen (~3.6 GB!)
!git lfs pull

# Abhängigkeiten installieren
!pip install -q -r requirements.txt

# Alle Tests (inkl. real-data)
!python run_full_suite.py
```

---

## 📋 Schritt-für-Schritt Anleitung

### **1. Neues Colab Notebook erstellen**

Gehe zu [Google Colab](https://colab.research.google.com/) und erstelle ein neues Notebook.

### **2. Repository-Variablen definieren**

```python
# Repository-Konfiguration
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"

print(f"📦 Repository: {REPO_NAME}")
print(f"🔗 URL: {REPO_URL}")
```

### **3. Workspace vorbereiten**

```python
import os
from pathlib import Path

# Prüfe ob Repository bereits existiert
if Path(REPO_NAME).exists():
    print(f"⚠️  Repository existiert bereits: {REPO_NAME}")
    print(f"🔄 Pullen der neuesten Änderungen...")
    !cd {REPO_NAME} && git pull
else:
    print(f"📥 Klone Repository: {REPO_URL}")
```

### **4. Repository klonen**

#### **Option A: Shallow Clone (schnell, ohne History)**

```python
# Schneller Clone ohne History
!git clone --depth 1 {REPO_URL} {REPO_NAME}
print(f"✅ Repository geklont!")
```

#### **Option B: Full Clone (mit kompletter History)**

```python
# Kompletter Clone mit History
!git clone {REPO_URL} {REPO_NAME}
print(f"✅ Repository geklont!")
```

### **5. In Repository wechseln**

```python
# Working Directory ändern
os.chdir(REPO_NAME)
print(f"📂 Working Directory: {os.getcwd()}")
```

### **6. Git LFS Setup (optional, für große Dateien)**

```python
# Git LFS installieren (wenn große Dateien benötigt werden)
!apt-get install -y git-lfs
!git lfs install

# Große Dateien herunterladen (~3.6 GB)
!git lfs pull

print(f"✅ Git LFS Setup abgeschlossen!")
print(f"⚠️  Download-Größe: ~3.6 GB")
```

### **7. Abhängigkeiten installieren**

```python
# Python-Pakete installieren
!pip install -q -r requirements.txt

# Zusätzliche Pakete (falls benötigt)
!pip install -q numpy scipy pandas matplotlib astropy pyarrow pytest

print(f"✅ Abhängigkeiten installiert!")
```

### **8. Verfügbarkeit prüfen**

```python
# Prüfe welche Dateien verfügbar sind
import subprocess

def check_file_size(filepath):
    """Prüfe Dateigröße in MB"""
    try:
        size = Path(filepath).stat().st_size / (1024 * 1024)
        return size
    except:
        return None

# Kleine Dateien (sollten direkt verfügbar sein)
small_files = [
    "models/cosmology/2025-10-17_gaia_ssz_v1/ssz_field.parquet",
    "models/cosmology/2025-10-17_gaia_ssz_nightly/ssz_field.parquet",
]

print("\n📄 KLEINE DATEIEN (sofort verfügbar):")
for f in small_files:
    size = check_file_size(f)
    if size:
        print(f"  ✅ {f} - {size:.2f} MB")
    else:
        print(f"  ❌ {f} - FEHLT!")

# Große Dateien (nur nach git lfs pull)
large_files = [
    "models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet",
]

print("\n📦 GROSSE DATEIEN (nach 'git lfs pull'):")
for f in large_files:
    size = check_file_size(f)
    if size and size > 100:
        print(f"  ✅ {f} - {size:.2f} MB (Vollständig)")
    elif size and size < 1:
        print(f"  ⚡ {f} - {size*1024:.2f} KB (LFS-Pointer)")
    else:
        print(f"  ❌ {f} - FEHLT!")
```

### **9. Tests ausführen**

```python
# Alle Tests (mit verfügbaren Dateien)
!python run_full_suite.py

# Oder einzelne Tests
!pytest tests/ -v -s

# Nur Tests mit kleinen Datasets
!pytest tests/ -v -s -k "not real"
```

---

## 🎯 Komplettes Setup-Script

Kopiere diesen gesamten Code-Block in eine Colab-Zelle:

```python
import os
from pathlib import Path

# ============================================================================
# KONFIGURATION
# ============================================================================
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"
INSTALL_LFS = False  # True für große Dateien (~3.6 GB), False für nur kleine

print("="*80)
print("Segmented Spacetime - GOOGLE COLAB SETUP")
print("="*80)
print(f"Repository: {REPO_NAME}")
print(f"Git LFS: {'Ja (große Dateien)' if INSTALL_LFS else 'Nein (nur kleine Dateien)'}")
print("="*80)

# ============================================================================
# 1. REPOSITORY KLONEN
# ============================================================================
if Path(REPO_NAME).exists():
    print(f"\n⚠️  Repository existiert bereits!")
    print(f"🔄 Pulling updates...")
    os.chdir(REPO_NAME)
    !git pull
else:
    print(f"\n📥 Klone Repository...")
    !git clone --depth 1 {REPO_URL} {REPO_NAME}
    os.chdir(REPO_NAME)
    print(f"✅ Repository geklont!")

# ============================================================================
# 2. GIT LFS SETUP (optional)
# ============================================================================
if INSTALL_LFS:
    print(f"\n📦 Installiere Git LFS...")
    !apt-get install -y git-lfs > /dev/null 2>&1
    !git lfs install
    print(f"⬇️  Lade große Dateien herunter (~3.6 GB)...")
    !git lfs pull
    print(f"✅ Git LFS Setup abgeschlossen!")
else:
    print(f"\n⚡ Skip Git LFS - Nur kleine Dateien verfügbar")

# ============================================================================
# 3. ABHÄNGIGKEITEN INSTALLIEREN
# ============================================================================
print(f"\n📦 Installiere Python-Pakete...")
!pip install -q -r requirements.txt
print(f"✅ Abhängigkeiten installiert!")

# ============================================================================
# 4. DATEIEN PRÜFEN
# ============================================================================
print(f"\n📄 Verfügbare Dateien:")

small_test = "models/cosmology/2025-10-17_gaia_ssz_v1/ssz_field.parquet"
large_test = "models/cosmology/2025-10-17_gaia_ssz_real/ssz_field.parquet"

def check_size(f):
    try:
        return Path(f).stat().st_size / (1024 * 1024)
    except:
        return None

small_size = check_size(small_test)
large_size = check_size(large_test)

if small_size:
    print(f"  ✅ Kleine Dateien: {small_size:.2f} MB (v1/nightly)")
else:
    print(f"  ❌ Kleine Dateien: FEHLEN!")

if large_size and large_size > 100:
    print(f"  ✅ Große Dateien: {large_size:.2f} MB (real-data)")
elif large_size and large_size < 1:
    print(f"  ⚡ Große Dateien: {large_size*1024:.2f} KB (LFS-Pointer)")
else:
    print(f"  ❌ Große Dateien: FEHLEN!")

# ============================================================================
# 5. BEREIT!
# ============================================================================
print("\n" + "="*80)
print("✅ SETUP ABGESCHLOSSEN!")
print("="*80)
print(f"Working Directory: {os.getcwd()}")
print(f"\n🚀 Nächste Schritte:")
print(f"   • Tests ausführen: !python run_full_suite.py")
print(f"   • Pytest: !pytest tests/ -v -s")
print(f"   • Nur kleine Datasets: !pytest tests/ -v -s -k 'not real'")
print("="*80)
```

---

## 🔧 Troubleshooting

### **Problem: "NameError: name 'REPO_NAME' is not defined"**

**Lösung:** Definiere die Variablen VOR dem Klonen:

```python
# ZUERST diese Zeilen ausführen:
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"

# DANN klonen:
!git clone --depth 1 {REPO_URL} {REPO_NAME}
```

### **Problem: "fatal: destination path '...' already exists"**

**Lösung:** Repository existiert bereits, entweder löschen oder pullen:

```python
# Option 1: Löschen und neu klonen
!rm -rf Segmented-Spacetime-Mass-Projection-Unified-Results
!git clone --depth 1 {REPO_URL}

# Option 2: Updates pullen
%cd Segmented-Spacetime-Mass-Projection-Unified-Results
!git pull
```

### **Problem: "FileNotFoundError" bei Tests**

**Ursache:** Große Dateien wurden nicht heruntergeladen

**Lösung:**

```python
# Entweder Git LFS installieren und pullen:
!apt-get install -y git-lfs
!git lfs install
!git lfs pull

# Oder nur Tests mit kleinen Dateien ausführen:
!pytest tests/ -v -s -k "not real"
```

### **Problem: "Out of Memory" bei großen Dateien**

**Ursache:** Colab hat begrenzte RAM (~12 GB)

**Lösung:**

```python
# Arbeite nur mit kleinen Dateien (v1/nightly)
# Große real-data Dateien NICHT mit git lfs pull herunterladen
# Nutze stattdessen kleinere Testdatensätze
```

---

## 💡 Best Practices für Colab

### **1. Modulares Setup**

Teile dein Notebook in Zellen auf:

```python
# Zelle 1: Variablen definieren
REPO_URL = "https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results"
REPO_NAME = "Segmented-Spacetime-Mass-Projection-Unified-Results"
```

```python
# Zelle 2: Klonen
!git clone --depth 1 {REPO_URL} {REPO_NAME}
%cd {REPO_NAME}
```

```python
# Zelle 3: Abhängigkeiten
!pip install -q -r requirements.txt
```

```python
# Zelle 4: Tests
!python run_full_suite.py
```

### **2. Reconnect-Safety**

Colab kann Verbindung verlieren. Speichere den Fortschritt:

```python
# Zu Beginn prüfen ob bereits geklont
from pathlib import Path

if not Path("Segmented-Spacetime-Mass-Projection-Unified-Results").exists():
    !git clone --depth 1 {REPO_URL}
else:
    print("✅ Repository bereits vorhanden")

%cd Segmented-Spacetime-Mass-Projection-Unified-Results
```

### **3. Drive Integration (optional)**

Große Dateien in Google Drive speichern:

```python
from google.colab import drive
drive.mount('/content/drive')

# Clone nach Drive (persistiert!)
!git clone {REPO_URL} /content/drive/MyDrive/SSZ-repo
%cd /content/drive/MyDrive/SSZ-repo
```

---

## 📊 Ressourcen-Übersicht

| Setup | Download | RAM | Zeit | Tests |
|-------|----------|-----|------|-------|
| Nur kleine Dateien | ~36 MB | ~2 GB | ~2 min | v1, nightly ✅ |
| Mit Git LFS | ~3.6 GB | ~8 GB | ~15 min | Alle ✅ |
| Drive-Integration | ~3.6 GB | ~4 GB | ~20 min | Alle ✅ (persistiert) |

---

## 🎓 Beispiel-Notebooks

### **Minimal Setup:**

```python
# 1. Clone (nur kleine Dateien)
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# 2. Install
!pip install -q -r requirements.txt

# 3. Test
!pytest tests/ -v -s -k "not real"
```

### **Full Setup:**

```python
# 1. Git LFS
!apt-get install -y git-lfs
!git lfs install

# 2. Clone
!git clone --depth 1 https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
%cd Segmented-Spacetime-Mass-Projection-Unified-Results

# 3. LFS Pull
!git lfs pull

# 4. Install
!pip install -q -r requirements.txt

# 5. Full Test
!python run_full_suite.py
```

---

## ✅ Zusammenfassung

**Für schnelle Tests (empfohlen):**
- Clone ohne Git LFS
- Nur kleine Dateien (~36 MB)
- Tests mit v1/nightly Datasets
- Funktioniert sofort in Colab

**Für vollständige Analyse:**
- Git LFS installieren
- Alle Dateien laden (~3.6 GB)
- Tests mit real-data
- Benötigt mehr Zeit & RAM

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
