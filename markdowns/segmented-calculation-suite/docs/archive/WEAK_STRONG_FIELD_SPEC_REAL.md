# WEAK/STRONG FIELD SPECIFICATION (REAL)

**Derived From:** ssz-qubits/paper_final/appendices/E_transition.md  
**Date:** 2025-01-16  
**Status:** BINDING - This is the authoritative spec from source documentation

---

## 1. Source Reference

| Document | Path | Lines | Authority |
|----------|------|-------|-----------|
| E_transition.md | ssz-qubits/paper_final/appendices/E_transition.md | 1-234 | PRIMARY |
| ssz_qubits.py | ssz-qubits/ssz_qubits.py | 117-178 | IMPLEMENTATION |
| 01_MATHEMATICAL_FOUNDATIONS.md | ssz-metric-pure/01_MATHEMATICAL_FOUNDATIONS.md | 800-900 | SUPPORTING |

---

## 2. Regime Definition (FROM E_transition.md Lines 17-23)

```
x = r / r_s

WEAK FIELD:   x > 110  →  Ξ(r) = 1/(2x) = r_s/(2r)
STRONG FIELD: x < 90   →  Ξ(r) = 1 - exp(-φx) = 1 - exp(-φr_s / r)
TRANSITION:   90 ≤ x ≤ 110  →  Quintic Hermite Blend
```

---

## 3. Weak Field Formula

**Source:** E_transition.md Line 20, ssz_qubits.py Line 174

```
Ξ_weak(r) = r_s / (2r)
```

**Properties:**
- Valid for: r/r_s > 110
- Scaling: 1/r (Newtonian-like)
- At Earth surface: Ξ ~ 7×10⁻¹⁰
- Gradient: dΞ/dr = -r_s/(2r²) < 0

**Test Tolerance (from test_ssz_physics.py Line 111):**
```python
assert 6e-10 < xi < 8e-10  # At Earth surface
```

---

## 4. Strong Field Formula

**Source:** E_transition.md Line 21, ssz_qubits.py Line 178

```
Ξ_strong(r) = 1 - exp(-φ × r_s / r)

where φ = (1 + √5) / 2 = 1.6180339887498948
```

**Properties:**
- Valid for: r/r_s < 90
- Saturation: Ξ → 1 as r → ∞ (within strong field context)
- At horizon (r = r_s): Ξ(r_s) = 1 - exp(-φ) = 0.8017
- Gradient: dΞ/dr = (φ/r_s) × exp(-φr_s / r) > 0

**CRITICAL: Ξ(r_s) = 0.8017 is COMPUTED, not a parameter!**

---

## 5. Transition Zone (FROM E_transition.md Lines 27-93)

**Range:** 90 ≤ r/r_s ≤ 110

### Quintic Hermite Blend Function

```
t = (x - 90) / 20    where x = r/r_s, so t ∈ [0, 1]

b(t) = 6t⁵ - 15t⁴ + 10t³
```

**Properties (E_transition.md Lines 32-35):**
```
b(0) = 0,  b'(0) = 0,  b''(0) = 0
b(1) = 1,  b'(1) = 0,  b''(1) = 0
```

### Blended Formula

```
Ξ_blend(r) = b(t) × Ξ_weak(r) + (1 - b(t)) × Ξ_strong(r)
```

**At x = 90:** b(0) = 0 → pure strong field
**At x = 110:** b(1) = 1 → pure weak field

---

## 6. Complete Implementation (FROM E_transition.md Lines 56-93)

