# Known Limitations and Open Issues

**This document tracks the current state of validation for SSZ-HOW-TO-BEAM.**

Last updated: June 2026

---

## ✅ What IS Validated

### 1. Algebraic Regularity (High Confidence)
- **Status:** ✅ **VERIFIED**
- **Method:** Direct computation
- **Result:** D(u) > 0, s(u) > 0, det(g) ≠ 0 for canonical parameter ranges
- **Files:** `bridge_metric.py`, `tensor/metric_tensor.py`

### 2. Worldline Continuity (High Confidence)
- **Status:** ✅ **VERIFIED**
- **Method:** Algebraic check of timelike condition
- **Result:** g_μνu^μu^ν < 0 maintained through bridge
- **Files:** `bridge_metric.py`, `worldline.py`

### 3. Distance Reduction Formula (High Confidence)
- **Status:** ✅ **VERIFIED**
- **Method:** Analytical integration
- **Result:** η = L_bridge/L_normal << 1 achievable
- **Files:** `bridge_metric.py`

---

## ⚠️ Partially Validated (Needs Extension)

### 4. Tensor Scaffold (Moderate Confidence)
- **Status:** ⚠️ **SCAFFOLD ONLY**
- **Issues:**
  - Christoffel symbols: Sign convention verified for Γ^r_tt
  - Riemann tensor: Index structure corrected (was broken tuples)
  - Determinant: Fixed to det(g) = -r⁴sin²θ (removed erroneous D⁴ factor)
- **Needs:** Cross-validation against known solutions (Schwarzschild, Minkowski)
- **Files:** `tensor/*.py`

### 5. Symbolic λ_crit Derivation (In Progress)
- **Status:** ⚠️ **PARTIAL**
- **Result:** Model-dependent threshold identified
- **Needs:** Full tensor-level derivation (not just algebraic proxy)
- **Files:** `symbolic/lambda_crit_derivation.py`

---

## ❌ NOT Validated (Critical Blockers)

### 6. Full Numerical GR Evolution
- **Status:** ❌ **NOT PERFORMED**
- **Blocker:** Requires 10⁶ CPU-hours on supercomputer
- **Current:** Only initial data generation scaffold exists
- **Files:** `numerical_gr/pipeline.py`

### 7. Energy Condition Verification
- **Status:** ❌ **NOT VERIFIED**
- **Blocker:** Requires full Einstein tensor from metric
- **Current:** Only proxy classification (heuristic_energy_class)
- **Files:** `energy_conditions.py`, `tensor/einstein.py`

### 8. Stability Analysis
- **Status:** ❌ **LINEAR ONLY**
- **Blocker:** Non-linear stability requires numerical GR
- **Current:** Linear perturbation theory only
- **Files:** `stability_analysis.py`

### 9. Extended-Body Transport (Human-scale)
- **Status:** ❌ **FAILS FOR DEFAULT PARAMETERS**
- **Result:** Tidal forces exceed human tolerance by 10¹⁶ g
- **Note:** Gradual entry protocol alone insufficient
- **Files:** `human_transport/gradual_entry_protocol.py`

### 10. Metric Formation Mechanism
- **Status:** ❌ **SPECULATIVE ONLY**
- **Blocker:** No physical mechanism to create bridge from flat spacetime
- **Current:** DCE (Dynamical Casimir Effect) proposal unverified
- **Files:** `docs/25_unresolved_solutions.md`

### 11. Energy Source
- **Status:** ❌ **NO VIABLE MECHANISM**
- **Blocker:** 10²⁰+ Joules sustained requires Dyson-scale infrastructure
- **Current:** Hybrid proposal (stellar + vacuum) unbuilt
- **Timeline:** Millennia

---

## 🚫 Fundamental Limits (Not Addressable)

### 12. Quantum Gravity Regime
- **Limit:** ρ > 10¹¹³ J/m³
- **Status:** Framework breaks down, needs quantum gravity

### 13. Exotic Matter Existence
- **Limit:** λ > λ_crit requires T_μν violating NEC
- **Status:** Macroscopic exotic matter unproven

---

## Summary Table

| Component | Status | Confidence | Blocker |
|-----------|--------|------------|---------|
| Algebraic regularity | ✅ Verified | High | None |
| Worldline continuity | ✅ Verified | High | None |
| Distance formula | ✅ Verified | High | None |
| Tensor scaffold | ⚠️ Partial | Moderate | Cross-validation |
| λ_crit symbolic | ⚠️ Partial | Moderate | Full tensor derivation |
| Numerical GR evolution | ❌ Not done | N/A | Supercomputer time |
| Energy conditions | ❌ Not verified | N/A | Full tensor computation |
| Non-linear stability | ❌ Not done | N/A | Numerical simulation |
| Extended-body transport | ❌ Fails default | N/A | Parameter search |
| Formation mechanism | ❌ Speculative | N/A | Unknown physics |
| Energy source | ❌ No mechanism | N/A | Infrastructure |

---

## Version History

- **v0.6.0:** Initial release with algebraic checks
- **v0.6.1:** Fixed portable paths, exports, removed .git
- **v0.6.2:** Fixed tensor bugs (determinant, Christoffel sign, Riemann indices)
- **v0.7.0 (planned):** Tensor cross-validation against known solutions
- **v0.8.0 (planned):** Full numerical GR pipeline execution

---

## For Researchers

**If you want to contribute:**

1. **Immediate (can do now):**
   - Cross-validate tensor scaffold against Schwarzschild metric
   - Extend symbolic derivation to full tensor components
   - Search parameter space for tidal-safe configurations

2. **Short-term (months):**
   - Set up numerical GR pipeline on university cluster
   - Design inert extended-body benchmarks
   - Validate energy condition classification

3. **Long-term (years-decades):**
   - Execute full 3D numerical relativity simulations
   - Develop metric formation experiments (if DCE scalable)
   - Design stellar energy collection (if Dyson swarm feasible)

---

© 2025-2026 Carmen N. Wrede, Lino P. Casu
