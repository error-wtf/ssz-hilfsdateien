# Git Synchronisation - Main Branch

Anleitung zum Synchronisieren des Projektordners mit dem main branch des GitHub-Repositories.

---

## 🎯 Ziel

Alle Änderungen (außer große Dateien wie Planck-Daten) zum main branch pushen.

---

## 🚀 Schnellstart

### **Automatisch (empfohlen):**
```powershell
.\sync_to_main.ps1
```

### **Manuell:**
```bash
git add -A
git commit -m "Update: Beschreibung der Änderungen"
git push origin main
```

---

## 📋 Was wird synchronisiert?

### **✅ Wird ins Repository committed:**

**Code:**
- Alle `.py` Python-Dateien
- Alle `.ps1` PowerShell-Skripte
- Alle `.sh` Bash-Skripte
- Test-Dateien (`test_*.py`)

**Dokumentation:**
- Alle `.md` Markdown-Dateien
- `papers/*.pdf` (Paper-PDFs)
- `README.md`, `LICENSE`

**Konfiguration:**
- `requirements.txt`
- `setup.py`, `pyproject.toml`
- `.gitignore`, `.gitattributes`

**Kleine Daten (~52 MB):**
- `data/real_data_full.csv`
- `data/gaia/gaia_sample_small.csv`
- `data/gaia/gaia_cone_g79.csv`
- `data/gaia/gaia_cone_cygx.csv`

**Reports:**
- `reports/RUN_SUMMARY.md`
- `reports/full-output.md`
- `reports/summary-output.md`

### **❌ Wird NICHT committed (via .gitignore):**

**Große Dateien:**
- `data/planck/*.txt` (~2 GB) - wird auto-fetched
- `data/gaia/*_full.csv` (große GAIA Datasets)

**Build-Artefakte:**
- `__pycache__/` (Python Cache)
- `.pytest_cache/` (Test Cache)
- `*.pyc`, `*.pyo` (Compiled Python)
- `build/`, `dist/` (Build-Ordner)

**IDE-Dateien:**
- `.vscode/`
- `.idea/`
- `*.swp`, `*.swo`

**Temporäre Dateien:**
- `*.log` (Log-Dateien)
- `*.tmp`, `*.temp`
- `*.bak`, `*.old`

**OS-Dateien:**
- `Thumbs.db` (Windows)
- `.DS_Store` (macOS)

---

## 🔍 Vor dem Sync prüfen

### **1. Git Status:**
```bash
git status
```

### **2. Was wird committed?**
```bash
git add -A
git status
```

### **3. Diff anzeigen:**
```bash
git diff --cached
```

---

## 📝 Commit Messages

### **Standard-Format:**
```
Update: [Kurzbeschreibung] (Datum)
```

### **Beispiele:**
```
Update: Pipeline fixes, Add-ons, SI units (2025-10-18)
Fix: UTF-8 encoding, subprocess stdout
Feature: Segment-Redshift Add-on
Docs: Extended metrics documentation
```

### **Detailliert:**
```
Update: Pipeline improvements

- Fixed subprocess stdout visibility (Windows + Linux)
- Added Segment-Redshift Add-on
- Corrected SI units in energy_conditions test
- Extended metrics for G79 and Cygnus X
- Added plot collection script
```

---

## 🛠️ Setup (Einmalig)

### **1. Git Repository initialisieren (falls noch nicht geschehen):**
```bash
git init
```

### **2. Remote hinzufügen:**
```bash
git remote add origin https://github.com/IHR_USERNAME/Segmented-Spacetime-Mass-Projection-Unified-Results.git
```

### **3. Branch erstellen:**
```bash
git checkout -b main
```

### **4. Erstes Commit:**
```bash
git add -A
git commit -m "Initial commit: SSZ Pipeline"
git push -u origin main
```

---

## 🔄 Workflow

### **1. Änderungen gemacht:**
```bash
# Dateien bearbeitet, Tests durchgeführt, etc.
```

### **2. Status prüfen:**
```bash
git status
```

### **3. Sync-Skript ausführen:**
```powershell
.\sync_to_main.ps1
```

**Das Skript macht:**
- Prüft Git-Status
- Staged alle Änderungen (respektiert .gitignore)
- Erstellt Commit mit Timestamp
- Pusht zu main branch

### **4. Fertig!**
```
✓ Repository auf GitHub aktualisiert
```

---

## 🚨 Troubleshooting

### **Problem: "No such remote 'origin'"**
```bash
git remote add origin https://github.com/USERNAME/REPO.git
```

### **Problem: "failed to push some refs"**
```bash
# Erst pullen, dann pushen:
git pull --rebase origin main
git push origin main
```

### **Problem: "Large files detected"**
```bash
# .gitignore prüfen:
cat .gitignore | grep planck

# Falls Datei schon staged:
git rm --cached data/planck/FILE.txt
git commit --amend
```

### **Problem: "Authentication failed"**
```bash
# GitHub Personal Access Token verwenden
# Settings > Developer Settings > Personal Access Tokens
```

---

## 📊 Repository-Größe

**Aktuell (ohne Planck):**
```
Quellcode:           ~5 MB
Kleine Daten:       ~52 MB
Dokumentation:       ~3 MB
Papers (PDF):        ~8 MB
Total:              ~68 MB
```

**Mit Planck (lokal):**
```
Total:              ~2.1 GB
```

**GitHub hat ein 2 GB Repository-Limit** → Planck wird auto-fetched!

---

## 🔐 Credentials

### **HTTPS (empfohlen):**
```bash
git remote set-url origin https://github.com/USERNAME/REPO.git
# Verwendet Personal Access Token
```

### **SSH:**
```bash
git remote set-url origin git@github.com:USERNAME/REPO.git
# Braucht SSH-Key Setup
```

---

## 📚 Weitere Git-Befehle

### **Log anzeigen:**
```bash
git log --oneline -10
git log --graph --oneline --all
```

### **Branch wechseln:**
```bash
git checkout main
git checkout -b feature-branch
```

### **Änderungen verwerfen:**
```bash
git checkout -- FILE.py          # Einzelne Datei
git reset --hard HEAD            # Alle Änderungen
```

### **Remote-Infos:**
```bash
git remote -v
git branch -a
```

---

## 🎯 Best Practices

1. **Regelmäßig committen:** Kleine, häufige Commits > große seltene
2. **Aussagekräftige Messages:** Was wurde geändert und warum
3. **Vor Push testen:** Pipeline sollte lokal funktionieren
4. **Branch-Strategie:** main = stabil, feature-branches für neue Features
5. **.gitignore pflegen:** Große/temporäre Dateien ausschließen

---

## 📞 Support

**Bei Problemen:**
1. Git-Status prüfen: `git status`
2. .gitignore prüfen: `cat .gitignore`
3. Remote prüfen: `git remote -v`
4. Log prüfen: `git log -1`

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
