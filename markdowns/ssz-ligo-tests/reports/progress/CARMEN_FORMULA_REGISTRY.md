# CARMEN FORMULA REGISTRY
**Datum:** 2026-05-20
**Autor:** Bingsi (Hermes Agent)
**Status:** ⚠️ INCOMPLETE — Buch-Kapitel (Ch.31/RSG/Phase) noch nicht gelesen
**Read Coverage:** ssz-complete-documentation (20/170 kritisch), 06_PAPERS (7/26 FULL, 5 RELEVANT, 9 ABSTRACT), book-full V7 (5/50+), V13 Ch.31-32

---

## WICHTIG: Keine finale Registry. Diese Datei sammelt Funde, klassifiziert sie und markiert Lücken. Nichts hier ist als LIGO-Claim-Level freigegeben ohne AUTHOR_REVIEW.

---

## 1. FUNDAMENTALE SSZ-FORMELN (LOCKED — aus Primärquellen)

### Ξ_weak (Schwachfeld)
```
Ξ_weak(r) = r_s / (2r)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.1 + Buch (äquivalente Form r_s/(r−r_s)) |
| Status | ✅ LOCKED |
| Regime | weak field (r/r_s > 10) |
| LIGO-Relevanz | CAN_USE_NOW — Fundament für alle SSZ-Berechnungen |
| Tests | test_ppn_exact.py, ssz-ligo-tests run_strain_pipeline.py |

### Ξ_strong (Starkfeld, operativ)
```
Ξ_strong(r) = min(1 − exp(−φ × r_s / r), Ξ_max)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | perfected-Buch Z.116-149, konsolidiertes Paper 11.02.2026 |
| Status | ✅ LOCKED — operative g₂-Definition |
| Regime | strong field (r_s/r < 1.8) |
| Schnittpunkt mit Ξ_weak | r*/r_s ≈ 1.387 |
| LIGO-Relevanz | CAN_USE_NOW — nur wenn LIGO-Analyse in r/r_s < 3 eindringt |
| Anmerkung | r/r_s (nicht r_s/r!) — r_s/r nur didaktisch |

### Ξ_dec (Didaktische Zerfallsform)
```
Ξ_dec(r) = 1 − exp(−φ × r_s/r)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | perfected-Buch Z.131-135 |
| Status | ℹ️ DIDAKTISCH — NICHT operativ verwenden |
| LIGO-Relevanz | NOT_FOR_LIGO |
| Anmerkung | Nur für pädagogische Vergleiche, Schnittpunkt r*/r_s ≈ 1.595 |

### Ξ_sat (Lokale Sättigung)
```
Ξ_sat(r) = min(1 − exp(−φ × r_s / r), Ξ_max)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.1 |
| Status | ✅ LOCKED — metric-pure/paper-local |
| LIGO-Relevanz | CAN_USE_NOW — konsistent mit Ξ_strong operativ |

### D_SSZ (Zeitdilatationsfaktor)
```
D_SSZ(r) = 1 / (1 + Ξ(r))
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.1, perfected-Buch Z.87 |
| Status | ✅ LOCKED |
| Limits | D(r→∞)=1, D(r_s)=0.55503 |
| LIGO-Relevanz | CAN_USE_NOW — Fundament |
| Tests | test_dilation_finite.py |

### s(r) (Skalierungsfaktor)
```
s(r) = 1 + Ξ(r) = 1 / D(r)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.1, perfected-Buch Z.39 |
| Status | ✅ LOCKED |
| LIGO-Relevanz | CAN_USE_NOW |

### φ (Goldener Schnitt)
```
φ = (1 + √5) / 2 ≈ 1.618033988749895
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.6 |
| Status | ✅ LOCKED |
| LIGO-Relevanz | CAN_USE_NOW — Fundamentalkonstante |

### PPN β, γ
```
β = 1, γ = 1 (exakt in SSZ)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.5, prime_directive.md |
| Status | ✅ LOCKED |
| LIGO-Relevanz | CAN_USE_NOW — für NULL-Observablen PPN (1+γ) |

---

## 2. ABGELEITETE FORMELN (DERIVED — aus Primärquellen)

