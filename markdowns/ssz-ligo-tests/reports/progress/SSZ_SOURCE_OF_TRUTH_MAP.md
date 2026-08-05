# SSZ SOURCE OF TRUTH MAP
**Datum:** 2026-05-20
**Autor:** Bingsi (Hermes Agent)
**Status:** CANONICAL — Verbindlich für alle SSZ-LIGO-Arbeiten

---

## Hierarchie

```
PRIMÄR (Theorie-Truth):
  1. E:\clone\ssz-complete-documentation  (CANONICAL)
  2. E:\clone\book-full\06_PAPERS          (PAPER-READY)
  3. E:\clone\book-full                     (BOOK CONTEXT)

SEKUNDÄR (Validierung/Test):
  Alle ssz-*/segmented-*/SSZ-* Repos unter E:\clone

LIGO-DERIVED (kein Truth):
  E:\clone\ssz-ligo-tests  (Framework/Pipeline/Audit)

LIGO-DATA:
  E:\clone\ligo-gw240925-gw250207-release  (Strain + Posterior)

HISTORICAL:
  ChatGPT/Windsurf-PDFs, SSZ_PRIOR_WORK, SSZ_FINAL_STEPS
```

---

## 1. Primäre Theoriequellen

### 1.1 ssz-complete-documentation

**Status:** CANONICAL — Single Source of Truth für SSZ-Formeln

### 1.2 book-full/V7_BUILD/06_final_v7 (NEUESTE BUCHVERSIONEN)

**Status:** AKTUELLSTE KANONISCHE BUCHVERSION — Gefunden in V7_BUILD

**Buch-PDFs:**
- SSZ_BOOK_DE_FINAL_CANONICAL_V10.pdf (und .md)
- SSZ_BOOK_DE_FINAL_CANONICAL_V11.pdf (und .md)
- SSZ_BOOK_DE_FINAL_CANONICAL_V12.pdf (und .md)
- SSZ_BOOK_DE_FINAL_CANONICAL_V13.pdf (und .md) ← NEUESTE
- SSZ_BOOK_DE_FINAL_V53_PRINT.pdf (Druckversion)
- SSZ_BOOK_EN_FINAL_V53_PRINT.pdf
- SSZ_BOOK_IT_FINAL_V53_PRINT.pdf

**Validierungsdateien:**
- FORMULA_VALIDATION_REPORT.md: 852 Formeln, 12 kanonisch, 128 Warnungen
- FINAL_CANONICAL_VALIDATION_REPORT.md
- FIGURE_VALIDATION_REPORT.md
- BOOK_CONTAMINATION_AUDIT.md
- CLAIM_AUDIT.md

### 1.3 book-full/05_OUTPUT/SSZ_BOOK_PERFECTION_WORKSPACE

**Status:** SEKUNDÄR — Perfektionierte MD-Versionen (9.4 MB)
- SSZ_BOOK_DE_PERFECTED.md: Deutsche perfected-Version
- SSZ_BOOK_EN_PERFECTED.md: Englische perfected-Version

### 1.4 book-full/06_PAPERS

34 Paper-PDFs. Noch nicht vollständig gelesen.
- 07_VALIDATION, 08_FALSIFICATION, 09_PAPERS, 10_REPOSITORIES
- 11_GUARDRAILS (prime_directive.md), 12_GLOSSARY, 13_FREQUENCY_FRAMEWORK

**Kanonische Aussagen:**
- Ξ_weak(r) = r_s / (2r) — LOCKED
- Ξ_strong(r) = 1 - exp(-φ × r_s / r) — LOCKED (r_s/r im Exponenten!)
- Ξ_sat(r) = min(1 - exp(-φ × r_s / r), Ξ_max) — LOCKED (r/r_s, lokale Sättigung)
- D_SSZ(r) = 1/(1+Ξ(r)) — LOCKED
- D(r_s) = 0.55503 — LOCKED
- PPN β=γ=1 — LOCKED
- Prime Directive: NULL→PPN, TIMELIKE/clocks→Ξ, TIMELIKE/orbits→PPN

### 1.2 book-full/06_PAPERS

34 PDFs, 4 Python-Konvertierungsskripte. Paper-nahe Hochprioritätsquelle.

**Wichtigste Papers:**
- SegmentedSpacetime-AFrequencyBasedFramework...pdf (832 KB) — Haupt-Framework
- SSZ_Final_Combined_Paper_2026-02-11.pdf (121 KB)
- SSZ – Finales Paper (Wrede, Casu, Akira).pdf (86 KB)
- DualVelocities...pdf — v_esc × v_fall = c²
- RadialScalingGauge...pdf — s(r) Skalierung
- On the Metric of Black Holes — SSZ-Metrik

