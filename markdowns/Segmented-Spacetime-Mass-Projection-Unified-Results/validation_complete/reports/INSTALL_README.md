# SSZ Suite - Installation & Test System

## Übersicht

Die Installation führt automatisch:
1. ✅ Python Environment Setup
2. ✅ Dependency Installation
3. ✅ Package Installation
4. ✅ **Komplette Test Suite** (mit allen Fixes!)

---

## Installation Scripts

### **Windows (PowerShell):**
```powershell
.\install.ps1
```

### **Linux / macOS:**
```bash
chmod +x install.sh
./install.sh
```

---

## Was wurde gefixt?

### **1. Pytest Crash Fix ✅**

**VORHER (CRASH):**
```bash
pytest tests/ -v --tb=short --disable-warnings
# → ValueError: I/O operation on closed file
```

**JETZT (FUNKTIONIERT):**
```bash
pytest tests/ -s -v --tb=short
# → Alle Tests laufen durch!
```

**Das `-s` Flag verhindert den Pytest I/O Bug!**

---

### **2. Beide Install Scripts gefixt:**

#### **install.ps1** (Windows):
```powershell
# Zeile 204:
pytest tests/ scripts/tests/ -s -v --tb=short  # ✅ GEFIXT
```

#### **install.sh** (Linux):
```bash
# Zeile 256:
pytest tests/ scripts/tests/ -s -v --tb=short  # ✅ GEFIXT
```

---

## Test-Ausgabe nach Installation

### **Erwartete Ausgabe:**

```
[7/9] Running test suite...
  Running ALL tests (root + tests/ + scripts/tests/)...

Root-level SSZ tests:
  test_ppn_exact.py PASSED
  test_vfall_duality.py PASSED
  test_energy_conditions.py PASSED
  test_c1_segments.py PASSED
  test_c2_segments_strict.py PASSED
  test_c2_curvature_proxy.py PASSED
  test_utf8_encoding.py PASSED

Pytest test suites:
================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
β = 1.000000000000 (perfect)
γ = 1.000000000000 (perfect)

Physical Interpretation:
  • β=1 → No preferred frame (GR-like)
  • γ=1 → Standard curvature response
  • Both match GR in weak field limit
================================================================================
PASSED

[... ALLE Tests mit detaillierten Physical Interpretations ...]

  ✓ All tests passed
```

---

## Detaillierte Test-Phasen

### **Phase 1: Root-Level Tests (Python Scripts)**
```
test_ppn_exact.py           → PPN Parameters β, γ
test_vfall_duality.py       → v_esc × v_fall = c²
test_energy_conditions.py   → WEC/DEC/SEC
test_c1_segments.py         → C1 Continuity
test_c2_segments_strict.py  → C2 Continuity
test_c2_curvature_proxy.py  → Curvature Smoothness
test_utf8_encoding.py       → UTF-8 Handling (silent)
```

### **Phase 2: Pytest Suites**
```
tests/test_segwave_core.py       → 16 Tests (Q-Factor, Velocity, Frequency, Residuals, γ)
tests/test_segwave_cli.py        → 16 Tests (CLI Arguments, Validation) - silent
tests/test_print_all_md.py       → 6 Tests (Markdown Printing) - silent
scripts/tests/test_ssz_kernel.py → 4 Tests (γ bounds, redshift, rotation, lensing)
scripts/tests/test_ssz_invariants.py → 6 Tests (Growth, boundary, density)
scripts/tests/test_segmenter.py  → 2 Tests (Coverage, scaling)
scripts/tests/test_cosmo_*.py    → 5 Tests (Multi-body fields)
tests/cosmos/test_*.py           → 1 Test (Two-body superposition)
```

**Total: ~50+ Tests**

---

## Installation Options

### **Standard Installation:**
```powershell
.\install.ps1
```
- Installiert Package
- Führt ALLE Tests aus
- Zeigt detaillierte Ausgaben

### **Skip Tests:**
```powershell
.\install.ps1 -SkipTests
```
- Installiert nur
- Keine Tests

### **Development Mode:**
```powershell
.\install.ps1 -Dev
```
- Installiert als `pip install -e .`
- Für Development

### **Dry Run:**
```powershell
.\install.ps1 -DryRun
```
- Zeigt nur was gemacht würde
- Führt nichts aus

---

## Nach der Installation

### **Tests nochmal ausführen:**

```bash
# Komplette Suite:
python run_full_suite.py

# Nur ein Test:
python test_ppn_exact.py

# Pytest Tests:
pytest tests/ -s -v
```

---

## Vollständiges Test-System

Nach Installation verfügbar:

### **1. run_full_suite.py** (Empfohlen!)
```bash
python run_full_suite.py
```

**Generiert:**
- `reports/RUN_SUMMARY.md` - Kompakte Übersicht
- `reports/summary-output.md` - Vollständiges detailliertes Log

**Features:**
- ✅ Alle Tests mit Physical Interpretations
- ✅ Silent Tests (UTF-8, CLI, MD Print) im Hintergrund
- ✅ Logging System (erfasst ALLES!)
- ✅ MD Echo (zeigt alle Reports)

