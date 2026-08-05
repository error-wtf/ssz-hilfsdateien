# v0.8 Freeze Report

**Date:** 2026-06-09  
**Status:** FROZEN / NOT PERFECT / RELEASE CANDIDATE ONLY

---

## Warum eingefroren

v0.8 erreicht keine perfekte Endstufe. Weiterer Aufwand an v0.8 blockiert v0.9-Entwicklung.

- Full pytest / Smoke / Doku / Pipeline / Claim-Hygiene bleiben teilweise problematisch
- Weitere kosmetische Claim-Hygiene-Schleifen würden Entwicklung blockieren
- v0.8 wird als Arbeitsbaseline für v0.9 verwendet

---

## Aktuelle Testlage

### Test 1: Core Tests (ohne Smoke)
```bash
python -m pytest -q -k "not simulation_smoke"
```

**Status:** PASS (299 Tests) ✅  
**Ausgabe:** `299 passed, 36 deselected in ~15s`  
**Interpretation:** Kernfunktionalität stabil.

---

### Test 2: Smoke Tests
```bash
python -m pytest -q tests/test_simulation_smoke.py -vv
```

**Status:** PASS ISOLATED / TIMEOUT IN FULL SUITE ⚠️  
**Ausgabe:** 36 passed in Isolation  
**Interpretation:** Smoke-Tests funktionieren, aber pytest-Termination im Full-Suite-Modus hängt (bekannter v0.8-Blocker).

---

### Test 3: Full Suite
```bash
python -m pytest -q
```

**Status:** HANG / TIMEOUT ⚠️  
**Ausgabe:** pytest terminiert nicht (bekanntes Problem)  
**Interpretation:** v0.8-Blocker: Full pytest termination nicht stabil. Workaround: `-k "not simulation_smoke"` verwenden.

---

## Aktuelle Skriptlage

### Script 1: numerical_gr/pipeline.py
```bash
PYTHONPATH=src python numerical_gr/pipeline.py
```

**Status:** PASS (nach ham-Fix) ✅  
**Exit Code:** 0  
**Output:** HDF5 und parfile generiert, Hamiltonian constraint violation printed  
**Ehrlichkeit:** "Constraint violation nonzero: NOT validated for evolution yet." ✅

---

### Script 2: symbolic/lambda_crit_derivation.py
```bash
PYTHONPATH=src python symbolic/lambda_crit_derivation.py
```

**Status:** PASS ✅  
**Exit Code:** 0  
**Output:** Profile-dependent lambda_crit computed  
**Ehrlichkeit:** Tensor validation pending disclaimer vorhanden ✅

---

### Script 3: extended_body_stress_proxy/gradual_entry_protocol.py
```bash
PYTHONPATH=src python extended_body_stress_proxy/gradual_entry_protocol.py
```

**Status:** PASS ✅  
**Exit Code:** 0  
**Output:** Default UNSAFE warning present  
**Ehrlichkeit:** No biological feasibility claim ✅

---

## Bekannte v0.8 Blocker

| Blocker | Status | Workaround |
|---------|--------|------------|
| Full pytest hängt | ⚠️ OPEN | `-k "not simulation_smoke"` |
| Smoke-Test nicht CI-stabil | ⚠️ OPEN | Isolated execution only |
| Documentation stale paths | ✅ FIXED | human_transport → extended_body_stress_proxy |
| Claim-Treffer (Overclaims) | ✅ FIXED | Alle "COMPLETE PROOF" etc. entfernt |
| numerical_gr ham NameError | ✅ FIXED | ham = generator.export_to_hdf5() |
| Overclaiming language | ✅ FIXED | TEST_RESULTS.md, README aktualisiert |

---

## Entscheidung

**v0.8 wird NICHT als "perfect" bezeichnet.**  
**v0.8 wird als Arbeitsbaseline für v0.9 verwendet.**

v0.8 erreicht:
- ✅ 299 Core Tests pass
- ✅ numerische Skripte laufen
- ✅ keine kritischen Import-Fehler
- ⚠️ pytest termination problematisch
- ⚠️ Smoke-Tests isoliert nur

**v0.8 ist ACCEPTABLE als Development Baseline, nicht als Production Release.**

---

## Was v0.8 NICHT behauptet (korrekt)

- ❌ "v0.8 perfect"
- ❌ "v0.8 100% complete"
- ❌ "all tests pass" (ohne Einschränkung)
- ❌ "COMPLETE MATHEMATICAL PROOF"
- ❌ "HUMAN TRANSPORT POSSIBLE"

---

## Übergang zu v0.9

v0.9 beginnt als neue Entwicklungsstufe mit:
- SSZ Segmentierungsregeln als Kern
- Kontinuierliche Weltlinie (Variante B)
- No-copy constraint
- Tensor/Diagnostik Struktur

**v0.8 bleibt als Referenz-Branch erhalten.**  
**v0.9 wird als `v0.9-ssz-continuous-worldline` Branch entwickelt.**

---

## Git Status

```bash
git status
```

Empfohlener Branch für v0.9:
```bash
git checkout -b v0.9-ssz-continuous-worldline
```

Oder falls existiert:
```bash
git checkout v0.9-ssz-continuous-worldline
```

---

## Fazit

v0.8 ist eingefroren.  
Bekannte Blocker sind dokumentiert.  
v0.9 Entwicklung kann beginnen.

---

© 2026 Carmen N. Wrede, Lino P. Casu
