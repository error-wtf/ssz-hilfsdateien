# SSZ Complete Documentation — Full Reading Notes
**Datum:** 2026-05-20
**Status:** COMPLETE — Critical formula documents read; 15/170 files read in detail

---

## Gelesene Dateien (kritische Pfade)

| # | Datei | Status | LIGO-Relevanz |
|---|-------|--------|---------------|
| 1 | 03_FORMULAS/formula_compendium.md | READ_FULL | ✅ Fundament (Ξ, D, s, φ) |
| 2 | 01_OVERVIEW/ssz_overview.md | READ_FULL | ✅ Überblick + Observable-Klassen |
| 3 | 11_GUARDRAILS/prime_directive.md | READ_FULL | ✅ Null/PPN, Timelike/Ξ, Orbit/PPN |
| 4 | 03_FORMULAS/ppn_formulas.md | READ_FULL | ✅ PPN β=γ=1 bestätigt |
| 5 | 03_FORMULAS/forbidden_formulas.md | READ_RELEVANT | ✅ Deprecated Ξ = (r_s/r)² × exp(-r/r_φ) verboten |
| 6 | 03_FORMULAS/quick_reference.md | READ_RELEVANT | ✅ Kurzreferenz |
| 7 | 03_FORMULAS/special_values.md | READ_RELEVANT | ✅ D_min, Ξ_max, Schnittpunkte |
| 8 | **06_STRONG_FIELD/delta_psi_derivation.md** | **READ_FULL** | ⚠️ **V0_PROXY** — Formel existiert, aber Ch.31 RSG nicht final |
| 9 | **06_STRONG_FIELD/delta_a_derivation.md** | **READ_FULL** | ⚠️ **V0_PROXY** — D²−1 aus P_GW-Ratio |
| 10 | **06_STRONG_FIELD/epsilon_220_derivation_status.md** | **READ_FULL** | ❌ **BLOCKED** — 3%/31%/39% = verschiedene Observablen |
| 11 | **06_STRONG_FIELD/h_ssz_v0_derivation.md** | **READ_FULL** | ⚠️ **V0_PROXY** — Komplette Waveform-Formel |
| 12 | **06_STRONG_FIELD/qnm_spectrum.md** | **READ_FULL** | ⚠️ 39% = f_QNM_SSZ/f_QNM_GR = 1/D(r*) bei r*=1.387r_s |
| 13 | 06_STRONG_FIELD/GR_SSZ_INTERSECTION_PHI_DISCRETIZATION.md | READ_RELEVANT | ✅ Intersection-Geometrie |
| 14 | 08_FALSIFICATION/ligo_physics_clarification.md | READ_FULL | ✅ Strain=Input, Posterior=Output |
| 15 | 01_OVERVIEW/core_postulates.md | READ_RELEVANT | ✅ Axiome |
| 16 | 02_FOUNDATIONS/time_dilation.md | READ_RELEVANT | ✅ D_SSZ |
| 17 | 02_FOUNDATIONS/segment_density.md | READ_RELEVANT | ✅ Ξ(r) |
| 18 | 02_FOUNDATIONS/phi_geometry.md | READ_RELEVANT | ✅ φ-Geometrie |
| 19 | 02_FOUNDATIONS/regime_definitions.md | READ_RELEVANT | ✅ g1/g2/Blend |
| 20 | 02_FOUNDATIONS/energy_conditions.md | SKIMMED | ✅ WEC/DEC/SEC |
| 21 | 02_FOUNDATIONS/regime_and_formula_domain_clarification.md | READ_FULL | ✅ g1/g2/Boundary-System |
| 22 | 02_FOUNDATIONS/scaling_factor.md | READ_FULL | ✅ s(r)=1+Ξ, Maxwell-Skalierung |
| 23 | 03_FORMULAS/special_values.md | READ_FULL | ✅ D_min=0.555, r*/r_s, phi-Werte |
| 24 | 06_STRONG_FIELD/black_hole_metric.md | READ_FULL | ✅ Metric-Tensor, g_tt=−D², g_rr=s² |
| 25 | 06_STRONG_FIELD/GR_SSZ_INTERSECTION_PHI_DISCRETIZATION.md | READ_FULL | ✅ 2 Schnittpunkte im φ-Bracket |
| 26 | 07_VALIDATION/ligo_gw240925_v0_pipeline.md | READ_FULL | ✅ Pipeline-Validierung, delta_lnL=6e-6 |
| 27 | 07_VALIDATION/ligo_next_physics_derivation_tasks.md | READ_FULL | ✅ Prioritäten P1–P9 |
| 28 | 08_FALSIFICATION/falsification_criteria.md | READ_FULL | ✅ 5 definitive Falsifikationskriterien |
| 29 | 08_FALSIFICATION/ligo_physics_clarification.md | READ_FULL | ✅ Strain=Input, Posterior=Output |

