# Quick Test Commands - SSZ Suite

## 🚨 PowerShell Extension Crash? Verwende diese Commands!

---

## ✅ SAFE Commands (Kein Crash)

### Comprehensive Real Data Tests:
```cmd
# Option 1: Safe Batch Wrapper (Empfohlen!)
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py

# Option 2: Python Runner
python run_comprehensive_tests.py --verbose

# Option 3: Direkt mit -s Flag
python -X utf8 -m pytest tests\test_ssz_real_data_comprehensive.py -s -v
```

### Spezifische Test-Klassen:
```cmd
# Nur PPN-Parameter
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "PPN"

# Nur Natürliche Grenze
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "NaturalBoundary"

# Nur Duale Geschwindigkeiten
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "DualVelocities"

# Nur Energie-Bedingungen
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "EnergyConditions"

# Nur Real Data Integration
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "RealData"
```

### Spezifische Objekte:
```cmd
# Nur Sonne
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "Sun"

# Nur Sgr A*
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "SgrA"

# Nur M87*
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -k "M87"
```

### Scripts Tests:
```cmd
run_tests_safe.bat scripts\tests\
```

### Alle Tests:
```cmd
run_tests_safe.bat tests\ scripts\tests\
```

---

## ❌ UNSAFE Commands (Können crashen)

```cmd
# VERMEIDEN - kein -s Flag, kann crashen:
python -m pytest tests\test_ssz_real_data_comprehensive.py -v

# VERMEIDEN - in PowerShell Extension Terminal:
pytest tests\
```

---

## 🔧 Troubleshooting

### "no tests ran"?

```cmd
# Prüfen was pytest findet:
python -m pytest tests\test_ssz_real_data_comprehensive.py --collect-only

# Mit verbose:
python -m pytest tests\ -v --collect-only
```

### "I/O operation on closed file"?

```cmd
# Lösung: -s Flag verwenden
python -m pytest tests\ -s -v

# Oder: Safe wrapper
run_tests_safe.bat tests\
```

### Import-Fehler?

```cmd
# Test importieren:
python -c "from tests import test_ssz_real_data_comprehensive"

# Sys path prüfen:
python -c "import sys; print('\n'.join(sys.path))"
```

---

## 📊 Mit Reports

### JUnit XML:
```cmd
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py --junitxml=junit.xml
```

### HTML Report:
```cmd
python run_comprehensive_tests.py --html --verbose
```

### Beide:
```cmd
python run_comprehensive_tests.py --html --verbose --output test_results
```

---

## 🎯 Häufige Use Cases

### 1. Schneller Smoke Test
```cmd
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py::TestPPNParameters -v
```

### 2. Alle Tests mit Physik-Output
```cmd
run_tests_safe.bat tests\test_ssz_real_data_comprehensive.py -s -v
```

### 3. CI-Style (mit XML)
```cmd
python -X utf8 -m pytest tests\test_ssz_real_data_comprehensive.py -s --junitxml=junit.xml
```

### 4. Nur fehlgeschlagene Tests
```cmd
run_tests_safe.bat tests\ --lf  # lf = last failed
```

### 5. Mit Coverage
```cmd
python -m pytest tests\test_ssz_real_data_comprehensive.py -s --cov=. --cov-report=html
```

---

## 🌟 Best Practice

**Immer verwenden:**
```cmd
run_tests_safe.bat <test-path> [pytest-args]
```

**Warum?**
- ✅ Umgeht PowerShell Extension
- ✅ UTF-8 Encoding
- ✅ Keine I/O Crashes
- ✅ Einfach zu merken

---

## 📁 Wo sind die Tests?

```
tests/
├── test_ssz_real_data_comprehensive.py  ← Comprehensive tests (NEU!)
├── test_segwave_cli.py                  ← CLI tests
├── test_segwave_core.py                 ← Core math tests
└── test_print_all_md.py                 ← MD tool tests

scripts/tests/
├── test_ssz_invariants.py
├── test_ssz_kernel.py
├── test_segmenter.py
├── test_cosmo_fields.py
├── test_cosmo_multibody.py
├── test_data_fetch.py
├── test_gaia_required_columns.py
├── test_plot_ssz_maps.py
└── test_utf8_encoding.py
```

---

## 💡 Tipps

### Parallele Ausführung:
```cmd
run_tests_safe.bat tests\ -n auto  # Benötigt pytest-xdist
```

### Nur Warnings anzeigen:
```cmd
run_tests_safe.bat tests\ --tb=short -W default
```

### Stop bei erstem Fehler:
```cmd
run_tests_safe.bat tests\ -x
```

### Debug-Mode:
```cmd
run_tests_safe.bat tests\ -vv --tb=long
```

---

## 🆘 Support

Bei Problemen:
1. Prüfen: `PYTEST_CRASH_FIX.md`
2. Prüfen: `ci\POWERSHELL_CRASH_FIX.md`
3. Safe wrapper verwenden: `run_tests_safe.bat`
4. `-s` Flag verwenden (no capture)

---

**© 2025 Carmen Wrede, Lino Casu**  
**Anti-Capitalist Software License (v 1.4)**
