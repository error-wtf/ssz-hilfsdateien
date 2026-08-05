# Sawin Claim Integrity Audit

**Date:** 2026-05-25

## Contradictions Found

1. claims.py UD-SAWIN-2026-001: LOCALLY_REPRODUCED_NUMERICAL / locally_validated=True -- NOT EVIDENCED
2. README.md:64 Sawin n^1.014 | LOCALLY_REPRODUCED_NUMERICAL -- NOT EVIDENCED
3. README.md:71 asymptotic limit verified numerically -- WRONG
4. sawin_construction.py: rational grid (i/m,j/m), hardcoded sawin_exponent()=1.014 -- NOT SAWIN CONSTRUCTION
5. test_sawin.py: malformed comment only, no tests
6. CLAIM_TO_SOURCE_MATRIX.md: correctly says SOURCE_DOCUMENTED / No -- INCONSISTENT with claims.py

## Required Changes

- claims.py: UD-SAWIN-2026-001 -> SOURCE_DOCUMENTED, locally_validated=False
- claims.py: add UD-BASE-RATIONAL-MESH-001 LOCALLY_REPRODUCED_EXACT
- README: Sawin row -> SOURCE_DOCUMENTED
- README: remove false asymptotic claim
- README: rename Sawin lattice image caption
- sawin_construction.py: replace with honest placeholder (NotImplementedError)
- rational_mesh_baseline.py: new file for the grid code
- test_sawin.py: real tests
- PROJECT_CAPABILITIES.yml: evidence-based entries

## MUST NOT Change

- CLAIM_TO_SOURCE_MATRIX.md Sawin row (already correct)
- Political mission / ACSL license
