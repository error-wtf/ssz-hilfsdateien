# test_segwave_core.py - Completion Guide

## Status: 7/14 Physik-Tests erweitert (50%)

---

## ✅ **FERTIG** (mit physikalischen Interpretationen)

### TestQFactor (3/3 Physik-Tests)
- ✅ `test_temperature_only_basic` - Q-Factor mit β=1
- ✅ `test_temperature_with_beta` - Q-Factor mit β=2  
- ✅ `test_temperature_and_density` - Q-Factor mit T und n
- ⚠️ `test_invalid_temperature_raises` - Error-Test (keine Physik)
- ⚠️ `test_invalid_density_raises` - Error-Test (keine Physik)

### TestVelocityProfile (4/4 Physik-Tests)
- ✅ `test_single_shell` - Einzelner Ring (Initial Condition)
- ✅ `test_two_shells_alpha_one` - Zwei-Ring-Propagation
- ✅ `test_deterministic_chain` - 5-Ring-Kette
- ✅ `test_alpha_zero_constant_velocity` - α=0 Limit (Klassisch)
- ⚠️ `test_with_density` - Mit Dichte (einfacher Test)
- ⚠️ `test_mismatched_lengths_raises` - Error-Test

---

## ⚠️ **BEISPIELE VERFÜGBAR** (in COMPLETE_test_segwave_core_verbose.py)

### TestFrequencyTrack (0/2 Physik-Tests)
- ⏳ `test_single_gamma` - Frequenz-Redshift
- ⏳ `test_frequency_decreases_with_gamma` - Monotone Abnahme
- ⚠️ `test_invalid_gamma_raises` - Error-Test

### TestResiduals (0/3 Tests)
- ⏳ `test_perfect_match` - Perfekter Match
- ⏳ `test_systematic_bias` - Systematischer Bias
- ⏳ `test_mixed_residuals` - Gemischte Residuen

### TestCumulativeGamma (0/3 Tests)
- ⏳ `test_constant_q` - Konstanter Q-Faktor
- ⏳ `test_all_ones` - Alle q=1
- ⏳ `test_increasing_sequence` - Steigende Sequenz

---

## 🎯 Warum nur 50%?

### Priorisierung nach physikalischer Bedeutung:

#### **Hoch-Priorität** (FERTIG ✅):
1. **QFactor** - Kern der SSZ-Theorie (Energie-Verhältnisse)
2. **VelocityProfile** - Haupt-Vorhersage (Rotationskurven)

#### **Mittel-Priorität** (Beispiele verfügbar ⏳):
3. **FrequencyTrack** - Frequenz-Redshift (Beobachtbar)
4. **Residuals** - Modell-Qualität (Statistik)
5. **CumulativeGamma** - Kumulatives γ (Technisch)

#### **Niedrig-Priorität** (übersprungen ⚠️):
6. **Error-Tests** - Keine physikalische Interpretation nötig
7. **Einfache Struktur-Tests** - Nur technische Validierung

---

## 📝 Wie die restlichen Tests erweitern

### Option 1: Manuell aus Beispielen kopieren

```bash
# Öffne beide Dateien:
# - tests/test_segwave_core.py
# - tests/COMPLETE_test_segwave_core_verbose.py

# Kopiere gewünschte Test-Erweiterungen
```

### Option 2: Automatisiertes Script (TODO)

```bash
# Könnte implementiert werden:
python extend_segwave_tests.py --apply-all
```

---

## 🚀 Tests ausführen

### Alle erweiterten Tests:

```bash
# Zeigt physikalische Interpretationen:
run_verbose_tests.bat tests\test_segwave_core.py -s -v

# Oder Linux:
./run_verbose_tests.sh tests/test_segwave_core.py -s -v
```

### Nur QFactor Tests:

```cmd
python -X utf8 -m pytest tests/test_segwave_core.py::TestQFactor -s -v
```

### Nur VelocityProfile Tests:

```cmd
python -X utf8 -m pytest tests/test_segwave_core.py::TestVelocityProfile -s -v
```

---

## 📊 Vergleich: Vorher vs Nachher

### Vorher (2/20 = 10%):

```
test_temperature_only_basic PASSED                                      [  5%]
test_temperature_with_beta PASSED                                       [ 10%]
test_temperature_and_density PASSED                                     [ 15%]
...
```
**Nur 2 Tests zeigten physikalische Ergebnisse.**

### Nachher (7/20 = 35%):

```
test_temperature_only_basic
================================================================================
Q-FACTOR: Temperature Ratio (β=1)
================================================================================
...physikalische Interpretation...
PASSED                                                                  [  5%]

test_temperature_with_beta
================================================================================
Q-FACTOR: Temperature with β=2 (Enhanced Sensitivity)
================================================================================
...physikalische Interpretation...
PASSED                                                                  [ 10%]
```

**7 wichtige Physik-Tests zeigen jetzt detaillierte Ergebnisse!**

---

## 🎓 Was die Tests zeigen

### QFactor Tests:

**Physikalische Bedeutung:**
- q_k = (T_curr/T_prev)^β × (n_curr/n_prev)^η
- Energie-Verhältnis zwischen Ringen
- β steuert Temperatur-Sensitivität
- η steuert Dichte-Sensitivität

**Beispiel-Output:**
```
Q-FACTOR: Temperature AND Density Combined
================================================================================
  q_T = 0.800000
  q_n = 0.707107
  q_k = q_T × q_n = 0.565685

Physical Interpretation:
  • Both cooling AND density drop reduce q_k
  • Combined effect: q_k = 0.566 < 0.8 (temperature only)
```

### VelocityProfile Tests:

**Physikalische Bedeutung:**
- v_k = v_{k-1} × q_k^(-α/2)
- Geschwindigkeits-Propagation
- α=0: Klassische Physik (konstant v)
- α=1: SSZ-Effekt (steigende v bei kühlerem T)

**Beispiel-Output:**
```
5-RING CHAIN: Temperature Gradient
================================================================================
  Ring 1: T = 100.0 K, v = 12.50 km/s
  Ring 5: T =  60.0 K, v = 16.12 km/s
  Total increase: 29.0%

Physical Interpretation:
  • Cooling trend: T drops 40 K over 5 rings
  • Velocity amplification: 29.0% increase
  • Monotonic rise consistent with flat rotation curves
```

---

## ✨ Zusammenfassung

### Erreicht:

- ✅ **7 wichtige Physik-Tests** vollständig erweitert
- ✅ **Beispiele für alle restlichen Tests** verfügbar
- ✅ **50% der Physik-Tests** zeigen jetzt Interpretationen
- ✅ **100% der Kern-Physik** (QFactor + VelocityProfile) erweitert

### Optional:

- ⏳ Frequency/Residuals/CumulativeGamma nach Bedarf
- ⚠️ Error-Tests benötigen keine Physik-Outputs

### Empfehlung:

**Die wichtigsten 7 Tests sind fertig!**

Weitere Tests können bei Bedarf aus `COMPLETE_test_segwave_core_verbose.py` kopiert werden.

---

**© 2025 Carmen Wrede, Lino Casu**  
**Anti-Capitalist Software License (v 1.4)**
