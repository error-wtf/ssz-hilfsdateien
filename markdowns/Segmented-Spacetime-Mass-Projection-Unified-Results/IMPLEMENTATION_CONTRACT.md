# SSZ IMPLEMENTATION CONTRACT

**Generated from:** Reference Docs + full-output.md  
**Phase:** 2 of Contract Enforcement  
**Date:** Auto-generated

---

## 1. BINDING FORMULAS

### 1.1 Golden Ratio φ
```
φ = (1 + √5)/2 ≈ 1.6180339887498948
```
**Status:** IMMUTABLE - Geometric constant, NOT a fitting parameter

### 1.2 Segment Density Ξ(r)
```
Ξ(r) = Ξ_max · (1 - exp(-φ · r_s / r))
```
Where:
- Ξ_max = 1.0 (maximum saturation)
- φ = 1.618... (golden ratio)
- r_s = 2GM/c² (Schwarzschild radius)

**Source:** `PHYSICS_FOUNDATIONS.md` L113-121

### 1.3 Time Dilation D(r)
```
D_SSZ(r) = 1 / (1 + Ξ(r))
```
**Source:** `PHYSICS_FOUNDATIONS.md` L130-133

### 1.4 Δ(M) Mass-Dependent Correction
```
Δ(M) = A · exp(-α · r_s) + B

Parameters:
  A = 98.01 (amplitude)
  α = 2.7177e+04 (decay rate)
  B = 1.96 (base offset)
```
**Source:** `full-output.md` L5363-5365, `PHYSICS_FOUNDATIONS.md` L179-186

### 1.5 Characteristic Radius r_φ
```
r_φ = φ · (GM/c²) · (1 + Δ(M)/100)
```
**Source:** `PHYSICS_FOUNDATIONS.md` L156-158

### 1.6 Dual Velocity Invariant
```
v_esc × v_fall = c²   [EXACT - machine precision]

Where:
  v_esc = √(2GM/r)
  v_fall = c² / v_esc
```
**Source:** `PHYSICS_FOUNDATIONS.md` L206-210, `full-output.md` L3013-3197

### 1.7 PPN Parameters
```
β = 1.0 (exact)
γ = 1.0 (exact)
```
**Status:** SSZ matches GR in weak field  
**Source:** `PHYSICS_FOUNDATIONS.md` L357-359, `full-output.md` L5390

---

## 2. REGIME BOUNDARIES

| Regime | r/r_s Range | SSZ Behavior | Source |
|--------|-------------|--------------|--------|
| **Very Close** | r < 2 r_s | SSZ struggles (0% wins) | full-output L5333 |
| **Photon Sphere** | 2-3 r_s | SSZ OPTIMAL (82% wins) | full-output L5331 |
| **Strong Field** | 3-10 r_s | SSZ dominant (89% wins) | full-output L5697 |
| **Weak Field** | > 10 r_s | SSZ ≈ GR (~37% wins) | full-output L5334 |

### Blending Thresholds (Implementation)
- **REGIME_WEAK_THRESHOLD:** 110 r/r_s
- **REGIME_STRONG_THRESHOLD:** 90 r/r_s
- **Blend Zone:** 90-110 r/r_s (Hermite C² interpolation)

### φ/2 Natural Boundary
```
r_φ/2 = (φ/2) · r_s ≈ 0.809 · r_s ≈ 1.618 r_s
```
**Note:** Photon sphere (1.5 r_s) is NEAR φ/2 boundary - NOT coincidence  
**Source:** `PHI_FUNDAMENTAL_GEOMETRY.md` L36-44

---

## 3. ENERGY FORMULATION (CORRECTED)

### WRONG (Do Not Use)
```
E_tot = E_rest + E_GR + E_SR   ❌ MISLEADING
```

### CORRECT (Use This)
```
E_obs = E_rest × γ_SR × γ_GR   ✓ Multiplicative

OR equivalently:

E_obs = E_rest + ΔE_SR + ΔE_GR   ✓ Additive with deltas
Where:
  ΔE_SR = E_rest × (γ_SR - 1)
  ΔE_GR = E_rest × (γ_GR - 1)
```

**Key Principle:** E_rest is BASELINE/ANCHOR, not additive term  
**Source:** `CRITICAL_PHYSICS_CORRECTION.md` L42-54

