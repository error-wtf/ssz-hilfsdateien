# SSZ Calculation Suite - Dokumentation

## Übersicht

| Dokument | Beschreibung | Zielgruppe |
|----------|--------------|------------|
| [GROUND_TRUTH_REFERENCE.md](GROUND_TRUTH_REFERENCE.md) | Kanonische Zahlen, Quellen, Konstanten | Alle |
| [INVARIANTS_SPECIFICATION.md](INVARIANTS_SPECIFICATION.md) | 7 harte Invarianten + Tests | Entwickler |
| [FAILURE_MODES.md](FAILURE_MODES.md) | Typische Fehler + Diagnose | Debugging |
| [QUICK_VALIDATION.md](QUICK_VALIDATION.md) | Schnelle Verifizierungsbefehle | Alle |
| [FORMULA_TRACE.md](FORMULA_TRACE.md) | Formel-Matrix (LaTeX ↔ Code) | Entwickler |
| [XI_WEAK_STRONG_EXPLAINED.md](XI_WEAK_STRONG_EXPLAINED.md) | Zwei Ξ-Formeln erklärt | Physiker |
| [XI_WEAK_STRONG_BRIDGE_FOR_CARMEN.md](XI_WEAK_STRONG_BRIDGE_FOR_CARMEN.md) | Bridge-Dokumentation (korrigiert) | Carmen |
| [XI_WEAK_STRONG_BRIDGE_NOTES.md](XI_WEAK_STRONG_BRIDGE_NOTES.md) | Detaillierte Bridge-Notizen | Forscher |

---

## Quick Start

### 1. Verifizierung (< 1 Min)

```bash
cd E:\clone\segmented-calculation-suite
python -c "import pandas as pd; df = pd.read_csv('data/unified_results.csv'); print('SEG:', (df['winner']=='SEG').sum(), '/', len(df))"
```

**Erwartete Ausgabe:** `SEG: 46 / 47`

### 2. Alle Tests (< 30 Sek)

```bash
python -m pytest tests/ -q
```

**Erwartete Ausgabe:** `69 passed`

### 3. Gradio UI starten

```bash
python app.py
# Öffnen: http://localhost:7860
```

---

## Ground Truth Zahlen

| Metrik | Wert |
|--------|------|
| Combined Success Rate | 99.1% (110/111) |
| ESO Spectroscopy | 97.9% (46/47) |
| Energy Framework | 100% (64/64) |
| Test Suite | 100% (69/69) |

---

## Die 7 Invarianten

1. **Weak-Field-Contract:** SSZ = GR im Weak Field
2. **Verbotene Formel:** z_ssz ≠ 1/D_ssz - 1
3. **Winner-Logik:** eps-basiert, kein freier Threshold
4. **Golden Dataset:** 46/47 SSZ wins
5. **Xi-Formeln:** weak + strong korrekt
6. **Horizont-Regularität:** D_SSZ(r_s) ~ 0.555
7. **Regime-Grenzen:** Suite-spezifisch

---

## Wichtige Dateien

```
segmented-calculation-suite/
├── app.py                    # Gradio UI
├── data/
│   └── unified_results.csv   # Golden Dataset (47 Objekte)
├── segcalc/
│   ├── config/constants.py   # Konstanten, PHI, c, G
│   └── methods/
│       ├── xi.py             # Ξ-Formeln
│       ├── dilation.py       # D_ssz, D_gr
│       ├── redshift.py       # z_ssz, Δ(M)
│       └── core.py           # calculate_single, Winner-Logik
├── tests/
│   ├── test_invariants_hard.py  # 15 Invarianten-Tests
│   ├── test_experimental_validation.py
│   ├── test_geodesics.py
│   └── test_qubit.py
└── docs/
    ├── README.md             # Diese Datei
    ├── GROUND_TRUTH_REFERENCE.md
    ├── INVARIANTS_SPECIFICATION.md
    ├── FAILURE_MODES.md
    ├── QUICK_VALIDATION.md
    └── ...
```

---

## Kontakt

**Autoren:** Carmen N. Wrede & Lino P. Casu  
**Repository:** https://github.com/error-wtf/segmented-calculation-suite

---

© 2025 Carmen N. Wrede & Lino P. Casu
