# SSZ Contract Sources - segmented-calculation-suite

**Created:** 2025-01-17  
**Purpose:** Anchor this suite to verified golden outputs from full-output.md

---

## 1. CONTRACT ARTIFACTS (Source of Truth)

All outputs from this suite MUST match these verified documents:

| Artifact | Location | Content |
|----------|----------|---------|
| **Truth Map** | `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\TRUTH_MAP_FROM_FULL_OUTPUT.md` | Line-by-line extraction from full-output.md |
| **Implementation Contract** | `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\IMPLEMENTATION_CONTRACT.md` | Binding formulas, regimes, invariants |
| **Test Inventory** | `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\TEST_SUITE_INVENTORY.md` | 47 test files, 54 pytests, 25 suites |
| **Golden Output** | `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\reports\full-output.md` | 6442 lines, 25/25 suites PASS |

---

## 2. GOLDEN REFERENCE VALUES (from full-output.md)

### 2.1 Δ(M) Correction Parameters
**Contract Source:** IMPLEMENTATION_CONTRACT.md §1.4, full-output.md L5363-5365

```
A = 98.01
α = 2.7177e+04
B = 1.96

Formula: Δ(M) = A × exp(-α × r_s) + B
```

### 2.2 φ-Geometry
**Contract Source:** IMPLEMENTATION_CONTRACT.md §1.1, PHI_FUNDAMENTAL_GEOMETRY.md

```
φ = 1.6180339887498948 (IMMUTABLE)
φ/2 boundary ≈ 0.809 r_s
```

### 2.3 PPN Parameters
**Contract Source:** full-output.md L5390

```
β = 1.0 (exact)
γ = 1.0 (exact)
```

### 2.4 Dual Velocity Invariant
**Contract Source:** full-output.md L3013-3197

```
v_esc × v_fall = c² (machine precision)
```

---

## 3. REGIME BOUNDARIES (Contract-Binding)

**Contract Source:** TRUTH_MAP §2, full-output.md L5331-5334, L5697-5713

| Regime | r/r_s Range | SSZ Performance | Contract Line |
|--------|-------------|-----------------|---------------|
| Very Close | r < 2 r_s | 0% wins | full-output L5333 |
| Photon Sphere | 2-3 r_s | 82% wins (67.9% in paired test) | full-output L5331, L5691-5695 |
| Strong Field | 3-10 r_s | 88.9% wins | full-output L5697-5701 |
| Weak Field | > 10 r_s | 34-37% wins (SSZ ≈ GR) | full-output L5334, L5703-5707 |
| High Velocity | v > 5% c | 85.7% wins | full-output L5709-5713 |

---

## 4. GOLDEN OUTPUT WIN RATES

**Contract Source:** TRUTH_MAP §6, full-output.md L5230-5234, L6147-6154

### Overall Performance (WITH φ-geometry)
| Metric | Value | Source |
|--------|-------|--------|
| Overall (paired test) | 82/127 = 64.6% | full-output L5230-5234 |
| ESO Spectroscopy | 46/47 = 97.9% | full-output L6150 |
| Energy Framework | 64/64 = 100% | full-output L6151 |
| Combined Success | 110/111 = 99.1% | full-output L6154 |

### φ-Geometry Impact (CRITICAL)
| Scenario | Win Rate | Source |
|----------|----------|--------|
| WITHOUT φ | 0% | full-output L5337 |
| WITH φ | 51-99.1% | full-output L5338, L6154 |

---

## 5. FORMULAS (Contract-Binding)

### 5.1 Segment Density Ξ(r)
**Contract Source:** IMPLEMENTATION_CONTRACT.md §1.2

```
Ξ(r) = Ξ_max × (1 - exp(-φ × r_s / r))
Ξ_max = 1.0
```

### 5.2 Time Dilation D_SSZ
**Contract Source:** IMPLEMENTATION_CONTRACT.md §1.3

```
D_SSZ(r) = 1 / (1 + Ξ(r))
```

### 5.3 SSZ Redshift
**Contract Source:** FORMULA_TRACE.md §4

```
z_SSZ = z_GR × (1 + Δ(M)/100)
```

### 5.4 Critical Values at Horizon
**Contract Source:** FORMULA_TRACE.md, TRUTH_MAP §5

```
Ξ(r_s) = 0.8017
D(r_s) = 0.5550 (FINITE - no singularity!)
```

---

## 6. INVARIANTS THAT MUST HOLD

**Contract Source:** IMPLEMENTATION_CONTRACT.md §4

| Invariant | Expected | Tolerance | Test |
|-----------|----------|-----------|------|
| v_esc × v_fall = c² | Exact | Machine precision | test_vfall_duality |
| PPN β | 1.0 | Exact | test_ppn_exact |
| PPN γ | 1.0 | Exact | test_ppn_exact |
| D(r_s) finite | 0.555 | ±0.001 | test_horizon_finite |
| C¹ continuity | Smooth | Derivative continuous | test_c1_segments |

---

## 7. ENERGY CONDITIONS

**Contract Source:** IMPLEMENTATION_CONTRACT.md §5, full-output.md L3312-3314

| Condition | r ≥ 5 r_s | r < 5 r_s |
|-----------|-----------|-----------|
| WEC | PASS | FAIL |
| DEC | PASS | FAIL |
| SEC | PASS | FAIL |

---

## 8. WHAT THIS SUITE MUST NOT DO

1. **Units mismatch:** z_obs and z_pred MUST be same scale (not micro vs unitless)
2. **Sun-only validation:** Single object is DEMO, not validation
3. **Wrong compare logic:** Residual/MAE must match Truth Map exactly
4. **Wrong regime assignment:** Weak/Strong boundaries must match §3 above
5. **Missing Δ(M):** Without Δ(M) correction, SSZ has 0% wins

---

## 9. PARITY CHECK PROCEDURE

To verify this suite matches golden output:

```bash
# 1. Run suite batch mode
python -m segcalc.batch --input data/validation_176.csv --output results/parity_check.csv

# 2. Compare key columns
# - z_ssz vs z_gr: SSZ should be HIGHER (z_ssz = z_gr × (1 + Δ/100))
# - regime: Must match Contract boundaries
# - win_rate: Must approach Contract values per regime

# 3. Check invariants
python test_physics_validation.py
```

---

## 10. DEVIATION TRACKING

Any deviation from Contract MUST be documented here:

| Date | Component | Contract Says | Suite Does | Resolution |
|------|-----------|---------------|------------|------------|
| - | - | - | - | - |

---

*This file is the binding reference for all validation in segmented-calculation-suite.*
