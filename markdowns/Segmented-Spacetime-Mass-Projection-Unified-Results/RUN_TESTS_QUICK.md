# SSZ Suite - Quick Test Guide

**Für Carmen - Sofort loslegen!**

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## 🚀 **Option 1: Nur Paper Export Tools testen (30s)**

```bash
python demo_paper_exports.py
```

**Oder mit PowerShell-Runner:**
```powershell
.\test_paper_exports.ps1
```

**Erwartete Ausgabe:**
```
✅ ALLE DEMOS ERFOLGREICH!

Erstellt:
  • 11 figure files
  • 1 FIGURE_INDEX.md
  • 2 Manifeste
```

---

## 🧪 **Option 2: Vollständige Test-Suite (2-3 Min)**

```bash
python run_full_suite.py
```

**Was wird getestet:**
1. ✅ Root-Level SSZ Tests (6 Tests)
2. ✅ SegWave Tests (16 Tests)
3. ✅ Scripts Tests (15 Tests)
4. ✅ Cosmos Tests (1 Test)
5. ✅ SSZ Analysis (vollständig)
6. ✅ G79 & Cygnus X Beispiele
7. ✅ **Paper Export Tools** ← **NEU!**
8. ✅ Summary Generation
9. ✅ MD Echo
10. ✅ Output Logs

**Erwartete Ausgabe:**
```
====================================================================================================
WORKFLOW COMPLETE
====================================================================================================

 Generated Files:
   • Summary Report:  reports\RUN_SUMMARY.md
   • Compact Output:  reports\summary-output.md
   • Full Log:        reports\full-output.md

✅ ALL TESTS PASSED
```

---

## ⚡ **Option 3: Schneller Test-Modus (1 Min)**

```bash
python run_full_suite.py --quick
```

**Überspringt:**
- Scripts Tests
- Cosmos Tests
- SSZ Analysis
- Paper Export Tools

**Testet nur:**
- Root-Level Tests
- SegWave Core Tests

---

## 🔍 **Problem: KeyboardInterrupt beim Volltest**

### **Symptom:**
```
[RUNNING] SegWave CLI & Dataset Tests
  Command: python -m pytest tests/test_segwave_cli.py -s -v --tb=short
Traceback (most recent call last):
  ...
KeyboardInterrupt
```

### **Ursache:**
Test wurde manuell mit `Ctrl+C` abgebrochen.

### **Lösung:**

**1. Tests laufen lassen (nicht abbrechen!)**

Die Tests sind **absichtlich langsam** (2-3 Minuten), weil sie:
- Komplette SSZ-Physik testen
- Planck CMB-Daten verwenden (2 GB)
- Alle Beispiele durchrechnen

**Warte einfach 2-3 Minuten!**

---

**2. Oder: Schneller Test-Modus verwenden**

```bash
python run_full_suite.py --quick
```

---

**3. Oder: Nur einzelne Phasen testen**

```bash
# Nur Root-Tests (1s)
python test_ppn_exact.py
python test_vfall_duality.py

# Nur SegWave Core (10s)
pytest tests/test_segwave_core.py -s -v

# Nur Paper Export Tools (30s)
python demo_paper_exports.py
```

---

## 📊 **Ergebnisse prüfen**

### **Nach dem Volltest:**

```bash
# Summary anzeigen
type reports\RUN_SUMMARY.md

# Oder: Vollständiges Log
type reports\full-output.md

# Oder: Nur Paper Export Tools
grep -A 50 "PHASE 7: PAPER EXPORT TOOLS" reports\full-output.md
```

### **Paper Export Tools Outputs:**

```bash
# Figures anzeigen
explorer reports\figures\demo
explorer reports\figures\DemoObject

# Index anzeigen
type reports\figures\FIGURE_INDEX.md

# Manifest prüfen
type reports\DEMO_MANIFEST.json
```

---

## ✅ **Erfolgs-Kriterien**

Nach dem Test solltest du sehen:

### **1. Console Output**
```
✅ ALL TESTS PASSED
```

### **2. Generated Files**
```
reports/
├── RUN_SUMMARY.md          ← Test-Übersicht
├── summary-output.md       ← Kompakte Summary
├── full-output.md          ← Vollständiges Log
└── figures/
    ├── demo/               ← Demo-Figures (5 files)
    ├── DemoObject/         ← Orchestrator-Figures (6 files)
    └── FIGURE_INDEX.md     ← Figure-Liste
```

### **3. Manifeste**
```
reports/
├── DEMO_MANIFEST.json              ← Demo-Manifest
└── PAPER_EXPORTS_MANIFEST.json     ← Produktions-Manifest
```

---

## 🐛 **Fehlerbehebung**

### **ImportError: No module named 'matplotlib'**

```bash
pip install matplotlib numpy
```

---

### **ModuleNotFoundError: No module named 'tools'**

**Lösung:** Von Projekt-Root ausführen:
```bash
cd h:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00
python run_full_suite.py
```

---

### **PermissionError: reports/figures/demo**

```bash
# Ordner erstellen
mkdir -p reports\figures

# Oder: Alte Outputs löschen
rmdir /s /q reports\figures
mkdir reports\figures
```

---

### **UTF-8 Encoding Error (Windows)**

```powershell
# UTF-8 aktivieren
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
$env:PYTHONIOENCODING="utf-8:replace"

# Tests nochmal ausführen
python run_full_suite.py
```

---

## 📚 **Weitere Dokumentation**

| Datei | Zweck |
|-------|-------|
| `PAPER_EXPORTS_README.md` | Vollständige Übersicht |
| `QUICK_START_PAPER_EXPORTS.md` | 5-Minuten Quick-Start |
| `TESTING_PAPER_EXPORTS.md` | Test-Details |
| `PAPER_EXPORTS_INTEGRATION.md` | Pipeline-Integration |
| `CLI_FIGURE_FLAGS.md` | CLI-Integration |

---

## 🎯 **Empfohlener Workflow für Carmen**

### **Erstmaliger Test:**

```bash
# 1. Nur Paper Export Tools (schnell)
python demo_paper_exports.py

# 2. Wenn OK: Vollständiger Test
python run_full_suite.py

# 3. Ergebnisse prüfen
explorer reports\figures
type reports\RUN_SUMMARY.md
```

### **Tägliche Entwicklung:**

```bash
# Schneller Test während Entwicklung
python run_full_suite.py --quick

# Paper Export Tools einzeln testen
python demo_paper_exports.py

# Volltest vor Commit
python run_full_suite.py
```

---

## ⏱️ **Geschwindigkeits-Übersicht**

| Test-Modus | Dauer | Was wird getestet |
|------------|-------|-------------------|
| `demo_paper_exports.py` | 30s | Nur Paper Export Tools |
| `test_paper_exports.ps1` | 1 min | Paper Export Tools + Checks |
| `run_full_suite.py --quick` | 1 min | Essential Tests |
| `run_full_suite.py` | 2-3 min | **ALLE Tests** |

---

## 🎉 **Nächste Schritte**

Nach erfolgreichem Test:

1. ✅ **CLI-Integration:** Flags in `cli/ssz_rings.py` einbauen
2. ✅ **Echte Daten testen:** G79 mit `--fig` Flag
3. ✅ **Paper-Workflow:** Figures in LaTeX einbinden
4. ✅ **CI/CD Setup:** GitHub Actions konfigurieren

**Los geht's! 🚀**

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
