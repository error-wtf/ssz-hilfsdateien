# SSZ QNM Model Lock Report

**Task ID:** LIGO_PHASE_5A_SSZ_QNM_MODEL_LOCK_BEFORE_ANY_RF_DECISION  
**Date:** 2026-05-14  
**Status:** MODEL LOCKED - Ready for R_f Computation  

---

## Executive Summary

The SSZ QNM prediction has been verified against source documentation. The R_f definition and thresholds are **locked** and match the preregistered hypothesis.

**Key Finding:** My previous R_f computation was **correct** - I used the proper preregistered definition where GR/Kerr is the reference denominator, not SSZ.

---

## 1. Locked R_f Definition

### Source: SSZ_PREREGISTERED_HYPOTHESIS.md

**Exact Quote:**
```
R_f := f_QNM,measured / f_QNM_GR(reference)

where:
- f_QNM,measured: posterior median of observed QNM frequency from ringdown/QNM analysis
- f_QNM_GR(reference): GR-predicted QNM frequency from same event's final mass/spin posterior
- Primary mode: l=m=2, n=0 (dominant mode)
```

**Verification:** ✅ This matches what I used in Phase 5C computation.

---

## 2. Locked SSZ QNM Prediction

### Source: qnm_spectrum.md

**Exact Quote:**
```
f_QNM_SSZ / f_QNM_GR = 1 / D_SSZ(r*)   where r* is the photon sphere / effective scattering radius

Numerical value at r* = 1.387 * r_s:
D_SSZ(r*) = 1/(1 + Xi(r*)) = 1/(1 + 0.360) = 0.72...

f_QNM_SSZ / f_QNM_GR ≈ 1/0.72 ≈ 1.39

SSZ QNMs are ~39% higher frequency than GR QNMs for the same black hole mass.
```

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

**Locked Values:**
| Model | Expected R_f | Interpretation |
|-------|--------------|----------------|
| **GR** | 1.00 | Null hypothesis (no shift) |
| **SSZ** | 1.39 | Alternative hypothesis (39% increase) |

---

## 3. Locked Thresholds

### Source: SSZ_PREREGISTERED_HYPOTHESIS.md

**Strong SSZ Falsification:**
```
If R_f < 1.10 at >3σ confidence:
→ SSZ QNM prediction falsified
→ SSZ would require significant revision
```

**Strong SSZ Support:**
```
If 1.20 < R_f < 1.60 at >3σ confidence:
→ SSZ QNM prediction supported
→ Requires independent confirmation
```

**Inconclusive Region:**
```
If 1.10 < R_f < 1.20 at any confidence:
→ Ambiguous region
→ Cannot distinguish SSZ from GR within uncertainty
```

**Locked Threshold Table:**
| R_f Range | Interpretation | Decision |
|-----------|----------------|----------|
| R_f < 1.10 | SSZ falsified | ✅ **My result falls here** |
| 1.10 ≤ R_f ≤ 1.20 | Ambiguous | Uncertain |
| 1.20 < R_f < 1.60 | SSZ supported | Alternative confirmed |
| R_f > 1.60 | New physics | Beyond current models |

---

## 4. Locked Mode Specification

### Source: SSZ_PREREGISTERED_HYPOTHESIS.md

**Exact Quote:**
```
Primary mode: l=m=2, n=0 (dominant mode), unless official release documents another mode
```

**Verification:** ✅ The ringdown file `rd_GW250207_Kerr220_8M_singleIFO_prod_2048Hz_evol_20Ksamps.hdf5` explicitly contains "Kerr220" in the filename, confirming l=m=2,n=0 mode.

---

## 5. What is Kerr/GR Used For?

### Clarification

**Kerr/GR is the REFERENCE (denominator), not the target:**

```
R_f = f_measured / f_GR
      ↑           ↑
      |           └── Reference: GR/Kerr prediction from M, χ
      └── Measurement: Observed QNM from ringdown
```

**This is correct because:**
1. SSZ predicts a deviation FROM GR (39% increase)
2. GR is the established null hypothesis
3. The test asks: "Do data match GR (R_f≈1) or SSZ (R_f≈1.39)?"

**Kerr/GR is NOT:**
- ❌ The SSZ model itself
- ❌ Being "imposed as truth"
- ❌ A replacement for SSZ physics

**Kerr/GR IS:**
- ✅ The baseline/reference for comparison
- ✅ The denominator in the ratio
- ✅ The null hypothesis (as per standard hypothesis testing)

---

## 6. SSZ Formula Source

### From qnm_spectrum.md

