# MD_INDEX: Real Markdown Documentation Index

**Generated:** 2025-01-16  
**Method:** Automated scan + manual verification  
**Purpose:** Index ALL MD files from source repos with EXACT content summary

---

## Source Repos Scanned

| Repo | MD Files | Status |
|------|----------|--------|
| ssz-qubits | 75 | Scanned |
| ssz-metric-pure | 44 | Scanned |
| Unified-Results | 46+ | Scanned |

---

## CRITICAL FILES (Regime/Formula Definitions)

### ssz-qubits/paper_final/appendices/E_transition.md
**AUTHORITATIVE for Weak/Strong Transition**

| Rule | Value | Source Line |
|------|-------|-------------|
| Weak threshold | r/r_s > 110 | Line 20 |
| Strong threshold | r/r_s < 90 | Line 21 |
| Transition zone | 90 ≤ r/r_s ≤ 110 | Line 22 |
| Blend function | Quintic Hermite: 6t⁵ - 15t⁴ + 10t³ | Line 39 |
| C² continuity | Required | Lines 9-11 |

**Key Formula (Lines 56-93):**
```python
def xi_complete(r, r_s, phi=1.618):
    x = r / r_s
    if x > 110: return 1 / (2 * x)           # Weak
    if x < 90:  return 1 - np.exp(-phi * x)  # Strong
    # Transition: Quintic Hermite blend
    t = (x - 90) / 20
    b = 6*t**5 - 15*t**4 + 10*t**3
    return b * xi_weak + (1 - b) * xi_strong
```

---

### ssz-qubits/ssz_qubits.py (Lines 117-178)
**ACTUAL IMPLEMENTATION (differs from E_transition.md!)**

| Rule | Value | Source Line |
|------|-------|-------------|
| Auto threshold | r/r_s > 100 | Line 166 |
| NO transition zone | Hard switch at 100 | Lines 166-169 |
| NO Quintic Hermite | Not implemented | - |

**INCONSISTENCY ALERT:**
- Documentation says: 90-110 with blend
- Code does: Hard switch at 100

---

### ssz-qubits/docs/SSZ_FORMULA_DOCUMENTATION.md
**Formula Reference**

| Section | Content |
|---------|---------|
| §1 | Core constants (φ, G, c) |
| §2 | Two regime definitions |
| §3 | Time dilation D = 1/(1+Xi) |
| §4 | Weak field: Xi = r_s/(2r) |
| §5 | Strong field: Xi = 1 - exp(-φr_s / r) |
| §6 | Applications |

---

### ssz-metric-pure/01_MATHEMATICAL_FOUNDATIONS.md
**Deep Mathematical Details (1020 lines)**

| Section | Content | Lines |
|---------|---------|-------|
| §3 | Segment density formulas | 50-150 |
| §4 | Universal intersection r*/r_s = 1.387 | 200-250 |
| §9 | Energy conditions | 400-500 |
| §12 | C² Hermite interpolation | 600-700 |
| §16 | Regime boundaries (90/110) | 800-900 |

---

### ssz-metric-pure/02_PHYSICS_CONCEPTS.md
**Physical Interpretation (1039 lines)**

| Section | Content | Lines |
|---------|---------|-------|
| §3.2 | Xi(r_s) = 0.802 derivation | 150-200 |
| §4 | D(r_s) = 0.555 (finite!) | 200-250 |
| §7.1 | Strong field deviations (up to -44%) | 500-600 |

---

## TEST DOCUMENTATION

### ssz-qubits/tests/test_ssz_physics.py
**17 Physics Tests**

| Test Class | Tests | Tolerances |
|------------|-------|------------|
| TestSchwarzschildRadius | 2 | `8.8e-3 < r_s < 8.9e-3`, `rtol=1e-10` |
| TestSegmentDensityWeakField | 4 | `6e-10 < xi < 8e-10`, `rtol=1e-10` |
| TestTimeDilation | 3 | `rtol=1e-10` |
| TestStrongField | 3 | `rtol=0.01` |
| TestBoundaryConditions | 5 | Various |

