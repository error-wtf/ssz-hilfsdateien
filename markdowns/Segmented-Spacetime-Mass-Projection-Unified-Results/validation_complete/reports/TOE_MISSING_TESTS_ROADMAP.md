# ToE Missing Tests - Implementation Roadmap

**Complete checklist of missing ToE-level validation tests**

Date: 2025-10-29  
Priority: HIGH  
Status: Implementation Required

© 2025 Carmen Wrede & Lino Casu

---

## Current Status

### ✅ Already Validated (6 Pillars)

1. **P1** Universal Intersection (GR↔SSZ) - L2 mismatch & root bracket
2. **P2** φ-Invariance - |φ_meas - φ| ≤ Tol
3. **P3** Neutron Star Stability Band - relative bandwidth
4. **P4** Singularity Resolution - R_proxy(r→0) finite
5. **P5** Black Hole Bomb - Gain reduction ≥ 6×
6. **P6** Cosmology (SN/BAO/fσ8) - RMSE caps

**Score:** 6/6 PASS (100%)

---

## 🧪 Missing Tests (ToE Level)

### Priority 1: Mathematical/Foundational (CRITICAL)

#### **A-1: Local Lorentz Invariance & Equivalence Principle**

**Test:** Local metric → Minkowski as ΔN→0, free-fall geodesic, m_g = m_i

**Target:** Deviations < 10⁻¹³ (modern Eötvös bounds)

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_lorentz_equivalence.py`

---

#### **A-2: Bianchi Identities & Energy-Momentum Conservation**

**Test:** ∇_μ G^{μν}_{SSZ} = 0 ↔ ∇_μ T^{μν}_{eff} = 0

**Target:** Numerical residual < 10⁻¹⁰ (double precision stable)

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_bianchi_conservation.py`

---

#### **A-3: GR Limit (PPN Parameters)**

**Test:** N→∞ / ΔN→0 ⇒ (β,γ) → (1,1)

**Target:** |γ-1| ≤ 2×10⁻⁵, |β-1| ≤ 10⁻⁴ (Solar System bounds)

**Status:** ⚠️ PARTIAL (only β=γ=1 checked, not limit)

**Implementation:** `test_ppn_limit.py`

---

### Priority 2: Local/Solar Precision Tests

#### **B-4: Gravitational Redshift (Pound-Rebka)**

**Test:** Δν/ν vs. ΔΦ/c² from SSZ time dilation

**Target:** RMSE ≤ 1×10⁻⁵

**Status:** ⚠️ INDIRECT (time dilation validated, but not specific experiments)

**Implementation:** `test_gravitational_redshift_experiments.py`

---

#### **B-5: Shapiro Delay**

**Test:** Radar echo delay vs. SSZ time geometry

**Target:** γ-compatible with bounds

**Status:** ⚠️ PROXY (shapiro_proxy done, but not real data)

**Implementation:** `test_shapiro_delay_cassini.py`

---

#### **B-6: Perihelion/Periastron Precession**

**Test:** Δϖ_{SSZ} per orbit (Mercury & pulsar binaries)

**Target:** |Δϖ_{SSZ} - obs| / obs ≤ 1%

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_orbital_precession.py`

---

### Priority 3: Strong-Field Astrophysics

#### **C-7: ISCO Frequency & QPOs**

**Test:** ν_{ISCO,SSZ}(a,M) vs. HF-QPO data

**Target:** |Δν|/ν ≤ 10%

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_isco_qpo.py`

---

#### **C-8: S2 Star Orbit around Sgr A***

**Test:** v(t), z(t) under SSZ geodesics

**Target:** χ²/ndof comparable to GR fit

**Status:** ❌ NOT IMPLEMENTED (CRITICAL)

**Implementation:** `test_s2_orbit_sgrA.py`

---

#### **C-9: Black Hole Shadow (M87*, Sgr A*)**

**Test:** θ_{shadow,SSZ}(M,D,a,Ξ) vs. EHT constraints

**Target:** Within 1σ-2σ band

**Status:** ⚠️ PREDICTED (shadow_predictions_exact.py exists but not EHT comparison)

**Implementation:** `test_bh_shadow_eht.py`

---

### Priority 4: Gravitational Waves

#### **D-10: GW Propagation Speed (GW170817)**

**Test:** c_{GW} = c in SSZ (segment corrections → 0)

**Target:** |c_{GW}-c|/c < 10⁻¹⁵

**Status:** ❌ NOT IMPLEMENTED (CRITICAL)

**Implementation:** `test_gw_speed.py`

---

#### **D-11: Inspiral Phase/Chirp Mass**

**Test:** PN phase evolution under SSZ in weak field

**Target:** Match-filter overlap ≥ 0.97 with LIGO/Virgo templates

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_gw_inspiral_chirp.py`

---

#### **D-12: Polarization Modes**

**Test:** No additional strongly-coupled scalar/tensor modes

**Target:** Amplitude bounds from detector networks

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_gw_polarization.py`

---

### Priority 5: Early Universe & Large-Scale Cosmology

#### **E-13: CMB Acoustic Peaks**

**Test:** θ_* and r_s(z_*) under SSZ expansion → Planck consistency

**Target:** Δℓ_peak/ℓ < 2%

**Status:** ⚠️ PLANCK DATA EXISTS (but not analyzed for SSZ)

**Implementation:** `test_cmb_acoustic_peaks.py`

---

#### **E-14: BBN Abundances (He⁴, D/H)**

**Test:** H(t) during BBN epoch (SSZ correction Ξ) vs. standard abundances

