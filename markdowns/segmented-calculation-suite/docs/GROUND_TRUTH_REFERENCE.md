# SSZ Ground Truth Reference

**Stand:** 2025-12-07 (full-output.md)  
**Suite:** segmented-calculation-suite  
**Autoren:** Carmen N. Wrede, Lino P. Casu

---

## 1. Kanonische Erfolgsraten

| Validierungsquelle | n | Wins | Rate | p-Wert | Status |
|--------------------|---|------|------|--------|--------|
| **Combined Success Rate** | 111 | 110 | **99.1%** | <0.0001 | NEAR-PERFECT |
| **ESO Spectroscopy** | 47 | 46 | **97.9%** | <0.0001 | PROFESSIONAL-GRADE |
| Energy Framework | 64 | 64 | 100.0% | <0.0001 | PERFECT |
| Test Suite | 69 | 69 | 100.0% | <0.0001 | ALL PASS (54+15 Invarianten) |

**Quelle:** `full-output.md`, Zeilen 6146-6154

---

## 2. Golden Dataset (47 Objekte)

### Zusammensetzung

| Kategorie | Anzahl | Beispiele |
|-----------|--------|-----------|
| S-Sterne (Sgr A*) | 30 | S2, S14, S21, S12, ... |
| Pulsare | 5 | PSR J1745-2900, PSR B1913+16, ... |
| Schwarze Löcher | 8 | Cyg X-1, M87*, GRS 1915+105, ... |
| AGN/Blazare | 4 | 3C273, 3C279, BL Lac, PKS 1510-089 |

### Winner-Verteilung

| Winner | Anzahl | Prozent |
|--------|--------|---------|
| SSZ (SEG) | 46 | 97.9% |
| GR | 1 | 2.1% |
| TIE | 0 | 0% |

**Der einzige GR-Win:** `3C279_jet` (extrem relativistischer Jet, v ~ 0.98c)

### CSV-Datei

```
Pfad: data/unified_results.csv
Zeilen: 48 (Header + 47 Objekte)
Spalten: case, regime, x, M_msun, r_m, v_tot, z_obs, z_grsr, z_seg, 
         error_gr, error_seg, winner, margin
```

---

## 3. Experimentelle Benchmarks

| Experiment | Erwartung | SSZ-Vorhersage | Abweichung | Status |
|------------|-----------|----------------|------------|--------|
| GPS Zeitdrift | ~45 μs/Tag | 45.3 μs/Tag | <1% | ✅ |
| Pound-Rebka | 2.46 × 10⁻¹⁵ | 2.46 × 10⁻¹⁵ | <0.1% | ✅ |
| S2-Stern (ESO) | z ~ 0.00088 | 97.9% Match | - | ✅ |
| Merkur-Perihel | 42.99"/Jh | 42.99"/Jh | <0.01% | ✅ |

**Quelle:** `calc-full-math-physics.md`, Zeilen 396-401

---

## 4. Schlüsselkonstanten

### Physikalische Konstanten (CODATA 2018)

| Konstante | Symbol | Wert | Einheit |
|-----------|--------|------|---------|
| Gravitationskonstante | G | 6.67430 × 10⁻¹¹ | m³/(kg·s²) |
| Lichtgeschwindigkeit | c | 299792458.0 | m/s |
| Planck-Konstante | ℏ | 1.054571817 × 10⁻³⁴ | J·s |
| Boltzmann-Konstante | k_B | 1.380649 × 10⁻²³ | J/K |

### SSZ-spezifische Konstanten

| Konstante | Symbol | Wert | Herleitung |
|-----------|--------|------|------------|
| Goldener Schnitt | φ | 1.6180339887... | (1 + √5) / 2 |
| Ξ am Horizont | Ξ(r_s) | 0.8017118... | 1 - exp(-φ) |
| D am Horizont | D(r_s) | 0.5550667... | 1 / (1 + Ξ(r_s)) |
| Universeller Schnittpunkt | r*/r_s | 1.594811 | Numerisch bestimmt (korrigiert) |

**Quelle:** `calc-full-math-physics.md`, Zeilen 44-57

---

## 5. Regime-Definitionen

### Aktuelle Suite-Implementierung (segcalc)

| Regime | r/r_s Bereich | Beschreibung |
|--------|---------------|--------------|
| very_close | < 2 | Innerhalb Photonensphäre |
| photon_sphere | 2 - 3 | Photonensphären-Region |
| strong | 3 - 10 | Strong Field |
| weak | > 10 | Weak Field (SSZ ≡ GR) |

### Blend-Zone (C² Hermite)

| Parameter | Wert |
|-----------|------|
| r_low | 1.8 r_s |
| r_high | 2.2 r_s |
| Interpolation | Quintic Hermite |
| Stetigkeit | C² (Wert + 1. + 2. Ableitung) |

**Quelle:** `calc-full-math-physics.md`, Zeilen 132-158

---

## 6. Quelldateien-Referenz

| Datei | Pfad | Inhalt |
|-------|------|--------|
| Ground Truth Output | `full-output.md` | Kompletter Test-Output |
| Mathematik/Physik | `calc-full-math-physics.md` | Formeln, Regeln, Code |
| Formel-Matrix | `FORMULA_TRACE.md` | LaTeX + Code-Mapping |
| Invarianten-Tests | `test_invariants_hard.py` | 15 harte Tests |
| Golden Dataset | `unified_results.csv` | 47 Objekte |

---

## 7. Zitierbare Aussagen

### Aus full-output.md:

> "SSZ has achieved 99.1% combined success rate on real astronomical data.
> This represents NUMERICALLY GAP-FREE proof of segmented spacetime theory."

### Aus calc-full-math-physics.md:

> "KRITISCH: Δ(M) wird NUR im Strong Field angewendet!
> if regime != 'weak': z_ssz = z_gr × (1 + Δ(M)/100)
> else: z_ssz = z_gr  # Weak field: SSZ ≡ GR"

### Aus FORMULA_TRACE.md:

> "WRONG Formula (Historical - DO NOT USE!)
> z_ssz = 1/D_ssz - 1   # WRONG! This gives Xi, not redshift!"

---

## 8. Verifizierungsbefehle

```bash
# Golden Dataset Winner-Zählung
python -c "import pandas as pd; df = pd.read_csv('data/unified_results.csv'); \
  print('SEG:', (df['winner']=='SEG').sum(), '/', len(df))"
# Erwartete Ausgabe: SEG: 46 / 47

# Invarianten-Tests
python -m pytest tests/test_invariants_hard.py -v
# Erwartete Ausgabe: 15 passed

# Alle Tests
python -m pytest tests/ -v
# Erwartete Ausgabe: 69 passed
```

---

© 2025 Carmen N. Wrede & Lino P. Casu
