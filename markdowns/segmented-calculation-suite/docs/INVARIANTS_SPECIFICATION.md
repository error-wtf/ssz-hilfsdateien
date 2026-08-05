# SSZ Invarianten-Spezifikation

**Version:** 1.0  
**Test-Datei:** `tests/test_invariants_hard.py`  
**Status:** 15/15 PASS

---

## Übersicht

Diese Spezifikation definiert die **7 harten Invarianten** der SSZ Calculation Suite.
Jede Invariante ist ein **nicht verhandelbarer Contract**. Verletzung = Suite ist kaputt.

| # | Invariante | Tests | Kritikalität |
|---|------------|-------|--------------|
| 1 | Weak-Field-Contract | 3 | 🔴 KRITISCH |
| 2 | Verbotene Formel | 1 | 🔴 KRITISCH |
| 3 | Winner-Logik | 2 | 🔴 KRITISCH |
| 4 | Golden Dataset Match | 2 | 🔴 KRITISCH |
| 5 | Xi-Formeln | 3 | 🟡 WICHTIG |
| 6 | Horizont-Regularität | 2 | 🟡 WICHTIG |
| 7 | Regime-Grenzen | 2 | 🟡 WICHTIG |

---

## Invariante 1: Weak-Field-Contract

### Regel

```
WENN regime == "weak" DANN z_ssz_grav == z_gr (EXAKT)
```

### Begründung

- PPN-Tests (Cassini, Merkur-Perihel) erfordern β = γ = 1
- Jede Abweichung von GR im Weak Field wäre sofort falsifizierbar
- SSZ ist eine **Erweiterung** von GR, nicht ein Ersatz

### Tests

```python
class TestWeakFieldContract:
    def test_sun_weak_field_z_ssz_equals_z_gr(self):
        """Sonne: r/r_s ~ 2.4e5 => WEAK => z_SSZ == z_GR"""
        
    def test_earth_weak_field_z_ssz_equals_z_gr(self):
        """Erde: r/r_s ~ 7e8 => WEAK => z_SSZ == z_GR"""
        
    def test_delta_m_is_zero_in_weak_field(self):
        """Delta(M) darf im Weak Field NICHT angewendet werden"""
```

### Verletzungssymptom

- z_ssz ≠ z_gr für Sonne/Erde/GPS
- Winner-Rate sinkt drastisch
- PPN-Tests schlagen fehl

---

## Invariante 2: Verbotene Formel

### Regel

```
z_ssz ≠ 1/D_ssz - 1
```

### Begründung

Die Formel `z = 1/D - 1` gibt **Ξ zurück, nicht die Rotverschiebung**!

- `D_ssz = 1/(1+Ξ)` → `1/D_ssz - 1 = Ξ`
- Die korrekte Rotverschiebung ist `z_gr = 1/D_gr - 1` (Schwarzschild)
- SSZ modifiziert `z_gr` mit Δ(M), nicht D_ssz

### Tests

```python
class TestForbiddenFormula:
    def test_z_ssz_is_not_one_over_d_minus_one(self):
        """z_ssz darf NICHT aus D_ssz berechnet werden"""
```

### Verletzungssymptom

- z_ssz-Werte sind um Größenordnungen falsch
- Im Weak Field: z_ssz ≠ z_gr
- Winner-Logik komplett kaputt

---

## Invariante 3: Winner-Logik

### Regel

```python
eps = 1e-12 * max(abs(R_SSZ), abs(R_GR), 1e-20)

if abs(R_SSZ - R_GR) <= eps:
    winner = "TIE"
elif R_SSZ < R_GR:
    winner = "SSZ"
else:
    winner = "GR"
```

### Begründung

- Kein "menschenfreundlicher" Threshold (z.B. 0.01)
- TIE nur bei **numerisch gleichen** Residuals
- Deterministisch: gleiche Inputs → gleicher Winner

### Tests

```python
class TestWinnerLogic:
    def test_winner_is_deterministic(self):
        """Gleiche Inputs -> Gleicher Winner"""
        
    def test_eps_based_tie_handling(self):
        """TIE nur bei numerisch gleichen Residuals"""
```

### Verletzungssymptom

- Mehr TIEs als erwartet (sollte 0 sein im Golden Dataset)
- Nicht-deterministische Ergebnisse
- Winner-Zahlen weichen von Ground Truth ab

