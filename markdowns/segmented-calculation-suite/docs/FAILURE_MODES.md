# SSZ Failure Modes - Typische Fehler und Erkennung

**Version:** 1.0  
**Zweck:** Schnelle Diagnose wenn "SSZ gewinnt nicht"

---

## Übersicht

Wenn jemand (z.B. Windsurf) behauptet "SSZ gewinnt nicht gegen GR", liegt es fast immer an einem dieser 5 Fehler:

| # | Failure Mode | Häufigkeit | Symptom |
|---|--------------|------------|---------|
| 1 | Verbotene z_ssz Formel | 🔴 Sehr häufig | z_ssz komplett falsch |
| 2 | Δ(M) im Weak Field | 🔴 Sehr häufig | SSZ ≠ GR im Weak Field |
| 3 | Erfundene Regime-Grenzen | 🟡 Häufig | Objekte im falschen Regime |
| 4 | Erfundener Winner-Threshold | 🟡 Häufig | Zu viele TIEs |
| 5 | Einheiten-Mix | 🟡 Häufig | Werte um Größenordnungen falsch |

---

## Failure Mode 1: Verbotene z_ssz Formel

### Der Fehler

```python
# ❌ FALSCH - NIEMALS VERWENDEN:
d_ssz = D_ssz(r, r_s)
z_ssz = 1.0 / d_ssz - 1.0  # Das gibt Xi zurück!
```

### Warum es falsch ist

- `D_ssz = 1/(1+Ξ)` per Definition
- `1/D_ssz - 1 = Ξ` (nicht die Rotverschiebung!)
- Die Rotverschiebung ist `z = 1/D_gr - 1` (Schwarzschild)

### Korrekte Implementierung

```python
# ✅ RICHTIG:
z_gr = z_gravitational(M, r)  # GR-Rotverschiebung
if regime != "weak":
    z_ssz = z_gr * (1 + delta_m / 100)
else:
    z_ssz = z_gr  # Weak field: SSZ = GR
```

### Erkennung

```python
# Wenn z_ssz ~ Xi statt ~ z_gr, ist die Formel falsch
# Test: Im Weak Field muss z_ssz == z_gr
result = z_ssz(M_SUN, R_SUN, 0, 0)
assert result["z_ssz_grav"] == result["z_gr"]  # Muss True sein
```

---

## Failure Mode 2: Δ(M) im Weak Field

### Der Fehler

```python
# ❌ FALSCH - Δ(M) überall anwenden:
delta_m = delta_m_correction(M)
z_ssz = z_gr * (1 + delta_m / 100)  # Auch im Weak Field!
```

### Warum es falsch ist

- Im Weak Field MUSS SSZ = GR sein (PPN-Konsistenz)
- Δ(M) ist eine Strong-Field-Korrektur
- Anwendung im Weak Field bricht den Weak-Field-Contract

### Korrekte Implementierung

```python
# ✅ RICHTIG - Δ(M) nur im Strong Field:
if regime != "weak":
    delta_m = delta_m_correction(M)
    z_ssz = z_gr * (1 + delta_m / 100)
else:
    z_ssz = z_gr  # KEINE Korrektur im Weak Field!
```

### Erkennung

```python
# Test: Im Weak Field darf z_ssz_grav nicht von z_gr abweichen
result = z_ssz(M_EARTH, R_EARTH, 0, 0)
assert result["regime"] == "weak"
assert abs(result["z_ssz_grav"] - result["z_gr"]) < 1e-14
```

---

## Failure Mode 3: Erfundene Regime-Grenzen

### Der Fehler

```python
# ❌ FALSCH - eigene Grenzen erfinden:
def get_regime(r, r_s):
    x = r / r_s
    if x > 50:      # Woher kommt 50?
        return "weak"
    elif x > 5:     # Woher kommt 5?
        return "strong"
    else:
        return "very_strong"  # Was ist das?
```

### Warum es falsch ist

- Die Suite hat **dokumentierte** Regime-Grenzen
- Andere Grenzen führen zu anderen Ergebnissen
- Vergleiche werden ungültig

### Korrekte Implementierung

```python
# ✅ RICHTIG - Suite-Grenzen verwenden:
# Aus segcalc/methods/redshift.py:
def get_regime(r, r_s):
    x = r / r_s
    if x < 2.0:
        return "very_close"
    elif x <= 3.0:
        return "photon_sphere"
    elif x <= 10.0:
        return "strong"
    else:
        return "weak"
```

