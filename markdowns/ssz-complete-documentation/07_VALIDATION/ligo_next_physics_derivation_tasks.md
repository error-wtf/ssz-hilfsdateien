# LIGO Next Physics Derivation Tasks

**Cross-ref:** `ssz-ligo-tests/reports/NEXT_PHYSICS_DERIVATION_TASKS.md`
**Status:** OPEN — prioritized derivation agenda after 2026-05-18 pipeline run

---

## Prioritätsliste

| # | Task | Claim-Blocker? | Typ | Nächste Aktion |
|---|------|--------------|-----|----------------|
| P1 | deltaPsi_SSZ exact (Ch.31 RSG Integral) | JA | Author | Ch.31 locken |
| P2 | deltaA physikalische Begründung | TEILWEISE | Derivation | h∝sqrt(P) verifizieren |
| P3 | Xi_strong-Branch (saturation vs decay) | JA (Ringdown) | Author | Branch-Entscheidung |
| P4 | Regime-Grenzen pro Observable | TEILWEISE | Author | rs, 1.8rs, 10rs klären |
| P5 | epsilon_220 kanonischer Wert | JA (Ringdown) | Author | Canonical branch wählen |
| P6 | GR-Control IMR vs 0PN | TEILWEISE | Derivation | IMR einbauen oder Scope begrenzen |
| P7 | Kalibrations-Envelope | TEILWEISE | Technical | Envelope-Modell |
| P8 | H1/L1 Kohärenztest | JA (echte Verifikation) | Technical | L1-Daten laden |
| P9 | Anti-Posterior-Firewall automatisch | Prozess | Technical | Automatischen Detektor |

---

## P1 — deltaPsi: Ker-Blocker

kappa=1.0 in der V0-Formel ist **nicht deriviert** — es ist implizit im s^6-Faktor.
Der exakte RSG-Phasenintegral aus Ch.31 muss locked werden:

```
deltaPsi = integral [Omega(r)/rdot_GR * (s^6 - 1)] dr   [V0 proxy]
         → ?   [exact Ch.31 formula]
```

Bis Ch.31 gelocked ist, bleibt deltaPsi DERIVED_V0_PROXY.

---

## P5 — epsilon_220: Drei Werte, drei Observablen

```
3%  → QNM freq shift (exploratorisch, Ch.30)
31% → Amplitudenfaktor bei r_s (anderer Observable-Typ)
39% → Quellframe-QNM-Frequenzverhältnis bei r* (kein LIGO-Strain-Observable)
```

Die 39% brauchen eine Strong→Weak RSG-Propagations-Ableitung,
bevor sie in den LIGO-Strain eingesetzt werden können.

---

## Was dieser Report NICHT ist

- Kein Physics-Claim
- Kein Versprechen dass P1–P9 SSZ beweisen
- Nur: Agenda zur Minimierung offener Derivations-Lücken