---

## Invariante 4: Golden Dataset Match

### Regel

```
Golden Dataset (47 Objekte):
- SEG wins: 46
- GR wins: 1 (3C279_jet)
- TIE: 0
- Rate: 97.9%
```

### Begründung

- Das Golden Dataset ist der **empirische Beweis** der SSZ-Theorie
- 46/47 = 97.9% ist das dokumentierte Ergebnis
- Der einzige GR-Win (3C279_jet) ist physikalisch begründet

### Tests

```python
class TestGoldenDatasetMatch:
    def test_golden_dataset_46_of_47(self):
        """Das Golden Dataset muss exakt 46/47 SSZ wins haben"""
        
    def test_single_gr_win_is_3c279(self):
        """Der einzige GR-Win muss 3C279_jet sein"""
```

### Verletzungssymptom

- Andere Winner-Zahlen als 46/47
- Anderer GR-Win als 3C279_jet
- TIEs im Dataset

---

## Invariante 5: Xi-Formeln

### Regeln

```
Ξ_weak(r) = r_s / (2r)

Ξ_strong(r) = ξ_max × (1 - exp(-φ × r_s / r))

Ξ(r_s) = 1 - exp(-φ) ≈ 0.802
```

### Begründung

- Weak-Field: PPN-kompatibel mit g_tt ≈ 1 - r_s/r
- Strong-Field: Konstruiert für Horizont-Regularität
- Am Horizont: Ξ muss ~0.802 sein (nicht 0, nicht ∞)

### Tests

```python
class TestXiFormulas:
    def test_xi_weak_formula(self):
        """Xi_weak = r_s / (2r)"""
        
    def test_xi_strong_formula(self):
        """Xi_strong = xi_max * (1 - exp(-phi * r_s / r))"""
        
    def test_xi_at_horizon_value(self):
        """Xi(r_s) = 1 - exp(-phi) ~ 0.802"""
```

### Verletzungssymptom

- Falsche Ξ-Werte
- Ξ(r_s) ≠ 0.802
- D(r_s) ≠ 0.555

---

## Invariante 6: Horizont-Regularität

### Regel

```
D_SSZ(r_s) ≈ 0.555 (endlich, > 0, < 1)
D_GR(r_s) = 0 (Singularität)
```

### Begründung

- SSZ **vermeidet** die Horizont-Singularität
- D_SSZ bleibt endlich → keine Divergenz
- Dies ist ein **Kernunterschied** zu GR

### Tests

```python
class TestHorizonFinite:
    def test_d_ssz_finite_at_horizon(self):
        """D_SSZ(r_s) ~ 0.555 (endlich, nicht 0)"""
        
    def test_d_gr_zero_at_horizon(self):
        """D_GR(r_s) = 0 (Singularität)"""
```

### Verletzungssymptom

- D_SSZ(r_s) = 0 oder ∞
- D_SSZ(r_s) ≠ 0.555 (±0.01)

---

## Invariante 7: Regime-Grenzen

### Regel

```
Suite-spezifische Grenzen verwenden:
- segcalc: 2/3/10 für very_close/photon_sphere/strong/weak
- Keine eigenen Grenzen erfinden!
```

### Begründung

- Regime-Grenzen sind **Engineering**, nicht Physik
- Verschiedene Repos können verschiedene Grenzen haben
- Die Suite-Grenzen sind **dokumentiert und getestet**

### Tests

```python
class TestRegimeBoundaries:
    def test_weak_regime_above_10_rs(self):
        """r/r_s > 10 => weak oder strong regime"""
        
    def test_photon_sphere_regime(self):
        """r/r_s = 2-3 => photon_sphere regime"""
```

### Verletzungssymptom

- Objekte im falschen Regime
- Δ(M) wird im Weak Field angewendet
- Winner-Zahlen weichen ab

---

## Ausführung

```bash
# Alle Invarianten-Tests
python -m pytest tests/test_invariants_hard.py -v

# Einzelne Invariante
python -m pytest tests/test_invariants_hard.py::TestWeakFieldContract -v

# Mit Details bei Fehler
python -m pytest tests/test_invariants_hard.py -v --tb=long
```

---

© 2025 Carmen N. Wrede & Lino P. Casu