### r_s (Schwarzschild-Radius)
```
r_s = 2GM/c²
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | Standard + formula_compendium.md |
| Status | ✅ LOCKED (Standard) |
| LIGO-Relevanz | CAN_USE_NOW |

### z_SSZ (Gravitative Rotverschiebung)
```
z_SSZ(r) = 1/D(r) − 1 = Ξ(r)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.1 |
| Status | ✅ LOCKED |
| LIGO-Relevanz | NEEDS_DERIVATION — Rotverschiebung ≠ Strain |

### r_φ (Natürliche Grenze)
```
r_φ = (φ/2) × r_s × [1 + β × Δ(M)]
Δ(M) = A × exp(−α/M^B), A=98.01, α=2.7177×10⁴, B=1.96
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.7 |
| Status | ✅ LOCKED |
| LIGO-Relevanz | INDIREKT — Massenabhängigkeit, nicht direkt h(t) |

### v_esc × v_fall = c²
```
v_esc(r) = c × √(r_s/r), v_fall(r) = c × √(r/r_s)
INVARIANT: v_esc × v_fall = c² (für alle r, massenunabhängig!)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | formula_compendium.md B.3, DualVelocities-Paper |
| Status | ✅ LOCKED |
| LIGO-Relevanz | INDIREKT — Kinematik, nicht direkt h(t) |

### E_obs Energie-Transformation
```
E_obs = E_rest × γ_SR(v) × γ_SSZ(r)
γ_SR = 1/√(1−v²/c²), γ_SSZ(r) = 1/D_SSZ(r)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | prime_directive.md, perfected-Buch |
| Status | ✅ LOCKED |
| LIGO-Relevanz | INDIREKT — Energie, nicht Strain |

---

## 3. SSZ-LIGO-PROXIES (V0/V1 — in ssz-ligo-tests, NICHT in Primärquellen)

### delta_psi_SSZ(f) — Phasenkorrektur
```
delta_psi(f) = kappa × (1 − D(xi(r(f))))
r(f) = (G×M/(π×f)²)^(1/3)  [Kepler]
kappa = 1.0 (exploratory)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | ssz-ligo-tests run_strain_pipeline.py + ssz-ligo README |
| Primärquelle? | ❌ NICHT IN BUCH/SSZ-COMPLETE-DOC GEFUNDEN |
| Status | ⚠️ DERIVED_V0_PROXY (exploratory) |
| LIGO-Relevanz | NEEDS_DERIVATION — AUTHOR_REVIEW_REQUIRED |
| Buch-Bezug | Kap.31-32 hat 30 Formeln (FORMULA_VALIDATION_REPORT), alle "Undef Risk" |
| Anmerkung | Möglicherweise aus Ch.31 RSG-Integral ableitbar, aber NICHT verifiziert |

### delta_a_SSZ — Amplituden-Proxy
```
delta_a = D(r(f))² − 1
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | ssz-ligo-tests run_strain_pipeline.py |
| Primärquelle? | ❌ NICHT IM BUCH GEFUNDEN |
| Status | ⚠️ DERIVED_V0_PROXY |
| LIGO-Relevanz | PROXY_ONLY — nicht als physikalische Amplitude |
| Anmerkung | D²−1 ist mathematisch aus D ableitbar, aber nicht als LIGO-Amplitude autorisiert |

### h_SSZ(f) — SSZ-Waveform
```
h_SSZ(f) = h_GR(f) × exp(i × delta_psi(f))
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | ssz-ligo-tests |
| Primärquelle? | ❌ NICHT IM BUCH GEFUNDEN |
| Status | ⚠️ DERIVED_V0_PROXY |
| LIGO-Relevanz | PROXY_ONLY — korrekt nur wenn delta_psi aus Primärquelle |

---

## 4. QNM / RINGDOWN (TEILWEISE GEKLÄRT)