### **2. Einzelne Tests:**
```bash
# Root-Level:
python test_ppn_exact.py
python test_vfall_duality.py

# Pytest:
pytest tests/test_segwave_core.py -s -v
pytest scripts/tests/test_ssz_kernel.py -s -v
```

---

## Troubleshooting

### **Problem: Pytest Crash**

```
ValueError: I/O operation on closed file
```

**Lösung:** Stelle sicher dass `-s` Flag verwendet wird!

```bash
# FALSCH:
pytest tests/ -v --disable-warnings

# RICHTIG:
pytest tests/ -s -v
```

---

### **Problem: Keine Details in Tests**

```
test_ppn_exact.py PASSED  ← Nur das!
```

**Lösung:** Cache löschen!

```powershell
# Windows:
python -c "import pathlib, shutil; [shutil.rmtree(p, ignore_errors=True) for p in pathlib.Path('.').rglob('__pycache__')]"

# Dann neu:
python test_ppn_exact.py
```

---

### **Problem: "Failed: 3" aber alle Tests PASSED**

**Das war ein Bug in der Summary-Zählung!**

**GEFIXT in run_full_suite.py:**
```python
# VORHER (FALSCH):
failed = total_tests_run - passed  # Zählte silent tests als failed!

# JETZT (RICHTIG):
failed = len(results) - passed  # Nur echte Failures!
```

---

## Verifikation nach Installation

### **1. Check Package:**
```bash
pip show segmented-spacetime-suite-extended
```

### **2. Run Quick Test:**
```bash
python test_ppn_exact.py
```

Erwartete Ausgabe:
```
================================================================================
PPN PARAMETERS: SSZ Metric Exactness Test
================================================================================
β = 1.000000000000
γ = 1.000000000000
...
PASSED
```

### **3. Full Suite:**
```bash
python run_full_suite.py
```

Sollte zeigen:
```
✅ ALL TESTS PASSED
📊 Summary Files:
   • reports/RUN_SUMMARY.md
   • reports/summary-output.md
```

---

## Unterschiede: install.ps1 vs run_full_suite.py

| Feature | install.ps1 | run_full_suite.py |
|---------|-------------|-------------------|
| Package Installation | ✅ Ja | ❌ Nein |
| Tests ausführen | ✅ Ja | ✅ Ja |
| Detaillierte Logs | ❌ Nein | ✅ Ja (summary-output.md) |
| Silent Tests | ❌ Alle sichtbar | ✅ Im Hintergrund |
| Summary Files | ❌ Nein | ✅ 2 Dateien |
| MD Echo | ❌ Nein | ✅ Ja |
| Logging System | ❌ Nein | ✅ Ja |

**Empfehlung:**
1. **Installation:** `.\install.ps1`
2. **Tests danach:** `python run_full_suite.py`

---

## Was die Install-Scripts machen

### **Schritt-für-Schritt:**

```
[1/9] Python Check        → Prüft Python 3.10+
[2/9] Virtual Environment → Erstellt .venv
[3/9] Activate venv       → Aktiviert .venv
[4/9] Upgrade pip         → Aktualisiert pip, setuptools, wheel
[5/9] Dependencies        → Installiert requirements.txt
[6/9] Package Install     → pip install .
[7/9] Test Suite          → Führt ALLE Tests aus ✅
[8/9] Verify              → Prüft Installation
[9/9] Complete            → Fertig!
```

---

## FAQ

### **Q: Warum crasht pytest mit `--disable-warnings`?**
**A:** Das ist ein bekannter Pytest Bug mit file handles. `-s` Flag verhindert das!

### **Q: Warum sehe ich "Failed: 3" obwohl alle Tests passed?**
**A:** Bug in alter Version! Jetzt gefixt - silent tests werden nicht mehr als "failed" gezählt.

### **Q: Muss ich nach install.ps1 noch run_full_suite.py ausführen?**
**A:** Nein, aber empfohlen! run_full_suite.py hat mehr Features (Logging, Summary, MD Echo).

### **Q: Kann ich install.ps1 ohne Tests ausführen?**
**A:** Ja! `.\install.ps1 -SkipTests`

---

## Production-Ready Analysis Scripts (NEW - Oct 2025)

**Nach der Installation verfügbar:**

### 1. Rapidity-Based Equilibrium Analysis
```bash
python perfect_equilibrium_analysis.py
```
- Eliminiert 0/0 Singularitäten
- Rapidity formulation
- Erwartete Verbesserung: 0% → 35-50%

### 2. Standalone Interactive Analysis
```bash
python perfect_seg_analysis.py --interactive
```
- 3 Modi (Interactive/Single/CSV)
- Für eigene Datensätze
- Production-ready

### 3. Perfect Paired Test Framework
```bash
python perfect_paired_test.py --csv data/real_data_full.csv
```
- Alle Findings inkorporiert
- Regime-spezifische Stats
- Framework für Integration

**Dokumentation:**
- [RAPIDITY_IMPLEMENTATION.md](RAPIDITY_IMPLEMENTATION.md)
- [PERFECT_SEG_ANALYSIS_GUIDE.md](PERFECT_SEG_ANALYSIS_GUIDE.md)
- [PERFECT_PAIRED_TEST_GUIDE.md](PERFECT_PAIRED_TEST_GUIDE.md)

---

## Copyright

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

**Installation & Tests sind jetzt komplett gefixt!** ✅