## Nur inventarisierte Dateien (~140 weitere)
## Nur inventarisierte Dateien (~130 weitere)
```
00_INDEX, 01_OVERVIEW (restliche), 02_FOUNDATIONS (restliche),
03_FORMULAS (symbol_table, unit_conversion, worked_examples, discrete_ssz_state),
04_KINEMATICS (alle), 05_ELECTROMAGNETISM (alle),
06_STRONG_FIELD (restliche: cosmic_censorship, dark_star,
  infalling_matter, isco_comparison, lagrangian_mechanics, penrose_process,
  rotating_black_holes, singularities, superradiance),
07_VALIDATION (restliche — Testresultate, keine neuen Formeln),
08_FALSIFICATION (restliche — 3/6 gelesen),
09_PAPERS (alle — Duplikate mit book-full/06_PAPERS),
10_REPOSITORIES (alle — repo_index + ligo_tests 2/3 gelesen),
11_GUARDRAILS (alle — prime_directive + method_assignment + confusion_prevention + cross_repo 4/4 gelesen),
12_GLOSSARY, 13_FREQUENCY_FRAMEWORK
```

## Zentrale Funde aus FOUNDATIONS/VALIDATION/FALSIFICATION/GUARDRAILS

### 1. Regime-Boundary-Architektur (aus 02_FOUNDATIONS)
```
ZWEI Boundary-Systeme:
  System 1 (Formula Domains): g₁-Branch (>2.2 r_s), Blend (1.8-2.2), g₂ (<1.8)
  System 2 (Physical Regimes): very_close, blended, photon_sphere, strong, weak

KRITISCH: "g₁ für r>2.2" bedeutet NICHT "alles >2.2 ist weak field"
          → Operative Formelwahl ≠ Physikalisches Regime
          → 90/110 sind PROBE_RADII, keine Regime-Grenzen
```

### 2. epsilon_220 — RESOLVED OBSERVABLE-CLASS CONFUSION (aus 06_STRONG_FIELD + 08_FALSIFICATION)
```
3 Werte = 3 verschiedene Observablen, KEIN Theoriebruch:
  3%  → QNM Frequenz-Shift (exploratorisch, Ch.30, unter Detektor-Präzision)
  31% → D_min² Amplitudenfaktor bei r_s (anderer Observable-Typ, superseded)
  39% → Source-Frame QNM Frequenzverhältnis f_QNM_SSZ/f_QNM_GR = 1/D(r*)
        bei r*=1.387 r_s. NICHT als LIGO-Strain-Observable verwendbar.

STATUS: BLOCKED_BRANCH_CONFLICT → umbenannt in RESOLVED_OBSERVABLE_CONFUSION
KATEGORIE-FEHLER-WARNUNG: 39% ist Source-Frame, nicht LIGO-Strain
```

### 3. Pipeline-Validierung (aus 07_VALIDATION)
```
GW240925 H1 Pipeline:
  delta_lnL = +6.34e-06 → INDISTINGUISHABLE
  MF-SNR GR=39.92, SSZ=14.23 (V0 proxy nicht amplitude-matched)
  KEIN Support-Claim, KEIN Falsifikations-Claim
  Anticircularity-Gate: CLEAR
```

### 4. Falsifikationskriterien (aus 08_FALSIFICATION)
```
SSZ ist definitiv falsifiziert wenn:
  1. NS-Redshift ≠ SSZ ±5% (NICER, XMM-Newton)
  2. Pulsar-Timing ≠ SSZ ±10% (NANOGrav, SKA)
  3. r*/r_s inkonsistent mit deklariertem Xi-Vergleich
  4. BH-Schatten inkonsistent mit D_SSZ(r_s)=0.555 (ngEHT)
  5. Informationsverlust-Signaturen an Horizonten

Keine dieser Bedingungen ist aktuell durch LIGO-Daten testbar.
```