### Erkennung

```bash
# Prüfen welches Regime die Suite liefert:
python -c "
from segcalc.methods.redshift import z_ssz
result = z_ssz(1e31, 1e5, 0, 0)
print('Regime:', result['regime'], 'r/r_s:', result['r_over_rs'])
"
```

---

## Failure Mode 4: Erfundener Winner-Threshold

### Der Fehler

```python
# ❌ FALSCH - "menschenfreundlicher" Threshold:
if abs(R_SSZ - R_GR) < 0.01:  # Woher kommt 0.01?
    winner = "TIE"
elif R_SSZ < R_GR:
    winner = "SSZ"
else:
    winner = "GR"
```

### Warum es falsch ist

- Der Threshold 0.01 ist willkürlich
- Er erzeugt viele falsche TIEs
- Die Ground Truth hat 0 TIEs im Golden Dataset

### Korrekte Implementierung

```python
# ✅ RICHTIG - eps-basierter Threshold:
eps = 1e-12 * max(abs(R_SSZ), abs(R_GR), 1e-20)

if abs(R_SSZ - R_GR) <= eps:
    winner = "TIE"  # Nur bei numerisch gleich!
elif R_SSZ < R_GR:
    winner = "SSZ"
else:
    winner = "GR"
```

### Erkennung

```python
# Das Golden Dataset hat 0 TIEs:
import pandas as pd
df = pd.read_csv('data/unified_results.csv')
tie_count = (df['winner'] == 'TIE').sum()
assert tie_count == 0, f"Zu viele TIEs: {tie_count}"
```

---

## Failure Mode 5: Einheiten-Mix

### Der Fehler

```python
# ❌ FALSCH - r in r_s-Einheiten mit Formel für Meter:
x = r / r_s  # x ist dimensionslos (r/r_s)
xi = r_s / (2 * x)  # FALSCH! Formel erwartet r in Metern

# ❌ FALSCH - Masse in Sonnenmassen statt kg:
M_msun = 10  # 10 Sonnenmassen
r_s = 2 * G * M_msun / c**2  # FALSCH! M muss in kg sein
```

### Warum es falsch ist

- Formeln haben spezifische Einheiten-Erwartungen
- Mischen führt zu Ergebnissen, die um Größenordnungen falsch sind

### Korrekte Implementierung

```python
# ✅ RICHTIG - Konsistente Einheiten:
M_kg = M_msun * 1.98847e30  # Umrechnung in kg
r_m = r_value  # r in Metern

r_s = 2 * G * M_kg / c**2  # r_s in Metern
xi = r_s / (2 * r_m)        # Beide in Metern
```

### Erkennung

```python
# Plausibilitätscheck:
r_s_sun = 2 * G * M_SUN / c**2
assert 2900 < r_s_sun < 3000, f"r_s Sonne falsch: {r_s_sun}"  # ~2953 m
```

---

## Diagnose-Checkliste

Wenn "SSZ gewinnt nicht" behauptet wird:

### 1. z_ssz Formel prüfen

```python
# Ist z_ssz = 1/D_ssz - 1 verwendet?
# → FALSCH, verboten
```

### 2. Weak-Field-Contract prüfen

```python
# Im Weak Field: z_ssz == z_gr?
result = z_ssz(M_SUN, R_SUN, 0, 0)
print(f"z_ssz={result['z_ssz_grav']}, z_gr={result['z_gr']}")
# Müssen gleich sein!
```

### 3. Regime-Grenzen prüfen

```python
# Welche Grenzen werden verwendet?
# Dokumentierte Suite-Grenzen oder eigene?
```

### 4. Winner-Logik prüfen

```python
# eps-basiert oder fester Threshold?
# Wie viele TIEs gibt es? (sollte 0 sein)
```

### 5. Einheiten prüfen

```python
# M in kg? r in m? v in m/s?
# r_s korrekt berechnet?
```

---

## Quick-Fix Befehl

```bash
# Invarianten-Tests laufen lassen - zeigt alle Probleme:
python -m pytest tests/test_invariants_hard.py -v --tb=long
```

Wenn alle 15 Tests PASS: Die Suite ist korrekt.
Wenn Tests FAIL: Der Fehler wird genau angezeigt.

---

© 2025 Carmen N. Wrede & Lino P. Casu
