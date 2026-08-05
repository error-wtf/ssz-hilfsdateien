# Sawin n^1.014 Reproduction Roadmap

**Claim:** UD-SAWIN-2026-001
**Current status:** SOURCE_DOCUMENTED (arXiv:2605.20579)
**Target status:** LOCALLY_REPRODUCED_EXACT (requires all stages below)

---

## Source Summary

Will Sawin (2026) constructs point sets in Q(sqrt(d))^2 for specially
chosen square-free d, achieving u(n) >= n^1.014 for infinitely many n.
The construction uses:

1. A quadratic field Q(sqrt(d)) with d chosen so the unit circle over
   Q(sqrt(d)) has many rational points.
2. A Gaussian-integer-like lattice in Q(sqrt(d))^2.
3. A counting argument showing the ratio of unit edges to points
   exceeds n^0.014.

Primary source: arXiv:2605.20579 (Will Sawin, 2026)

---

## Reproduction Levels

| Level | Description | Blocker |
|-------|-------------|---------|
| L0 | Read and understand the paper | None — do this first |
| L1 | Identify a concrete d, verify unit circle has many Q(sqrt(d)) points | Requires algebraic geometry in SymPy or SageMath |
| L2 | Generate a small finite instance of the Sawin lattice exactly | Requires L1 complete |
| L3 | Count unit edges exactly on that instance | Requires L2 + SymPy rational arithmetic |
| L4 | Show edge ratio > n^0.014 for the instance | Requires L3 |
| L5 | Reproduce for multiple n, fit empirical exponent | Requires L4 |
| L6 | Full asymptotic argument verified | Out of scope for this project |

---

## Immediate Next Steps

1. Read Section 2 of arXiv:2605.20579; identify explicit d values used.
2. Install SageMath or use SymPy NumberField to enumerate unit-circle
   points over Q(sqrt(d)).
3. Implement generate_sawin_field_points(d, bound) in sawin_construction.py.
4. Verify at least one small instance: n points, e unit edges, e/n > 1.
5. Write tests in tests/test_sawin.py that remove NotImplementedError
   guards only for implemented levels.
6. Update UD-SAWIN-2026-001 status atomically per CLAIM_TO_SOURCE_MATRIX.md
   upgrade requirements.

---

## What Is Already Done

- Exact finite rational-mesh baseline (UD-BASE-RATIONAL-MESH-001):
  LOCALLY_REPRODUCED_EXACT. See rational_mesh_baseline.py.
- This is NOT a reproduction of Sawin. It is an exploratory baseline.

---

## What Must NOT Be Done

- Do not upgrade UD-SAWIN-2026-001 based on the rational mesh baseline.
- Do not claim numerical evidence without running the actual construction.
- Do not merge changes that set locally_validated=True without a code
  implementation that passes tests.