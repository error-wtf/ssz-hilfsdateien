# Carmen's g1/g2 Operationalization

**Autor:** Carmen N. Wrede  
**Datum:** 2025-01-17  
**Status:** KANONISCH für segcalc

---

## Kurzfassung

Die SSZ-Theorie unterscheidet zwei fundamentale Ebenen:

| Symbol | Name | Beschreibung |
|--------|------|--------------|
| **g1** | Observable Layer | Messbare Grenzflächensignaturen |
| **g2** | Formal Layer | Interner formaler Zustandsraum |

**Kernregel:** Wir erheben Ansprüche NUR auf g1-Observablen.  
g2 bleibt formal und nicht direkt testbar.

---

## g1: Observable Boundary Signatures

### Definition

g1 umfasst alle **messbaren physikalischen Effekte** an der Grenzfläche
zwischen Regionen unterschiedlicher Segmentdichte Ξ(r).

### Beispiele

| Observable | Formel | Experiment |
|------------|--------|------------|
| Zeitdilatation | D = 1/(1+Ξ) | GPS, Pound-Rebka |
| Gravitationsrotverschiebung | z = 1/D - 1 | Spektroskopie |
| Frequenzverschiebung | Δf/f = ΔΞ | Atomuhren |
| S-Stern Orbits | z_obs vs z_pred | ESO VLT/GRAVITY |

### Validierungsstatus (segcalc)

```
GPS Zeitdilatation:       45.7 μs/Tag ✅
Pound-Rebka:              2.46×10⁻¹⁵ ✅  
NIST Optical Clock:       ~4×10⁻¹⁷ ✅
S2-Stern (ESO):           46/47 wins ✅
```

---

## g2: Internal Formal State/Process Space

### Definition

g2 beschreibt den **internen formalen Zustandsraum** der SSZ-Metrik,
der die Segmentstruktur der Raumzeit definiert.

### Eigenschaften

- **Nicht direkt messbar** - keine direkten Observablen
- **Formal konsistent** - mathematisch wohldefiniert
- **Keine Singularität** - D(r_s) = 0.555 ist FINIT
- **Hermite C² Blend** - glatter Übergang zwischen Regimen

### Vorsichtsmaßnahmen

> "Wir erheben keine direkten Ansprüche auf g2.  
> Alle testbaren Vorhersagen beziehen sich auf g1-Observablen."

---

## Regime-Zuordnung für Observablen

### Kanonische segcalc-Grenzen

| Regime | r/r_s | Ξ-Formel | g1-Status |
|--------|-------|----------|-----------|
| Very Close | < 2 | 1 - e^(-φr_s / r) | ⚠️ 0% wins |
| Blended | 1.8-2.2 | Hermite C² | Übergang |
| Photon Sphere | 2-3 | 1 - e^(-φr_s / r) | ✅ 82% wins |
| Strong | 3-10 | 1 - e^(-φr_s / r) | ✅ Robust |
| Weak | > 10 | r_s/(2r) | ✅ = GR |

### SSZ vs GR Methoden-Zuordnung

| Observable | Methode | Warum |
|------------|---------|-------|
| Zeitdilatation | Xi | Nur g_tt |
| Frequenz | Xi | Nur g_tt |
| **Lichtablenkung** | **PPN (1+γ)** | g_tt + g_rr |
| **Shapiro-Delay** | **PPN (1+γ)** | g_tt + g_rr |
| Perihel-Präzession | PPN | Komplette Metrik |

---

## Implementierung in segcalc

### Relevante Dateien

| Datei | g1/g2 Relevanz |
|-------|----------------|
| `segcalc/methods/xi.py` | g2 → g1 Transformation |
| `segcalc/methods/dilation.py` | g1 Observable |
| `segcalc/methods/redshift.py` | g1 Observable |
| `segcalc/methods/ppn.py` | g1 für Null-Geodäten |
| `segcalc/config/constants.py` | Regime-Definitionen |

### Code-Beispiel

```python
from segcalc.methods.xi import xi_auto
from segcalc.methods.dilation import D_ssz

# g2: Berechne Segmentdichte
xi = xi_auto(r, r_s)

# g1: Observable Zeitdilatation
D = D_ssz(r, r_s)  # = 1/(1+xi)

# g1: Observable Rotverschiebung
z = 1/D - 1
```

---

## Invarianten (g1/g2 Brücke)

### Fundamentale Identitäten

| Invariante | Formel | Bedeutung |
|------------|--------|-----------|
| Energie-Erhaltung | D × (1 + Ξ) = 1 | g2 → g1 |
| Duale Geschwindigkeit | v_esc × v_fall = c² | g1 |
| Universeller Schnittpunkt | r*/r_s = 1.595 | g1 = GR |

### Tests

```bash
# Invarianten-Tests
python -m pytest tests/test_invariants_hard.py -v
```

---

## Referenzen

1. Wrede, C.N., Casu, L.P. - "Radial Scaling Gauge for Maxwell Fields"
2. ESO/GRAVITY Collaboration - S2-Stern Observationen
3. NIST - Optische Uhr Experimente

---

© 2025 Carmen N. Wrede & Lino P. Casu
