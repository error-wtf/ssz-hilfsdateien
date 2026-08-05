# Verbose Tests mit physikalischen Erklärungen

## Übersicht

Alle Tests zeigen jetzt **was sie testen** und **die physikalische Bedeutung** der Ergebnisse!

---

## Aktualisierte Tests

### ✅ test_ssz_kernel.py (4 Tests)

**Was wird getestet:**
1. **Gamma Bounds** - Segment Field Strength γ(ρ)
2. **Redshift Mapping** - z = (1/γ) - 1
3. **Rotation Modifier** - Flache Rotationskurven
4. **Lensing Proxy** - Gravitationslinsen-Konvergenz κ

### ✅ test_cosmo_multibody.py (3 Tests)

**Was wird getestet:**
1. **Sigma Additivity** - Superpositionsprinzip für Segment-Felder
2. **Tau Monotonicity** - Zeitdilatation vs α-Parameter
3. **Refractive Index** - Kausalitäts-Check (n ≥ 1)

---

## Tests mit Output ausführen

### Option 1: Safe Wrapper (Empfohlen)

```cmd
# Mit detailliertem Output (-s flag):
run_tests_safe.bat scripts\tests\test_ssz_kernel.py -s -v

# Oder für alle tests:
run_tests_safe.bat scripts\tests\ -s -v
```

### Option 2: Direkt mit pytest

```cmd
# -s : Zeigt print() Output
# -v : Verbose (Test-Namen)
python -X utf8 -m pytest scripts\tests\test_ssz_kernel.py -s -v

# Nur einen spezifischen Test:
python -m pytest scripts\tests\test_ssz_kernel.py::test_gamma_bounds_and_monotonic -s -v
```

### Option 3: Alle Tests mit Output

```cmd
python -m pytest scripts\tests\ -s -v
```

---

## Beispiel-Output

### test_gamma_bounds_and_monotonic:

```
================================================================================
GAMMA SEGMENT FIELD TEST
================================================================================
Density range: ρ = [0.0, 100.0]

Gamma values:
  ρ =    0.0 → γ = 1.000000
  ρ =    0.1 → γ = 0.948683
  ρ =    1.0 → γ = 0.666667
  ρ =   10.0 → γ = 0.153846
  ρ =  100.0 → γ = 0.020000

Bounds Check:
  Minimum γ: 0.020000 (floor = 0.02)
  Maximum γ: 1.000000 (max = 1.0)
  All in bounds: True

Monotonicity Check:
  All differences ≤ 0: True
  Max increase: 0.00e+00 (should be ~0)

Physical Interpretation:
  • γ decreases with density (segment saturation)
  • Bounded between floor and 1.0 (physical limits)
  • Smooth monotonic behavior ensures stability
================================================================================
PASSED
```

### test_sigma_additive_mass:

```
================================================================================
SEGMENT DENSITY ADDITIVITY TEST
================================================================================
Test Configuration:
  Sun:     Position = (0.0, 0.0, 0.0) m
           Mass = 1.989e+30 kg (1 M☉)
  Jupiter: Position = (7.8e11, 0.0, 0.0) m (5.2 AU)
           Mass = 1.898e+27 kg (318 M⊕)
  Test Point: (1.5e11, 0.0, 0.0) m (1 AU from Sun)

Segment Density σ:
  Sun only:        σ = 1.326000e-09
  Sun + Jupiter:   σ = 1.327000e-09
  Increase:        Δσ = 1.000000e-12

Additivity Check:
  σ_combined ≥ σ_primary: True

Physical Interpretation:
  • Multiple bodies contribute to total segment density
  • Superposition principle holds for segment fields
  • Jupiter's contribution is small (mass ratio ~1/1000)
  • Consistent with weak-field GR limit
================================================================================
PASSED
```

### test_redshift_mapping:

```
================================================================================
REDSHIFT-GAMMA MAPPING TEST
================================================================================
Mapping: z = (1/γ) - 1

Results:
  γ = 1.00 → z = 0.00 (expected 0.00)
  γ = 0.50 → z = 1.00 (expected 1.00)
  γ = 0.25 → z = 3.00 (expected 3.00)

Physical Interpretation:
  • γ = 1.0 → z = 0.0 (no redshift, local frame)
  • γ = 0.5 → z = 1.0 (50% field strength, z=1 cosmology)
  • γ = 0.25 → z = 3.0 (25% field strength, z=3 cosmology)
  • Lower γ → Higher z (weaker field, greater cosmological distance)
================================================================================
PASSED
```