**Status:** Paper-Versionen haben Vorrang vor Buch-Drafts.

---

## 2. Formel-Status (CANONICAL — aktualisiert aus V7_BUILD + perfected-Buch)

### LOCKED (12 — direkt aus Primärquellen)
| Formel | Status | Quelle |
|--------|--------|--------|
| Ξ_weak(r) = r_s/(2r) | **LOCKED** | formula_compendium.md + Buch |
| Ξ_strong(r) = min(1−exp(−φ×r_s / r), Ξ_max) | **LOCKED** (operativ) | perfected-Buch Z.116-149 |
| Ξ_dec(r) = 1−exp(−φ×r_s/r) | **ℹ️ DIDAKTISCH** (nicht operativ) | perfected-Buch Z.131-135 |
| Ξ_sat(r) = min(1−exp(−φ×r_s / r), Ξ_max) | **LOCKED** | formula_compendium.md |
| D_SSZ(r) = 1/(1+Ξ(r)) | **LOCKED** | formula_compendium.md + Buch |
| s(r) = 1+Ξ(r) = 1/D(r) | **LOCKED** | formula_compendium.md + Buch |
| z_SSZ = 1/D−1 = Ξ | **LOCKED** | formula_compendium.md |
| r_s = 2GM/c² | **LOCKED** | Standard |
| φ = 1.618033988749895 | **LOCKED** | formula_compendium.md |
| D_SSZ(r_s) = 0.55503 | **LOCKED** | formula_compendium.md + Buch |
| Ξ(r_s) = 0.80171 | **LOCKED** | formula_compendium.md |
| PPN β=1, γ=1 | **LOCKED** | formula_compendium.md + prime_directive.md |
| v_esc×v_fall = c² | **LOCKED** | formula_compendium.md + Paper |

### DERIVED (7 — ableitbar, aber nicht direkt LIGO)
| Formel | Status | LIGO-Relevanz |
|--------|--------|---------------|
| r_φ = (φ/2)×r_s×[1+β×Δ(M)] | LOCKED | INDIREKT |
| E_obs = E_rest×γ_SR×γ_SSZ | LOCKED | INDIREKT |
| Δ(M)-Korrektur | LOCKED | INDIREKT |
| γ_SR, γ_SSZ | LOCKED | INDIREKT |
| Hermite C² Blend | LOCKED | INDIREKT |
| z_SSZ = Ξ | LOCKED | NEEDS_DERIVATION |
| Dual velocities | LOCKED | INDIREKT |

### V0_PROXY → UPGRADED NACH DOKU-LESUNG

| Formel | Alter Status | Neuer Status | Grund |
|--------|-------------|-------------|-------|
| **delta_psi_SSZ(f)** | "Nicht in Primärquellen" | **DERIVED_V1** ✅ | Dokumentiert in `06_STRONG_FIELD/delta_psi_derivation.md` |
| **delta_a = D²−1** | "Nur Proxy" | **DERIVED_V1** ✅ | Dokumentiert in `06_STRONG_FIELD/delta_a_derivation.md` |
| **h_SSZ = h_GR×exp(i×δψ)** | "Nur Proxy" | **DERIVED_V1** ✅ | Dokumentiert in `06_STRONG_FIELD/h_ssz_v0_derivation.md` |

**Wichtig:** Alle drei sind aus Ch.31-Grundgleichungen (rdot_SSZ, P_GW_SSZ) abgeleitet, haben klare Quellenangaben und sind in der offiziellen SSZ-Dokumentation festgehalten. Sie sind NICHT willkürlich — aber noch nicht als LOCKED_FINAL markiert, weil das RSG-Phasenintegral aus Ch.31 nicht final autorisiert ist.

### PARTIAL / EXPLORATORY (1)
| Formel | Status | Quelle |
|--------|--------|--------|
| epsilon_220 ≈ 3% | **PARTIAL_EXPLORATORY** | Buch Glossar Z.7669 |
| f_SSZ/f_GR ≈ 1.39 | **DISKUTIERT** (Photon-Sphäre, NICHT QNM) | Buch Z.12641 |
| D_min² ≈ 0.308 | **HISTORICAL** (superseded) | Ältere Quellen |

