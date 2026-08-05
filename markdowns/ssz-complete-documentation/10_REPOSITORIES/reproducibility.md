# Reproducibility Guide

**Status:** CANONICAL

---

## Requirements

- **Python:** 3.10+
- **Core packages:** numpy, scipy, matplotlib
- **Optional:** astropy, pandas (for some repos)
- **OS:** Windows, Linux, macOS

---

## How to Reproduce

### 1. Clone All Repos
```bash
git clone https://github.com/error-wtf/segmented-calculation-suite
git clone https://github.com/error-wtf/ssz-qubits
git clone https://github.com/error-wtf/frequency-curvature-validation
git clone https://github.com/error-wtf/ssz-lensing
git clone https://github.com/error-wtf/ssz-metric-pure
git clone https://github.com/error-wtf/ssz-schumann
git clone https://github.com/error-wtf/g79-cygnus-tests
git clone https://github.com/error-wtf/ssz-paper-plots
git clone https://github.com/error-wtf/segmented-energy
git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
git clone https://github.com/error-wtf/Segmented-Spacetime-Starmaps
```

### 2. Install Dependencies
```bash
pip install numpy scipy matplotlib
```

### 3. Run Tests
```bash
# Individual repo
cd segmented-calculation-suite
python -m pytest tests/

# Or run all tests
python run_consistency_suite.ps1  # PowerShell
```

### 4. Verify Key Results

Check these values match:
```
Ξ(r_s) = 0.80171
D(r_s) = 0.55503
r*/r_s = 1.594811 (decay/global) or 1.386562 (saturation/local)
β = γ = 1
```

---

## Validation Levels

| Level | Description | Pass Criteria |
|-------|-------------|---------------|
| L1: Unit | Individual function tests | All assertions pass |
| L2: Integration | Multi-function tests | Consistent results |
| L3: Cross-repo | Same calculation in multiple repos | Values agree |
| L4: Observational | Comparison to real data | Within measurement error |

---

## Unified Test Suite

The `Unified-Results` repository runs all 25 test suites:
- Runtime: ~231 seconds
- Result: 25/25 suites PASS
- 97.9% ESO accuracy
- Full report: `reports/full-output.md`

---

## Commit Hashes

For exact reproduction, each repo's commit hash at validation time is documented in the Unified-Results repository.

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
