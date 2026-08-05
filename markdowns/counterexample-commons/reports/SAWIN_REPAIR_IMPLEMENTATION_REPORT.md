# Sawin Integrity Repair — Implementation Report

**Date:** 2026-05-25
**Test result:** 231/231 PASS

---

## PASS/FAIL Gate

| Check | Result |
|-------|--------|
| UD-SAWIN-2026-001 is SOURCE_DOCUMENTED | PASS |
| UD-SAWIN-2026-001 locally_validated=False | PASS |
| UD-BASE-RATIONAL-MESH-001 is LOCALLY_REPRODUCED_EXACT | PASS |
| sawin_construction.py raises NotImplementedError | PASS |
| rational_mesh_baseline.py exists and tested | PASS |
| README Sawin row = SOURCE_DOCUMENTED | PASS |
| README false asymptotic claim removed | PASS |
| Image caption corrected | PASS |
| UI Overview tab has SOURCE_DOCUMENTED caveat | PASS |
| run_gradio_local.py exposes all 6 modes | PASS |
| CLAIM_TO_SOURCE_MATRIX upgrade checklist added | PASS |
| SAWIN_REPRODUCTION_ROADMAP.md written | PASS |
| All 231 tests pass | PASS |

---

## Files Changed

| File | Change |
|------|--------|
| `counterexample_commons/claims.py` | UD-SAWIN-2026-001 -> SOURCE_DOCUMENTED; new UD-BASE-RATIONAL-MESH-001 |
| `README.md` | Sawin row, false claim text, image caption corrected |
| `references/CLAIM_TO_SOURCE_MATRIX.md` | Rational mesh row + upgrade checklist |
| `case_studies/erdos_unit_distance_2026/sawin_construction.py` | Honest placeholder with NotImplementedError |
| `tests/test_sawin.py` | 15 new tests (NotImplementedError guards + rational mesh) |
| `tests/test_claims.py` | 2 new integrity guard tests |
| `app/main.py` | UI Overview SOURCE_DOCUMENTED caveat |
| `scripts/run_gradio_local.py` | All 6 modes exposed |

## Files Added

| File | Purpose |
|------|---------|
| `case_studies/erdos_unit_distance_2026/rational_mesh_baseline.py` | Actual finite exact baseline |
| `case_studies/erdos_unit_distance_2026/SAWIN_REPRODUCTION_ROADMAP.md` | 6-level reproduction plan |
| `case_studies/__init__.py` | Package marker |
| `case_studies/erdos_unit_distance_2026/__init__.py` | Package marker |
| `reports/SAWIN_CLAIM_INTEGRITY_AUDIT.md` | Audit findings |

---

## Forbidden Actions Confirmed Not Taken

- No premature claim upgrade (Sawin remains SOURCE_DOCUMENTED)
- No fake implementation (all Sawin functions raise NotImplementedError)
- No secret leakage
- No changes outside E:\clone\counterexample-commons
- Political mission and ACSL license unchanged