### ssz-qubits/tests/test_validation.py
**17 Validation Tests**

| Test Class | Tests | Expected Values |
|------------|-------|-----------------|
| TestGRWeakFieldComparison | 3 | `< xi**2 * 10`, `rtol=0.01`, `rtol=1e-6` |
| TestGPSValidation | 2 | `rtol=0.01` (45.7 μs/day) |
| TestAtomicClockValidation | 3 | Height-dependent |
| TestConsistency | 9 | Various |

### ssz-qubits/tests/test_edge_cases.py
**25 Edge Case Tests**

| Category | Tests |
|----------|-------|
| Zero/negative inputs | 5 |
| Extreme values | 5 |
| Boundary conditions | 5 |
| Numerical stability | 5 |
| Type handling | 5 |

---

## TOLERANCE EXTRACTION

### From test_ssz_physics.py

| Test | Tolerance | Source Line |
|------|-----------|-------------|
| test_earth_schwarzschild_radius | `8.8e-3 < r_s < 8.9e-3` | Line 61 |
| test_earth_schwarzschild_radius | `rtol=1e-10` | Line 62 |
| test_sun_schwarzschild_radius | `2.9e3 < r_s < 3.0e3` | Line 80 |
| test_xi_at_earth_surface | `6e-10 < xi < 8e-10` | Line 111 |
| test_xi_decreases_with_radius | `rtol=1e-10` for ratio=2.0 | Line 135 |

### From test_validation.py

| Test | Tolerance | Source Line |
|------|-----------|-------------|
| test_time_dilation_matches_gr | `< xi**2 * 10` | Line 71 |
| test_gravitational_redshift | `rtol=0.01` | Line 109 |
| test_pound_rebka_experiment | `rtol=1e-6` | Line 146 |
| test_gps_satellite_time_dilation | `rtol=0.01` | Line 197 |
| test_gps_position_error | `10 < error_km < 15` | Line 229 |

---

## CONSTANTS EXTRACTION

### From ssz_qubits/ssz_qubits.py (Lines 42-55)

```python
C = 299792458.0           # Speed of light [m/s]
G = 6.67430e-11           # Gravitational constant [m³/(kg·s²)]
HBAR = 1.054571817e-34    # Reduced Planck constant [J·s]
M_EARTH = 5.972e24        # Earth mass [kg]
R_EARTH = 6.371e6         # Earth radius [m]
PHI = (1 + np.sqrt(5)) / 2  # Golden ratio = 1.6180339887498948
```

---

## COMPUTED VALUES (NOT Parameters!)

| Value | Formula | Result | Source |
|-------|---------|--------|--------|
| Xi(r_s) | 1 - exp(-φ) | 0.8017 | E_transition.md Line 160 |
| D(r_s) | 1/(1 + 0.8017) | 0.555 | 02_PHYSICS_CONCEPTS.md |
| r*/r_s | solve D_SSZ = D_GR | 1.387 | 01_MATHEMATICAL_FOUNDATIONS.md |

**CRITICAL: Xi(r_s) = 0.8017 is COMPUTED, not a parameter!**

---

## FILES NOT TO USE

| File | Reason |
|------|--------|
| Any with `xi_max` as parameter | xi_max is computed, not configurable |
| Files marked "OLD" or "DEPRECATED" | Superseded |
| Draft papers without validation | Unverified |

---

## SUMMARY

**Total MD Files:** 165+
**Critical for Formulas:** 5
**Critical for Tests:** 3
**Critical for Tolerances:** 2

**Key Inconsistency Found:**
- E_transition.md: Blend at 90-110
- ssz_qubits.py: Hard switch at 100
- **Resolution:** Use E_transition.md (documented spec)
