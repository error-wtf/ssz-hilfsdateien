# PARITY_GATES: Definition of Done

**Date:** 2025-01-16  
**Status:** BINDING - All gates must pass for acceptance

---

## Gate Definition: GREEN = ACCEPTED

A gate is GREEN if and only if ALL criteria are met.  
Any RED gate = **WORK NOT ACCEPTED**.

---

## GATE 1: Method Coverage

### Criteria
```
✓ ALL method_ids from INVENTORY_METHODS.json are callable
✓ Each method has: compute(method_id, inputs, config) -> results
✓ No "NOT IMPLEMENTED" for core methods (P1)
✓ Method signatures match source repos exactly
```

### Verification
```bash
python -c "from segcalc.methods import *; print('Methods OK')"
```

### Current Status
| Metric | Required | Actual | Status |
|--------|----------|--------|--------|
| Core methods | 13 | 13 | ✅ GREEN |
| Extended methods | 8 | 8 | ✅ GREEN |
| Advanced methods | 5 | 0 | ⚠️ YELLOW (not required for core) |

---

## GATE 2: Test Parity

### Criteria
```
✓ ALL tests from source repos run
✓ Pass rate matches source (target: 100% for ssz-qubits)
✓ Skipped = 0 for core functionality
✓ Tolerances match source exactly
✓ Delta analysis for ANY deviation
```

### Verification
```bash
python -c "from segcalc.tests import run_all_tests; r = run_all_tests(); print(f'Pass: {r.passed}/{r.total}')"
```

### Source Benchmarks
| Suite | Tests | Pass Rate | Source |
|-------|-------|-----------|--------|
| ssz-qubits | 74 | 100% | Reference |
| ssz-metric-pure | 12+ | 100% | Reference |
| Unified-Results | 31 | 100% | Reference |

### Required Tests (MUST PASS)
| Test | Tolerance | Source Value |
|------|-----------|--------------|
| test_golden_ratio | 1e-15 | 1.618033988749895 |
| test_schwarzschild_sun | 0.5 m | 2953.25 m |
| test_xi_at_horizon | 0.001 | 0.802 |
| test_D_ssz_finite_at_horizon | 0.001 | 0.555 |
| test_universal_intersection | 0.002 | 1.387 |
| test_gps_timing | 5 μs | 45.7 μs/day |
| test_pound_rebka | 0.1e-15 | 2.46e-15 |
| test_dual_velocity_invariance | 1e13 | c² |

---

## GATE 3: Plot Coverage

### Criteria
```
✓ ALL plot_ids from INVENTORY_PLOTS.json render
✓ No crashes during render
✓ Plots saved in run bundle
✓ Visual equivalence to source plots
```

### Required Plots (MUST RENDER)
| plot_id | Status |
|---------|--------|
| xi_and_dilation | Required |
| gr_vs_ssz_comparison | Required |
| universal_intersection | Required |
| regime_zones | Required |
| dilation_profile | Required |
| xi_profile | Required |
| redshift_breakdown | Required |
| power_law | Required |
| comparison_scatter | Required |
| residuals_plot | Required |

---

## GATE 4: UI Functionality

### Criteria
```
✓ ALL 6 tabs functional
✓ No placeholder outputs
✓ Real calculations only
✓ Clear error messages
✓ Online-first (no local paths shown)
```

### Tab Requirements
| Tab | Required Features | Gate |
|-----|-------------------|------|
| Single Object | Presets, Calculate, Plots, Bundle | GREEN |
| Data | Upload, Template, Fetch, Preview | GREEN |
| Batch Calculate | Run, Results, Plots, Export | GREEN |
| Compare | Object select, z_obs check, Residuals | GREEN |
| Theory Plots | Plot selection, Generate | GREEN |
| Reference | Constants, Formulas, Regime rules | GREEN |

---

## GATE 5: Run Bundle Completeness

### Criteria
```
✓ params.json contains ALL run parameters
✓ data_input.csv normalized
✓ results.csv complete
✓ report.md human-readable
✓ plots/*.png all generated plots
✓ errors.log if any
✓ ZIP download works
✓ Run-ID displayed (no paths!)
```

### Bundle Structure
```
run_<id>/
├── params.json      ✓ Required
├── data_input.csv   ✓ Required
├── results.csv      ✓ Required
├── report.md        ✓ Required
├── plots/           ✓ Required
│   ├── *.png
└── errors.log       ○ Optional
```

---

## GATE 6: Deployment Ready

### Criteria
```
✓ Dockerfile works
✓ requirements.txt complete
✓ No hardcoded local paths
✓ Environment variables for config
✓ README with deploy instructions
```

### Verification
```bash
docker build -t ssz-suite .
docker run -p 7860:7860 ssz-suite
```

---

## GATE 7: Documentation Complete

### Required Files
| File | Content | Status |
|------|---------|--------|
| INVENTORY_METHODS.json | All methods | Required |
| INVENTORY_TESTS.json | All tests | Required |
| INVENTORY_PLOTS.json | All plots | Required |
| METHOD_TEST_PLOT_MAP.md | Traceability | Required |
| GAPS.md | Missing items | Required |
| PARITY_PROGRESS.md | Progress tracker | Required |
| PARITY_REPORT.md | Final report | Required |
| WEAK_STRONG_FIELD_SPEC.md | Regime spec | Required |
| PROOF_OF_READING.md | Source analysis | Required |
| TRACEABILITY_MATRIX.md | Full mapping | Required |
| ROADMAP.md | Milestones | Required |

---

## Overall Gate Status

| Gate | Status | Blocker |
|------|--------|---------|
| G1: Methods | ✅ GREEN | - |
| G2: Tests | ⚠️ YELLOW | 4 tests need adjustment |
| G3: Plots | ✅ GREEN | - |
| G4: UI | ✅ GREEN | - |
| G5: Bundles | ✅ GREEN | - |
| G6: Deploy | ✅ GREEN | - |
| G7: Docs | ✅ GREEN | - |

---

## Definition of DONE

**DONE** means:
1. ALL gates GREEN
2. PARITY_REPORT.md shows 100% pass
3. No "skipped" for core functionality
4. No placeholders anywhere
5. No features removed
6. Online deployable

---

## Escalation Path

If a gate cannot be made GREEN:

1. **Document** the exact blocker in GAPS.md
2. **Link** to source code showing the issue
3. **Propose** fix with implementation plan
4. **Get approval** before marking as exception

**NO EXCEPTIONS** for:
- Core physics tests (G2)
- UI functionality (G4)
- Run bundles (G5)

---

**This document is the acceptance criteria. ALL gates must be GREEN.**
