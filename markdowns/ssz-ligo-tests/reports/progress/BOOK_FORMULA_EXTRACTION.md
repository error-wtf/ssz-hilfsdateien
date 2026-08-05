# BOOK FORMULA EXTRACTION
**Datum:** 2026-05-20
**Quelle:** SSZ_BOOK_DE_PERFECTED.md (9.4 MB, ~10.000/115.000 Zeilen gelesen)
**Status:** PARTIAL — Weitere Buch-PDFs und TEX-Dateien noch nicht gelesen

---

## Extrahierte Formeln (aus perfektionierter DE-Version)

### 1. Fundamentale Formeln

| Formel | Buch-Version | formula_compendium | Match? |
|--------|-------------|-------------------|--------|
| Ξ(r) = r_s/(r−r_s) | SSZ_BOOK_DE_PERFECTED | Ξ_weak = r_s/(2r) | ⚠️ ANDERE SCHREIBWEISE (mathematisch äquivalent) |
| D(r) = (r−r_s)/r = 1/(1+Ξ) | SSZ_BOOK_DE_PERFECTED | D = 1/(1+Ξ) | ✅ KONSISTENT |
| s(r) = s₀ × D(r) | SSZ_BOOK_DE_PERFECTED | s(r) = 1/D(r) | ✅ KONSISTENT (s₀=1) |
| φ = (1+√5)/2 ≈ 1.618 | SSZ_BOOK_DE_PERFECTED | φ = 1.618... | ✅ LOCKED |

### 2. Ξ_strong: KLÄRUNG

| Form | Beschreibung | Verwendung | Status |
|------|-------------|-----------|--------|
| min(1−exp(−φ×r_s / r), Ξ_max) | Operative g₂-Definition | Konsolidiertes Paper, Buch | ✅ LOCKED |
| 1−exp(−φ×r_s/r) | Didaktische Zerfallsform | Nur Vergleich/Kontrast | ℹ️ DIDAKTISCH (nicht operativ) |

### 3. QNM / ε220

| Aussage | Wert | Quelle | Status |
|---------|------|--------|--------|
| QNM-Verschiebung | ~3% vs ART | Z.7669, Glossar | PARTIAL_EXPLORATORY |
| Photon-Sphären-Limit | f/f_GR ≈ 1.39 (39%) | Z.12641, Ch.30 | DISKUTIERT (Photonensphäre, NICHT QNM) |
| D_min²-Ableitung | ~31% | Ältere Quelle | HISTORICAL/SUPERSEDED |

### 4. Im Buch FEHLENDE Formeln (für LIGO relevant)

| Formel | Status | Anmerkung |
|--------|--------|-----------|
| delta_psi / δψ | ❌ NICHT GEFUNDEN | Kein Phase-Shift für GW |
| delta_phi / δφ | ❌ NICHT GEFUNDEN | Keine Phasenkorrektur |
| delta_a / δA | ❌ NICHT GEFUNDEN | Keine Amplitudenkorrektur |
| epsilon_220 explizit | ❌ NICHT GEFUNDEN | Nur allgemeine QNM-Erwähnung |
| twist / rotor / polarization für LIGO | ❌ NICHT GEFUNDEN | Nur Sagnac/Rotation allgemein |
| h_SSZ / h_GR Strain-Level | ❌ NICHT GEFUNDEN | Kein GW-Strain-Modell |
| PSD / Whitening | ❌ NICHT GEFUNDEN | Keine LIGO-Datenverarbeitung |
| Interferometer-Modellierung | ❌ NICHT GEFUNDEN | Nur Sagnac |
| Inspiral-Phase / rdot | ⚠️ Kap.31 erwähnt | Lagrange/Hamilton — noch nicht gelesen |

---

## LIGO-Relevanz-Einstufung

| Formel | LIGO-Status |
|--------|------------|
| Ξ, D, s, φ | ✅ CAN_USE_NOW (Fundament) |
| Ξ_strong (r/r_s) | ✅ CAN_USE_NOW (operativ) |
| QNM ~3% | ⚠️ PROXY_ONLY (exploratory, unter Detektor-Präzision) |
| f/f_GR ≈ 1.39 | ❌ NOT_FOR_LIGO (Photonensphäre, nicht Ringdown) |
| delta_psi, delta_a, twist | ❌ NEEDS_DERIVATION (nicht im Buch) |

**Zentrales Ergebnis: Das Buch liefert Ξ, D, s, φ als Fundament. Alles Weitere für LIGO muss ssz-ligo-tests selbst ableiten.**