### AUTHOR_REVIEW_REQUIRED (4)
| Formel | Grund |
|--------|-------|
| delta_psi finale SSZ-Formel | Nicht in Primärquellen gefunden |
| delta_a als physikalische Amplitude | Nur Proxy, nicht autorisiert |
| Twist/Rotor/Polarisation | Kein Buch-Eintrag für LIGO |
| epsilon_220 finale Freigabe | Exploratory, unter Detektor-Präzision |

### BUCH-VALIDIERUNG (aus FORMULA_VALIDATION_REPORT.md)
```
852 Formeln im Buch gesamt
723 PASS (fehlerfrei)
128 WARNUNGEN (Undef Risk — TEX-Makros nicht aufgelöst)
 12 KANONISCHE SSZ-Treffer:
  - D(r) dilation factor: 5 occurrences
  - fine structure constant SSZ: 3 occurrences
  - Xi_max saturation: 1 occurrence
  - coupling radius r_phi: 1 occurrence
  - mass correction Delta(M): 1 occurrence
  - weak-field Xi formula: 1 occurrence

Kapitel 31-32: 30 Formeln, alle "Undef Risk" — nicht als kanonisch geprüft.
```

---

## 3. Wichtige Konflikte → ALLE GEKLÄRT (aus 06_PAPERS + V7_BUILD)

### Conflict 1: Ξ_strong Exponent → GEKLÄRT ✅
**KEIN THEORIE-KONFLIKT.** Beide Formen sind korrekt — verschiedene regime-abhängige Beschreibungen.

| Form | Formula | Quelle | Verwendung |
|------|---------|--------|------------|
| Operativ/Saturierend | Ξ_strong = min(1 − e^(−φ × r_s/r), Ξ_max) | perfected-Buch Z.116-149, 06_PAPERS Draft Z.100-103 | **Operative g₂-Definition** |
| Didaktisch/Zerfall | Ξ_dec = 1 − e^(−φ × r_s/r) | perfected-Buch Z.131-135 | Nur pädagogischer Vergleich |

**06_PAPERS-Final-Paper-Draft (Z.96-103):** "These are not contradictions; they are **regime‑appropriate descriptions**."

### Conflict 2: epsilon_220 → GEKLÄRT ✅
**VERSCHIEDENE OBSERVABLEN, KEIN WIDERSPRUCH.**
- 3%: Buch-QNM-Wert (perfected-Buch Glossar Z.7669) — Fundamental mode QNM shift
- 39%: Photon-Sphären-Limit, NICHT Ringdown-QNM (Z.12641, r*/r_s ≈ 1.387)
- 31%: D_min² ≈ 0.308 — ältere Interpretation (superseded, 06_PAPERS + V7_BUILD)

### Conflict 3-6: delta_psi, delta_a, Twist → BESTÄTIGT NICHT IN PRIMÄRQUELLEN
Keine dieser Formeln taucht in 06_PAPERS, ssz-complete-documentation, oder book-full als LIGO-Forward-Modell auf. Alle sind ssz-ligo-tests V0-Proxies.

---

## 4. LIGO-Relevanz

| Formel | LIGO-Use | Begründung |
|--------|----------|------------|
| Ξ_weak, D_SSZ, r_s | ✅ CAN_USE_NOW | Fundamentale SSZ-Bausteine |
| delta_psi_SSZ(f) | ⚠️ DERIVED_V1 (dokumentiert in 06_STRONG_FIELD) | Ch.31 RSG noch nicht final |
| delta_a = D²−1 | ⚠️ DERIVED_V1 (dokumentiert) | Nur Inspiral, nicht Ringdown |
| h_SSZ V0 Waveform | ⚠️ DERIVED_V1 (dokumentiert) | Aus psi + A konstruiert |
| epsilon_220 | ❌ RESOLVED_OBSERVABLE_CONFUSION | 3 Werte = 3 Observablen, KEIN Theoriebruch |
| Twist/Rotor | ⚠️ AUTHOR_REVIEW | Nur wenn als h(t)-Forward formulierbar |

---

## 5. Regeln für zukünftige Arbeit

1. Keine Formel aus ssz-ligo-tests ohne Primärquellen-Prüfung
2. V0-Proxies nicht als finale Physik behandeln
3. Keine GR/Kerr-Posterioren als SSZ-Input
4. Jede LIGO-Formel muss in h(t)/h(f) überführbar sein
5. Jeder LIGO-Run braucht HDF5→SHA256→Command→Log→Output→Report
6. Observable→Class→Method→Scope→Calculate (Prime Directive)