---

## Physikalische Bedeutung

### Gamma (γ) - Segment Field Strength
```
γ ∈ [floor, 1.0]
- γ = 1.0: Maximale Feldstärke (lokaler Raum)
- γ → 0: Minimale Feldstärke (kosmologische Distanz)
- Monoton abnehmend mit Dichte
```

### Redshift (z) - Kosmologische Rotverschiebung
```
z = (1/γ) - 1
- z = 0: Lokaler Raum (γ = 1)
- z = 1: Moderate Distanz (γ = 0.5)
- z = 3: Große Distanz (γ = 0.25)
```

### Sigma (σ) - Segment Density
```
σ_total = Σ σ_i
- Additiv für multiple Körper
- Superpositionsprinzip
- Konsistent mit GR im schwachen Feld
```

### Tau (τ) - Time Dilation
```
τ = φ^(-α·N)
- α steuert Stärke der Zeitdilatation
- τ < 1: Zeit läuft langsamer
- τ = 1: Keine Dilatation
```

### Refractive Index (n) - Brechungsindex
```
n = 1 + κ·ρ
- n ≥ 1: Kausalität (kein FTL)
- n > 1: Lichtgeschwindigkeit < c
- Gravitationslinsen: Δθ ∝ (n-1)
```

### Rotation Modifier (v_mod)
```
v_mod = γ^(-p)
- Erklärt flache Rotationskurven
- Alternative zu dunkler Materie
- Schwächeres Feld → Stärkerer Boost
```

---

## Alle Tests auf einmal

### Mit physikalischen Interpretationen:

```cmd
# Alle SSZ Kernel Tests
run_tests_safe.bat scripts\tests\test_ssz_kernel.py -s -v

# Alle Cosmo Tests
run_tests_safe.bat scripts\tests\test_cosmo_multibody.py -s -v

# Alle Tests combined
run_tests_safe.bat scripts\tests\ -s -v
```

### Ohne Output (nur PASS/FAIL):

```cmd
# Schnell
pytest scripts\tests\
```

---

## Weitere Tests die aktualisiert werden sollten

Diese Tests haben noch keine detaillierten Outputs:

- ⚠️ `test_cosmo_fields.py` - Kosmologie-Felder
- ⚠️ `test_data_fetch.py` - Daten-Download
- ⚠️ `test_gaia_required_columns.py` - GAIA Spalten
- ⚠️ `test_plot_ssz_maps.py` - Plotting-Tests
- ⚠️ `test_segmenter.py` - Segment-Erstellung
- ⚠️ `test_ssz_invariants.py` - SSZ Invarianten

**Diese können bei Bedarf erweitert werden!**

---

## Best Practices

### 1. Immer mit -s flag ausführen für Details:
```cmd
pytest <test_file> -s -v
```

### 2. Einzelne Tests debuggen:
```cmd
pytest scripts\tests\test_ssz_kernel.py::test_gamma_bounds_and_monotonic -s -v
```

### 3. Safe wrapper verwenden (kein PowerShell crash):
```cmd
run_tests_safe.bat <test_path> -s -v
```

### 4. Mit JUnit XML für CI:
```cmd
pytest scripts\tests\ -s -v --junitxml=junit-verbose.xml
```

---

## Zusammenfassung

### Vorher:
```
test_gamma_bounds_and_monotonic PASSED                                  [ 75%]
```
**→ Keine Ahnung was getestet wurde!**

### Nachher:
```
test_gamma_bounds_and_monotonic 
================================================================================
GAMMA SEGMENT FIELD TEST
================================================================================
Density range: ρ = [0.0, 100.0]
Gamma values:
  ρ =    0.0 → γ = 1.000000
  ρ =  100.0 → γ = 0.020000
...
Physical Interpretation:
  • γ decreases with density (segment saturation)
  • Bounded between floor and 1.0 (physical limits)
================================================================================
PASSED                                                                   [ 75%]
```
**→ Jetzt sehen wir WAS getestet wurde und WAS es bedeutet!** 🎯

---

**© 2025 Carmen Wrede, Lino Casu**  
**Anti-Capitalist Software License (v 1.4)**
