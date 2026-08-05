# Installation Scripts Overview

**Datum:** 2025-11-27  
**Status:** 3 Install-Scripts verfügbar für alle Plattformen

---

## 🎯 **Welches Script verwenden?**

### **Windows Benutzer:**

| Script | Empfehlung | Warum? |
|--------|------------|--------|
| **install.bat** | ✅ **Empfohlen für die meisten** | Einfach, keine Admin-Rechte nötig |
| **install.ps1** | ⭐ **Für PowerShell-Profis** | Mehr Features, bessere Fehlerbehandlung |

### **Linux/Mac Benutzer:**

| Script | Empfehlung | Warum? |
|--------|------------|--------|
| **install.sh** | ✅ **Einzige Option** | Standard Unix Shell Script |

---

## 📋 **Windows: install.bat vs install.ps1**

### **install.bat (Batch)**
```batch
# Starten:
.\install.bat

# Oder doppelklicken in Windows Explorer
```

**Vorteile:**
- ✅ Funktioniert überall (keine Execution Policy Probleme)
- ✅ Keine Admin-Rechte nötig
- ✅ Einfacher für Anfänger
- ✅ Direkter Doppelklick möglich

**Nachteile:**
- ⚠️ Einfachere Fehlerbehandlung
- ⚠️ Weniger farbige Ausgabe

### **install.ps1 (PowerShell)**
```powershell
# Starten:
.\install.ps1

# Falls Execution Policy Error:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**Vorteile:**
- ✅ Bessere Fehlerbehandlung
- ✅ Farbige Ausgabe (schöner)
- ✅ Mehr Informationen während Installation
- ✅ Moderne PowerShell Features

**Nachteile:**
- ⚠️ Braucht evtl. Execution Policy Änderung
- ⚠️ Nicht auf sehr alten Windows Versionen

---

## 🚀 **Installation (Alle Plattformen)**

### **Windows (Option 1: Batch - Empfohlen)**
```cmd
# Clone repository
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Install
.\install.bat

# Done! Virtual environment ist aktiv
```

### **Windows (Option 2: PowerShell)**
```powershell
# Clone repository
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Install
.\install.ps1

# Falls Policy Error:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
.\install.ps1
```

### **Linux/Mac**
```bash
# Clone repository
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results

# Install
chmod +x install.sh
./install.sh

# Done! Virtual environment ist aktiv
```

---

## ⚠️ **KRITISCH: Pytest Cache Warnung**

**ALLE drei Scripts zeigen diese Warnung am Ende:**

```
═══════════════════════════════════════════════════════════════
⚠️  IMPORTANT: PYTEST CACHE WARNING
═══════════════════════════════════════════════════════════════

ALWAYS run ./CLEAR_CACHE.bat (or .sh) BEFORE running tests!

Why? Pytest caches old file versions and can cause false test failures.
The cache must be cleared to ensure tests use the current code.

Correct workflow:
  1. ./CLEAR_CACHE.bat        # Clear cache first
  2. python run_full_suite.py   # Then run tests

See PYTEST_CACHE_PROBLEM_SOLUTION.md for details.
```

**Warum ist das wichtig?**
- Pytest cached alte Test-Files
- Auch wenn du Code änderst, werden alte Versionen verwendet
- **Result:** Tests schlagen fehl obwohl dein Code korrekt ist!

**Lösung:**
```bash
# IMMER vor Tests:
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux/Mac
```

---

## 📝 **Was die Scripts machen**

### **Alle Scripts (gleiche Schritte):**

1. **[1/5] Python Check**
   - Prüft ob Python 3.10+ installiert
   - Zeigt Python Version
   - Stoppt wenn Python fehlt

2. **[2/5] Virtual Environment**
   - Erstellt `.venv/` Ordner
   - Isoliert von System-Python
   - Vermeidet Konflikte

3. **[3/5] Pip Upgrade**
   - Aktiviert venv
   - Updated pip auf neueste Version

4. **[4/5] Dependencies**
   - Installiert aus requirements.txt
   - numpy, scipy, matplotlib, pandas, etc.
   - ~2-5 Minuten

5. **[5/5] Validation**
   - Läuft run_ssz_validation.py
   - Quick-Check ob Installation funktioniert
   - ~2 Minuten

---

## 🔧 **Troubleshooting**

### **Problem: "Python not found"**
```bash
# Lösung: Python installieren
# Windows: https://www.python.org/downloads/
# Linux: sudo apt install python3.10
# Mac: brew install python@3.10
```

### **Problem: "Execution Policy" (PowerShell)**
```powershell
# Lösung:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Dann nochmal:
.\install.ps1
```

### **Problem: "Permission denied" (Linux/Mac)**
```bash
# Lösung:
chmod +x install.sh
./install.sh
```

### **Problem: Tests schlagen fehl**
```bash
# Lösung: Cache löschen!
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux/Mac

# Dann nochmal:
python run_full_suite.py
```

---

## 📊 **Vergleich der Scripts**

| Feature | install.bat | install.ps1 | install.sh |
|---------|-------------|-------------|------------|
| **Plattform** | Windows | Windows | Linux/Mac |
| **Admin-Rechte** | ❌ Nein | ❌ Nein | ❌ Nein |
| **Farbige Ausgabe** | ⚠️ Basic | ✅ Gut | ✅ Gut |
| **Fehlerbehandlung** | ⚠️ Basic | ✅ Gut | ✅ Gut |
| **Doppelklick** | ✅ Ja | ⚠️ Policy | ❌ Nein |
| **Cache Warnung** | ✅ Ja | ✅ Ja | ✅ Ja |
| **Virtual Env** | ✅ Ja | ✅ Ja | ✅ Ja |

---

## ✅ **Empfehlung**

### **Für Windows:**
```batch
# Anfänger oder unsicher? → install.bat
.\install.bat

# PowerShell-Profi? → install.ps1
.\install.ps1
```

### **Für Linux/Mac:**
```bash
# Einzige Option:
./install.sh
```

### **Nach Installation:**
```bash
# IMMER vor Tests Cache löschen!
.\CLEAR_CACHE.bat  # Windows
./CLEAR_CACHE.sh   # Linux/Mac

# Dann Tests laufen:
python run_full_suite.py
```

---

## 🎯 **Quick Start Commands**

### **Windows (Batch):**
```cmd
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
.\install.bat
.\CLEAR_CACHE.bat
python run_full_suite.py
```

### **Windows (PowerShell):**
```powershell
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
.\install.ps1
.\CLEAR_CACHE.bat
python run_full_suite.py
```

### **Linux/Mac:**
```bash
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git
cd Segmented-Spacetime-Mass-Projection-Unified-Results
chmod +x install.sh CLEAR_CACHE.sh
./install.sh
./CLEAR_CACHE.sh
python3 run_full_suite.py
```

---

## 📚 **Weitere Dokumentation**

- **INSTALL_README.md** - Detaillierte Installation
- **TEST_SUITE_README.md** - Testing Guide
- **PYTEST_CACHE_PROBLEM_SOLUTION.md** - Cache Problem erklärt
- **README.md** - Project Overview

---

**© 2025 Carmen Wrede & Lino Casu – All rights reserved.**

**Lizenz:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4
