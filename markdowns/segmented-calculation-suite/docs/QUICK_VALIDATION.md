# SSZ Quick Validation Guide

**Zweck:** Schnelle Verifizierung der Calculation Suite  
**Dauer:** < 2 Minuten

---

## 1. One-Liner Checks

### Golden Dataset Winner-Zählung

```bash
cd E:\clone\segmented-calculation-suite
python -c "import pandas as pd; df = pd.read_csv('data/unified_results.csv'); print('SEG:', (df['winner']=='SEG').sum(), 'GR:', (df['winner']=='GR').sum(), 'TIE:', (df['winner']=='TIE').sum(), '/', len(df))"
```

**Erwartete Ausgabe:**
```
SEG: 46 GR: 1 TIE: 0 / 47
```

### GR-Win Objekt prüfen

```bash
python -c "import pandas as pd; df = pd.read_csv('data/unified_results.csv'); print(df[df['winner']=='GR']['case'].values)"
```

**Erwartete Ausgabe:**
```
['3C279_jet']
```

### Win-Rate berechnen

```bash
python -c "import pandas as pd; df = pd.read_csv('data/unified_results.csv'); print(f\"Win-Rate: {(df['winner']=='SEG').sum()/len(df)*100:.1f}%\")"
```

**Erwartete Ausgabe:**
```
Win-Rate: 97.9%
```

---

## 2. Test-Suite Befehle

### Alle Tests (69 Tests)

```bash
python -m pytest tests/ -v --tb=short
```

**Erwartete Ausgabe:**
```
============================= 69 passed in X.XXs ==============================
```

### Nur Invarianten-Tests (15 Tests)

```bash
python -m pytest tests/test_invariants_hard.py -v
```

**Erwartete Ausgabe:**
```
============================= 15 passed in X.XXs ==============================
```

### Schneller Smoke-Test

```bash
python -m pytest tests/test_invariants_hard.py -v -x
```

(`-x` stoppt beim ersten Fehler)

---

## 3. Einzelne Invarianten prüfen

### Weak-Field-Contract

```bash
python -m pytest tests/test_invariants_hard.py::TestWeakFieldContract -v
```

### Verbotene Formel

```bash
python -m pytest tests/test_invariants_hard.py::TestForbiddenFormula -v
```

### Winner-Logik

```bash
python -m pytest tests/test_invariants_hard.py::TestWinnerLogic -v
```

### Golden Dataset

```bash
python -m pytest tests/test_invariants_hard.py::TestGoldenDatasetMatch -v
```

---

## 4. Manuelle Verifizierung

### Einzelobjekt berechnen

```python
from segcalc.methods.redshift import z_ssz
from segcalc.config.constants import M_SUN

# S2-Stern bei Sgr A*
M = 4.297e6 * M_SUN  # Sgr A* Masse
r = 3.8e13           # Periapsis ~1200 AU
v = 7.65e6           # ~7650 km/s

result = z_ssz(M, r, v, v, use_delta_m=True)

print(f"z_gr:   {result['z_gr']:.6f}")
print(f"z_ssz:  {result['z_ssz_grav']:.6f}")
print(f"Regime: {result['regime']}")
print(f"r/r_s:  {result['r_over_rs']:.1f}")
```

### Weak-Field-Contract manuell prüfen

```python
from segcalc.methods.redshift import z_ssz

# Sonne (definitiv Weak Field)
M = 1.98847e30  # kg
r = 6.96e8      # Sonnenradius in m

result = z_ssz(M, r, 0, 0, use_delta_m=True)

assert result['regime'] == 'weak', "Sonne muss weak sein!"
assert result['z_ssz_grav'] == result['z_gr'], "Contract verletzt!"
print("✅ Weak-Field-Contract OK")
```

---

## 5. Gradio UI starten

```bash
cd E:\clone\segmented-calculation-suite
python app.py
```

Dann öffnen: http://localhost:7860

### UI-Features:
- Einzelobjekt-Berechnung
- CSV-Batch-Verarbeitung
- Winner-Visualisierung
- Regime-Anzeige

---

## 6. Erwartete Zahlen (Cheat Sheet)

| Metrik | Erwarteter Wert |
|--------|-----------------|
| Golden Dataset SEG wins | 46 |
| Golden Dataset GR wins | 1 |
| Golden Dataset TIEs | 0 |
| Golden Dataset Total | 47 |
| Win-Rate | 97.9% |
| GR-Win Objekt | 3C279_jet |
| Invarianten-Tests | 15/15 PASS |
| Alle Tests | 69/69 PASS |
| Ξ(r_s) | ~0.802 |
| D(r_s) | ~0.555 |

---

## 7. Troubleshooting

### Tests schlagen fehl

```bash
# Details anzeigen:
python -m pytest tests/test_invariants_hard.py -v --tb=long

# Einzelnen Test debuggen:
python -m pytest tests/test_invariants_hard.py::TestWeakFieldContract::test_sun_weak_field_z_ssz_equals_z_gr -v --tb=long
```

### Falsche Winner-Zahlen

1. CSV prüfen: `data/unified_results.csv`
2. Winner-Spalte inspizieren
3. Vergleichen mit Ground Truth (46/1/0)

### Import-Fehler

```bash
# Sicherstellen dass im richtigen Verzeichnis:
cd E:\clone\segmented-calculation-suite

# PYTHONPATH setzen (falls nötig):
set PYTHONPATH=%PYTHONPATH%;E:\clone\segmented-calculation-suite
```

---

## 8. Vollständige Validierung

```bash
# Alles auf einmal:
cd E:\clone\segmented-calculation-suite

echo "=== Golden Dataset ===" && \
python -c "import pandas as pd; df = pd.read_csv('data/unified_results.csv'); print('SEG:', (df['winner']=='SEG').sum(), 'GR:', (df['winner']=='GR').sum())" && \
echo "" && \
echo "=== Invarianten-Tests ===" && \
python -m pytest tests/test_invariants_hard.py -v --tb=line && \
echo "" && \
echo "=== Alle Tests ===" && \
python -m pytest tests/ -q
```

**Erwartete Ausgabe:**
```
=== Golden Dataset ===
SEG: 46 GR: 1

=== Invarianten-Tests ===
... 15 passed ...

=== Alle Tests ===
69 passed
```

---

© 2025 Carmen N. Wrede & Lino P. Casu
