# SSZ OBSERVABLE TEST MAP
**Datum:** 2026-05-20
**Phase:** B — Observable-Klassifikation
**Status:** COMPLETE (Inventar-basiert, nicht alle Tests gelesen)

---

## Zentrale Einsicht

```
Frühere SSZ-Tests validieren Formeln in ihren eigenen Observable-Regimen.
Sie ersetzen KEINEN LIGO-spezifischen Strain-Level-Forward-Test.
```

---

## Observable-Regime und LIGO-Relevanz

| Observable-Typ | Was gemessen wird | LIGO-Relevant? | Warum nicht direkt übertragbar |
|---------------|-------------------|----------------|-------------------------------|
| **LIGO_STRAIN** | h(t), h(f), PSD, DQ, H1/L1/V1 | ✅ DIREKT | Strain-Level-Tests |
| **NICER** | Puls-Timing, Neutronenstern-Observable | ❌ NEIN | Andere Observable: Pulsphase ≠ Interferometerphase |
| **ALMA** | Spektrallinien, Rotverschiebung | ❌ NEIN | Spektroskopie ≠ Strain |
| **LENSING** | Lichtablenkung, Shapiro-Delay | ❌ NEIN | Null-Geodäten, PPN (γ=1) |
| **REDSHIFT** | Frequenzverschiebung, Quasar-Spektren | ❌ NEIN | SSZ z=Ξ, aber LIGO misst Strain-Amplitude/-Phase |
| **MASS_PROJECTION** | Massen-Schätzung aus SSZ-Formeln | ❌ NEIN | Massen-Parameter ≠ Strain |
| **TRAJECTORY** | Bahnkurven, orbitale Elemente | ❌ NEIN | Orbital-Parameter ≠ Strain |
| **METRIC_CONSISTENCY** | Ξ, D, s, PPN-Konsistenz | ✅ METHODISCH | Validierung der Grundformeln |
| **SCHUMANN** | Schumann-Resonanz, EM-Feld | ❌ NEIN | Andere Physik (Elektromagnetik) |
| **QUBIT** | Quanten-Kohärenz, Qubit-Timing | ❌ NEIN | Labor-Quanten ≠ LIGO |
| **STARMAP** | Sternpositionen, Astrometrie | ❌ NEIN | Positionsmessung ≠ Strain |
| **FREQUENCY_CURVATURE** | Frequenz-Krümmungs-Relation | ⚠️ INDIREKT | Konzeptuell verwandt, aber nicht LIGO-Strain |
| **INTERFEROMETER_PHASE** | Phase, Armprojektion, Sagnac | ✅ RELEVANT | Braucht LIGO-spezifische Ableitung |

---

## Repos nach Observable-Typ

### LIGO_STRAIN (direkt relevant)
| Repo | Tests | Anmerkung |
|------|-------|-----------|
| ssz-ligo-tests | 1.555 | GW240925 H1/L1/V1, real GWOSC HDF5 |
| ligo-gw240925-gw250207-release | 1.180 | Datenrepo, Extraktions-Skripte |
| gauge-gravitationslinse-quadratur | 6 | LIGO + Lensing-Referenzen |

### METRIC_CONSISTENCY (methodisch relevant)
| Repo | Tests | Fokus |
|------|-------|-------|
| ssz-metric-pure | 7 | Ξ, D, s, PPN-Grundlagen |
| ssz-metric-final | 15 | Metrische Konsistenz, QNM |
| ssz-full-metric | 17 | Vollständige Metrik-Tests |
| ssz-radial-scaling | 5 | RSG, radiale Skalierung |

### ASTROPHYSIK (nicht direkt LIGO-relevant)
| Repo | Tests | Observable |
|------|-------|------------|
| ssz-lensing | 24 | LENSING, REDSHIFT |
| ssz-trajectories | 4 | TRAJECTORY, CURVATURE |
| frequency-curvature-validation | 12 | FREQUENCY, CURVATURE |
| ssz-lagrange | 1 | METRIC, Lagrange-Formalismus |

### MASSEN / PROJEKTION
| Repo | Tests | Observable |
|------|-------|------------|
| Segmented-Spacetime-Mass-Projection-Unified-Results | 2.737 | MASS_PROJECTION |
| segmented-energy | 3 | Energie-Relation |

### SPEZIALGEBIETE
| Repo | Tests | Observable |
|------|-------|------------|
| ssz-schuhman-experiment | 12 | SCHUMANN |
| ssz-qubits | 11 | QUBIT |
| Segmented-Spacetime-StarMaps | 4.307 | STARMAP (größtes Repo) |
| ssz-paper-plots | 6 | Plot-Generierung |

### GENERAL (unspezifisch)
| Repo | Tests | Anmerkung |
|------|-------|-----------|
| ssz-all-tests | 3.262 | Größte Test-Suite — muss Observable analysiert werden |
| ssz-all-tests-run | 352 | Abgeleitet von ssz-all-tests |
| ssz-all-tests-test | 352 | Abgeleitet, Hints: LENSING, SCHUMANN, PPN, TRAJECTORY |

---

## LIGO-Relevanz-Score

| Kategorie | Repo | LIGO-Score |
|-----------|------|------------|
| **DIREKT** | ssz-ligo-tests | 10/10 |
| **DIREKT** | ligo-gw240925-gw250207-release | 9/10 (Daten) |
| **METHODISCH** | ssz-metric-pure | 7/10 |
| **METHODISCH** | ssz-metric-final | 7/10 |
| **METHODISCH** | ssz-full-metric | 7/10 |
| **METHODISCH** | ssz-radial-scaling | 6/10 |
| **INDIREKT** | ssz-all-tests | 4/10 (ohne Detail-Analyse) |
| **INDIREKT** | ssz-lensing | 3/10 |
| **INDIREKT** | frequency-curvature-validation | 3/10 |
| **NICHT** | ssz-schuhman-experiment | 1/10 |
| **NICHT** | ssz-qubits | 1/10 |
| **NICHT** | Segmented-Spacetime-StarMaps | 1/10 |
| **NICHT** | Segmented-Spacetime-Mass-Projection | 2/10 |

---

## Nächste Phase

PHASE C: Formula Coverage Map — welche konkreten SSZ-Formeln wurden in welchen Tests mit welchen Ergebnissen getestet?
