# SSZ-HOW-TO-BEAM v0.9.0 Release

**Date:** 2026-06-09  
**Version:** 0.9.0  
**Status:** Tensor-Core Implementation Complete

---

## Summary

v0.9.0 implements the complete tensor-core framework with:
- Array-based tensor computations (numpy)
- SSZ Prime Directive observable classification
- Strict separation: proxy vs tensor-derived diagnostics
- SSZ-referenced validation (not Minkowski as physical truth)

---

## New in v0.9.0

### 1. Tensor Core (`src/beam_ssz/tensor_core/`)

Array-based tensor calculations:
- `coordinates.py` - CoordinateIndex (t=0, r=1, theta=2, phi=3)
- `metric_backend.py` - Minkowski, SSZ metric arrays
- `finite_differences.py` - Central diff, convergence tests
- `christoffel.py` - Gamma[lam,mu,nu]
- `riemann.py` - R[rho,sigma,mu,nu]
- `ricci.py` - Ricci[mu,nu] + scalar
- `einstein.py` - G[mu,nu]
- `stress_energy.py` - T[mu,nu] from Einstein
- `null_vectors.py` - Test null vectors
- `energy_conditions.py` - NEC/WEC checks (tensor-derived)
- `validation.py` - Tensor validation gates
- `status.py` - TensorStatus, EnergyConditionStatus

### 2. Observable Dispatcher (`tensor_core/observable_dispatcher.py`)

**Implements SSZ Prime Directive:**
```
Observable → Class → Method → Scope → Calculate
```

Critical rules:
- NULL (light) → PPN (1+γ)
- TIMELIKE STATIC (clocks) → Ξ-proxy
- TIMELIKE ORBIT → PPN (γ,β)
- Factor-2 rule: Ξ-only = 50% of GR for null

### 3. Energy Proxy Separation (`src/beam_ssz/energy_proxy.py`)

**Strict separation:**
- `EnergyProxyStatus` - HEURISTIC ONLY
- `EnergyConditionStatus` - TENSOR-DERIVED ONLY

**Rule:** Proxy CANNOT claim NEC pass. Only tensor T_mu_nu can.

### 4. SSZ Validation Tests

**Gate 0:** `test_tensor_core_minkowski.py` - Code sanity (Minkowski)
**Gate A:** `test_ssz_segmentation_rules.py` - SSZ laws
**Gate B:** `test_ssz_effective_distance.py` - d_eff collapse
**Gate C:** `test_ssz_continuous_worldline.py` - Worldline continuity
**Gate D/E:** Within worldline tests - No-copy, matter continuity

### 5. Observable Tests

`test_observable_dispatcher.py`:
- Regime classification (very_close → weak)
- Observable classification (null vs timelike)
- Factor-2 rule validation
- Prime Directive pipeline

---

## Architecture

### Minkowski vs SSZ

| | Minkowski | SSZ |
|---|---|---|
| **Role** | Code sanity baseline | Physical reference |
| **Purpose** | Test if tensor engine works | Validate segmentation laws |
| **Claim** | "Calculator outputs 2+2=4" | "Xi/D/s obey SSZ rules" |

**Minkowski:** Riemann = 0 tests the code, not the physics.

### Transport Model

**Variante B: Continuous Worldline**
```
d_eff(A,B) → 0
N(A) ∩ N(B) ≠ ∅
x^μ(τ): A → B, dτ > 0
```

**NOT:**
- Destructive scan
- Copy-reconstruction
- Pattern buffer as identity

**Carmen bleibt Carmen because:**
- Her worldline doesn't break
- Not because she's copied

---

## Test Suite

### Core Tests (v0.4/v0.6)
- 299 tests passing
- Bridge metric, validators, geodesics

### Tensor Core Tests (v0.9)
- `test_tensor_core_minkowski.py` - Gate 0
- `test_tensor_core_flat_bridge.py` - Xi=0 limit
- `test_tensor_core_shapes.py` - Shape/symmetry
- `test_ssz_segmentation_rules.py` - Gate A
- `test_ssz_effective_distance.py` - Gate B
- `test_ssz_continuous_worldline.py` - Gates C,D,E
- `test_observable_dispatcher.py` - Prime Directive
- `test_energy_proxy_separation.py` - Proxy vs tensor

**Total:** 335+ tests

---

## Claim Gates

| Gates | Allowed | Forbidden |
|---|---|---|
| 0 | "Tensor engine: OK" | "SSZ physics validated" |
| 0+A | "SSZ segmentation: consistent" | "Transport solved" |
| 0+A+B | "d_eff reduction: proxy passes" | "Physical beaming" |
| 0+A+B+C | "Worldline continuity: proxy passes" | "Identity proven" |
| 0+A+B+C+D | "No-copy mode: enforced" | "Copy mode OK" |
| 0+A+B+C+D+E | "Matter continuity: documented" | "Matter recreation OK" |
| **All** | "SSZ candidate at proxy level" | **"Human transport possible"** |

**Regardless:**
- Biological transport: NOT_VALIDATED
- Physical formation: UNRESOLVED
- Experimental validation: NONE

---

## Scientific Statement

**English:**
> BEAM-SSZ does not treat a person as information to be copied, but as a continuous worldline whose effective segment-distance between origin and target is reduced by a controlled SSZ bridge.

**German:**
> BEAM-SSZ behandelt eine Person nicht als kopierbares Informationsmuster, sondern als kontinuierliche Weltlinie, deren effektiver Segmentabstand zwischen Ursprung und Ziel durch eine kontrollierte SSZ-Brücke reduziert wird.

---

## Files

### Source
```
src/beam_ssz/
├── __init__.py (v0.9.0 exports)
├── tensor_core/ (12 modules)
├── energy_proxy.py
└── [v0.4/v0.6 modules]
```

### Tests
```
tests/
├── test_tensor_core_*.py (3 files)
├── test_ssz_*.py (3 files)
├── test_observable_dispatcher.py
├── test_energy_proxy_separation.py
└── [v0.4/v0.6 tests]
```

### Documentation
```
docs/
├── SSZ_VALIDATION_FRAMEWORK.md
├── V1_0_ROADMAP.md
└── [existing docs]
```

---

## Usage

```python
from beam_ssz import (
    # v0.9 tensor core
    CoordinateIndex,
    ssz_metric,
    compute_christoffel,
    compute_einstein,
    # v0.9 observable dispatcher
    ObservableType,
    classify_regime,
    compute_observable_factor,
    # v0.9 energy proxy
    EnergyProxyStatus,
)

# SSZ metric
x = np.array([0.0, 2.0, np.pi/2, 0.0])
Xi = 0.5
D = 1.0 / (1.0 + Xi)
s = 1.0 + Xi
g = ssz_metric(x, D, s)

# Observable classification
result = compute_observable_factor(
    ObservableType.TIMELIKE_STATIC,
    r=10.0,
    r_s=1.0,
)
# Returns: Xi, D, method="XI_PROXY", regime="WEAK"
```

---

## Version History

- **v0.4:** Base SSZ framework
- **v0.6:** Bridge metric
- **v0.8:** Release cleanup, ham fix
- **v0.9.0:** Tensor core, Prime Directive, SSZ validation framework

---

## Next: v1.0

Target: Full validation pipeline with
- Observable proxies (phase, time delay, redshift)
- Numerical-GR convergence diagnostics
- Paper-ready claim gates

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
