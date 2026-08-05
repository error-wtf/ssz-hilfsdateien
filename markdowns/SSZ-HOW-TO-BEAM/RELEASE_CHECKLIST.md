# Release Checklist

**Version:** v0.8.0  
**Date:** 2026-06-09

---

## Pre-Release Verification

### Core Tests
- [ ] Run `pytest -k "not simulation_smoke"` → 299 passed
- [ ] Run `pytest tests/` → All tests complete
- [ ] Verify no import errors in `src/beam_ssz/`

### Smoke Tests
- [ ] All simulations have `if __name__ == "__main__": main()` guards
- [ ] Smoke tests run with 20s timeout per simulation
- [ ] No top-level code execution during import

### Code Quality
- [ ] No `__pycache__` directories in repository
- [ ] No `.pyc` files in repository
- [ ] No `.git` directory in ZIP
- [ ] No `.venv` or virtual environment in ZIP

### Overclaiming Check
- [ ] No files named `*complete*`, `*proven*`, `*solved*`, `*ultimate*`, `*final*`
- [ ] Search for "PROVEN" in code → Replace with precise categories
- [ ] Search for "COMPLETE" in docs → Verify not overstated
- [ ] Verify all theorem claims are marked as "candidate" or "framework"

### Documentation
- [ ] `CURRENT_STATUS.md` is up-to-date
- [ ] `README.md` has prominent link to `CURRENT_STATUS.md`
- [ ] `TEST_RESULTS.md` reflects actual test numbers
- [ ] No "100% pass" claims unless actually true
- [ ] No "publication ready" without tensor validation

### Tensor Backend
- [ ] `metric_array.py` exists with 4D array implementation
- [ ] `christoffel_array.py` exists with numerical Christoffels
- [ ] `riemann_array.py` exists with curvature tensors
- [ ] Minkowski test: Riemann = 0
- [ ] Flat bridge test: Riemann finite or zero

### Energy Classification
- [ ] Heuristic energy class separated from tensor energy class
- [ ] `SSZ_CANONICAL`, `GR_EXOTIC` marked as heuristic/proxy
- [ ] No "NEC satisfied" without actual tensor calculation

### Numerical GR
- [ ] `pipeline.py` runs without errors
- [ ] Output says "SCAFFOLD" not "READY"
- [ ] Constraint violation clearly reported (not hidden)
- [ ] No "validated" claims without convergence study

### Naming
- [ ] `proof_status.py` (not `complete_proof.py`)
- [ ] `candidate_strategy_explorer.py` (not `ultimate_solver.py`)
- [ ] `candidate_mitigation_strategies.py` (not `final_solutions.py`)
- [ ] `extended_body_stress_proxy/` (not `human_transport/`)

### ZIP Integrity
```bash
# Run these commands:
make test      # or: pytest -k "not simulation_smoke"
make smoke     # or: pytest tests/test_simulation_smoke.py
make verify    # Manual: grep -r "PROVEN\|COMPLETE" src/ docs/
make zip       # or: ./scripts/build_zip.sh

# Verify ZIP contents:
unzip -l SSZ-HOW-TO-BEAM.zip | grep -v "__pycache__\|.pyc\|.git"
```

### Final Verification
- [ ] Clean git status: `git status` shows no uncommitted changes
- [ ] Version number updated in:
  - `README.md`
  - `pyproject.toml`
  - `CURRENT_STATUS.md`
- [ ] ZIP file created and copied to `/home/error/`
- [ ] ZIP size reasonable (~250-300 KB)

---

## Sign-off

**Release Manager:** _______________  
**Date:** _______________  
**Notes:** _______________

---

## Post-Release

- [ ] Tag release: `git tag v0.8.0`
- [ ] Push tag: `git push origin v0.8.0`
- [ ] Create GitHub release with notes
- [ ] Attach ZIP to release
- [ ] Update documentation site (if applicable)
