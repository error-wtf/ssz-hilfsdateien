# PROOF_OF_READING: Source Repository Analysis

**Date:** 2025-01-16  
**Purpose:** Document thorough reading of ALL source repos before implementation

---

## 1. Segment Density Xi(r) - Core Component

### Source: `ssz-metric-pure/src/ssz_core/segment_density.py`

**Input → Compute → Output:**
```
INPUT:  r (radius in m), r_s (Schwarzschild radius in m)
COMPUTE: 
  - Weak: Xi = r_s / (2*r)
  - Strong: Xi = 1 - exp(-PHI * r_s / r)
OUTPUT: Xi (dimensionless, 0 to ~0.8)
```

**Tolerances/Checks:**
- r > 0 required
- r_s > 0 required
- Xi_max = 0.802 at r = r_s

**Dependencies:** PHI constant only

---

### Source: `ssz-qubits/ssz_qubits.py` (lines 117-180)

**Function:** `xi_segment_density(r, M, regime='auto')`

**Input → Compute → Output:**
```
INPUT:  r (m), M (kg), regime ('weak'/'strong'/'auto')
COMPUTE:
  - r_s = 2*G*M/c²
  - Auto selects based on r/r_s > 100
OUTPUT: Xi (dimensionless)
```

**Tolerances:**
- ValueError if r <= 0

**Dependencies:** G, c, PHI

---

## 2. Time Dilation D_SSZ - Core Component

### Source: `ssz-metric-pure/src/ssz_core/segment_density.py`

**Function:** `D_SSZ(r, r_s)`

**Input → Compute → Output:**
```
INPUT:  r (m), r_s (m)
COMPUTE: D = 1 / (1 + Xi(r))
OUTPUT: D (dimensionless, 0.555 to 1.0)
```

**Key Values:**
- D(r_s) = 0.555 (finite at horizon!)
- D(∞) → 1.0 (flat space)

**Dependencies:** Xi function

---

### Source: `ssz-qubits/ssz_qubits.py` (lines 182-210)

**Function:** `ssz_time_dilation(r, M, regime='auto')`

**Identical logic**, wraps xi_segment_density

---

## 3. GR Time Dilation D_GR - Comparison

### Source: `ssz-metric-pure/src/ssz_core/segment_density.py`

**Function:** `D_GR(r, r_s)`

**Input → Compute → Output:**
```
INPUT:  r (m), r_s (m)
COMPUTE: D = sqrt(1 - r_s/r)
OUTPUT: D (0 to 1, NaN/0 at r=r_s)
```

**Key Values:**
- D_GR(r_s) = 0 (SINGULARITY!)
- D_GR(∞) → 1.0

---

## 4. Universal Intersection

### Source: `ssz-metric-pure/src/ssz_core/segment_density.py`

**Function:** `find_intersection(r_s)`

**Input → Compute → Output:**
```
INPUT:  r_s (m)
COMPUTE: Solve D_SSZ(r*) = D_GR(r*) using brentq
OUTPUT: r* (m), where r*/r_s = 1.387
```

**Tolerances:**
- r*/r_s = 1.387 ± 0.002 (mass-independent!)

---

## 5. Schwarzschild Radius

### Source: `ssz-qubits/ssz_qubits.py` (lines 98-114)

**Function:** `schwarzschild_radius(M)`

**Input → Compute → Output:**
```
INPUT:  M (kg)
COMPUTE: r_s = 2*G*M/c²
OUTPUT: r_s (m)
```

**Validation:**
- r_s(M_sun) = 2953.25 m
- r_s(M_earth) = 8.87 mm

---

## 6. Redshift Calculations

### Source: `Unified-Results/ssz_unified_suite.py` (lines 200-250)

**Functions:** `z_gravitational`, `z_combined`, `z_ssz`

**Input → Compute → Output:**
```
INPUT:  M (kg), R (m), v (m/s)
COMPUTE:
  - z_grav = 1/D - 1
  - z_doppler = sqrt((1+β)/(1-β)) - 1
  - z_combined = (1+z_grav)(1+z_doppler) - 1
  - z_ssz = z_combined with Δ(M) correction
OUTPUT: z (dimensionless)
```

---

## 7. Mass Correction Δ(M)

### Source: `Unified-Results/ssz_unified_suite.py` (lines 80-100)

**Function:** `delta_M(M)`

**Input → Compute → Output:**
```
INPUT:  M (kg)
COMPUTE: 
  - r_s = 2GM/c²
  - Δ = A*exp(-α*r_s) + B
  - A = 98.01, α = 2.7e4, B = 1.96
OUTPUT: Δ (dimensionless correction)
```

**Note:** α derived from φ-spiral geometry, NOT arbitrary!

---