**Target:** Within 1-2σ of compilation values

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_bbn_abundances.py`

---

#### **E-15: Strong Lensing Time Delays**

**Test:** Δt_{SSZ} vs. measured time delays (H₀-independent check)

**Target:** RMSE ≤ 10%

**Status:** ❌ NOT IMPLEMENTED

**Implementation:** `test_strong_lensing_delays.py`

---

### Priority 6: Numerics & Reproducibility (YOUR PAIN POINT)

#### **F-16: Grid/Resolution Convergence**

**Test:** h-refinement (h, h/2, h/4) → Richardson convergence order ≥ 1.8

**Target:** Extrapolation error < 1% for reference quantities

**Status:** ❌ NOT IMPLEMENTED (CRITICAL)

**Implementation:** `test_grid_convergence.py`

---

#### **F-17: Parameter Sensitivity (K, λ_A, Ξ_max)**

**Test:** Latin Hypercube over parameter space → stability region unchanged

**Target:** ≥95% of points consistent with thresholds

**Status:** ⚠️ PARTIAL (single values tested, not sweep)

**Implementation:** `test_parameter_sensitivity.py`

---

#### **F-18: Error Bars/Uncertainties**

**Test:** Bootstrap/Jackknife on fit metrics

**Target:** All key results with 68% CI

**Status:** ❌ NOT REPORTED

**Implementation:** `test_uncertainty_quantification.py`

---

#### **F-19: Reproducibility Suite**

**Test:** Seeds + version lock; bit-reproducible core metrics

**Target:** ΔMetric = 0 over 3 runs / 2 machines (or < 1e-12 rel)

**Status:** ✅ IMPLEMENTED (run_toe_validation_v2.py)

**Implementation:** Already done

---

## Summary

### Test Status Overview

| Category | Total | Implemented | Partial | Missing |
|----------|-------|-------------|---------|---------|
| Already Validated | 6 | 6 | 0 | 0 |
| Math/Foundation (A) | 3 | 0 | 1 | 2 |
| Local/Solar (B) | 3 | 0 | 2 | 1 |
| Strong Field (C) | 3 | 0 | 1 | 2 |
| Gravitational Waves (D) | 3 | 0 | 0 | 3 |
| Cosmology (E) | 3 | 0 | 1 | 2 |
| Numerics (F) | 4 | 1 | 1 | 2 |
| **TOTAL** | **25** | **7** | **6** | **12** |

**Completion:** 28% (7/25) fully implemented

**ToE Readiness:** 50% (including partial)

---

## Recommended Implementation Order

### Phase 1: Critical Mathematical Foundations (Weeks 1-2)

1. **F-16** Grid Convergence → Fix your current pain point
2. **A-3** PPN Limit → Prove GR recovery
3. **A-1** Lorentz/Equivalence → Mathematical consistency
4. **A-2** Bianchi Identities → Energy-momentum conservation

**Goal:** Establish mathematical rigor

---

### Phase 2: Strong Field Observables (Weeks 3-4)

5. **C-8** S2 Orbit → Real data, high precision
6. **C-9** BH Shadow → EHT comparison
7. **D-10** GW Speed → Critical constraint
8. **C-7** ISCO/QPO → X-ray binaries

**Goal:** Validate strong field regime

---

### Phase 3: Solar System Precision (Weeks 5-6)

9. **B-6** Perihelion Precession → Mercury + pulsars
10. **B-4** Redshift Experiments → Pound-Rebka etc.
11. **B-5** Shapiro Delay → Cassini tracking

**Goal:** Solar system precision tests

---

### Phase 4: Gravitational Waves (Weeks 7-8)

12. **D-11** Inspiral/Chirp → LIGO templates
13. **D-12** Polarization → No extra modes

**Goal:** GW consistency

---

### Phase 5: Cosmology (Weeks 9-10)

14. **E-13** CMB Peaks → Planck data
15. **E-14** BBN → Light element abundances
16. **E-15** Strong Lensing → Time delays

**Goal:** Large-scale structure

---

### Phase 6: Robustness (Week 11)

17. **F-17** Parameter Sensitivity → Latin hypercube
18. **F-18** Uncertainties → Bootstrap/Jackknife

**Goal:** Quantify uncertainties

---

## Next Steps

### Immediate Actions (Today)

1. ✅ Create this roadmap document
2. 🔄 Implement **F-16** Grid Convergence Test
3. 🔄 Implement **A-3** PPN Limit Test
4. 🔄 Implement **C-8** S2 Orbit Test
5. 🔄 Implement **D-10** GW Speed Test

### This Week

- Complete Phase 1 tests
- Validate mathematical foundations
- Document results

### This Month

- Complete Phases 1-3
- Submit preprint with Phase 1+2 results
- Plan Phase 4-6 with collaborators

---

## Success Criteria

**ToE-Ready Publication:**
- Phase 1: 100% complete (mathematical rigor)
- Phase 2: ≥75% complete (strong field validation)
- Phase 3: ≥50% complete (solar system)
- Phase 4: ≥50% complete (GW constraints)
- Phase 5: ≥25% complete (cosmology plausibility)
- Phase 6: 100% complete (robustness)

**Minimum for First Paper:**
- All Phase 1 tests PASS
- S2 Orbit (C-8) PASS
- GW Speed (D-10) PASS
- Grid Convergence (F-16) PASS

---

## Resources Needed

**Computational:**
- Grid refinement studies: ~100 CPU-hours
- Parameter sensitivity: ~50 CPU-hours
- S2 orbit fits: ~10 CPU-hours

**Data:**
- S2 orbit data (Gravity Collaboration)
- EHT shadow data (public release)
- LIGO/Virgo GW data (public)
- Planck CMB data (already downloaded)

**Literature:**
- PPN formalism papers
- GW template banks
- CMB analysis codes (e.g., CAMB)

---

**Status:** Roadmap complete, ready for implementation

**Next:** Create actual test implementations
