# NEXT PHYSICS DERIVATION TASKS

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18
Status: OPEN — prioritized derivation agenda

---

## Ausgangslage

Der Exploratory-V0-Pipeline-Lauf hat keine großen Unterschiede zum GR-Template erzeugt.
Das ist kein Ergebnis — es ist ein Hinweis auf die Lücken.
Diese Datei listet, was als nächstes deriviert und gelocked werden muss.

---

## Prioritätsliste

### P1 — δΨ_SSZ(f): Von V0-Proxy zur abgeleiteten Formel

**Aktueller Stand:** V0-Proxy mit kappa=1.0 (exploratorisch, nicht deriviert).
Formel: `dPsi ≈ kappa * (1 - D(r(f)))` — kappa ist nicht aus Quellen.

**Was fehlt:**
- Exaktes RSG-Phasenintegral aus SSZ Book Ch.31
- Ableitung: `dPsi = integral [1/D(r') - 1] * Omega(r') / rdot_GR(r') dr'`
  mit `rdot_SSZ = rdot_GR * D²/s⁴` (locked: formula_compendium §C.1)
- Dimensionscheck: [rad] ✓ (bereits verifiziert für V0-Proxy)
- Regime: LIGO-Band (20–800 Hz) ist schwaches Feld (r/rs >> 1)
  → Xi_weak = rs/(2r) → D ≈ 1 − rs/(2r) → dPsi sehr klein. ERWARTBAR.

**Blocker:** SSZ Book Ch.31 RSG-Phasenintegral noch nicht final gelocked.

**Schritt:** Author-Decision einholen, Ch.31-Formel locken, kappa eliminieren.

---

### P2 — δA_SSZ(f): Dimensionsprüfung und Physik-Begründung

**Aktueller Stand:** `deltaA = D(r(f))² − 1` aus P_GW-Verhältnis (§B.4).
Bereich: ∈ (−1, 0]. Im LIGO-Band: ca. −0.06 bis −0.69.

**Was fehlt:**
- Vollständige Ableitung von P_GW_SSZ/P_GW_GR = D²/s²
- Warum geht D² in die Amplitude und s² in den Nenner? — Quellbelegung vollständig?
- Dimensionscheck P_GW: [W] → Amplitude ∝ √(P_GW) → deltaA ∝ D/s − 1 (Alternative?)
- Klärung: Ist P_GW-Verhältnis der richtige Observable für h(f)-Amplitude?

**Schritt:** Vollständige Herleitung von h_SSZ/h_GR aus Strahlungsleistung dokumentieren.

---

### P3 — Xi_strong-Branch: saturation vs decay — FINAL LOCK

**Aktueller Stand:** g2_decay = `1 − exp(−φ·rs/r)` operativ per FORMULA_BRANCH_LOCK.md.
g1_saturation nicht verwendet.

**Was fehlt:**
- Explizite Begründung: Warum g2_decay für LIGO-Inspiral-Band?
- Im LIGO-Band ist r/rs >> 1 → beide Formeln → Xi_weak (identisch)
- Im Ringdown-Band: r/rs ≈ 1–3 → Xi_strong relevant → hier unterscheiden sie sich!
- Author muss entscheiden: Welcher Branch gilt für Ringdown-Emission?

**Schritt:** Author-Decision. Branch-Lock-Datei mit expliziter Begründung erweitern.

---

### P4 — Regime-Grenzen: 1.8 rs vs 10 rs — FINAL LOCK

**Aktueller Stand:** FORMULA_BRANCH_LOCK.md: BLEND_START = 1.8 rs, BLEND_END = 2.2 rs.

**Was fehlt:**
- Die meisten SSZ-Dokumente nennen verschiedene Blend-Grenzen (1.8, 2.2, 10 rs)
- Im CONSISTENCY_REPORT wird 10 rs in einigen Texten erwähnt
- Welche Grenze gilt für welches Observable? Inspiral ≠ Ringdown ≠ Strong-field
- Hermite-C²-Blend: korrekte Implementierung verifizieren

**Schritt:** Author-Decision über Regime-Grenzen für jeden Observable-Typ separat.

---

### P5 — ε220-Ast klären: 3%, 31%, 39%

**Aktueller Stand:** BLOCKED_BRANCH_CONFLICT. Drei Quellen, drei verschiedene Observablen.

