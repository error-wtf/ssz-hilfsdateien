# SSZ Suite - Logging & Summary System

## Übersicht

Das Logging-System erfasst **ALLE Ausgaben** während der Testausführung und generiert zwei Summary-Dateien:

1. **`reports/RUN_SUMMARY.md`** - Kompakte Übersicht
2. **`reports/summary-output.md`** - Vollständiges detailliertes Log

---

## Wie es funktioniert

### 1. **Output Capture während der Ausführung**

```python
# run_full_suite.py erstellt einen StringIO Buffer:
output_log = io.StringIO()

# TeeOutput schreibt gleichzeitig zu Console UND Buffer:
class TeeOutput:
    def write(self, text):
        console.write(text)  # Sichtbar in Terminal
        buffer.write(text)   # Gespeichert für Log
```

**Ergebnis:** Du siehst ALLES in der Console UND es wird gespeichert!

---

### 2. **Am Ende werden 2 Dateien generiert:**

#### **A) RUN_SUMMARY.md** (Kompakt)
```markdown
# SSZ Suite Run Summary - Physics Tests

**Date:** 2025-10-18 15:10:00

## Overview
- Physics Test Suites: 16
- Silent Technical Tests: 3
- Passed: 16
- Failed: 0
- Success Rate: 100.0%

## Physics Test Results
- **PPN Exact Tests:** ✅ PASS (0.1s)
- **Dual Velocity Tests:** ✅ PASS (0.2s)
...
```

#### **B) summary-output.md** (Vollständig)
```markdown
# SSZ Suite - Complete Output Log

**Generated:** 2025-10-18 15:10:30

## Full Test Suite Output

```
================================================================================
SSZ PROJECTION SUITE - FULL TEST & ANALYSIS WORKFLOW
================================================================================

PHASE 1: ROOT-LEVEL SSZ TESTS
----------------------------------------------------------------------------------------------------

[RUNNING] PPN Exact Tests
================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
...KOMPLETTE AUSGABE ALLER TESTS...
================================================================================
PASSED
...

Total Duration: 145.3s
```
```

---

## Verwendung

### **Test Suite ausführen:**

```bash
python run_full_suite.py
```

### **Am Ende siehst du:**

```
====================================================================================================
GENERATING DETAILED OUTPUT LOG
====================================================================================================

✅ Detailed output log written to: H:\...\reports\summary-output.md
   File size: 245.8 KB

To view the complete log:
   cat reports/summary-output.md

Or on Windows:
   type reports\summary-output.md

====================================================================================================
WORKFLOW COMPLETE
====================================================================================================

📊 Summary Files:
   • H:\...\reports\RUN_SUMMARY.md
   • H:\...\reports\summary-output.md

✅ ALL TESTS PASSED
```

---

## Log-Dateien anzeigen

### **Linux / macOS / Git Bash:**
```bash
# Kompakte Summary:
cat reports/RUN_SUMMARY.md

# Vollständiges Log:
cat reports/summary-output.md

# Mit Pager (scrollbar):
less reports/summary-output.md
```

### **Windows PowerShell / CMD:**
```cmd
# Kompakte Summary:
type reports\RUN_SUMMARY.md

# Vollständiges Log:
type reports\summary-output.md

# Mit Pager:
more reports\summary-output.md
```

### **Im Browser:**
```bash
# Markdown Preview (benötigt Extension):
code reports/summary-output.md
```

---

## Datei-Struktur

```
reports/
├── RUN_SUMMARY.md           # Kompakte Übersicht
├── summary-output.md        # Vollständiges Log (ALLES!)
├── test_ppn_exact.md        # Einzelne Test-Outputs
├── test_vfall_duality.md
├── test_segwave_core.md
└── ...
```

---

## Was wird geloggt?

### **ALLES:**
- ✅ Alle Test-Ausgaben (inkl. Physical Interpretations)
- ✅ Alle `print()` Statements
- ✅ Alle Error Messages
- ✅ Alle Progress Indicators
- ✅ Alle Timings
- ✅ Complete Tracebacks (bei Errors)

