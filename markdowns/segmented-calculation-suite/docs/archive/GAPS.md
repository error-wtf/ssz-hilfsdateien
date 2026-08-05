# GAPS Analysis: What's Missing for 100% Parity

**Generated:** 2025-01-16  
**Status:** PASS 1 Analysis Complete

---

## Executive Summary

| Category | Implemented | Missing | Parity % |
|----------|-------------|---------|----------|
| Methods | 13/26 | 13 | 50% |
| Tests | 31/35 | 4 | 89% |
| Plots | 15/30 | 15 | 50% |
| **Overall** | **59/91** | **32** | **65%** |

---

## Critical Gaps (Must Fix)

### 1. Missing Core Methods

| Method | Source | Priority | Effort |
|--------|--------|----------|--------|
| `sigma` | Unified-Results | HIGH | Low |
| `tau` | Unified-Results | HIGH | Low |
| `delta_M` | Unified-Results | HIGH | Low |
| `r_phi` | Unified-Results | HIGH | Low |
| `dual_velocity` | Unified-Results | MEDIUM | Low |

**Impact:** These methods are used in the Unified Test Suite but not yet integrated.

### 2. Missing Tests

| Test | Method | Priority |
|------|--------|----------|
| `test_dual_velocity_invariance` | dual_velocity | MEDIUM |
| `test_sigma_formula` | sigma | HIGH |
| `test_tau_formula` | tau | HIGH |
| `test_n_index` | n_index | LOW |

**Impact:** Cannot validate full physics without these tests.

### 3. Missing Plots (Paper-Quality)

| Plot | Source | Priority |
|------|--------|----------|
| coherence_collapse_dynamics | ssz-paper-plots | MEDIUM |
| nested_submetric_analysis | ssz-paper-plots | MEDIUM |
| continuity_series (8) | ssz-paper-plots | LOW |
| curvature_series (8) | ssz-paper-plots | LOW |
| energy_series (11) | ssz-paper-plots | LOW |
| ppn_analysis (3) | ssz-paper-plots | MEDIUM |
| proper_time_series (7) | ssz-paper-plots | LOW |
| metric_components | ssz-metric-pure | MEDIUM |
| ricci_scalar | ssz-metric-pure | LOW |
| kretschmann_scalar | ssz-metric-pure | LOW |

**Impact:** Publication-ready plots not available.

---

## Moderate Gaps

### 4. Advanced Methods Not Implemented

| Method | Category | Reason |
|--------|----------|--------|
| `ppn_lensing` | PPN | Requires spatial metric component |
| `ppn_shapiro` | PPN | Requires ray tracing |
| `metric_tensor_ssz` | Tensor | Complex symbolic computation |
| `einstein_tensor` | Tensor | Requires Christoffel symbols |
| `geodesic_equation` | Dynamics | Requires ODE integration |
| `segment_saturation_derivative` | Calculus | Analytical derivative |
| `euler_spiral` | Geometry | Visualization helper |
| `n_index` | Optics | Refractive index calculation |

### 5. UI Gaps

| Feature | Current State | Needed |
|---------|---------------|--------|
| Sgr A* preset | Missing | Add to Single Object |
| M87* preset | Missing | Add to Single Object |
| Dynamic Reference | Static | Show current run params |
| Plot selection | Limited | All plot_ids from inventory |
| Fetch caching info | Hidden | Show cache hit/miss |

### 6. Data Pipeline Gaps

| Feature | Current State | Needed |
|---------|---------------|--------|
| Ring data schema | Partial | Full G79 ring support |
| ESO archive fetch | Basic | Full catalog integration |
| SDSS fetch | Missing | Add SDSS queries |
| Gaia fetch | Missing | Add Gaia DR3 queries |

---

## Low Priority Gaps

### 7. Documentation Gaps

| Doc | Current | Needed |
|-----|---------|--------|
| API Reference | Missing | Full docstrings |
| Tutorial | Missing | Step-by-step guide |
| Theory Guide | Partial | Full LaTeX derivations |

### 8. CI/CD Gaps

| Feature | Current | Needed |
|---------|---------|--------|
| Automated tests | Basic | Full pytest suite |
| Coverage report | Missing | pytest-cov integration |
| Lint check | Missing | ruff/black |
| Type checking | Missing | mypy |

---

## Gap Resolution Plan

### Phase 1: Core Method Parity (Est: 2 hours)
1. Implement `sigma`, `tau`, `delta_M`, `r_phi`
2. Add missing tests for these methods
3. Wire into existing calculation pipeline

### Phase 2: Test Parity (Est: 1 hour)
1. Add `test_dual_velocity_invariance`
2. Ensure all 35 tests pass
3. Generate test coverage report

### Phase 3: Plot Parity (Est: 3 hours)
1. Integrate ssz-paper-plots generators
2. Add plot dispatcher for all plot_ids
3. Ensure all plots land in run bundle

### Phase 4: UI Parity (Est: 1 hour)
1. Add Sgr A*, M87* presets
2. Dynamic Reference tab
3. Full plot selector

### Phase 5: Advanced Features (Est: 4+ hours)
1. Tensor calculations
2. Geodesic solver
3. PPN methods

---

## Acceptance Criteria for 100% Parity

- [ ] All 26 methods callable via `compute(method_id, inputs, config)`
- [ ] All 35 tests pass with `run_all_tests()`
- [ ] All 30 plots renderable via `render_plot(plot_id, ...)`
- [ ] Run bundle contains all artifacts
- [ ] No "NOT IMPLEMENTED" for core features
- [ ] Identical results to legacy repos (within tolerances)

---

## Notes

1. **Formula Variants:** Unified-Results uses `sigma`/`tau` notation while ssz-metric-pure uses `Xi`/`D`. Both are valid; we support both.

2. **Regime Boundaries:** Current implementation uses 90/110 thresholds with Hermite blending. This matches ssz-qubits.

3. **PPN Methods:** These are NOT Xi-based and require separate implementation. Do not confuse with core SSZ time dilation.

4. **Paper Plots:** Many are specific to certain papers and may not be needed for general use. Prioritize core theory plots.

---

*This analysis identifies concrete gaps. Implementation should follow the priority order above.*