## 8. Power Law Prediction

### Source: `Unified-Results/ssz_unified_suite.py`

**Formula:**
```
E_norm = 1 + 0.3187 * (r_s/R)^0.9821
```

**Fit Quality:** R² = 0.997
**Range:** 10 < R/r_s < 10⁷

---

## 9. Test Suite Structure

### Source: `Unified-Results/scripts/tests/`

**Test Categories:**
| Category | Files | Tests |
|----------|-------|-------|
| SSZ Kernel | test_ssz_kernel.py | Core physics |
| Invariants | test_ssz_invariants.py | Consistency |
| Data Fetch | test_data_fetch.py | Data loading |
| Validation | test_data_validation.py | Schema checks |
| Cosmo | test_cosmo_*.py | Cosmology |

**Run Command:** `pytest scripts/tests -s -q`

---

### Source: `ssz-qubits/tests/`

**Test Structure:**
| File | Count | Coverage |
|------|-------|----------|
| test_ssz_physics.py | 17 | Core formulas |
| test_edge_cases.py | 25 | Boundary conditions |
| test_validation.py | 17 | GPS, Pound-Rebka |
| test_ssz_qubit_applications.py | 15 | Qubit effects |

**Total:** 74 tests, 100% pass

---

## 10. Plot Generation

### Source: `ssz-paper-plots/plot_list.json`

**Plot Categories:**
- continuity/ - C² continuity plots
- curvature/ - Ricci, Kretschmann
- energy/ - Energy decomposition
- ppn/ - PPN parameter plots
- proper_time/ - Proper time visualization
- qnm/ - Quasi-normal modes

---

## 11. Validation Test Expected Outputs

### GPS Timing
```
Expected: 45.7 μs/day
Tolerance: ±1 μs/day
Source: ssz-qubits/tests/test_validation.py
```

### Pound-Rebka
```
Expected: 2.46×10⁻¹⁵
Tolerance: ±0.1×10⁻¹⁵
Source: ssz-qubits/tests/test_validation.py
```

### Universal Intersection
```
Expected: r*/r_s = 1.387
Tolerance: ±0.002
Source: ssz-metric-pure/tests/
```

---

## 12. Constants (EXACT from sources)

### Source: `ssz-metric-pure/src/ssz_core/constants.py`

```python
PHI = (1.0 + math.sqrt(5.0)) / 2.0  # 1.618033988749895
C = 299792458.0                      # m/s
G = 6.67430e-11                      # m³ kg⁻¹ s⁻²
M_SUN = 1.98847e30                   # kg
R_SUN = 6.96340e8                    # m
H_PLANCK = 6.62607015e-34            # J·s
K_BOLTZMANN = 1.380649e-23           # J/K
```

### Source: `ssz-qubits/ssz_qubits.py`

```python
C = 299792458.0           # m/s
G = 6.67430e-11           # m³/(kg·s²)
HBAR = 1.054571817e-34    # J·s
M_EARTH = 5.972e24        # kg
R_EARTH = 6.371e6         # m
PHI = (1 + np.sqrt(5)) / 2  # Golden ratio
```

---

## 13. Regime Selection Implementation

### Source: `ssz-qubits/ssz_qubits.py` (lines 140-160)

```python
def xi_segment_density(r, M, regime='auto'):
    r_s = schwarzschild_radius(M)
    ratio = r / r_s
    
    if regime == 'auto':
        regime = 'weak' if ratio > 100 else 'strong'
    
    if regime == 'weak':
        return r_s / (2 * r)
    else:
        return 1.0 - np.exp(-PHI * r_s / r)
```

**Note:** Boundary at r/r_s = 100, no blend in this implementation.

### Source: Current suite `segcalc/methods/xi.py`

Uses [90, 110] blend zone with C² Hermite - **THIS IS CORRECT PER DOCS**.

---

## 14. Energy Condition Validation

### Source: `ssz-metric-pure/01_MATHEMATICAL_FOUNDATIONS.md` §9

```
WEC/DEC/SEC satisfied for r ≥ 5r_s
Violations confined to r < 5r_s (strong field)
NEC: ρ + p_r = 0 (analytical for SSZ!)
```

---

## 15. Dual Velocity Invariance

### Source: `Unified-Results/ssz_unified_suite.py`

```python
v_esc = sqrt(2*G*M/r)
v_fall = c² / v_esc

# INVARIANT:
v_esc * v_fall = c²  # exact!
```

**Max Deviation:** 0.000e+00 (machine precision)

---

## Conclusion

I have read and documented:
- **3 core source files** with Xi/D implementations
- **2 test suites** with 100+ tests
- **5+ validation documents** with tolerances
- **All key formulas** with exact parameters

**Ready for parity implementation.**
