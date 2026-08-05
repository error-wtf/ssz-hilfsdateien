# Implementation Log - Perfection Roadmap v2

**Gestartet:** 2025-01-17 13:50 UTC+1  
**Branch:** chore/perfection-roadmap-v2  
**Ziel:** Legacy-Schwellen (90/100/110) → kanonische segcalc-Werte (1.8-2.2, 10)

---

## Baseline Snapshot (vor Änderungen)

```
Datum: 2025-01-17 13:50
pytest tests/ -v: 69/69 PASSED (7.48s)
pytest tests/test_invariants_hard.py -v: 15/15 PASSED
```

---

## KANONISCHE REFERENZWERTE (Source of Truth)

| Parameter | Wert | Notizen |
|-----------|------|---------|
| φ | 1.6180339887 | Golden Ratio |
| Ξ(r_s) | 0.8017118 | Präzise (gerundet ~0.802) |
| D(r_s) | 0.5550667 | FINIT am Horizont |
| r*/r_s | 1.594811 | Universeller Schnittpunkt (korrigiert) |
| Blend-Zone | [1.8, 2.2] | Xi Hermite C² |
| Weak Field | r/r_s > 10 | NICHT >110! |
| Photon Sphere | [2, 3] | SSZ optimal |
| Golden Dataset | 47/46/1/0 | Total/SEG/GR/TIE |

**LEGACY (ssz-qubits Kontext, NICHT segcalc):** 90/100/110

---

## Phase 1: Kritische Fixes

### B.1 xi.py Docstring ✅
- **Datei:** `segcalc/methods/xi.py`
- **Problem:** Docstring erwähnt "90 < r/r_s < 110"
- **Fix:** Korrigiert auf [1.8, 2.2] mit Legacy-Kontext-Hinweis
- **Validiert:** Datei lesen, Docstring prüfen

### B.2 xi.py xi_blended() Defaults ✅
- **Datei:** `segcalc/methods/xi.py`
- **Problem:** Defaults nutzen REGIME_STRONG_THRESHOLD (90)
- **Fix:** Import REGIME_BLEND_LOW/HIGH, Defaults geändert
- **Validiert:** pytest tests/test_invariants_hard.py

### B.3 app.py Reference-Tab Tabelle ✅
- **Datei:** `app.py`
- **Problem:** UI zeigt weak>110, strong<90
- **Fix:** Kanonische segcalc-Werte
- **Validiert:** UI Smoke Test

### B.4 app.py Reference-Tab Code-Snippet ✅
- **Datei:** `app.py`
- **Problem:** Python snippet nutzt 90/110
- **Fix:** Snippet auf 1.8/2.2/10 aktualisiert
- **Validiert:** UI Smoke Test

### B.5 redshift.py Kommentar ✅
- **Datei:** `segcalc/methods/redshift.py`
- **Problem:** Kommentar sagt "r/r_s < 110"
- **Fix:** Korrigiert auf "r/r_s < 10"
- **Validiert:** Datei lesen

### B.6 constants.py get_regime() ✅
- **Datei:** `segcalc/config/constants.py`
- **Problem:** Unreachable code, inkonsistente Logik
- **Fix:** Logik korrigiert, keine Verhaltensänderung
- **Validiert:** pytest + neuer test_regime_classification

### B.7 app.py Regimes-Tab ✅
- **Datei:** `app.py`
- **Problem:** Inkonsistente Darstellung
- **Fix:** Einheitliche Werte/Labels
- **Validiert:** UI Smoke Test

### B.8 theory_plots.py ✅
- **Datei:** `segcalc/plotting/theory_plots.py`
- **Problem:** Hardcoded Grenzen
- **Fix:** Import aus constants.py
- **Validiert:** Plot-Generierung

---

## Phase 2: Wichtige Verbesserungen

### C.1 RunConfig Defaults ✅
- **Datei:** `segcalc/config/constants.py`
- **Fix:** Felder umbenannt: regime_blend_low/high, regime_weak_boundary
- **Validiert:** pytest

### C.8 test_regime_classification ✅
- **Datei:** `tests/test_regime_classification.py`
- **Fix:** 12 neue Tests für kanonische Regime-Grenzen
- **Validiert:** 12/12 PASSED

---

## Validierung nach Phase 1+2

```
Datum: 2025-01-17 14:30
pytest tests/ -v: 81/81 PASSED (1.35s)
  - Original: 69 Tests
  - Neu: 12 Tests (test_regime_classification.py)
```

---

## Änderungszusammenfassung

| Datei | Änderung | Status |
|-------|----------|--------|
| `segcalc/methods/xi.py` | Import + Defaults auf REGIME_BLEND_LOW/HIGH | ✅ |
| `segcalc/config/constants.py` | get_regime() Logic, RunConfig Felder | ✅ |
| `segcalc/methods/redshift.py` | Kommentar 110→10 | ✅ |
| `app.py` | Reference-Tab + Regimes-Tab Tabellen | ✅ |
| `tests/test_regime_classification.py` | 12 neue Tests | ✅ |

---

## Offene Punkte (Optional/Phase 3)

- [ ] qubit.py: M_EARTH/R_EARTH nach constants.py verschieben
- [ ] Cassini Validierung in ppn.py
- [ ] Tab-Reihenfolge in app.py optimieren
- [ ] Farbschema vereinheitlichen

---

## Phase 3: Overlap-Fix + Dokumentation (2025-01-17 14:06)

### 3.1 Regime-Overlap behoben ✅
- **Problem:** Very Close (<2.0) überlappte mit Blend [1.8, 2.2]
- **Lösung:** Very Close jetzt < 1.8 (KEIN Overlap)
- **Dateien:**
  - `segcalc/config/constants.py`: get_regime() korrigiert
  - `tests/test_regime_classification.py`: Tests angepasst
  - `app.py`: Reference-Tab Code-Snippet aktualisiert

### 3.2 Neue Dokumentation ✅
- `docs/G1_G2_METHODS_NOTE.md`: Paper-taugliche g1/g2 Methodik
- `docs/XI_WEAK_STRONG_EXPLAINED.md`: Regime-Schwellen aktualisiert

### 3.3 Validierung ✅
```
Datum: 2025-01-17 14:08
pytest tests/ segcalc/tests/ -q: 137/137 PASSED (1.64s)
```

### Kanonische Regime-Grenzen (FINAL, KEIN OVERLAP)

| Regime | r/r_s | Beschreibung |
|--------|-------|--------------|
| very_close | < 1.8 | Near-horizon |
| blended | [1.8, 2.2] | Hermite C² |
| photon_sphere | (2.2, 3.0] | SSZ optimal (82% wins) |
| strong | (3.0, 10.0] | Strong field |
| weak | > 10.0 | PPN-kompatibel |

---

© 2025 Carmen N. Wrede & Lino P. Casu