```python
def xi_complete(r, r_s, phi=1.6180339887498948):
    """
    Complete SSZ segment density with C² smooth transition.
    
    SOURCE: ssz-qubits/paper_final/appendices/E_transition.md Lines 56-93
    """
    x = r / r_s
    
    # Weak field: r >> r_s
    if x > 110:
        return 1 / (2 * x)
    
    # Strong field: r ~ r_s
    if x < 90:
        return 1.0 - np.exp(-phi * x)
    
    # Transition zone: 90 ≤ x ≤ 110
    t = (x - 90) / 20  # Normalize to [0, 1]
    b = 6*t**5 - 15*t**4 + 10*t**3  # Quintic Hermite
    
    xi_weak = 1 / (2 * x)
    xi_strong = 1.0 - np.exp(-phi * x)
    
    return b * xi_weak + (1 - b) * xi_strong
```

---

## 7. Time Dilation (FROM ssz_qubits.py Lines 224-246)

```
D_SSZ(r) = 1 / (1 + Ξ(r))
```

**Key Values (FROM E_transition.md Line 160):**

| r/r_s | Ξ | D_SSZ |
|-------|---|-------|
| 1 | 0.802 | 0.555 |
| 2 | 0.961 | 0.510 |
| 90 | ~1.000 | 0.500 |
| 100 | 0.503 | 0.665 |
| 110 | 0.00455 | 0.995 |
| 10⁶ | 5×10⁻⁷ | ~1 |

---

## 8. Comparison with GR

**GR Formula:**
```
D_GR(r) = √(1 - r_s/r)
```

**Key Difference at Horizon:**
```
D_GR(r_s) = √(1 - 1) = 0  (SINGULAR!)
D_SSZ(r_s) = 1/(1 + 0.802) = 0.555  (FINITE!)
```

---

## 9. INCONSISTENCY ALERT

### Documentation (E_transition.md):
- Transition zone: 90-110
- Blend function: Quintic Hermite

### Implementation (ssz_qubits.py Line 166):
```python
if ratio > 100:  # Hard threshold, no blend!
    regime = 'weak'
else:
    regime = 'strong'
```

**Resolution:** Use E_transition.md specification (with blend).

---

## 10. Test Tolerances (FROM Source)

| Test | Tolerance | Source |
|------|-----------|--------|
| r_s(Earth) | 8.8e-3 < r_s < 8.9e-3 | test_ssz_physics.py:61 |
| r_s(Sun) | 2.9e3 < r_s < 3.0e3 | test_ssz_physics.py:80 |
| Xi(Earth) | 6e-10 < xi < 8e-10 | test_ssz_physics.py:111 |
| Xi ratio | rtol=1e-10 | test_ssz_physics.py:135 |
| SSZ vs GR | < xi² × 10 | test_validation.py:71 |
| Redshift | rtol=0.01 | test_validation.py:109 |
| Pound-Rebka | rtol=1e-6 | test_validation.py:146 |
| GPS | rtol=0.01 | test_validation.py:197 |

---

## 11. Constants (FROM ssz_qubits.py Lines 42-55)

```python
C = 299792458.0              # m/s (EXACT)
G = 6.67430e-11              # m³/(kg·s²) (CODATA 2018)
PHI = (1 + np.sqrt(5)) / 2   # 1.6180339887498948 (EXACT)
M_EARTH = 5.972e24           # kg
R_EARTH = 6.371e6            # m
```

---

## 12. What is NOT a Parameter

| Value | Why | Computed From |
|-------|-----|---------------|
| Ξ(r_s) = 0.8017 | Result of formula | 1 - exp(-φ) |
| D(r_s) = 0.555 | Result of formula | 1/(1 + 0.8017) |
| r*/r_s = 1.387 | Intersection point | Solve D_SSZ = D_GR |

**DO NOT** make these configurable parameters!

---

## 13. Traceability

| Specification | Source File | Lines |
|---------------|-------------|-------|
| Weak threshold = 110 | E_transition.md | 20 |
| Strong threshold = 90 | E_transition.md | 21 |
| Quintic Hermite | E_transition.md | 39 |
| Weak formula | ssz_qubits.py | 174 |
| Strong formula | ssz_qubits.py | 178 |
| Time dilation | ssz_qubits.py | 246 |

---

**This document is BINDING. All implementations must follow these specifications.**
