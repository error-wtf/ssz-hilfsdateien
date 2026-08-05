# UI Canonicalization Report

**Date:** 2025-01-17  
**Status:** COMPLETE  
**Scope:** Frontend-Kanonisierung für SSZ Calculation Suite

---

## Kanonische Referenzwerte (Single Source of Truth)

| Parameter | Kanonischer Wert | Legacy (VERBOTEN) |
|-----------|------------------|-------------------|
| Very Close | r_s/r < 1.8 | r/r_s < 2.0 ❌ |
| Blended | 1.8 ≤ r/r_s ≤ 2.2 | 90-110 ❌ |
| Photon Sphere | 2.2 < r/r_s ≤ 3.0 | (nicht definiert) |
| Strong Field | 3.0 < r/r_s ≤ 10.0 | < 90 ❌ |
| Weak Field | r/r_s > 10.0 | > 110 ❌ |
| Label | SSZ | SEG (legacy) |

**Source:** `segcalc/config/constants.py` → `get_regime()`

---

## Gefundene Legacy-Stellen (Audit Phase 0)

### 1. Reference Tab - Regime-Tabelle (FIXED)

**Datei:** `app.py` Zeile ~1330-1340

**Problem:** Tabelle zeigte "Very Close < 2" statt "< 1.8"

**Vorher:**
```markdown
| **Very Close** | r/r_s < 2 | Ξ = 1 - e^(-φ·r/r_s) |
| **Photon Sphere** | 2 < r/r_s ≤ 3 | ... |
```

**Nachher:**
```markdown
| **Very Close** | r_s/r < 1.8 | Ξ = 1 - e^(-φ·r/r_s) |
| **Photon Sphere** | 2.2 < r/r_s ≤ 3.0 | ... |
```

### 2. Reference Tab - Legacy-Notiz (REMOVED)

**Problem:** Verwirrender Hinweis auf ssz-qubits 90/110

**Vorher:**
```
*NOTE: ssz-qubits nutzt 90/100/110 – das ist ein ANDERER Kontext!*
```

**Nachher:** Entfernt - UI zeigt nur kanonische Werte.

### 3. Regime-Farben (FIXED)

**Datei:** `app.py` Zeile ~243

**Problem:** Farben nur für alte Regime-Namen (blend statt blended)

**Nachher:**
```python
colors = {
    'very_close': '#9b59b6',      # Purple
    'blended': '#f39c12',         # Orange
    'photon_sphere': '#e74c3c',   # Red
    'strong': '#e67e22',          # Dark orange
    'weak': '#3498db'             # Blue
}
```

### 4. Code-Snippet im Reference Tab (VERIFIED)

**Status:** Bereits korrekt (< 1.8)

```python
def get_regime(r, r_s):
    ratio = r / r_s
    if ratio < 1.8:
        return "very_close"   # Near-horizon (< 1.8)
    elif ratio <= 2.2:
        return "blended"      # Hermite C² [1.8, 2.2]
    ...
```

---

## Winner-Logik (VERIFIED)

### Korrekte Implementierung

**Datei:** `app.py` Zeile ~1237-1254

```python
has_obs = z_val is not None and z_val > 0

if has_obs:
    # WITH observation: can show winner
    winner = "SSZ" if ssz_res < gr_res else "GR×SR"
    verdict = f"**Winner: {winner}** | ..."
else:
    # WITHOUT observation: only show delta, NO winner claims
    verdict = f"**Prediction only (no z_obs)** | ..."
```

**Ergebnis:** Winner wird NUR bei echter z_obs berechnet. Keine z_obs=z_GR Tricks.

---

## Verbleibende Legacy-Dateien (BEWUSST GETRENNT)

Diese Dateien gehören zu separaten Kontexten und werden NICHT modifiziert:

| Datei | Kontext | Begründung |
|-------|---------|------------|
| `ssz_core.py` | Standalone-Modul | Eigene Defaults (90/110) |
| `unified_validation.py` | Legacy-Tests | Historische Referenz |
| `test_tie_regression.py` | Legacy-Kontext | Backward compatibility |

---

## Acceptance Criteria

| Kriterium | Status |
|-----------|--------|
| Kein UI-Tab enthält Legacy 90/110 | ✅ |
| Reference Tab intern konsistent | ✅ |
| Code-Snippet zeigt < 1.8 | ✅ |
| Regime-Farben für kanonische Namen | ✅ |
| Winner nur bei echter z_obs | ✅ |
| Keine Legacy-Notizen im UI | ✅ |

---

## Regression Tests

Siehe `tests/test_ui_canonicalization.py` für automatisierte Checks:
- Legacy-Strings nicht in UI-Markdown
- Regime-Grenzen korrekt
- Winner-Logik bei fehlender z_obs

---

© 2025 Carmen N. Wrede & Lino P. Casu
