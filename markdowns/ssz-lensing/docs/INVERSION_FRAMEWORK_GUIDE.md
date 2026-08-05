# RSG Lensing Inversion Framework - Complete Guide

## Overview

This framework implements a **three-path inversion strategy** for gravitational lensing analysis, with automatic **regime classification** that replaces the old "FORBIDDEN" approach.

## Core Paradigm Shift

**OLD:** Underdetermined systems → ABORT  
**NEW:** Underdetermined systems → EXPLORE & LEARN

---

## The Four Regimes

| Regime | Condition | Action |
|--------|-----------|--------|
| **DETERMINED** | constraints = params, good condition | Unique solution via Path A |
| **OVERDETERMINED** | constraints > params | Solve + use residual as model check |
| **UNDERDETERMINED** | constraints < params | Explore nullspace via Path C |
| **ILL-CONDITIONED** | condition > 10¹⁰ | Solve with uncertainty bounds |

---

## The Three Paths

### Path A: Algebraic (Canonical)
- **Parametrization:** `(a_m, b_m)` Cartesian components
- **Method:** Direct linear solve `A·x = b`
- **Phase:** OUTPUT (derived as `φ_m = atan2(b_m, a_m)`)
- **Properties:** Deterministic, fast, canonical reference
- **Use when:** DETERMINED or OVERDETERMINED

### Path B: Phase Scan (Hypothesis Test)
- **Parametrization:** `(A_m, φ_m)` amplitude/phase  
- **Method:** Scan over φ values, linear solve at each point
- **Phase:** INPUT (scanned)
- **Properties:** Shows residual landscape, detects degeneracies
- **Use when:** Phase degeneracy suspected, want visual confirmation

### Path C: Underdetermined Explorer
- **Method:** SVD nullspace analysis + multiple solutions
- **Output:** Parameter ranges, non-identifiable params, regularized solutions
- **Regularizers:** Minimal norm (Occam), Minimal multipole power (smooth lens)
- **Use when:** UNDERDETERMINED regime

---

## Key Files

| File | Purpose |
|------|---------|
| `src/models/regime_classifier.py` | RegimeClassifier, UnderdeterminedExplorer |
| `src/models/dual_path_inversion.py` | AlgebraicSolver, PhaseScanSolver |
| `tests/test_regime_explorer.py` | 10 regime tests |
| `tests/test_validation_lab.py` | 9 validation tests |
| `tests/test_comprehensive_analysis.py` | Full scenario comparison |

---

## Generated Plots

All plots in `plots/output/`:

| Plot | Content |
|------|---------|
| `01_regime_overview.png` | Matrix visualization of all 4 regimes |
| `02_nullspace.png` | Nullspace exploration for underdetermined |
| `03_phase_scan.png` | Residual landscape from Path B |
| `04_path_comparison.png` | Path A vs B comparison |
| `05_dof_rescue.png` | Adding sources reduces degeneracy |
| `06_framework_overview.png` | Complete framework diagram |
| `07_decision_tree.png` | Regime decision flowchart |
| `08_sensitivity.png` | Sensitivity analysis across regimes |
| `09_solution_space.png` | Solution space visualization |
| `10_learning_insights.png` | Key learning insights |

---

## Usage Example

```python
from models.regime_classifier import RegimeClassifier, UnderdeterminedExplorer
from models.dual_path_inversion import AlgebraicSolver, PhaseScanSolver

# 1. Classify the regime
analysis = RegimeClassifier.classify(A, param_names)
print(f"Regime: {analysis.regime.value}")
print(f"Nullspace: {analysis.nullspace_dim}D")

# 2. Choose path based on regime
if analysis.regime == Regime.UNDERDETERMINED:
    explorer = UnderdeterminedExplorer(param_names)
    result = explorer.explore(A, b, analysis)
    print(f"Multiple solutions: {len(result.solutions)}")
else:
    solver = AlgebraicSolver(m_max=2)
    result = solver.solve([images])
    print(f"Residual: {result.max_residual}")
```

---

## Test Results Summary

```
test_regime_explorer.py:     10/10 PASSED
test_validation_lab.py:       9/9 PASSED
test_comprehensive_analysis:  All scenarios pass
```

---

## Key Insights

1. **DETERMINED:** Residual = numerical noise only
2. **OVERDETERMINED:** Residual = model adequacy diagnostic
3. **UNDERDETERMINED:** Explore what CAN be learned, not just abort
4. **ILL-CONDITIONED:** Near caustic/degenerate - report with uncertainty

---

## Authors

Carmen N. Wrede, Lino P. Casu
