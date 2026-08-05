# TRUTH MAP - Extracted from full-output.md

**Source:** `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\reports\full-output.md`
**Lines:** 1-6442
**Generated:** Phase 1 of Contract Enforcement

---

## 1. TEST SUITE SUMMARY

| Metric | Value | Source Line |
|--------|-------|-------------|
| Total Phases | 25 | L6368 |
| Passed | 25/25 (100%) | L6369-6371 |
| Total Test Time | 189.0s | L6372 |
| Total Suite Time | 231.2s | L6373 |

---

## 2. MODULES/COMPONENTS TESTED

### Core Physics Tests
| Test Suite | Duration | Status | Source |
|------------|----------|--------|--------|
| PPN Exact Tests | 0.3s | PASS | L6376, L114-173 |
| Dual Velocity Tests | 0.7s | PASS | L6377, L175-292 |
| Energy Conditions Tests | 0.3s | PASS | L6378, L294-407 |
| C1 Segments Tests | 0.2s | PASS | L6379, L409-457 |
| C2 Segments Strict Tests | 0.3s | PASS | L6380 |
| C2 Curvature Proxy Tests | 0.2s | PASS | L6381 |

### SegWave Tests
| Test Suite | Duration | Status | Source |
|------------|----------|--------|--------|
| SegWave Core Math Tests | 5.9s | PASS | L6382 |
| Multi-Ring Validation Tests | 5.3s | PASS | L6385 |

### SSZ Kernel Tests
| Test Suite | Duration | Status | Source |
|------------|----------|--------|--------|
| SSZ Kernel Tests | 5.3s | PASS | L6386 |
| SSZ Invariants Tests | 5.7s | PASS | L6387 |
| Segmenter Tests | 5.4s | PASS | L6388 |

### Cosmological Tests
| Test Suite | Duration | Status | Source |
|------------|----------|--------|--------|
| Cosmo Fields Tests | 5.6s | PASS | L6389 |
| Cosmo Multibody Tests | 6.5s | PASS | L6390 |
| Cosmos Multi-Body Sigma Tests | 6.7s | PASS | L6392 |

### Data & Validation Tests
| Test Suite | Duration | Status | Source |
|------------|----------|--------|--------|
| Data Validation Tests | 5.5s | PASS | L6391 |
| SSZ Complete Analysis | 115.8s | PASS | L6393 |
| SSZ Theory Predictions | 2.7s | PASS | L6396 |
| Final Validation | 0.1s | PASS | L6400 |

### Production Tools Tests
| Test Suite | Duration | Status | Source |
|------------|----------|--------|--------|
| Rapidity Equilibrium Analysis | 1.5s | PASS | L6394 |
| Perfect Paired Test | 2.8s | PASS | L6395 |
| G79 Analysis | 2.4s | PASS | L6397 |
| Cygnus X Analysis | 2.5s | PASS | L6398 |
| Paper Export Tools | 5.5s | PASS | L6399 |

---

## 3. REGIME DEFINITIONS & BOUNDARIES

| Regime | r/r_s Range | SSZ Performance | Source |
|--------|-------------|-----------------|--------|
| Very Close | r < 2 r_s | 0% wins (even WITH φ) | L5333, L5375 |
| Photon Sphere | r = 2-3 r_s | 82% wins WITH φ | L5331, L5343 |
| Strong Field | r = 3-10 r_s | 88.9% wins | L5697-5700 |
| Weak Field | r > 10 r_s | ~37% wins | L5334, L5703-5706 |
| High Velocity | v > 5% c | 86% wins WITH φ | L5333, L5709-5713 |

### Blending Thresholds (from constants)
- **REGIME_WEAK_THRESHOLD:** 110 r/r_s
- **REGIME_STRONG_THRESHOLD:** 90 r/r_s
- **Blend Zone:** 90-110 r/r_s (Hermite C² interpolation)

---

## 4. CRITICAL FORMULAS & PARAMETERS

### Δ(M) φ-based Correction Parameters
| Parameter | Value | Source |
|-----------|-------|--------|
| A (pre-exponential) | 98.01 | L5363 |
| α (exponential decay) | 2.7177e+04 | L5364 |
| B (constant offset) | 1.96 | L5365 |

### Golden Ratio φ
| Constant | Value | Status | Source |
|----------|-------|--------|--------|
| φ | 1.6180339887498948 | VERIFIED | L5359-5360 |
| φ/2 boundary | ~0.809 (≈1.618 r_s) | VERIFIED | L5368-5369 |

### PPN Parameters
| Parameter | Value | Status | Source |
|-----------|-------|--------|--------|
| β | 1 (exact) | PASS | L3420, L5390 |
| γ | 1 (exact) | PASS | L3420, L5390 |

### Universal Power Law
```
E/E_rest = 1 + 0.32(r_s/R)^0.98
R² = 0.997
```
Source: L6164, L6320, L6351

---

## 5. KEY INVARIANTS

### Dual Velocity Invariant
```
v_esc × v_fall = c²
```
| Test | Relative Error | Status | Source |
|------|---------------|--------|--------|
| Sun @ 1.1 r_s | 1.780e-16 | PASS | L3013 |
| SgrA* @ 1.1 r_s | 1.780e-16 | PASS | L3036 |
| Earth @ 2.0 r_s | 1.780e-16 | PASS | L3059 |
| All @ 5.0, 10.0 r_s | 0.000e+00 | PASS | L3128, L3197 |

