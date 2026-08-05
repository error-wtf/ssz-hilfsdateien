# Reproducibility and Validation Levels

BEAM-SSZ follows the SSZ reproducibility style:

- Python 3.10+
- stdlib-only core for v0.4
- `pytest` for test execution
- no fitting as a substitute for derivation

Validation levels:

| Level | Meaning | v0.4 status |
|---|---|---|
| L1 | Unit tests for formulas and guards | implemented |
| L2 | Internal integration/smoke tests | implemented via simulations |
| L3 | Cross-check against canonical SSZ values | partial: Xi(rs), D(rs), metric, method rules |
| L4 | Observational comparison | out of scope for BEAM-SSZ core |

Run:

```bash
python -m pytest
for f in simulations/*.py; do python "$f"; done
```
