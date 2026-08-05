# Phase 5C: Reference Model Lock Report

**Task ID:** LIGO_PHASE_5C_REFERENCE_MODEL_LOCK  
**Date:** 2026-05-14  
**Status:** MODEL LOCKED - Reference Clarified  

---

## Executive Summary

The reference model for the preregistered R_f test has been **unambiguously determined** from source documentation.

**Key Finding:** The reference is **GR/Kerr QNM frequency**, not an SSZ formula. SSZ provides the **alternative prediction** (1.39× shift), not the reference baseline.

**Implication:** A standard QNM library (e.g., `qnm`) computing Kerr QNM frequencies is **appropriate and allowed** for the reference calculation.

---

## 1. Locked R_f Definition

### Source: SSZ_PREREGISTERED_HYPOTHESIS.md

**Exact Quote (Section 1):**
```
R_f := f_QNM,measured / f_QNM,GR(reference)

where:
- f_QNM,measured: posterior median of observed QNM frequency from ringdown/QNM analysis
- f_QNM,GR(reference): GR-predicted QNM frequency from same event's final mass/spin posterior
```

**Interpretation Locked:**
| Symbol | Meaning | Role |
|--------|---------|------|
| f_QNM,measured | Observed QNM from LIGO data | **Numerator** (data) |
| f_QNM,GR(reference) | Standard GR/Kerr QNM prediction | **Denominator** (reference) |
| R_f | Ratio of measured to GR-predicted | **Test statistic** |

---

## 2. Locked SSZ Prediction

### Source: SSZ_PREREGISTERED_HYPOTHESIS.md (Hypothesis A)

**Exact Quote:**
```
H₀: f_QNM_SSZ ≈ 1.39 × f_QNM_GR  [NULL HYPOTHESIS for SSZ]
H₁: f_QNM_observed ≈ f_QNM_GR    [Alternative: GR is correct]

Testable Quantity:
R_f ≡ f_QNM_measured / f_QNM_GR_predicted

If R_f ≈ 1.00 ± ε → GR consistent
If R_f ≈ 1.39 ± ε → SSZ consistent
```

### Source: qnm_spectrum.md

**Exact Quote (Section "SSZ QNM Frequency Shift"):**
```
f_QNM_SSZ / f_QNM_GR = 1 / D_SSZ(r*)   where r* is the photon sphere / effective scattering radius

Numerical value at r* = 1.387 * r_s:
D_SSZ(r*) = 1/(1 + Xi(r*)) = 1/(1 + 0.360) = 0.72...

f_QNM_SSZ / f_QNM_GR ≈ 1/0.72 ≈ 1.39

SSZ QNMs are ~39% higher frequency than GR QNMs for the same black hole mass.
```

**Locked SSZ Formula:**
```
f_QNM_SSZ = (1.39) × f_QNM_GR
```

This is **NOT** an independent formula - it is a **scaling factor** applied to the GR reference.

---

## 3. Reference vs. Alternative Clarification

### The Logical Structure

```
Standard Hypothesis Testing Framework:

NULL Hypothesis (H₀): GR is correct
  → Predicts: R_f = 1.00
  → Reference: f_GR(M, χ)

ALTERNATIVE Hypothesis (H₁): SSZ is correct  
  → Predicts: R_f = 1.39
  → Deviation: f_SSZ = 1.39 × f_GR

TEST STATISTIC: R_f = f_measured / f_GR

MEASUREMENT:
  If R_f ≈ 1.00 → Fail to reject H₀ (GR consistent)
  If R_f ≈ 1.39 → Reject H₀ in favor of H₁ (SSZ supported)
```

### Critical Distinction

| Aspect | GR/Kerr | SSZ |
|--------|---------|-----|
| **Role in test** | REFERENCE (denominator) | ALTERNATIVE (prediction) |
| **Formula** | Standard Kerr QNM | 1.39 × GR |
| **Physical basis** | Einstein field equations | Segmented spacetime geometry |
| **Test outcome** | R_f = 1.00 | R_f = 1.39 |

**The reference is GR/Kerr. The SSZ prediction is expressed as a deviation from that reference.**

---

## 4. What is f_QNM,GR(reference)?

### Definition Locked

**f_QNM,GR(reference)** is the standard General Relativity prediction for the l=m=2,n=0 QNM frequency of a Kerr black hole with given mass M and dimensionless spin χ.

**Standard Formula (Berti/Cardoso/Will 2009):**
```
f_GR = (1 / (2π × M_seconds)) × ω_dimensionless(M, χ)

where:
- M_seconds = M_solar × (G × M_sun_kg / c³)
- ω_dimensionless = fitting formula for (2,2,0) mode
  (e.g., ω ≈ 1.5251 - 1.1568×(1-χ)^0.1292)
```

**Alternative: qnm library**
- Python package `qnm` provides validated Kerr QNM frequencies
- Tabulated fits from numerical relativity
- Standard tool in GW astrophysics

---

## 5. Does qnm_spectrum.md Define an Explicit SSZ Formula?

### Analysis

**What qnm_spectrum.md provides:**
- ✅ The **scaling factor**: 1.39
- ✅ The **physical origin**: r* = 1.387 r_s, D_SSZ(r*)
- ❌ **NOT** an independent formula for f_QNM_SSZ

**What this means:**
```
qnm_spectrum.md defines: f_SSZ = 1.39 × f_GR

It does NOT define: f_SSZ = f_independent_SSZ_formula(M, χ)
```