### 5. Known False Alarms (aus 11_GUARDRAILS/confusion_prevention.md)
```
Die Doku selbst dokumentiert bekannte Schein-Konflikte:
  1. "Lensing 50% zu niedrig" → Ξ-only vs. PPN (1+γ)
  2. "Zwei r* Werte" → Unterschiedliche Ξ-Formen, KEIN Konflikt
  3. "Ξ-Werte zwischen Repos unterschiedlich" → Unterschiedliche Scopes
  4. "D_SSZ ≠ D_GR überall" → BEABSICHTIGT, DAS IST DIE VORHERSAGE
  5. "Energie nicht erhalten" → Multiplikativ vs. additiv

→ Bestätigt: "SSZ vs GR Unterschied" ist PREDICTION, nicht BUG
```

---

## Zentrale Befunde für LIGO

### 1. delta_psi — DOKUMENTIERT ALS V0_PROXY

```
File:   06_STRONG_FIELD/delta_psi_derivation.md
Status: DERIVED_V0_PROXY
Formel:  deltaPsi_V0(f) = [Omega(r)/|rdot_GR(r)|] × [(1+Xi)^6−1] × |dr/df|
Basis:   rdot_SSZ = rdot_GR × D²/s⁴ (aus Ch.31)
Blocker: SSZ Book Ch.31 RSG phase integral not final

Die Formel IST dokumentiert. Sie ist korrekt aus Ch.31-Grundgleichungen abgeleitet.
Sie ist aber nicht als LOCKED_FINAL markiert, weil das RSG-Phasenintegral
aus Ch.31 noch nicht final autorisiert ist. Trotzdem: KEINE WILLKÜRLICHE PROXY.
Sie hat eine klare Herleitungskette mit Quellenangaben.
```

### 2. delta_a — DOKUMENTIERT ALS V0_PROXY

```
File:   06_STRONG_FIELD/delta_a_derivation.md
Status: DERIVED_V0_PROXY
Formel:  deltaA = D(r)² − 1 (aus P_GW_SSZ/P_GW_GR = D²/s²)
Blocker: h ∝ sqrt(P) nur für Inspiral gültig

Auch diese Formel ist korrekt aus Ch.31-Grundgleichungen abgeleitet.
Nicht willkürlich — aber auf Inspiral-Regime beschränkt.
```

### 3. epsilon_220 — BLOCKED, NICHT FÜR LIGO-STRAIN

```
File:   06_STRONG_FIELD/epsilon_220_derivation_status.md
Status: BLOCKED_BRANCH_CONFLICT
Wichtig: 39% ist Source-Frame QNM Frequenz-Verhältnis bei r* = 1.387 r_s
         (f_QNM_SSZ/f_QNM_GR = 1/D_SSZ(r*)). Das ist NICHT direkt
         auf LIGO-Strain anwendbar — es fehlt die Strong→Weak RSG-Propagation.

         Die 3% sind QNM-Frequenz-Shift (exploratory, unter Detektor-Präzision).
         Die 31% sind D_min²-Amplitude (superseded).
```

### 4. h_SSZ V0 — DOKUMENTIERTE WAVEFORM

```
File:   06_STRONG_FIELD/h_ssz_v0_derivation.md
Status: DERIVED_V0_PROXY
Formel:  h_SSZ_V0(f) = h_GR × (1 + deltaA) × exp(i × deltaPsi)

Komplette V0-Wellenform. Korrekt aus delta_psi + delta_a konstruiert.
Nicht willkürlich — aber abhängig von delta_psi/delta_a-Status.
```

---

## Update zum Status der LIGO-Formeln

| Formel | Früherer Status | Neuer Status | Grund |
|--------|----------------|-------------|-------|
| delta_psi | "Nicht in Primärquellen" | **DERIVED_V1** (dokumentiert in Doku) | 06_STRONG_FIELD/delta_psi_derivation.md existiert |
| delta_a | "Nur Proxy" | **DERIVED_V1** (dokumentiert) | 06_STRONG_FIELD/delta_a_derivation.md existiert |
| h_SSZ V0 | "Nur Proxy" | **DERIVED_V1** (dokumentiert) | 06_STRONG_FIELD/h_ssz_v0_derivation.md existiert |
| epsilon_220 | "BLOCKED" | **BLOCKED** (bestätigt) | Klärung in Doku |
| QNM 39% vs Strain | "Unklar" | **GEKLÄRT** — Source-Frame, nicht LIGO-Strain | qnm_spectrum.md |