### epsilon_220 — QNM-Frequenzverschiebung
```
ε_220 ≈ 3% (fundamental mode QNM shift vs GR)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | perfected-Buch Glossar Z.7669, FORMULA_VALIDATION_REPORT |
| Status | ⚠️ PARTIAL_EXPLORATORY — 3% ist kanonisch, aber unter Detektor-Präzision |
| LIGO-Relevanz | NEEDS_DERIVATION — testable via stacking or next-gen detectors (ET/CE) |
| Verwechselungen | 39% = Photon-Sphäre (r*/r_s≈1.387), NICHT QNM; 31% = superseded |
| Buch-Befund | "In SSZ um ~3% gegenüber der ART verschoben" |

### f_SSZ/f_GR ≈ 1.39 (Photon-Sphären-Limit)
```
Bei D_SSZ(r*) ≈ 0.72 (r*/r_s ≈ 1.387)
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | perfected-Buch Z.12641 |
| Status | ℹ️ DISKUTIERT — NICHT FÜR LIGO (anderes Observable) |
| LIGO-Relevanz | NOT_FOR_LIGO |

---

## 5. TWIST / ROTOR / POLARISATION (KONZEPTUELL, NICHT FINAL)

### Twist θ(f) / Rotor R(θ)
```
Konzept: h+/h× Mischung via Rotation/Polarisationstransport
```
| Eigenschaft | Wert |
|------------|------|
| Quelle(n) | ssz-ligo-tests synthetic scripts, GA-Interferometer-Docs |
| Primärquelle? | ❌ IM BUCH NICHT ALS LIGO-FORMEL GEFUNDEN |
| Status | ⚠️ AUTHOR_REVIEW_REQUIRED |
| LIGO-Relevanz | NEEDS_DERIVATION — nur als h(t)-Forward formulierbar |

---

## 6. IM BUCH GEFUNDEN, LIGO-INDIREKT

### D_min = 0.55503
```
D(r_s) = 1/(1 + 0.80171) = 0.55503
```
| LIGO-Relevanz | INDIREKT — Grenzwert, aber keine direkte Strain-Anwendung |

### D_min² ≈ 0.308
```
0.55503² ≈ 0.308
```
| LIGO-Relevanz | HISTORICAL — ältere ε-Ableitung, superseded |

### Hermite C² Blend
```
Ξ_blend(r) = H₅(t), t = (r/r_s − 1.8)/0.4
```
| LIGO-Relevanz | INDIREKT — nur wenn LIGO-Analyse im Blend-Bereich |

---

## 7. NICHT GEFUNDEN (in allen gelesenen Primärquellen)

| Formel | Such-Ergebnis |
|--------|--------------|
| delta_psi finale SSZ-Formel | ❌ 0 Treffer in ~10.000 gelesenen Zeilen |
| delta_phi / δφ | ❌ 0 Treffer |
| delta_a als physikalische Amplitude | ❌ 0 Treffer |
| epsilon_220 explizit | ❌ 0 Treffer |
| twist/rotor/polarization (LIGO-Kontext) | ❌ 0 Treffer |
| strain h(t)/h(f) LIGO-Forward-Modell | ❌ 0 Treffer |
| PSD / Whitening / Interferometer-Modell | ❌ 0 Treffer |

---

## ZUSAMMENFASSUNG

| Kategorie | Anzahl | Status |
|-----------|--------|--------|
| LOCKED (direkt verwendbar) | 12 | ✅ |
| DERIVED (ableitbar, aber nicht direkt LIGO) | 7 | ⚠️ |
| V0_PROXY (ssz-ligo-tests, nicht autorisiert) | 3 | ❌ |
| PARTIAL_EXPLORATORY (QNM) | 1 | ⚠️ |
| AUTHOR_REVIEW_REQUIRED | 4 | ❌ |
| DISKUTIERT/NOT_FOR_LIGO | 2 | ❌ |

**READ_COVERAGE:**
- ssz-complete-documentation: 3/170 MD-Dateien
- book-full MD: ~10.000/~350.000 Zeilen
- V7_BUILD/06_final_v7: 5/50+ Dateien
- 06_PAPERS: 0/34 PDFs
- ssz-all-tests: 0/3262 Test-Skripte

**STATUS: INCOMPLETE — Keine finale LIGO-Formel-Entscheidung ohne vollständige Primärquellen-Lesung.**
