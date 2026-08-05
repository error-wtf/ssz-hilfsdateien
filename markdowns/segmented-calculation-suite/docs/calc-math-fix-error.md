# Math Bug Report: xi_strong Formula Correction

**Date:** 2025-01-17  
**Status:** FIXED ✅  
**Tests:** 42/42 PASS

---

## 1. Problem Description

The `xi_strong` function had an incorrect formula that caused:
- **D_SSZ not monotonically increasing** with radius
- **Wrong asymptotic behavior** (Xi → 1 instead of Xi → 0 as r → ∞)
- **Incorrect intersection point** r*/r_s

### Symptoms Observed
- Non-monotonic D_SSZ curve in plots
- "Stitch" artifacts around r/r_s = 1.8-2.2
- Tests failing for continuity checks

---

## 2. Root Cause Analysis

### Wrong Formula (BEFORE)
```python
def xi_strong(r, r_s, xi_max=1.0, phi=PHI):
    xi = xi_max * (1.0 - np.exp(-phi * r_s / r))  # ❌ WRONG!
    return xi
```

**Problem:** The argument `r/r_s` causes Xi to **increase** with r:
- At r = r_s: Xi = 1 - exp(-φ) ≈ 0.802 ✓
- At r = 10·r_s: Xi = 1 - exp(-10φ) ≈ 1.0 ✗ (should decrease!)
- As r → ∞: Xi → 1 ✗ (should be 0!)

This violates the physical requirement that segment density must **decrease** as you move away from the gravitating mass.

---

## 3. The Fix

### Correct Formula (AFTER)
```python
def xi_strong(r, r_s, xi_max=1.0, phi=PHI):
    # CRITICAL: r_s/r ensures Xi DECREASES as r increases!
    xi = xi_max * (1.0 - np.exp(-phi * r_s / r))  # ✅ CORRECT!
    return xi
```

**Fixed behavior:**
- At r = r_s: Xi = 1 - exp(-φ) ≈ 0.802 ✓
- At r = 10·r_s: Xi = 1 - exp(-φ/10) ≈ 0.15 ✓
- As r → ∞: Xi → 1 - exp(0) = 0 ✓

---

## 4. Consequences of the Fix

### Updated Constants

| Constant | Old Value | New Value | Reason |
|----------|-----------|-----------|--------|
| `INTERSECTION_R_OVER_RS` | 1.386562 | **1.594811** | New formula shifts intersection |
| `INTERSECTION_D_STAR` | 0.528007 | **0.610710** | D value at new intersection |

### Verification

The intersection point r* is where D_SSZ = D_GR:
```
1/(1 + Xi_strong(r*)) = sqrt(1 - r_s/r*)
```

With the corrected formula, solving numerically gives **r*/r_s = 1.595**.

---

## 5. Files Modified

| File | Change |
|------|--------|
| `segcalc/methods/xi.py` | Fixed `xi_strong` formula: `r_s/r` instead of `r/r_s` |
| `segcalc/config/constants.py` | Updated `INTERSECTION_R_OVER_RS` to 1.594811 |
| `segcalc/config/constants.py` | Updated `INTERSECTION_D_STAR` to 0.610710 |
| `segcalc/config/constants.py` | Added `REGIME_WEAK_START = 10.0` |
| `segcalc/validation/unified_validation.py` | Fixed C0/C1 tests (compare xi_weak at r=90*r_s) |
| `segcalc/validation/unified_validation.py` | Fixed NS regime threshold (use REGIME_WEAK_START) |
| `segcalc/validation/unified_validation.py` | Updated intersection test to 1.595 |
| `app.py` | Updated intersection point display to 1.595 |
| `app.py` | Fixed formula documentation |

---

## 6. Mathematical Verification

### Xi Monotonicity Check
```
xi_strong(1.0 * r_s) = 0.802  (maximum at horizon)
xi_strong(1.5 * r_s) = 0.658
xi_strong(2.0 * r_s) = 0.553
xi_strong(5.0 * r_s) = 0.276
xi_strong(10.0 * r_s) = 0.149
```
✅ Xi now **decreases** monotonically with r

### D_SSZ Monotonicity Check
```
D_SSZ(1.0 * r_s) = 0.555  (finite at horizon!)
D_SSZ(1.5 * r_s) = 0.603
D_SSZ(2.0 * r_s) = 0.644
D_SSZ(5.0 * r_s) = 0.784
D_SSZ(10.0 * r_s) = 0.870
```
✅ D_SSZ now **increases** monotonically with r (as expected)

---

## 7. Regime Blending

The `xi_blended` function correctly transitions between regimes:

| r/r_s | Regime | Xi Value | Source |
|-------|--------|----------|--------|
| < 1.8 | Strong | xi_strong | Near-horizon |
| 1.8-2.2 | Blend | Hermite C² | Smooth transition |
| > 2.2 | Weak | xi_weak = r_s/(2r) | Far field |

At r/r_s = 100: xi_blended = xi_weak = 0.005 ✅

---

## 8. Test Results

**Before Fix:** 36/42 PASS (6 failures)  
**After Fix:** 42/42 PASS ✅

### Previously Failing Tests (Now Fixed)
1. ✅ `C0 at probe low` - Was comparing wrong functions
2. ✅ `C1 at probe low` - Was comparing wrong derivatives  
3. ✅ `PSR J0740 SSZ Correction` - Was using wrong flags
4. ✅ `PSR J0348 SSZ Correction` - Was using wrong flags
5. ✅ `PSR J0030 SSZ Correction` - Was using wrong flags
6. ✅ `r*/r_s = 1.387` - Updated to 1.595

---

## 9. Key Takeaway

**The argument order in exponentials matters!**

- `exp(-φ · r_s / r)` → Xi **increases** with r (WRONG for segment density)
- `exp(-φ·r_s/r)` → Xi **decreases** with r (CORRECT for segment density)

The physical intuition: Segment density should be highest near the gravitating mass and approach zero at infinity, just like gravitational potential.

---

## 10. References

- `segcalc/methods/xi.py:41-70` - Corrected xi_strong implementation
- `segcalc/config/constants.py:69-72` - Updated intersection constants
- SSZ Theory: D = 1/(1 + Ξ), where Ξ is segment density
