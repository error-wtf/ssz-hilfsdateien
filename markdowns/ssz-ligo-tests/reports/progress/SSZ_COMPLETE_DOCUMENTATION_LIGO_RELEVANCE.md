# SSZ Complete Documentation — LIGO-Relevance Map
**Datum:** 2026-05-20
**Read Coverage:** 29/170 files in detail; 141 files inventoried

---

## FUNDAMENTAL (LOCKED — CAN_USE_NOW für LIGO)

| Formel | Wert/Gleichung | Quelle(n) | LIGO-Relevanz |
|--------|---------------|-----------|---------------|
| Ξ_weak(r) | r_s/(2r) | formula_compendium.md §A.2 | Fundament aller SSZ-Berechnungen |
| Ξ_strong(r) | min(1−exp(−φ×r_s / r), Ξ_max) | formula_compendium.md §A.3 | Starkfeld, r_s/r < 1.8 |
| D_SSZ(r) | 1/(1+Ξ(r)) | formula_compendium.md §A | Zeitdilatation |
| s(r) | 1+Ξ(r) = 1/D(r) | scaling_factor.md | Skalierungsfaktor |
| Ξ_max | 0.80171 | special_values.md | Sättigung bei r=r_s |
| D_min | 0.55503 | special_values.md | Minimale Zeitdilatation (endlich!) |
| r_s | 2GM/c² | Standard | Schwarzschild-Radius |
| φ | 1.618033988749895 | special_values.md | Goldener Schnitt |
| PPN β=γ=1 | Exakte GR-Übereinstimmung | ppn_formulas.md | Schwachfeld=GR |
| g_tt = −D²(r) | Metric-Tensor-Komponente | black_hole_metric.md | SSZ-Metrik |
| g_rr = s²(r) | Metric-Tensor-Komponente | black_hole_metric.md | SSZ-Metrik |
| Blend-Zone | Hermite C² bei 1.8−2.2 r_s | regime_definitions.md | Stetiger Übergang |

---

## DERIVED_V1 (DOKUMENTIERT — NICHT LOCKED für LIGO Claim)

| Formel | Wert/Gleichung | Quelle | Blocker |
|--------|---------------|--------|---------|
| delta_psi_SSZ(f) | [Ω(r)/|rdot_GR|] × [(1+Ξ)⁶−1] × |dr/df| | 06_STRONG_FIELD/delta_psi_derivation.md | Ch.31 RSG Phasenintegral |
| delta_a = D²−1 | D(r)² − 1 ∈ (-1, 0] | 06_STRONG_FIELD/delta_a_derivation.md | h ∝ √P nur Inspiral |
| h_SSZ_V0(f) | h_GR × (1+δA) × exp(i×δψ) | 06_STRONG_FIELD/h_ssz_v0_derivation.md | Abhängig von δψ/δA |
| rdot_SSZ | rdot_GR × D²/s⁴ = rdot_GR/s⁶ | formula_compendium.md §C.1 + delta_psi_derivation | Teil von Ch.31 |
| P_GW_SSZ | P_GW_GR × D²/s² | formula_compendium.md §B.4 | Teil von Ch.31 |

**Herleitungskette nachvollziehbar:** rdot_SSZ aus Ch.31 → delta_psi aus Phasenakkumulation → delta_a aus P_GW-Ratio → h_SSZ aus beiden. Alle dokumentiert in `06_STRONG_FIELD/`.

---

## RESOLVED_OBSERVABLE_CONFUSION (KEIN THEORIEKONFLIKT)

| Label | Wert | Tatsächliche Observable | LIGO-Strain-Nutzung |
|-------|------|------------------------|---------------------|
| "epsilon_220 39%" | 1/D(r*) = 1.39 | Source-Frame QNM-Frequenzverhältnis bei r*=1.387r_s | ❌ NICHT als Strain-Amplitude/Frequenz verwendbar |
| "epsilon_220 3%" | 0.03 | QNM-Frequenz-Shift (exploratorisch) | ❌ Unter Detektor-Präzision |
| "epsilon_220 31%" | D_min² = 0.308 | Amplitudenfaktor bei r_s | ❌ Superseded, anderer Observable-Typ |

**Klärung aus Doku:** `epsilon_220_derivation_status.md` + `qnm_spectrum.md` + `ligo_physics_clarification.md`:
- Die drei Werte sind verschiedene physikalische Größen, die fälschlich alle als "epsilon_220" bezeichnet wurden
- 39% = 1/D(r*) ist ein SOURCE-FRAME-Frequenzverhältnis; für LIGO-Strain fehlt Strong→Weak RSG-Propagation
- Dies ist eine OBSERVABLE-CLASS CONFUSION, kein Theoriebruch
- STATUS: RESOLVED — nicht BLOCKED, sondern KLASSIFIZIERT

---

## FALSIFIKATIONSKRITERIEN (NICHT DURCH LIGO TESTBAR)

| Kriterium | Instrument | Zeitrahmen |
|-----------|-----------|------------|
| NS-Redshift ≠ SSZ ±5% | NICER, XMM-Newton | 2025-2027 |
| Pulsar-Timing ≠ SSZ ±10% | NANOGrav, SKA | 2025-2028 |
| r*/r_s inkonsistent | Multi-Objekt NS | Ongoing |
| BH-Schatten ≠ D(r_s)=0.555 | ngEHT | 2028-2030 |
| Informationsverlust an Horizonten | — | — |

Aktuell testet LIGO keine dieser Bedingungen.

---

## METHOD-ASSIGNMENT (CRITICAL für LIGO)

| Observable | Methode | Formula |
|-----------|---------|---------|
| Zeitdilatation/Redshift (timelike) | Ξ | D = 1/(1+Ξ), z = Ξ |
| Lensing/Shapiro (null/light) | PPN | α = (1+γ)r_s/b = 2r_s/b |
| Orbit (timelike) | PPN | Δω = 6πGM/[a(1-e²)c²] |
| GW-Strain (h(t)/h(f)) | ??? | NOCH NICHT METHOD-ASSIGNED |
| GW-Phase (delta_psi) | ??? | DERIVED_V1 aus Ch.31 |

GW-Strain und GW-Phase sind in `method_assignment.md` NICHT zugewiesen. Das ist für LIGO eine offene methodologische Frage.
