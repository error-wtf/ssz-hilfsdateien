# MD_INDEX: Complete Markdown Documentation Index

**Generated:** 2025-01-16  
**Purpose:** Index of ALL MD files from SSZ source repositories  
**Status:** MANDATORY READING before implementation

---

## ssz-metric-pure (44 files)

| File | Summary | Key Rules/Definitions | Impact |
|------|---------|----------------------|--------|
| `01_MATHEMATICAL_FOUNDATIONS.md` | **CRITICAL** - Complete formula collection | Weak/Strong Xi formulas, D_SSZ, PPN, tolerances | ALL methods |
| `02_PHYSICS_CONCEPTS.md` | **CRITICAL** - Theory framework | 7 pillars, time emergence, regime physics | ALL physics |
| `03_SCRIPT_ARCHITECTURE.md` | Script organization | Pipeline structure, module layout | Architecture |
| `04_FINDINGS_UNIFIED_RESULTS.md` | Validation results | Win rates, test outcomes | Tests |
| `05_FINDINGS_SSZ_METRIC_PURE.md` | Metric-specific findings | Tensor results, curvature | Tensors |
| `06_FINDINGS_G79_CYGNUS_TESTS.md` | Cygnus X-1 validation | LBV predictions | G79 tests |
| `CAUTION_RESOLUTION_EXPLANATION.md` | Numerical cautions | Precision issues | Edge cases |
| `CHANGELOG.md` | Version history | Breaking changes | Versions |
| `CHANGELOG_2PN_CALIBRATION.md` | 2PN calibration | φ²_G formula update | Metric |
| `COMPARISON_README.md` | SSZ vs GR comparison | Deviation tables | Compare tab |
| `COMPLETE_TENSOR_PACKAGE_README.md` | Tensor package | 4D metric, Einstein tensor | Tensors |
| `IMPLEMENTATION_PLAN_100_PERCENT.md` | Implementation plan | Phases, gates | Roadmap |
| `INDEX.md` | Repo index | File locations | Navigation |
| `LINO_SPEC_VERIFICATION.md` | Spec verification | Lino's requirements | Tests |
| `MASTER_README.md` | Main readme | Setup, usage | Getting started |
| `QUICKSTART.md` | Quick start guide | Essential steps | Onboarding |
| `README.md` | Standard readme | Overview | General |
| `ROADMAP_TO_100_PERCENT.md` | Roadmap | Milestones | Planning |
| `SSZ_VALIDATION_SUMMARY_V2.md` | Validation summary | Test results | Tests |
| `WHY_DEVIATIONS_ARE_NORMAL.md` | Deviation explanation | Expected differences | Tolerance |
| `docs/SPECIFICATION.md` | Formal spec | API contracts | API |
| `reports/FINAL_COMPLETE_REPORT.md` | Complete report | All results | Summary |
| `reports/SSZ_QUICK_REFERENCE.md` | Quick reference | Formulas, constants | Reference |
| `reports/SSZ_VALIDATION_REPORT.md` | Validation report | Pass/fail details | Tests |

---

## ssz-qubits (75 files)

| File | Summary | Key Rules/Definitions | Impact |
|------|---------|----------------------|--------|
| `README.md` | **CRITICAL** - Main documentation | SSZ for qubits, formulas | Core |
| `docs/SSZ_FORMULA_DOCUMENTATION.md` | **CRITICAL** - Two regimes spec | Weak r/r_s>100, Strong r/r_s<100 | Xi formulas |
| `docs/SSZ_MATHEMATICAL_PHYSICS.md` | Deep theory | Derivations, proofs | Theory |
| `docs/SSZ_QUBIT_APPLICATIONS.md` | Qubit applications | Height effects, decoherence | Qubits |
| `docs/SSZ_QUBIT_THEORY_SUMMARY.md` | Theory summary | Core concepts | Reference |
| `docs/CONSISTENCY_REPORT.md` | Consistency checks | Cross-validation | Tests |
| `docs/paper_a_revised.md` | Paper A content | Theory paper | Papers |
| `docs/paper_b_revised.md` | Paper B content | Applications paper | Papers |
| `docs/paper_c_revised.md` | Paper C content | Falsifiability | Papers |
| `docs/paper_d_master_rewrite.md` | Paper D content | Master paper | Papers |
| `COMPLETE_PROJECT_REPORT.md` | Project report | All outcomes | Summary |
| `FINAL_REPORT.md` | Final report | Conclusions | Summary |
| `PAPER_D_VALIDATION_REPORT.md` | Paper D validation | Test results | Validation |
| `paper_final/appendices/E_transition.md` | **IMPORTANT** - Transition zone | Blend zone details | Xi blending |

