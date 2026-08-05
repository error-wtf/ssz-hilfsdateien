# GW-Strain Method Assignment — Ch.31 Auswertung
**Datum:** 2026-05-20
**Buch-Quelle:** SSZ_BOOK_EN_PERFECTED.md, Ch.31–32 (Zeilen 18540–19000)

---

## FUND: P_GW_SSZ und rdot_SSZ sind autorisiert

In Ch.31, Abschnitt "Metric Perturbations in the Lagrangian Formalism" (Z.18692–18705):

```
P_GW_SSZ = P_GW_GR × D(r)²/s(r)²              [Z.18696]
rdot_SSZ  = rdot_GR  × D(r)²/s(r)⁴            [Z.18700]
```

Das sind die EXAKTEN Quellgleichungen, die in `delta_psi_derivation.md` und
`delta_a_derivation.md` als Herleitungsbasis verwendet werden.

**→ DERIVED_V1 bestätigt: Die Herleitungskette in ssz-ligo-tests ist korrekt.**

---

## KEIN FIND: Explizite h_SSZ(t) oder h_SSZ(f) Formel

Ch.31 enthält KEINE explizite Gravitationswellen-Wellenform. Es gibt:
- Quadrupol-Formel (P_GW)
- Inspiral-Dämpfung (rdot)
- Ringdown-Frequenz (f_QNM_SSZ ≈ 1.39 × f_QNM_GR)

Aber: Kein h_SSZ(t), kein h_SSZ(f), keine Strain-Level-Waveform.

Das ist konsistent mit dem DERIVED_V1-Status: Die Bausteine sind autorisiert,
das vollständige Forward-Modell muss daraus abgeleitet werden.

---

## METHOD ASSIGNMENT: GW-Phase

Die Phase wird in Ch.31 NICHT über ein separates RSG-Phasenintegral behandelt.
Stattdessen kommt sie aus:

1. **Lagrangian → Effective Potential → Hamilton-Jacobi**
   ```
   S_r(r) = ∫ s(r)/D(r) × √[E²/(D²c⁴) − L²/(r²s²) − ε/s²] dr   [Z.18677]
   ```
   Das ist der radiale Teil der Hamilton-Jacobi-Wirkung.

2. **Inspiral-Rate → Phasenakkumulation (V0-Proxy)**
   ```
   dphi/dr|_SSZ = Omega(r) / |rdot_SSZ(r)|
   ```
   Das ist die Newtonian-Kepler-Proxymethode aus delta_psi_derivation.md.

Die Hamilton-Jacobi-Phase ist allgemeiner (gilt für alle Orbits, nicht nur
quasi-zirkuläre Inspiral-Phasen). Die V0-Methode ist eine Spezialisierung auf
den quasi-zirkulären Fall mit Kepler-Näherung.

**→ Method Assignment: GW-Phase = HAMILTON-JACOBI (autorisiert)**
**→ V0-Proxy = KEPLER-APPROXIMATION (für quasi-zirkuläre Inspiral-Phase)**

---

## METHOD ASSIGNMENT: GW-Amplitude

Die Amplitude folgt aus:

```
h ∝ √(P_GW)   [quadrupole relation]
A_SSZ/A_GR = D(r)/s(r) = D(r)²   [Z.18696 implizit]
deltaA = D(r)² − 1
```

Das ist in Ch.31 durch die autorisierte P_GW_SSZ-Formel abgesichert.

**→ Method Assignment: GW-Amplitude = QUADRUPOLE_POWER (autorisiert)**

---

## METHOD ASSIGNMENT: GW-Strain (Gesamt)

```
h_SSZ(f) = h_GR × (1 + deltaA) × exp(i × deltaPsi)

mit:
  deltaA    = D(r)² − 1            [QUADRUPOLE_POWER]
  deltaPsi  = Phasendifferenz      [HAMILTON-JACOBI oder KEPLER-APPROX]
  h_GR      = Analytisches GR-Template [TAYLORF2_0PN oder höher]
```

**→ Method Assignment: GW-Strain = QUADRUPOLE_POWER + HAMILTON-JACOBI**

Das ist KONSTRUKTIV — die GW-Strain-Formel ist kein eigenständiger Eintrag in
der Method-Assignment-Tabelle, sondern eine Kombination autorisierter Bausteine.

---

## STATUS DER HERLEITUNGSKETTE

```
P_GW_SSZ (Ch.31 §Metric Perturbations)     → AUTHORIZED_SOURCE ✅
  ↓
deltaA = D² − 1 (algebraic from P_GW)      → DERIVED_FROM_AUTHORIZED_SOURCE ✅
  ↓
rdot_SSZ (Ch.31 §Inspiral)                 → AUTHORIZED_SOURCE ✅
  ↓
deltaPsi (Hamilton-Jacobi or Kepler-Approx) → DERIVED_FROM_AUTHORIZED_SOURCE ✅
  ↓
h_SSZ_V0(f) = h_GR × (1+δA) × exp(i×δψ)   → DERIVED_WAVEFORM ⚠️
```

**DERIVED_WAVEFORM bedeutet:** Die Formel ist aus autorisierten Quellen
abgeleitet, aber nicht als fertige LIGO-Wellenform im Buch abgesegnet.
Das ist der STATUS QUO — und er ist deutlich besser als "nur Proxy".

---

## WAS NOCH FEHLT FÜR LOCKED_FINAL

1. **Hamilton-Jacobi → Kepler-Approximation:** Klären, ob die Kepler-Näherung
   (Newtonian r(f), Omega(r)) für den LIGO-Inspiral-Bereich ausreichend ist
   oder ob das volle Hamilton-Jacobi-Integral nötig ist.

2. **Merger/Ringdown:** Ch.31 enthält nur Inspiral + Ringdown-Frequenz.
   Keine vollständige IMR-Wellenform. Das ist eine strukturelle Lücke,
   die nur durch Autorenentscheidung geschlossen werden kann.

3. **Detektor-Propagation:** Die SSZ-Metrik modifiziert nicht nur die Quelle,
   sondern auch die Propagation zum Detektor. Das fehlt in den aktuellen
   V0/V1-Formeln (wird in `delta_psi_derivation.md` als Blocker genannt).

---

## FAZIT

```
✅ P_GW_SSZ und rdot_SSZ sind in Ch.31 autorisiert
✅ delta_psi und delta_a sind korrekt aus autorisierten Quellen abgeleitet
⚠️ h_SSZ ist DERIVED_WAVEFORM — nicht fertig, aber nachvollziehbar
❌ Keine vollständige IMR-Wellenform im Buch
❌ Keine Detektor-Propagation

Method Assignment für GW-Strain:
  NICHT in method_assignment.md als eigener Eintrag vorhanden
  ABER aus autorisierten Bausteinen rekonstruierbar:
  QUADRUPOLE_POWER + HAMILTON-JACOBI → DERIVED_WAVEFORM
```