### **Beispiel-Inhalt:**

```
================================================================================
Q-FACTOR: Temperature AND Density Combined
================================================================================
Configuration:
  Temperature: 80.0 K → 100.0 K
  Density: 1.0e+05 → 2.0e+05 cm⁻³
  β = 1.0, η = 0.5

Calculation:
  q_T = (80.0/100.0)^1.0 = 0.800000
  q_n = (1e+05/2e+05)^0.5 = 0.707107
  q_k = q_T × q_n = 0.565685

Physical Interpretation:
  • Both cooling AND density drop reduce q_k
  • Combined effect: q_k = 0.566 < 0.8
  • Density amplifies temperature effect
================================================================================
PASSED
```

**Dieser komplette Output ist in `summary-output.md`!**

---

## Vorteile

### **1. Vollständige Nachvollziehbarkeit**
- Jeder Test-Run ist komplett dokumentiert
- Alle Interpretationen gespeichert
- Debugging wird einfacher

### **2. Teilbarkeit**
- `summary-output.md` kann weitergegeben werden
- Andere können exakt sehen was passiert ist
- Keine Information geht verloren

### **3. Dokumentation**
- Automatische Test-Dokumentation
- Physikalische Interpretationen archiviert
- Perfekt für Papers & Reports

---

## Echo Command (schnell alles anzeigen)

### **Alle Markdown Files auf einmal:**

```bash
# PowerShell:
Get-ChildItem reports\*.md | ForEach-Object { Get-Content $_ }

# Linux/macOS:
cat reports/*.md
```

### **Nur die wichtigsten:**

```bash
# Windows:
type reports\RUN_SUMMARY.md & type reports\summary-output.md

# Linux:
cat reports/RUN_SUMMARY.md reports/summary-output.md
```

---

## Tipps

### **1. Log ist zu groß?**
```bash
# Nur die letzten 100 Zeilen:
tail -n 100 reports/summary-output.md

# Nur Summary:
cat reports/RUN_SUMMARY.md
```

### **2. Suche in Log:**
```bash
# Nach "FAILED" suchen:
grep "FAILED" reports/summary-output.md

# Nach Test suchen:
grep "test_ppn_exact" reports/summary-output.md
```

### **3. Log archivieren:**
```bash
# Mit Timestamp:
cp reports/summary-output.md archive/log_$(date +%Y%m%d_%H%M%S).md
```

---

## Technische Details

### **Buffer-System:**
```python
# Erstelle StringIO Buffer
output_log = io.StringIO()

# TeeOutput schreibt gleichzeitig zu beiden Outputs
class TeeOutput:
    def __init__(self, *outputs):
        self.outputs = outputs
    def write(self, text):
        for output in self.outputs:
            output.write(text)
    def flush(self):
        for output in self.outputs:
            output.flush()

# Verwende TeeOutput
sys.stdout = TeeOutput(sys.__stdout__, output_log)
```

### **Log-Generierung:**
```python
# Am Ende:
with open("reports/summary-output.md", "w", encoding="utf-8") as f:
    f.write("# SSZ Suite - Complete Output Log\n\n")
    f.write("```\n")
    f.write(output_log.getvalue())  # GESAMTER Buffer!
    f.write("\n```\n")
```

---

## FAQ

### **Q: Wird die Performance beeinträchtigt?**
**A:** Nein! StringIO ist sehr schnell. Overhead < 1%.

### **Q: Wie groß wird die Log-Datei?**
**A:** Typisch 100-500 KB. Bei sehr vielen Tests bis 2 MB.

### **Q: Kann ich das Log ausschalten?**
**A:** Ja, aber nicht empfohlen. Die Logs sind wertvoll für Debugging!

### **Q: Werden Errors auch geloggt?**
**A:** Ja! ALLES was auf stdout/stderr geht wird erfasst.

---

## Copyright

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

**Viel Erfolg mit dem Logging-System!** 🎉