### Energy Conditions
| Condition | r ≥ 5 r_s | r < 5 r_s | Source |
|-----------|-----------|-----------|--------|
| WEC (Weak) | ✓ PASS | ✗ FAIL | L3312, L3264 |
| DEC (Dominant) | ✓ PASS | ✗ FAIL | L3313, L3265 |
| SEC (Strong) | ✓ PASS | ✗ FAIL | L3314, L3266 |

### Metric Continuity
- **C¹ continuous:** PASS (L3428)
- **C² strict:** PASS (L6380)

---

## 6. SSZ vs GR×SR COMPARISON METRICS

### Overall Performance WITH φ-geometry
| Metric | Value | Source |
|--------|-------|--------|
| Total pairs | 143 | L5320 |
| SSZ wins | 73/143 (51%) | L5320, L5338 |
| WITHOUT φ | 0% wins | L5337 |

### Stratified Performance (Perfect Paired Test)
| Regime | n | SSZ Wins | p-value | Source |
|--------|---|----------|---------|--------|
| Overall | 127 | 82 (64.6%) | 0.0013 | L5230-5234 |
| Photon Sphere | 28 | 19 (67.9%) | 0.0872 | L5691-5695 |
| Strong Field | 54 | 48 (88.9%) | 0.0000 | L5697-5701 |
| Weak Field | 44 | 15 (34.1%) | 0.0488 | L5703-5707 |
| High Velocity | 21 | 18 (85.7%) | 0.0015 | L5709-5713 |

---

## 7. VALIDATION RESULTS

### Combined Success Rate
| Source | n | Wins | Rate | Source |
|--------|---|------|------|--------|
| ESO Spectroscopy | 47 | 46 | 97.9% | L6150-6151 |
| Energy Framework | 64 | 64 | 100.0% | L6151-6152 |
| Test Suite | 63 | 63 | 100.0% | L6152-6153 |
| **COMBINED** | **111** | **110** | **99.1%** | L6154 |

### Mass Validation (Roundtrip)
| Object | M_true | M_rec | RelErr | Source |
|--------|--------|-------|--------|--------|
| Elektron | 9.109e-31 kg | 9.109e-31 kg | 1.1e-50% | L4699-4701 |
| Sonne | 1.988e+30 kg | 1.988e+30 kg | 0% | L4726 |
| Sagittarius A* | 8.544e+36 kg | 8.544e+36 kg | 0% | L4727 |

---

## 8. CRITICAL FINDINGS

### φ-Geometry Impact
```
WITHOUT φ-based geometry: 0/143 wins (0%) - Total failure!
WITH φ-based geometry: 73/143 wins (51%) - Competitive with GR×SR
φ-geometry enables: +51 percentage points (from 0% to parity!)
```
Source: L5336-5339

### Key Insight (verbatim from L5341)
> "φ is GEOMETRIC FOUNDATION (not fitting parameter!)"

### Rapidity Solution for r < 2 r_s
- **Problem:** 0/0 singularity at equilibrium points
- **Solution:** Rapidity formulation χ = arctanh(v/c)
- **Expected improvement:** 0% → 35-50%
Source: L5046-5047, L5410-5416

---

## 9. WEAK FIELD BEHAVIOR (per Repo Logic)

### Why GR Sometimes Closer in Weak Field

From `full-output.md` L5334, L5703-5707:
- Weak field (r > 10 r_s): SSZ wins only 34-37%
- This is **EXPECTED** per the theoretical framework
- SSZ is optimized for **strong field / photon sphere** regime
- In weak field, SSZ ≈ GR by design (PPN exactness)

### PPN Exactness Confirmation
```
Weak-field sector: PPN(beta=gamma=1) and classic tests match GR at machine precision.
```
Source: L5390

---

## 10. TEST FILE LOCATIONS (from full-output.md)

| Test File | Source Line |
|-----------|-------------|
| `tests/test_ssz_real_data_comprehensive.py` | L2975, L3021, L3044 |
| `scripts/tests/test_cosmo_fields.py` | L3455 |
| `scripts/tests/test_cosmo_multibody.py` | L3488 |
| `scripts/tests/test_data_validation.py` | L3568 |
| `scripts/tests/test_horizon_hawking_predictions.py` | L3760 |
| `scripts/tests/test_ssz_invariants.py` | L3932 |
| `scripts/tests/test_ssz_kernel.py` | L3991 |
| `scripts/tests/test_segmenter.py` | L3891 |

---

## 11. PYTEST OUTPUT SUMMARY

From L3442:
```
============================= 78 passed in 32.38s =============================
```

From L4095:
```
================== 46 passed, 1 skipped, 1 warning in 21.21s ==================
```

Total from summary (L6368-6371):
```
Total Phases: 25
Passed: 25
Failed: 0
Success Rate: 100.0%
```

---

## CONCLUSION

**Status:** All 25 test suites PASS (100%)
**φ-Geometry:** FUNDAMENTAL (0% without → 51-99.1% with)
**Δ(M) Correction:** Applied in ALL regimes for SSZ competitiveness
**Weak Field:** SSZ ≈ GR by design (PPN exact, ~37% wins expected)
**Strong Field/Photon Sphere:** SSZ dominates (82-89% wins)

---

*Truth Map extracted from full-output.md per Phase 1 of SSZ Test Suite Contract*
