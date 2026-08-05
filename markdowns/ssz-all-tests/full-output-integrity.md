# SSZ ALL-TESTS FULL OUTPUT INTEGRITY

**Generated:** 2026-04-29T08:00:13.239857+00:00

| Repo | Type | tests_run | pass | fail | exit | failures_expected | status |
|------|------|-----------|------|------|------|-------------------|--------|
| ssz-qubits | CANONICAL | 184 | 184 | 0 | 0 | no | ok |
| ssz-metric-pure | CANONICAL | 36 | 36 | 0 | 0 | no | ok |
| ssz-schumann | CANONICAL | 201 | 201 | 0 | 0 | no | ok |
| g79-cygnus-tests | CANONICAL | 3 | 3 | 0 | 0 | no | ok |
| ssz-lensing | CANONICAL | 279 | 279 | 0 | 0 | no | ok |
| ssz-trajectories | CANONICAL | 63 | 63 | 0 | 0 | no | ok |
| Unified-Results | CANONICAL | 125 | 125 | 0 | 0 | no | ok |
| segmented-calculation-suite | CANONICAL | 158 | 158 | 0 | 0 | no | ok |
| segmented-energy | CANONICAL | 2 | 2 | 0 | 0 | no | ok |
| ssz-paper-plots | VALIDATION | 16 | 13 | 3 | 1 | no | ok |
| Segmented-Spacetime-Starmaps | VALIDATION | 0 | 0 | 0 | -1 | no | exit_-1 |
| frequency-curvature-validation | CANONICAL | 64 | 64 | 0 | 0 | no | ok |
| ssz-all-tests-own | CANONICAL | 44 | 0 | 0 | 1 | no | ok |

## Summary

- Repos: 13
- Total executed: 1175
- Tests mapped: 228
- Duplicates: 0
- Expected ≥1128: PASS

## Repo Classification

- `CANONICAL`: ✅ CANONICAL   — official SSZ, failures are real bugs
- `DERIVATION`: ⚠️  DERIVATION  — GR-based exploration, failures EXPECTED
- `CUSTOM`: 🔧 CUSTOM      — own runner (not pytest)
- `VALIDATION`: 📊 VALIDATION  — cross-validation / paper output
- `ARCHIVE`: 📁 ARCHIVE     — historical reference, not maintained

## INTEGRITY STATUS: PASS