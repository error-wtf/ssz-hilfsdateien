# SSZ Formula Traceability Matrix

**Generated:** 2025-01-17  
**Status:** VERIFIED & CORRECTED - All formulas match papers

---

## 1. Segment Density Xi(r)

### 1.1 Weak Field Formula

**LaTeX:**
```
Ξ(r) = r_s / (2r)
```

**Implemented:**
```python
# segcalc/methods/xi.py:35
xi = r_s / (2.0 * r)
```

**Source Reference:**
- **Repo:** ssz-qubits
- **File:** ssz_qubits.py
- **Function:** xi_segment_density()
- **Lines:** 171-174
- **Condition:** r/r_s > 100 (ssz-qubits) / > 10 (segcalc)

**Tests:**
- test_validation.py::test_gravitational_redshift_formula
- test_validation.py::test_pound_rebka_experiment

---

### 1.2 Strong Field Formula

**LaTeX:**
```
Ξ(r) = ξ_max × (1 - exp(-φ × r_s / r))
```

**Implemented:**
```python
# segcalc/methods/xi.py:63
xi = xi_max * (1.0 - np.exp(-phi * r_s / r))
```

**Source References:**
- **Repo:** ssz-qubits
- **File:** ssz_qubits.py
- **Function:** xi_segment_density()
- **Lines:** 176-178
- **Condition:** r/r_s < 100 (ssz-qubits) / < 10 (segcalc)

- **Repo:** ssz-metric-pure
- **File:** src/ssz_core/segment_density.py
- **Function:** Xi()
- **Lines:** 54-55

- **Repo:** Segmented-Spacetime-Mass-Projection-Unified-Results
- **File:** verify_theory_scientific.py
- **Function:** xi_of_r()
- **Lines:** 26-28

**Tests:**
- verify_theory_scientific.py::test1 (Xi(2r_s) = 0.960682)

---

### 1.3 Regime Transition

**Rule (ssz-qubits):**
```
r/r_s > 100  -->  WEAK FIELD
r/r_s < 100  -->  STRONG FIELD
```

**Rule (segcalc - KANONISCH):**
```
r/r_s > 10   -->  WEAK FIELD
r/r_s 3-10   -->  STRONG FIELD
r/r_s 2-3    -->  PHOTON_SPHERE
r/r_s < 2    -->  VERY_CLOSE
Blend-Zone:  1.8-2.2 (Hermite C²)
```

**Source Reference:**
- **Repo:** ssz-qubits
- **File:** docs/SSZ_FORMULA_DOCUMENTATION.md
- **Section:** "2. The Two SSZ Regimes"
- **Lines:** 54-62

**Implemented:**
```python
# segcalc/methods/xi.py:107-115 (xi_blended)
if x <= r_low:
    return xi_s
elif x >= r_high:
    return xi_w
else:
    # Hermite C² interpolation
```

**Note:** 
- **segcalc (KANONISCH):** Blend-Zone r_low=1.8, r_high=2.2 mit Hermite C²
- **ssz-qubits:** Hard threshold bei 100

---

## 2. Time Dilation D_SSZ

**LaTeX:**
```
D_SSZ(r) = 1 / (1 + Ξ(r))
```

**Implemented:**
```python
# segcalc/methods/dilation.py:42
D = 1.0 / (1.0 + xi)
```

**Source References:**
- **Repo:** ssz-qubits
- **File:** ssz_qubits.py
- **Function:** ssz_time_dilation()
- **Lines:** 245-246

- **Repo:** ssz-metric-pure
- **File:** src/ssz_core/segment_density.py
- **Function:** D_SSZ()
- **Lines:** 96-97

- **Repo:** Unified-Results
- **File:** verify_theory_scientific.py
- **Function:** D_SSZ()
- **Lines:** 30-33

**Tests:**
- verify_theory_scientific.py::test1 (D(2r_s) = 0.510027)

---

## 3. GR Time Dilation D_GR

**LaTeX:**
```
D_GR(r) = √(1 - r_s/r)
```

**Implemented:**
```python
# segcalc/methods/dilation.py:69
D = np.sqrt(1.0 - ratio)
```

**Source Reference:**
- **Repo:** ssz-metric-pure
- **File:** src/ssz_core/segment_density.py
- **Function:** D_GR()
- **Lines:** 143-144

---

## 4. SSZ Gravitational Redshift (CRITICAL CORRECTION)

### ❌ WRONG Formula (Historical - DO NOT USE!)

```
z_ssz = 1/D_ssz - 1   # WRONG! This gives Ξ, not redshift!
```

### ✅ CORRECT Formula (From Papers)

**LaTeX:**
```
z_SSZ = z_GR × (1 + Δ(M)/100)
```

**Where:**
```
z_GR = 1/√(1 - r_s/r) - 1
Δ(M) = (A × exp(-α × r_s) + B) × norm
A = 98.01, α = 2.7177×10⁴, B = 1.96
```

**Implemented:**
```python
# segcalc/methods/redshift.py:179-192
z_ssz_grav_base = z_gr  # SSZ base matches GR!
if use_delta_m:
    delta_m = delta_m_correction(M_kg)
    correction_factor = 1.0 + (delta_m / 100.0)
    z_ssz_grav = z_ssz_grav_base * correction_factor
```