---

## Segmented-Spacetime-Mass-Projection-Unified-Results (45+ files)

| File | Summary | Key Rules/Definitions | Impact |
|------|---------|----------------------|--------|
| `README.md` | Main readme | Unified suite overview | Core |
| `UNIFIED_VALIDATION_README.md` | **CRITICAL** - 11-step validation | All validation steps | Tests |
| `TEST_SUITE_RESULTS_*.md` | Test results | Pass/fail, tolerances | Tests |
| `ALL_PIPELINES_100_PERCENT_PASS.md` | 100% pass proof | All tests green | Benchmark |
| `31_OF_31_TESTS_PASSED_FINAL.md` | 31/31 tests | Complete pass | Benchmark |
| `COMPREHENSIVE_TESTS_SUMMARY.md` | Test summary | Coverage, results | Tests |
| `COMPLETE_VALIDATION_FINAL.md` | Final validation | All checks | Tests |
| `CODE_DOCUMENTATION.md` | Code docs | Function specs | API |
| `COMPREHENSIVE_SCIENTIFIC_DOCUMENTATION.md` | Science docs | Physics explanations | Theory |
| `BOUND_ENERGY_SCRIPTS_CLARIFICATION.md` | Energy scripts | E_bound formulas | Energy |
| `CHANGELOG.md` | Version history | Breaking changes | Versions |

---

## Key Regime Rules (extracted from ALL sources)

### Regime Boundaries (CONSISTENT across all repos)
```
Weak Field:   r/r_s > 100 (some docs say > 110)
Strong Field: r/r_s < 100 (some docs say < 90)
Blend Zone:   90 < r/r_s < 110 (C² Hermite interpolation)
```

### Xi Formulas (AUTHORITATIVE)
```python
# Weak Field (r/r_s > 100)
Xi = r_s / (2 * r)

# Strong Field (r/r_s < 100)
Xi = 1 - exp(-PHI * r_s / r)

# Time Dilation (BOTH regimes)
D_SSZ = 1 / (1 + Xi)
```

### Key Constants
```python
PHI = 1.6180339887498948
XI_MAX = 0.802  # Xi(r_s)
D_HORIZON = 0.555  # D_SSZ(r_s)
R_STAR_OVER_RS = 1.387  # Universal intersection
```

### Method Selection Rule
| Observable | Method | NOT Xi-based? |
|------------|--------|---------------|
| Time dilation | Xi | |
| Frequency shift | Xi | |
| Lensing | PPN | YES - use (1+γ)r_s/b |
| Shapiro delay | PPN | YES - use (1+γ) factor |

---

## Critical Tolerances (from validation reports)

| Test | Tolerance | Source |
|------|-----------|--------|
| GPS timing | ±1 μs/day | ssz-qubits |
| Pound-Rebka | ±0.1×10⁻¹⁵ | ssz-qubits |
| Universal intersection | ±0.002 (r*/r_s) | ssz-metric-pure |
| D(r_s) | ±0.001 | ssz-metric-pure |
| Power law R² | > 0.99 | Unified-Results |

---

## Files NOT to use (deprecated)

| File | Reason |
|------|--------|
| Any with `(r_s/r)² × exp(-r/r_φ)` | DEPRECATED Xi formula |
| Files marked "OLD" or "LEGACY" | Superseded |
| Draft papers without validation | Unverified |

---

## Reading Priority

### Must Read (STOP-GATE)
1. `ssz-metric-pure/01_MATHEMATICAL_FOUNDATIONS.md`
2. `ssz-metric-pure/02_PHYSICS_CONCEPTS.md`
3. `ssz-qubits/docs/SSZ_FORMULA_DOCUMENTATION.md`
4. `Unified-Results/UNIFIED_VALIDATION_README.md`

### Should Read
5. `ssz-metric-pure/SSZ_VALIDATION_SUMMARY_V2.md`
6. `ssz-qubits/COMPLETE_PROJECT_REPORT.md`
7. `Unified-Results/ALL_PIPELINES_100_PERCENT_PASS.md`

### Reference
- All CHANGELOG files for breaking changes
- All test result files for expected outputs

---

**This index must be consulted before ANY implementation work.**
