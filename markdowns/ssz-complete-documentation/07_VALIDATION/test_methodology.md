# Test Methodology

**Status:** CANONICAL

---

## Validation Philosophy

SSZ validation follows a **forward-prediction pipeline**:

```
Mass M → r_s → Ξ(r) → D(r) → Observable → Compare to data
```

The chain is one-directional. Reverse inference (observable → Ξ → M) is used only for consistency checks, never for calibration.

---

## Anti-Circularity Principle

SSZ formulas must never be calibrated against the data they predict:

1. Ξ formulas are derived from φ-geometry, not data
2. Regime/formula-domain boundaries are fixed canonical rules; `r*` values are `D_SSZ = D_GR` comparisons for declared Xi forms, not fitted thresholds
3. Δ(M) is from φ-geometry, not object-specific tuning
4. No per-object parameter adjustment is allowed

Test: `test_anti_circularity.py` in segmented-calculation-suite

---

## Test Categories

### 1. Weak-Field Validation (SSZ ≡ GR)

SSZ must reproduce all confirmed GR results to measurement precision.

| Test | Measurement | SSZ Prediction | Status |
|------|-------------|----------------|--------|
| GPS time correction | 45.85 μs/day | 45.85 μs/day | ✅ PASS |
| Pound-Rebka | Δν/ν = 2.46×10⁻¹⁵ | 2.46×10⁻¹⁵ | ✅ PASS |
| Mercury perihelion | 42.98"/century | 42.98"/century | ✅ PASS |
| Eddington lensing | 1.75" | 1.75" (PPN) | ✅ PASS |
| Cassini Shapiro | γ = 1.000021±0.000023 | γ = 1 (exact) | ✅ PASS |
| S2 star redshift | z = 0.00018 | 0.00018 | ✅ PASS |

### 2. Strong-Field Predictions (SSZ ≠ GR)

| Prediction | GR Value | SSZ Value | Testable? |
|-----------|----------|-----------|----------|
| NS redshift excess | z_GR | z_GR + 13% | NICER (2025-2027) |
| Shapiro strong-field | Δt_GR | Δt_GR + 12% | SKA (2028+) |
| BH shadow diameter | d_GR | d_GR - 1.3% | ngEHT (2028-2030) |
| D(r_s) | 0 | 0.555 | Indirect |
| Pulsar timing | Δt_GR | Δt_GR + 30% | NANOGrav (2025-2028) |

### 3. Internal Consistency

| Check | What it verifies | Status |
|-------|-----------------|--------|
| C² continuity at blend | Ξ, dΞ/dr, d²Ξ/dr² | ✅ |
| r* comparisons | `D_SSZ(r*) = D_GR(r*)` for the declared Xi form | ✅ |
| Asymptotic flatness | D → 1 as r → ∞ | ✅ |
| PPN recovery | β = γ = 1 in weak field | ✅ |
| Energy conditions | WEC, DEC, SEC for r ≥ 5r_s | ✅ |

---

## Test Infrastructure

### Canonical All-Tests Snapshot

The current validation baseline is the all-tests run from 2026-05-07:

| Metric | Value |
|--------|-------|
| Total expected tests/checks | 1296 |
| Total passed | 1296 |
| Total failed | 0 |
| Pass rate | 100.0% |
| Source output | `E:\clone\ssz-all-tests\really-full-output.md` |

See [all_tests_2026-05-07.md](all_tests_2026-05-07.md). Older partial counts in this documentation set are superseded by this snapshot.

### Repositories with Tests

| Repository | # Tests | Focus |
|-----------|---------|-------|
| ssz-qubits | 184 | GPS, Pound-Rebka, S2, qubits |
| ssz-metric-pure | 36 | 4D tensors, Einstein equations |
| segmented-calculation-suite | 158 | Core Ξ/D/regime |
| ssz-schumann | 178 | Schumann resonance |
| ssz-lensing | 279 | Gravitational lensing |
| Unified-Results | 147 | Unified validation framework |
| ssz-trajectories | 63 | Geodesic trajectory integration |
| g79-cygnus-tests | 5 | G79 LBV nebula |
| ssz-lagrange | 54 | Lagrange, Kerr, quantum corrections |
| segmented-energy | 7 | Stellar energy and astronomical objects |
| frequency-curvature-validation | 82 | PPN, Shapiro, lensing |
| chord-partition (local) | 103 | Eigenmodes and phi resonance |
| **TOTAL** | **1296** | |

### Unified Validation

The all-tests runner executes native test runners per repository and captures verbose output in `really-full-output.md`. `Unified-Results` remains one component of the full validation suite, not the complete validation source by itself.

### Reproducibility

- All repos are public on GitHub (github.com/error-wtf)
- Python 3.10+ with numpy, scipy, matplotlib
- Automated test runner: `run_consistency_suite.ps1`
- Commit hashes documented for exact reproduction

---

## Method Assignment in Tests

**CRITICAL:** Tests must use the correct method for each observable:

| Observable | Method | Test file |
|-----------|--------|-----------|
| Time dilation | Ξ-based | test_time_dilation.py |
| Redshift | Ξ-based | test_redshift.py |
| Lensing | PPN (1+γ) | test_ppn_lensing.py |
| Shapiro | PPN (1+γ) | test_shapiro_delay.py |
| Perihelion | PPN (β,γ) | test_perihelion.py |

Using Ξ-only for null observables gives 50% of GR — this is NOT a bug, it's the g_tt-only contribution.

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
