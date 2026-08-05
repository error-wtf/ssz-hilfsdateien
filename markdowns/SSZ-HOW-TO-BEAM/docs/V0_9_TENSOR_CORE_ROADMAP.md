# v0.9 Tensor-Core Roadmap

**Date:** 2026-06-09

## Goal

Move from proxy/algebraic bridge checks to tensor-derived validation for v0.9.

## Non-Goals (Explicit)

- ❌ No human transport claim
- ❌ No "solved beaming" claim
- ❌ No experimental claim
- ❌ No metric formation claim unless actually implemented

---

## Required Modules

```
src/beam_ssz/tensor_core/
├── __init__.py
├── coordinates.py          # CoordinateIndex, COORD_NAMES
├── metric_backend.py       # Minkowski, SSZ metric arrays
├── finite_differences.py   # Central diff, convergence
├── christoffel.py          # Gamma[lam,mu,nu]
├── riemann.py              # R[rho,sigma,mu,nu]
├── ricci.py                # Ricci[mu,nu], R_scalar
├── einstein.py             # Einstein[mu,nu]
├── stress_energy.py        # T[mu,nu] from Einstein
├── null_vectors.py         # Test null vectors k^mu
├── energy_conditions.py    # NEC/WEC/SEC/DEC status
├── validation.py           # Tensor validation gates
└── status.py               # TensorStatus, EnergyConditionStatus
```

---

## Required Data Structures

**Use arrays, NOT string tuple keys:**

```python
g[mu, nu]           # Metric tensor
g_inv[mu, nu]       # Inverse metric
Gamma[lam, mu, nu]  # Christoffel symbols
R[rho, sigma, mu, nu]  # Riemann tensor
Ricci[mu, nu]       # Ricci tensor
Einstein[mu, nu]    # Einstein tensor
T[mu, nu]           # Stress-energy tensor
```

**Index convention:**
- 0 = t (time)
- 1 = r (radial)
- 2 = theta
- 3 = phi

---

## Required Tests

### tests/test_tensor_core_minkowski.py
- Minkowski metric gives Christoffel = 0
- Riemann = 0
- Ricci = 0  
- Einstein = 0

### tests/test_tensor_core_flat_bridge.py
- Xi=0, lambda=0 bridge gives flat limit
- Determinant finite
- No false curvature (numerical zero)

### tests/test_tensor_core_ssz_horizon.py
- SSZ metric near r_s has finite D, s, determinant
- No singular divergence from SSZ regularization
- Tensor components remain finite

### tests/test_energy_conditions_proxy_vs_tensor.py
- Heuristic energy class remains PROXY_ONLY
- Tensor energy class requires T_mu_nu computation
- NEC/WEC/SEC/DEC statuses cannot be claimed from heuristic proxy
- Test confirms heuristic cannot auto-produce NEC_PASS

### tests/test_numerical_convergence.py
- Finite-difference derivative convergence on known analytic functions
- Grid refinement reduces error
- Convergence rate estimation works

---

## Required Validation Gates

### Gate 1: Minkowski Zero-Curvature
- Cartesian: All curvature tensors exactly zero
- Spherical: Numerically zero within tolerance

### Gate 2: Flat Bridge Zero-Curvature
- Xi=0, lambda=0 → no curvature
- Determinant = -r^4 sin^2(theta) for s=1/D case

### Gate 3: SSZ Finite-Horizon
- r near critical point: D finite, s finite
- No NaN/inf in Gamma, Ricci, Einstein

### Gate 4: Einstein Tensor Finite
- G[mu,nu] finite everywhere tested
- Symmetric: G[mu,nu] == G[nu,mu]

### Gate 5: Energy-Condition Classifier
- Works on known toy stress tensors
- Positive energy density → NEC pass
- Negative energy density → NEC fail

### Gate 6: Bridge Candidate Application
- Only after Gates 1-5 pass
- Each candidate gets explicit tensor diagnostic

---

## Output Statuses

### Allowed Status Values:

**Tensor Status:**
```python
TENSOR_NOT_RUN
TENSOR_PASS_FLAT_LIMIT
TENSOR_PASS_FINITE
TENSOR_NUMERIC_WARNING
TENSOR_FAILED
```

**Energy Condition Status:**
```python
NOT_RUN
PROXY_ONLY
TENSOR_PENDING
NEC_PASS_NUMERIC
NEC_FAIL_NUMERIC
WEC_PASS_NUMERIC
WEC_FAIL_NUMERIC
SEC_PASS_NUMERIC
SEC_FAIL_NUMERIC
DEC_PASS_NUMERIC
DEC_FAIL_NUMERIC
ENERGY_UNDEFINED
```

### Forbidden (without tensor evidence):
```
"NEC satisfied"
"Energy conditions proven"
"No exotic matter required"
```

---

## Acceptance Criteria for v0.9

- [ ] All new tensor_core tests pass
- [ ] All v0.8 tests still pass
- [ ] TensorStatus and EnergyConditionStatus implemented
- [ ] Heuristic energy cannot auto-pass NEC
- [ ] CURRENT_STATUS.md updated with tensor results
- [ ] README honest about tensor progress
- [ ] No unqualified energy-condition claims

### Tensor Validation Claim Progression:

**v0.8 (current):**
- Tensor-level curvature validation: PENDING
- Energy-condition validation: PENDING

**v0.9 (target):**
- Tensor-level curvature validation: PARTIAL / PASS (depending on Gate results)
- Energy-condition validation: still pending unless tensor T_mu_nu fully implemented

---

## Paper Positioning for v0.9

### v0.9 MAY Support:
- Mathematical bridge-candidate classification
- Tensor diagnostic results (flat limit, finiteness)
- Falsifiable numerical predictions from proxies
- Observable design framework

### v0.9 MAY NOT Claim:
- Solved beaming
- Human transport feasibility
- Full metric formation
- Experimental validation
- Complete energy-condition proof (unless fully implemented)

---

## Implementation Notes

### Finite Differences:
```python
def central_diff_scalar(f, x, i, h):
    """Central difference for scalar function."""
    x_plus = x.copy()
    x_minus = x.copy()
    x_plus[i] += h
    x_minus[i] -= h
    return (f(x_plus) - f(x_minus)) / (2*h)
```

### Metric Access:
```python
class CoordinateIndex(IntEnum):
    T = 0
    R = 1
    THETA = 2
    PHI = 3
```

### Energy Condition Check:
```python
def check_nec(T, g, null_vectors, tolerance=1e-10):
    """
    Check NEC: T_mu_nu k^mu k^nu >= -tolerance
    Only valid if T is computed from Einstein tensor.
    """
    for k in null_vectors:
        if contract(T, k, k, g) < -tolerance:
            return NEC_FAIL_NUMERIC, k
    return NEC_PASS_NUMERIC, None
```

---

## Success Metrics

v0.9 is successful when:
1. `pytest tests/test_tensor_core_*.py` passes
2. `pytest tests/test_energy_conditions_proxy_vs_tensor.py` passes
3. Minkowski curvature numerically zero (< 1e-6)
4. Flat bridge has no false curvature
5. SSZ candidate tensors are finite
6. Heuristic proxy cannot claim NEC pass
7. CURRENT_STATUS.md updated honestly

---

## Next After v0.9

**v1.0 target:**
- Full validation pipeline with tensor gates
- Observable proxies (phase, time delay, redshift)
- Numerical-GR convergence diagnostics
- Release-quality framework with peer-review prep

---

© 2025-2026 Carmen N. Wrede, Lino P. Casu