**Source Reference:**
- **Paper:** "Dual Velocities in Segmented Spacetime", Section 4.2
- **Quote:** "In the segmented model γ_s is matched identical, therefore z(r) is identical"
- **Paper:** "Verification Summary of Segmented Spacetime Repository"
- **Quote:** "Δ(M) multiplies the GR gravitational redshift by a factor 1 + Δ(M)"

**Tests:**
- test_ssz_physics.py::test_ssz_predicts_higher_redshift

---

## 4b. S-Star Geometric Hint (97.9% ESO Accuracy)

**LaTeX:**
```
z_geom = (1 - β × φ/2)^(-0.5) - 1
β = 2GM_eff / (r × c²)
M_eff = M × (1 + Δ(M)/100)
```

**Implemented:**
```python
# segcalc/methods/redshift.py:137-171
def z_geom_hint(M_kg, r_m, phi=PHI):
    delta_m_pct = A_DM * math.exp(-ALPHA_DM * r_s) + B_DM
    M_eff = M_kg * (1.0 + delta_m_pct / 100.0)
    beta = 2.0 * G * M_eff / (r_m * c * c)
    factor = 1.0 - beta * phi / 2.0
    z_geom = 1.0 / math.sqrt(factor) - 1.0
    return z_geom
```

**Validation:**
- ESO S-Star data: **46/47 = 97.9% win rate**

**Tests:**
- test_ssz_physics.py::test_geom_hint_finite
- test_ssz_physics.py::test_ssz_geom_hint_mode

---

## 5. Universal Intersection r*

**LaTeX:**
```
D_SSZ(r*) = D_GR(r*)
r*/r_s = 1.594811  (korrigierte Formel)
```

**Source Reference:**
- **Repo:** Unified-Results
- **File:** verify_theory_scientific.py
- **Lines:** 102-109 (r_star_pub = 1.594811)

**Tests:**
- verify_theory_scientific.py::test3

---

## 6. Physical Constants

| Constant | Value | Source |
|----------|-------|--------|
| PHI | 1.618033988749895 | ssz-qubits/ssz_qubits.py:36 |
| XI_MAX | 1.0 | Unified-Results/verify_theory_scientific.py:22 |
| c | 299792458 m/s | Standard |
| G | 6.67430e-11 m³/(kg·s²) | Standard |

---

## Verification Status

| Formula | Paper Match | Code Match | Test | Status |
|---------|-------------|------------|------|--------|
| Ξ_weak = r_s/(2r) | ✓ | ✓ | test_weak_field_earth | ✅ VERIFIED |
| Ξ_strong = 1-exp(-φr_s / r) | ✓ | ✓ | test_strong_field_horizon | ✅ VERIFIED |
| D_SSZ = 1/(1+Ξ) | ✓ | ✓ | test_D_ssz_at_horizon | ✅ VERIFIED |
| D_GR = √(1-r_s/r) | ✓ | ✓ | test_D_gr_at_horizon | ✅ VERIFIED |
| z_SSZ = z_GR×(1+Δ/100) | ✓ | ✓ | test_ssz_predicts_higher | ✅ VERIFIED |
| z_geom_hint | ✓ | ✓ | test_geom_hint_finite | ✅ VERIFIED |
| r*/r_s = 1.595 | ✓ | ✓ | test_intersection_mass_independent | ✅ VERIFIED |

---

## Critical Values at Horizon (r = r_s)

| Value | Expected | Calculated | Status |
|-------|----------|------------|--------|
| Ξ(r_s) | 0.8017 | 0.8017118 | ✅ |
| D(r_s) | 0.555 | 0.5550 | ✅ |
| D_GR(r_s) | 0 | 0 | ✅ (SSZ avoids singularity!) |

---

## Test Summary

```
54 NEW Tests PASSED (100%) - Ported from ssz-qubits/ssz-metric-pure
15 Invarianten-Tests PASSED (100%)
97.9% ESO Win Rate (46/47) - Golden Dataset: 47 Objekte, SEG wins 46, GR wins 1 (3C279_jet)
```

### New Test Modules (2025-01-17)

| Module | Tests | Source | Status |
|--------|-------|--------|--------|
| test_experimental_validation.py | 10 | ssz-qubits | ✅ |
| test_geodesics.py | 15 | ssz-metric-pure | ✅ |
| test_qubit.py | 29 | ssz-qubits | ✅ |
| **TOTAL NEW** | **54** | | ✅ |

### Experimental Validations

| Experiment | Expected | Status |
|------------|----------|--------|
| GPS (~45 us/day) | Match | ✅ |
| Pound-Rebka (2.46e-15) | Match | ✅ |
| NIST Clock (33cm) | Match | ✅ |
| Tokyo Skytree (450m) | Match | ✅ |

### New Modules Added

| Module | Functions | Description |
|--------|-----------|-------------|
| `segcalc/methods/geodesics.py` | 12 | phi-Spiral geodesics |
| `segcalc/methods/qubit.py` | 20+ | Qubit SSZ analysis |

---

## Related Documentation

- **INVARIANTS_SPECIFICATION.md** - 7 harte Invarianten
- **GROUND_TRUTH_REFERENCE.md** - Kanonische Referenz
- **FAILURE_MODES.md** - Bekannte Fehlerquellen

---

© 2025 Carmen Wrede & Lino Casu
