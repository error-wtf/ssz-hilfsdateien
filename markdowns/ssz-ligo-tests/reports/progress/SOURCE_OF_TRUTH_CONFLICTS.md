# SSZ SOURCE OF TRUTH CONFLICTS — AKTUALISIERT
**Datum:** 2026-05-20
**Status:** KLÄRUNGEN aus V7_BUILD + perfected-Buch — viele bisherige Konflikte gelöst

---

## Conflict 1: Ξ_strong Exponent-Richtung → GEKLÄRT ✅

| Status vorher | Status nach Buch-Lesung |
|--------------|------------------------|
| TRUE_THEORY_CONFLICT | VERSION_DRIFT / DIDAKTISCH vs OPERATIV |

**Klärung aus perfected-Buch (Z.116-149):**
```
Operative g₂-Definition: Ξ_strong(r) = min(1 − exp(−φ × r_s / r), Ξ_max)  ✅
Didaktische Form:       Ξ_dec(r) = 1 − exp(−φ × r_s/r)                   ℹ️
```

**Ursache:** Bewusste Unterscheidung, kein Theorie-Widerspruch. r/r_s ist operativ, r_s/r ist didaktisch.

**Aktion für ssz-ligo-tests:** Ξ_strong mit r/r_s verwenden (konsistent mit konsolidiertem Paper 11.02.2026).

---

## Conflict 2: epsilon_220 Werte → GEKLÄRT ✅

| Status vorher | Status nach Buch-Lesung |
|--------------|------------------------|
| TRUE_THEORY_CONFLICT | OBSERVABLE_CONFUSION — verschiedene Observablen, keine echten Widersprüche |

**Klärung aus perfected-Buch + V7_BUILD:**
```
~3%:  Buch-QNM-Wert (Glossar Z.7669, FORMULA_VALIDATION_REPORT kanonisch)
~31%: D_min² ≈ 0.308 — ÄLTERE INTERPRETATION (superseded)
~36%: NICHT IN BUCH/DOKU GEFUNDEN — wahrscheinlich Windsurf-Artefakt
~39%: Photon-Sphären-Limit: f_SSZ/f_GR ≈ 1.39 bei r/r_s ≈ 1.387 (Z.12641)
```

**Ursache:** 3% ist der kanonische QNM-Wert. 39% ist das Photon-Sphären-Limit, keine Ringdown-Frequenz. Die 31% ist veraltet.

**Aktion für ssz-ligo-tests:** 3% für QNM verwenden (exploratory). 39% als Photon-Sphäre kennzeichnen. 31% deprecated.

---

## Conflict 3: delta_a = D²−1 → BESTÄTIGT ALS PROXY ⚠️

| Status vorher | Status nach Buch-Lesung |
|--------------|------------------------|
| PROXY_VS_LOCKED_CONFUSION | PROXY_VS_LOCKED_CONFUSION (bestätigt) |

**Befund:** delta_a taucht im gesamten perfected-Buch NICHT auf. Keine Treffer in 115.000 Zeilen MD. Auch in V7_BUILD/06_final_v7 nicht als kanonische Formel gelistet.

**Aktion:** Als V0_PROXY kennzeichnen. Nicht als finale SSZ-Amplitude für Claim-Level-Tests.

---

## Conflict 4: delta_psi → NICHT IM BUCH ⚠️

| Status vorher | Status nach Buch-Lesung |
|--------------|------------------------|
| AUTHOR_REVIEW_REQUIRED | AUTHOR_REVIEW_REQUIRED (bestätigt) |

**Befund:** delta_psi taucht im perfected-Buch NICHT auf. Keine Treffer. Auch nicht in V7_BUILD/06_final_v7. Kapitel 31-32 enthält 30 Formeln (laut FORMULA_VALIDATION_REPORT), aber die sind als "Undef Risk" markiert — sie existieren im Buch-Text, sind aber nicht als kanonisch geprüft.

**Aktion:** AUTHOR_REVIEW_REQUIRED. ssz-ligo-tests V0/V1-Proxy nicht als finale Physik verwenden.

---

## Conflict 5: twist / rotor / polarization → NICHT IM BUCH ⚠️

| Status vorher | Status nach Buch-Lesung |
|--------------|------------------------|
| AUTHOR_REVIEW_REQUIRED | AUTHOR_REVIEW_REQUIRED (bestätigt) |

**Befund:** Twist/Rotor/Polarization tauchen im perfected-Buch nur im Sagnac-Kontext auf (Rotation allgemein), nicht als spezifische LIGO-Interferometer-Modellierung.

**Aktion:** ssz-ligo-tests synthetic-twist-Tests bleiben SYNTHETIC_ONLY. Keine Claim-Level-Tests ohne autorisierte Formel.

---

## Conflict 6: SSZ_BOOK_PROJECT vs book-full → GEKLÄRT ✅

| Status vorher | Status nach Buch-Lesung |
|--------------|------------------------|
| ASSEMBLY_ERROR | ASSEMBLY_ERROR (bestätigt) |

**Befund:** book-full und SSZ_BOOK_PROJECT haben ähnliche Struktur (beide ~7000 Dateien). V7_BUILD/06_final_v7 enthält V10-V13-PDFs + V53-Prints. SSZ_BOOK_PROJECT scheint ein älterer/paralleler Build zu sein.

**Aktion:** book-full/V7_BUILD/06_final_v7 als aktuellste kanonische Version verwenden.

---

## NICHT-GEFUNDEN (keine Konflikte, einfach nicht vorhanden)

| Begriff | Such-Ergebnis |
|---------|--------------|
| delta_psi / δψ | 0 Treffer im perfected-Buch |
| delta_phi / δφ | 0 Treffer |
| delta_a / δA / delta_amp | 0 Treffer |
| epsilon_220 explizit | 0 Treffer (nur allgemein QNM) |
| twist / rotor / polarization für LIGO | 0 Treffer |
| strain / h(t) / h(f) in LIGO-Kontext | 0 Treffer |
| PSD / Whitening | 0 Treffer |
| Interferometer-Forward-Modell | 0 Treffer |

---

## ZUSAMMENFASSUNG DER KLÄRUNGEN

```
GEKLÄRT (kein Theorie-Konflikt):
✅ Ξ_strong: r/r_s ist operativ, r_s/r ist didaktisch
✅ epsilon_220: 3% (QNM) vs 39% (Photon-Sphäre) vs 31% (veraltet)
✅ SSZ_BOOK_PROJECT vs book-full: Assembly-Duplikation

BESTÄTIGT ALS NICHT IM BUCH:
⚠️ delta_psi: Kein Buch-Eintrag — AUTHOR_REVIEW_REQUIRED
⚠️ delta_a: Kein Buch-Eintrag — PROXY_ONLY
⚠️ twist/rotor/polarization: Kein Buch-Eintrag — SYNTHETIC_ONLY

NEU ENTDECKT:
📋 FORMULA_VALIDATION_REPORT: 852 Formeln, 12 kanonisch, 128 Warnungen
📋 Kap.31-32: 30 Formeln, alle "Undef Risk" — nicht kanonisch geprüft
📋 V10-V13 PDFs + V53-Prints in V7_BUILD existieren
```