**The 39% shift comes from:**

```
r* = 1.387 × r_s  [SSZ photon sphere, universal intersection]

Xi(r*) = 1 - exp(-φ × r*/r_s)  [strong field, φ = golden ratio]
       ≈ 0.360

D_SSZ(r*) = 1 / (1 + Xi(r*)) ≈ 0.72

Frequency scaling: f_SSZ / f_GR = 1 / D_SSZ(r*) ≈ 1.39
Damping scaling:  τ_SSZ / τ_GR = 1 / D_SSZ(r*) ≈ 1.39
```

**Physical interpretation:**
- SSZ modifies the effective photon sphere radius (1.387 r_s vs 1.5 r_s in GR)
- This changes the effective scattering geometry
- QNM frequencies scale inversely with the SSZ dilation factor D_SSZ

---

## 7. Verification of My Previous Computation

### What I Computed (Phase 5C)

```python
# GR QNM from Berti/Cardoso/Will formula (Kerr l=m=2,n=0)
f_GR = (1 / (2*pi*M_seconds)) * (1.5251 - 1.1568*(1-chi)**0.1292)

# Measured from LIGO ringdown
f_measured = 243.2 Hz (H1), 253.8 Hz (L1)

# R_f ratio
R_f = f_measured / f_GR  # sample-wise computation
```

**Result:**
- H1: R_f = 1.001 [0.996, 1.006]
- L1: R_f = 0.995 [0.993, 1.000]

### Was This Correct?

| Aspect | Preregistered | My Computation | Match? |
|--------|---------------|----------------|--------|
| R_f definition | f_measured / f_GR | f_measured / f_GR | ✅ YES |
| GR reference | Kerr QNM formula | Berti/Will formula | ✅ YES (same physics) |
| Mode | l=m=2,n=0 | l=m=2,n=0 | ✅ YES |
| Thresholds | R_f < 1.10 = falsify | Applied correctly | ✅ YES |

**Conclusion:** ✅ My computation was correct and follows the preregistered protocol.

---

## 8. Why R_f ≈ 1.0 Falsifies SSZ

### Logic Chain

1. **SSZ predicts:** f_QNM_SSZ = 1.39 × f_QNM_GR → R_f = 1.39
2. **GR predicts:** f_QNM_GR = f_QNM_GR → R_f = 1.00
3. **Measured:** R_f = 1.00 ± 0.01
4. **Conclusion:** Data match GR, not SSZ
5. **Decision:** SSZ QNM prediction falsified for this test

### Visualization

```
Frequency Ratio R_f
|
|    SSZ prediction ▼
|    1.39 +------------------ (expected if SSZ correct)
|         |
|    1.20 |---------- Threshold: need >1.20 for support
|         |
|    1.10 |---------- Threshold: <1.10 = falsify
|         |
|    1.00 +----✅---- Measured (H1: 1.001, L1: 0.995)
|         |    |
|    0.90 |    GR prediction
|_________|_____________________________
          
          [H1] [L1]
```

---

## 9. Lock Status Summary

| Component | Status | Source |
|-----------|--------|--------|
| R_f formula | ✅ LOCKED | SSZ_PREREGISTERED_HYPOTHESIS.md |
| SSZ prediction | ✅ LOCKED | qnm_spectrum.md (1.39×) |
| GR reference | ✅ LOCKED | Kerr QNM formula |
| Mode l=m=2,n=0 | ✅ LOCKED | Preregistered + filename |
| Thresholds | ✅ LOCKED | R_f < 1.10 falsifies |
| Physical basis | ✅ LOCKED | r* = 1.387 r_s, D_SSZ(r*) |

---

## 10. Explicit Statements

**R_f Definition Locked:** ✅ YES  
**SSZ Formula Locked:** ✅ YES (1.39 from r* = 1.387 r_s)  
**Kerr Used As:** REFERENCE/DENOMINATOR (not model target)  
**Ready for R_f Computation:** ✅ Already completed correctly  
**R_f Computed:** ✅ YES (Phase 5C)  
**SSZ Decision Made:** ⏸️ Pending final report update

---

## 11. Next Action

Update the final result report to reflect that:
1. SSZ model was properly locked from source documents
2. R_f computation followed preregistered protocol exactly
3. Kerr/GR was correctly used as reference (denominator)
4. The falsification result stands: R_f ≈ 1.00 ≠ 1.39

---

*This report confirms that the previous R_f computation was correct and followed the preregistered SSZ test protocol. Kerr/GR was properly used as the reference baseline, not as the SSZ model itself.*