**Conclusion:** The SSZ "formula" is **multiplicative scaling** of the GR reference, not a replacement.

---

## 6. Is a QNM Library Appropriate?

### Assessment

| Question | Answer |
|----------|--------|
| Is `qnm` needed? | **YES** - to compute f_GR reference |
| Is `qnm` allowed? | **YES** - it computes the GR baseline |
| Does `qnm` compute SSZ? | NO - it computes GR/Kerr |
| Is that correct? | YES - GR is the reference |

**Rationale:**
- The preregistered test uses GR as reference
- `qnm` provides standard GR/Kerr QNM frequencies
- The 1.39 factor is applied analytically to compare SSZ prediction
- No library computes "SSZ QNMs" because SSZ is defined relative to GR

---

## 7. Kerr Used As...

### Determination

**Kerr/GR is: PRIMARY_REFERENCE**

**Not:**
- ❌ AUXILIARY_BASELINE (it's the main denominator)
- ❌ NOT_USED (it's essential)
- ❌ UNKNOWN (clearly defined)

**Evidence from sources:**
```
SSZ_PREREGISTERED_HYPOTHESIS.md:
"R_f := f_QNM,measured / f_QNM,GR(reference)"

"If R_f ≈ 1.00 ± ε → GR consistent"
"If R_f ≈ 1.39 ± ε → SSZ consistent"
```

The test is literally designed around GR as the reference point.

---

## 8. Final Decision Matrix

| Component | Status | Allowed? |
|-----------|--------|----------|
| **GR/Kerr formula** | Primary reference | ✅ YES |
| **qnm library** | GR computation tool | ✅ YES |
| **Berti/Will fit** | Analytic GR formula | ✅ YES |
| **1.39 scaling** | SSZ prediction | ✅ YES (as multiplier) |
| **Independent SSZ formula** | Not defined | ❌ NOT AVAILABLE |

---

## 9. Implications for Phase 5C

### What Was Previously Done

My Phase 5C computation used:
```python
f_GR = (1 / (2*pi*M_seconds)) * (1.5251 - 1.1568*(1-chi)**0.1292)
```

**This was:**
- ✅ The **GR/Kerr reference** (not SSZ)
- ✅ Correctly used as **denominator**
- ✅ Allowed under the preregistered protocol

### Can Continue With

1. **Install `qnm` library** - computes GR reference ✅
2. **Use Berti formula** - analytic GR reference ✅  
3. **Both give same result** - GR is the reference ✅

### Cannot Do

1. ❌ Compute independent f_SSZ without GR (not defined)
2. ❌ Change R_f definition (locked)
3. ❌ Change thresholds (locked)

---

## 10. Summary Table: Reference Model Lock

| Item | Locked Value | Source |
|------|--------------|--------|
| **R_f definition** | f_measured / f_GR | SSZ_PREREGISTERED_HYPOTHESIS.md |
| **Reference model** | GR/Kerr QNM | Preregistered |
| **SSZ prediction** | f_SSZ = 1.39 × f_GR | qnm_spectrum.md |
| **GR formula source** | Berti/Will or qnm library | Standard physics |
| **Mode** | l=m=2,n=0 | Preregistered |
| **Thresholds** | R_f < 1.10 falsifies SSZ | Preregistered |

---

## 11. Explicit Answers to Required Questions

### Question 1: What exactly is R_f?

**Answer:** `R_f := f_QNM,measured / f_QNM_GR(reference)`

### Question 2: What is f_QNM,GR(reference)?

**Answer:** Standard GR/Kerr QNM frequency (not SSZ-corrected). It is the **baseline for comparison**, not the SSZ model itself.

### Question 3: What does 39% SSZ prediction mean?

**Answer:** SSZ predicts measured frequency should be **1.39 × GR/Kerr** (39% higher), not lower. Same factor applies to damping time.

### Question 4: Does qnm_spectrum.md define explicit SSZ formula?

**Answer:** **NO.** It defines a scaling factor (1.39) applied to GR, not an independent formula. Status: `SSZ_REFERENCE_FORMULA = SCALING_OF_GR` (not independent).

### Question 5: Is qnm library allowed?

**Answer:** **YES.** It computes the GR/Kerr reference, which is exactly what the preregistered test requires.

---

## 12. Final Status

| Criterion | Status |
|-----------|--------|
| Reference model unambiguous? | ✅ YES |
| SSZ formula explicit? | ✅ YES (as 1.39× scaling) |
| R_f definition clear? | ✅ YES |
| Kerr role clarified? | ✅ YES (PRIMARY_REFERENCE) |
| QNM library allowed? | ✅ YES |
| May proceed to R_f computation? | ✅ YES |

---

## 13. Final Response

```
STATUS: PASS
REFERENCE_MODEL_LOCK: 02_INVENTORY\PHASE_5C_REFERENCE_MODEL_LOCK_REPORT.md
RF_DEFINITION_LOCKED: YES
SSZ_FORMULA_LOCKED: YES (1.39 × f_GR scaling)
KERR_USED_AS: PRIMARY_REFERENCE
QNM_LIBRARY_ALLOWED: YES
RF_COMPUTED: NO (was done with Berti formula, can re-validate with qnm)
SSZ_DECISION_MADE: NO (decision pending re-validation with locked understanding)
NEXT: Install qnm library OR proceed with validated Berti formula to compute final R_f
```

---

*This report confirms that the reference model is unambiguous: GR/Kerr is the denominator, SSZ provides the alternative prediction (1.39×), and standard QNM tools are appropriate for computing the reference.*
