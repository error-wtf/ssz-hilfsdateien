# REPAIR REPORT - Calculation Suite vs full-output.md

**Datum:** 2025-01-17
**Status:** ✅ ALLE KRITISCHEN FIXES IMPLEMENTIERT

---

## Bug 1: UI Regime-Dokumentation falsch

### Problem
UI zeigte **Legacy-Werte (90-110 r_s)** statt **korrekter SSZ-Werte (1.8-2.2 r_s)**

### Ursache
`app.py:1277-1285` verwendete hardcodierte Legacy-Werte in der Markdown-Dokumentation

### Fix
```python
# VORHER (falsch):
| **Weak** | >110 | Ξ = r_s/(2r) |
| **Blend** | 90-110 | C² Hermite |
| **Strong** | <90 | Ξ = 1-e^(-φr_s / r) |

# NACHHER (korrekt):
| **Very Close** | <2 | Ξ = 1-e^(-φr_s / r) | SSZ struggles (0% wins) |
| **Photon Sphere** | 2-3 | Ξ = 1-e^(-φr_s / r) | SSZ OPTIMAL (82% wins) |
| **Strong** | 3-10 | Ξ = 1-e^(-φr_s / r) | Strong field |
| **Weak** | >10 | Ξ = r_s/(2r) | Weak field (~37% wins) |
**Blend Zone:** 1.8 < r/r_s < 2.2 (Hermite C² join)
```

### Datei
`app.py:1275-1288`

### Test
Visuell im Regimes-Tab prüfen

---

## Bug 2: Compare-Tab Regime-Trigger falsch

### Problem
Compare-Tab zeigte Legacy-Thresholds (90/110) statt korrekter SSZ-Werte

### Ursache
`app.py:1215-1230` verwendete `REGIME_STRONG_THRESHOLD` und `REGIME_WEAK_THRESHOLD` (Legacy)

### Fix
```python
# VORHER:
from segcalc.config.constants import REGIME_STRONG_THRESHOLD, REGIME_WEAK_THRESHOLD
strong_thresh = REGIME_STRONG_THRESHOLD  # 90
weak_thresh = REGIME_WEAK_THRESHOLD      # 110

# NACHHER:
from segcalc.config.constants import REGIME_BLEND_LOW, REGIME_BLEND_HIGH
if r_over_rs < REGIME_BLEND_LOW:
    regime_trigger = f"r/r_s={r_over_rs:.2f} < {REGIME_BLEND_LOW} → very_close"
# ... korrekte SSZ-Regime-Logik
```

### Datei
`app.py:1215-1230`

### Test
Compare-Tab: Regime-Trigger muss korrekte Grenzen zeigen

---

## Bug 3: plot_regime_zones() falsche Grenzen

### Problem
Plot zeigte Legacy-Regime-Zonen (90-110) statt SSZ-Werte (1.8-2.2)

### Ursache
`theory_plots.py:312-373` verwendete hardcodierte Legacy-Werte

### Fix
```python
# VORHER:
strong_mask = r_normalized < 90
blend_mask = (r_normalized >= 90) & (r_normalized <= 110)
weak_mask = r_normalized > 110

# NACHHER:
from ..config.constants import REGIME_BLEND_LOW, REGIME_BLEND_HIGH
inner_mask = r_normalized < REGIME_BLEND_LOW  # 1.8
blend_mask = (r_normalized >= REGIME_BLEND_LOW) & (r_normalized <= REGIME_BLEND_HIGH)  # 1.8-2.2
photon_mask = (r_normalized > REGIME_BLEND_HIGH) & (r_normalized <= 3.0)  # 2.2-3
# ... plus korrekter X-Range (0.5-20 statt 1-200)
```

### Datei
`segcalc/plotting/theory_plots.py:312-400`

### Test
Regime-Plot muss korrekte Grenzen (1.8, 2.2, 3, 10 r_s) zeigen

---

## BEREITS KORREKT IMPLEMENTIERT

### ✅ Tie-Handling
**Datei:** `segcalc/methods/core.py:145-156`
```python
eps = 1e-12 * max(abs_ssz, abs_gr, 1e-20)
if abs(abs_ssz - abs_gr) <= eps:
    result["winner"] = "TIE"
```

### ✅ Batch Dataset Check
**Datei:** `app.py:715-720`
```python
if not STATE.has_data():
    return ("**No data loaded.** Upload a CSV or load template first.", ...)
```

### ✅ "Vorteil" nur mit z_obs
**Datei:** `app.py:1237-1254`
```python
has_obs = z_val is not None and z_val > 0
if has_obs:
    verdict = f"**Winner: {winner}** | ..."
else:
    verdict = f"**Prediction only (no z_obs)** | Δ(SSZ-GR) = {delta_pct:+.2f}%"
```

### ✅ Regime-Definitionen in constants.py
**Datei:** `segcalc/config/constants.py:48-54`
```python
REGIME_BLEND_LOW = 1.8   # r_s/r < 1.8 → Inner (strong) field
REGIME_BLEND_HIGH = 2.2  # r/r_s > 2.2 → Outer field
```

### ✅ get_regime() Funktion
**Datei:** `segcalc/config/constants.py:145-170`
- very_close: x < 2
- photon_sphere: 2.2 < x ≤ 3
- strong: 3 < x ≤ 10
- weak: x > 10
- blended: 1.8 ≤ x ≤ 2.2

---

## ZUSAMMENFASSUNG

| Bug | Status | Fix |
|-----|--------|-----|
| UI Regime-Doku | ✅ FIXED | app.py:1275-1288 |
| Compare Regime-Trigger | ✅ FIXED | app.py:1215-1265 |
| plot_regime_zones() | ✅ FIXED | theory_plots.py:312-400 |
| Tie-Handling | ✅ WAR KORREKT | core.py:145-156 |
| Batch Dataset Check | ✅ WAR KORREKT | app.py:715-720 |
| "Vorteil" Gating | ✅ WAR KORREKT | app.py:1237-1254 |

---

## REPRO-BEFEHLE

```bash
# Tests ausführen
cd E:\clone\segmented-calculation-suite
python -m pytest test_weak_field_contract.py -v
python -m pytest test_tie_regression.py -v
python parity_check.py

# Gradio App starten und manuell prüfen
python app.py
```

---

*Repariert von Cascade, 2025-01-17*
