# Beispiele & Anwendungen – Segmented Spacetime (SSZ)

**Praktische Beispiele und reale Anwendungen**

© Carmen Wrede & Lino Casu, 2025

Lizenz: Anti-Capitalist Software License v1.4

**🌐 Languages:** [🇬🇧 English](EXAMPLES_AND_APPLICATIONS.md) | [🇩🇪 Deutsch](EXAMPLES_AND_APPLICATIONS_DE.md)

---

## 📋 Inhalt

1. [Grundlegende Beispiele](#1-grundlegende-beispiele)
2. [Sonnensystem-Anwendungen](#2-sonnensystem-anwendungen)
3. [Stellare Analyse](#3-stellare-analyse)
4. [Schwarze-Loch-Studien](#4-schwarze-loch-studien)
5. [Galaktische Anwendungen](#5-galaktische-anwendungen)
6. [Kosmologische Entfernungsleiter](#6-kosmologische-entfernungsleiter)
7. [Mehrkörper-Systeme](#7-mehrkörper-systeme)
8. [Gravitationswellen-Proxy](#8-gravitationswellen-proxy)
9. [GAIA-Datenanalyse](#9-gaia-datenanalyse)
10. [Benutzerdefinierte Analysen](#10-benutzerdefinierte-analysen)

---

## 1. Grundlegende Beispiele

### Beispiel 1.1: Berechne r_φ für die Sonne

**Problem:** Finde den SSZ-charakteristischen Radius für die Sonne.

**Gegeben:**
- M_☉ = 1.98847 × 10³⁰ kg
- G = 6.67430 × 10⁻¹¹ m³ kg⁻¹ s⁻²
- c = 2.99792458 × 10⁸ m/s
- φ = 1.618033988749...

**Lösung:**

```python
from ssz_theory_segmented import rphi_from_mass, delta_percent, M_SUN
from decimal import Decimal

# Berechne r_φ mit hoher Präzision
M = M_SUN
r_phi = rphi_from_mass(M, use_decimal=True)
delta = delta_percent(M, use_decimal=True)

# Konvertiere zu float für Anzeige
r_phi_m = float(r_phi)
delta_pct = float(delta)

print(f"Masse: M = {M:.3e} kg")
print(f"Δ(M) = {delta_pct:.2f}%")
print(f"r_φ = {r_phi_m:.6e} m")
print(f"r_φ = {r_phi_m/1000:.3f} km")

# Vergleich mit Schwarzschild-Radius
r_s = 2 * 6.67430e-11 * float(M) / (2.99792458e8)**2
print(f"\nVergleich:")
print(f"r_s (Schwarzschild) = {r_s:.6e} m = {r_s/1000:.3f} km")
print(f"r_φ/r_s = {r_phi_m/r_s:.4f}")
```

**Ausgabe:**
```
Masse: M = 1.988e+30 kg
Δ(M) = 100.00%
r_φ = 2.386e+03 m
r_φ = 2.386 km

Vergleich:
r_s (Schwarzschild) = 2.953e+03 m = 2.953 km
r_φ/r_s = 0.8080
```

**Physikalische Interpretation:**
- SSZ sagt r_φ ≈ 2.4 km für die Sonne vorher
- Dies ist ~81% des Schwarzschild-Radius
- Δ(M) = 100% bedeutet SSZ ≈ GR in diesem Regime

---

_Vollständige Dokumentation siehe englische Version [EXAMPLES_AND_APPLICATIONS.md](EXAMPLES_AND_APPLICATIONS.md)_

**Alle Code-Beispiele sind identisch in beiden Sprachen.**

---

## 📊 Zusammenfassung der Anwendungen

### Nach wissenschaftlicher Domäne

| Domäne | Beispiele | Hauptergebnisse |
|--------|-----------|-----------------|
| **Sonnensystem** | Perihel, Lichtablenkung | β = γ = 1 ✓ |
| **Stellar** | Hauptreihe, Doppelsterne | Δ(M) ≈ 100% |
| **Kompakte Objekte** | Schwarze Löcher, Neutronensterne | Δ(M) → 2% |
| **Galaktisch** | Massenprofile, DM-Halos | Multi-Skalen-Analyse |
| **Kosmologisch** | Hubble-Diagramm, SN Ia | Entfernungsleiter |
| **Mehrkörper** | Doppelsterne, Cluster | Superpositionsprinzip |
| **Gravitationswellen** | Verschmelzungen, Ringdown | Frequenzskalierung |

### Rechenressourcen

**Erforderlich:**
- Python 3.8+
- Bibliotheken: numpy, pandas, scipy, matplotlib
- Speicher: ~2 GB für vollständige GAIA-Analyse
- CPU: Standard-Desktop (2-4 Kerne)

**Optional:**
- Numba (für Beschleunigung)
- Jupyter (für interaktive Analyse)
- GPU (für groß angelegte Studien)

---

## 🔗 Weiterführende Literatur

**Verwandte Dokumentation:**
- [PHYSICS_FOUNDATIONS_DE.md](PHYSICS_FOUNDATIONS_DE.md) - Physikalische Konzepte
- [MATHEMATICAL_FORMULAS_DE.md](MATHEMATICAL_FORMULAS_DE.md) - Alle Formeln
- [CODE_IMPLEMENTATION_GUIDE_DE.md](CODE_IMPLEMENTATION_GUIDE_DE.md) - Implementierung

**Quellcode:**
- `ssz_theory_segmented.py` - Kernfunktionen
- `segspace_all_in_one_extended.py` - Analyse-Pipeline
- `tests/` - Beispiel-Testfälle

**Theorie-Papers:**
- `papers/SegmentedSpacetime-ANewPerspectiveonLightGravityandBlackHoles.md`
- `papers/DualVelocitiesinSegmentedSpacetime.md`

---

**Vollständige praktische Beispiele für SSZ-Theorie-Anwendungen! 🔬✨**