| Wert | Quelle | Observable |
|------|--------|------------|
| 3% | SSZ Book V51 Ch.30 | QNM-Frequenzshift (exploratorisch) |
| 31% | formula_compendium §B.7 (D_min²) | Amplitudendämpfung bei rs |
| 39% | qnm_spectrum.md (r*=1.387 rs) | f_QNM_SSZ/f_QNM_GR Quell-Frame |

**Was fehlt:**
- Author muss explizit entscheiden: Welcher Wert gilt als kanonischer ε220?
- Oder: Alle drei sind verschiedene Observablen → verschiedene Namen!
- Für LIGO-Strain: Welcher Wert ist der richtige h(f)-Ringdown-Parameter?

**Schritt:** Author-Decision. Bis dahin: BLOCKED in allen Claims.

---

### P6 — GR-Control durch dokumentiertes analytisches Template ersetzen/begrenzen

**Aktueller Stand:** TaylorF2 0PN — kein Spin, kein Merger, kein Ringdown.

**Was fehlt:**
- Für echten SSZ-LIGO-Test: vollständiges IMR-Template als GR-Referenz
- Alternativen: IMRPhenomD, SEOBNRv4 — aber: Posterior-basierten Templates vermeiden
- Oder: Den Gültigkeitsbereich des Tests explizit begrenzen auf den 0PN-Inspiral-Bereich

**Schritt:** Entweder IMR-Template einbauen (analytisch, nicht PE-basiert)
oder den 0PN-Bereich explizit in allen Reports als Einschränkung festhalten.

---

### P7 — Kalibrations- und PSD-Sensitivitätstest

**Aktueller Stand:** Welch-PSD aus off-source Rohstrain. Keine Kalibrations-Unsicherheit.

**Was fehlt:**
- LIGO-Kalibrierung hat ~3–5% Amplituden- und Phasen-Unsicherheit im Band
- Ein SSZ-Signal mit dPsi ≈ 0.06–10 rad könnte durch Kalibrierungsfehler maskiert sein
- Sensitivitätstest: Wie viel muss dPsi sein, damit es über Kalibrierung nachweisbar ist?

**Schritt:** Kalibrations-Envelope-Modell einbauen (aus GWOSC-Kalibrations-Files).

---

### P8 — H1/L1-Kohärenztest vorbereiten

**Aktueller Stand:** Nur H1 analysiert.

**Was fehlt:**
- Echter SSZ-Test: Signal müsste in H1 UND L1 kohärent erscheinen
- L1-Strain für GW240925 ebenfalls verfügbar (GWOSC O4b)
- Cross-Korrelation H1↔L1: eliminiert Detektor-spezifische Artefakte

**Schritt:** L1-HDF5 laden, gleiche Pipeline anwenden, Kohärenzmaß berechnen.

---

### P9 — Anti-Posterior-Firewall dokumentieren und testen

**Aktueller Stand:** Posterior-Daten explizit geblockt in pipeline.

**Was fehlt:**
- Formaler Test: Pipeline-Run schlägt FEHL wenn Posterior-Input erkannt wird
- Aktuell: nur manuell geprüft (keine programmatische Sperre)

**Schritt:** Automatischen Posterior-Detektor im Pipeline-Eingang implementieren.
Test: gibt `ANTI_CIRCULARITY_GATE: FAIL` zurück wenn Posterior erkannt.

---

## Prioritätsmatrix

| Task | Blockiert Claim? | Aufwand | Nächste Aktion |
|------|-----------------|---------|----------------|
| P1: δΨ exact | JA | Author | Ch.31 locken |
| P2: δA Begründung | TEILWEISE | Mittel | Ableitung vervollständigen |
| P3: Xi-Branch | JA (Ringdown) | Author | Branch-Entscheidung |
| P4: Regime-Grenzen | TEILWEISE | Author | Grenzen pro Observable |
| P5: ε220 | JA (Ringdown) | Author | Kanonischen Wert wählen |
| P6: GR-Control | TEILWEISE | Mittel | IMR oder Scope begrenzen |
| P7: Kalibrierung | TEILWEISE | Mittel | Envelope-Modell |
| P8: H1/L1 | JA (echte Verifikation) | Mittel | L1-Daten laden |
| P9: Anti-Posterior-Firewall | PROZESS | Klein | Automatischen Test |

---

## Was dieser Report NICHT ist

- KEIN Physics-Claim
- KEIN Beweis dass P1–P9 lösbar sind
- KEIN Versprechen dass nach P1–P9 ein SSZ-LIGO-Claim möglich ist

Es ist eine Agenda zur **Minimierung der offenen Derivations-Lücken**.