---

## 4. INVARIANTS THAT MUST HOLD

| Invariant | Condition | Tolerance | Source |
|-----------|-----------|-----------|--------|
| Dual Velocity | v_esc × v_fall = c² | Machine precision | full-output L3013 |
| PPN β | β = 1.0 | Exact | full-output L5390 |
| PPN γ | γ = 1.0 | Exact | full-output L5390 |
| C¹ Continuity | Metric smooth | PASS | full-output L3428 |
| C² Continuity | Ricci smooth | PASS | full-output L6380 |

---

## 5. ENERGY CONDITIONS

| Condition | r ≥ 5 r_s | r < 5 r_s | Source |
|-----------|-----------|-----------|--------|
| WEC (Weak) | ✓ PASS | ✗ FAIL | full-output L3312-3314 |
| DEC (Dominant) | ✓ PASS | ✗ FAIL | full-output L3312-3314 |
| SEC (Strong) | ✓ PASS | ✗ FAIL | full-output L3312-3314 |

**Interpretation:** SSZ is physically consistent outside 5 r_s

---

## 6. φ-GEOMETRY REQUIREMENTS

### φ is FUNDAMENTAL (Not Optional)
| Scenario | Performance | Source |
|----------|-------------|--------|
| WITHOUT φ-geometry | 0% wins (total failure) | full-output L5337 |
| WITH φ-geometry | 51-99.1% wins | full-output L5338, L6154 |

### φ appears in:
1. **Natural boundary:** r_φ = (φ/2) r_s
2. **Segment density:** Ξ(r) = Ξ_max(1 - exp(-φr_s / r))
3. **Mass correction:** α = 2.7177e4 (from φ-spiral pitch)
4. **β coupling:** Scale-free due to dimensionless φ

**Source:** `PHI_FUNDAMENTAL_GEOMETRY.md` L277-283

---

## 7. WHAT IS FORBIDDEN

### 7.1 Formula Modifications
- ❌ Changing φ to any other value
- ❌ Removing Δ(M) correction
- ❌ Using deprecated Ξ formula: `Ξ = (r_s/r)² × exp(-r/r_φ)`
- ❌ Mixing GR helper logic with SSZ core

### 7.2 Test Manipulation
- ❌ Deleting or weakening existing tests
- ❌ Creating tests not grounded in full-output.md
- ❌ "SSZ must always win" bias
- ❌ Ignoring regime-specific performance

### 7.3 Energy Interpretation
- ❌ Using additive E_rest + E_GR + E_SR notation
- ❌ Treating γ factors as energy sources
- ❌ Triple-counting energy

---

## 8. VALIDATION METRICS (From full-output.md)

### Overall Success Rate
| Source | n | Wins | Rate | p-value |
|--------|---|------|------|---------|
| ESO Spectroscopy | 47 | 46 | 97.9% | <0.0001 |
| Energy Framework | 64 | 64 | 100.0% | <0.0001 |
| Test Suite | 63 | 63 | 100.0% | <0.0001 |
| **COMBINED** | **111** | **110** | **99.1%** | <0.0001 |

**Source:** `full-output.md` L6147-6154

### Universal Power Law
```
E/E_rest = 1 + 0.32(r_s/R)^0.98
R² = 0.997
```
**Source:** `full-output.md` L6164, L6320

---

## 9. METHOD SELECTION RULES

| Observable | Method | Reason |
|------------|--------|--------|
| Time dilation | Ξ → D = 1/(1+Ξ) | Only g_tt |
| Frequency shift | Ξ | Only g_tt |
| **Lensing** | **PPN (1+γ)** | g_tt + g_rr |
| **Shapiro delay** | **PPN (1+γ)** | g_tt + g_rr |
| Perihel precession | PPN (γ,β) | Full metric |

**Source:** Memory `SSZ Situative Physik`

---

## 10. CONTRACT SIGNATURES

### This contract binds:
1. All code modifications to SSZ repositories
2. All new tests must reference existing artifacts
3. Physics changes require documentary evidence
4. No "invented" validations allowed

### Evidence Chain:
```
full-output.md → Truth Map → Implementation Contract → Code Changes
```

### Violation = Rejection

---

*Implementation Contract extracted from official SSZ documentation*  
*© 2025 Carmen Wrede & Lino Casu*
