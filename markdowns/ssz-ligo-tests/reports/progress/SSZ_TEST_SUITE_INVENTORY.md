# SSZ TEST SUITE INVENTORY
**Datum:** 2026-05-20
**Phase:** A — Test Suite Inventory (keine Formel-Interpretation)
**Status:** COMPLETE (Inventar, nicht gelesen)

---

## Übersicht

```
35 SSZ-Repos gescannt
14.264 Test-Skripte insgesamt
12 Repos mit pytest-Konfiguration
```

---

## Test-Repos nach Größe

| # | Repo | Tests | Test-Dirs | pytest | Observable-Hints |
|---|------|-------|-----------|--------|-----------------|
| 1 | **Segmented-Spacetime-StarMaps** | 4.307 | 377 | ✅ | METRIC, STARMAP |
| 2 | **ssz-all-tests** | 3.262 | 235 | ✅ | (README nicht gefunden) |
| 3 | **Segmented-Spacetime-Mass-Projection-Unified-Results** | 2.737 | 214 | ✅ | MASS_PROJECTION |
| 4 | **ssz-ligo-tests** | 1.555 | 54 | ✅ | METRIC, LIGO, QNM |
| 5 | **ligo-gw240925-gw250207-release** | 1.180 | 15 | ✅ | (LIGO-Datenrepo) |
| 6 | ssz-all-tests-run | 352 | 1 | ✅ | (keine Hints) |
| 7 | ssz-all-tests-test | 352 | 1 | ✅ | LENSING, SCHUMANN, PPN, TRAJECTORY |
| 8 | book-full | 187 | 17 | ✅ | (Buchbau-Skripte) |
| 9 | SSZ_BOOK_PROJECT | 185 | 16 | ✅ | (Buchbau-Skripte) |
| 10 | segmented-calculation-suite | 24 | 3 | — | (Berechnungssuite) |
| 11 | ssz-lensing | 24 | 2 | — | LENSING, REDSHIFT |
| 12 | ssz-full-metric | 17 | 3 | ✅ | METRIC, QNM |
| 13 | ssz-metric-final | 15 | 3 | ✅ | METRIC, QNM |
| 14 | ssz-schuhman-experiment | 12 | 2 | — | SCHUMANN, FREQUENCY |
| 15 | frequency-curvature-validation | 12 | 1 | — | FREQUENCY, CURVATURE |
| 16 | ssz-qubits | 11 | 2 | — | QUBIT |
| 17 | ssz-metric-pure | 7 | 1 | ✅ | METRIC, MASS_PROJECTION, PPN |
| 18 | ssz-paper-plots | 6 | 2 | — | (keine Hints) |
| 19 | gauge-gravitationslinse-quadratur | 6 | 2 | — | LENSING, LIGO |
| 20 | ssz-radial-scaling | 5 | 1 | — | METRIC |
| 21 | ssz-trajectories | 4 | 1 | ✅ | TRAJECTORY, CURVATURE |
| 22 | segmented-energy | 3 | 0 | ✅ | (keine Hints) |
| 23 | ssz-lagrange | 1 | 0 | — | METRIC |
| 24-35 | 12 weitere Repos | 0 | 0 | — | (Doku/Paper/Historisch) |

---

## Klassifikation

### PRIMÄRE VALIDIERUNG (pytest, viele Tests, echte Daten)

| Repo | Tests | Daten-Typ | Observable |
|------|-------|-----------|------------|
| ssz-all-tests | 3.262 | Mixed (real + synthetic) | Breites Spektrum |
| Segmented-Spacetime-Mass-Projection-Unified-Results | 2.737 | Real (NICER/ALMA-artig) | MASS_PROJECTION |
| ssz-ligo-tests | 1.555 | Real GWOSC HDF5 | LIGO_STRAIN |
| ssz-metric-pure | 7 | Synthetic | METRIC, PPN |
| ssz-full-metric | 17 | Synthetic | METRIC, QNM |
| ssz-metric-final | 15 | Synthetic | METRIC, QNM |

### SEKUNDÄRE VALIDATION (Tests vorhanden, spezifische Observable)

| Repo | Observable |
|------|------------|
| ssz-lensing | LENSING, REDSHIFT |
| ssz-trajectories | TRAJECTORY, CURVATURE |
| frequency-curvature-validation | FREQUENCY, CURVATURE |
| ssz-schuhman-experiment | SCHUMANN, FREQUENCY |
| ssz-qubits | QUBIT |
| ssz-radial-scaling | METRIC |
| segmented-calculation-suite | Berechnung |
| segmented-energy | Energie |
| gauge-gravitationslinse-quadratur | LENSING |
| ssz-paper-plots | Plots |
| ssz-lagrange | METRIC |

### SYNTHETIC / NUMERICAL

| Repo | Anmerkung |
|------|-----------|
| Segmented-Spacetime-StarMaps | 4.307 Tests — größtes Repo, aber wahrscheinlich StarMap-Berechnungen |
| ssz-all-tests-run/test | Abgeleitete Runs von ssz-all-tests |

### BUCHBAU / DOKUMENTATION

| Repo | Anmerkung |
|------|-----------|
| book-full | 187 Tests — Buchbau-Skripte, keine Physik-Tests |
| SSZ_BOOK_PROJECT | 185 Tests — Buchbau-Skripte |
| ssz-complete-documentation | 0 Tests — reine Doku |
| 06_PAPERS | 0 Tests — Paper-PDFs |

---

## Nächste Phase

PHASE B: Observable Map — welche Tests testen welche Observablen? LIGO-relevant oder nicht?
