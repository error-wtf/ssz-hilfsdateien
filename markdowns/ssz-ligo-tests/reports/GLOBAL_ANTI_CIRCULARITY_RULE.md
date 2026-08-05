# Global Anti-Circularity Rule

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Applies to:** All SSZ testing, especially LIGO data analysis  
**Status:** MANDATORY  
**Principle:** No quantity may simultaneously be the source of prediction and proof of prediction

---

## Core Rule

```
Keine Größe darf zugleich Ursprung der Vorhersage und Beweis der Vorhersage sein.

No quantity may simultaneously:
- Generate the prediction, AND
- Validate the prediction
```

---

## Practical Implementation (7-Step Protocol)

### Step 1: Fix Hypothesis Before Data Inspection
```
BEFORE any data inspection:
- Document expected effect
- Document magnitude/direction
- Document testable quantity
- Timestamp the prediction
```

### Step 2: Determine Reference Independently
```
Reference quantity must come from:
- Different measurement
- Different dataset
- Different analysis pipeline
- Different physical observable

NOT from:
- Same dataset used for test
- Derived from test measurement
- Circular computation
```

### Step 3: Measure Test Quantity Separately
```
Test measurement must be:
- Independent data product
- Independent analysis
- No shared processing steps with reference
- Blind to expected result
```

### Step 4: Check Calibration Separately
```
Calibration robustness:
- C00/C01/envcal comparison
- Independent of test result
- Stability across variants
```

### Step 5: Pre-Define Falsification Criteria
```
BEFORE data inspection:
- Define falsification threshold
- Define significance level
- Define mode/method
- No post-hoc changes allowed
```

### Step 6: No Post-Hoc Changes
```
After data inspection, FORBIDDEN:
- Changing thresholds
- Changing mode selection
- Changing formulas
- Changing reference definition

Allowed only as:
- Separate exploratory analysis
- Clearly marked as POST-HOC
- Not used as preregistered evidence
```

### Step 7: Mark Exploratory Changes
```
Any change after data inspection must be:
- Documented as change
- Justified scientifically
- Marked as EXPLORATORY
- Not claimed as confirmation
```

---

## Required Documentation for Every Test

For every claimed SSZ test, document:

| Element | Description | Example (QNM) |
|---------|-------------|---------------|
| **Prediction Source** | Where does prediction come from? | qnm_spectrum.md: r* = 1.387 r_s |
| **Reference Quantity** | What is the GR/comparison value? | f_GR from M_final, χ_final |
| **Measured Quantity** | What is being tested? | f_QNM,measured from ringdown |
| **Independence Relation** | How are reference and measured independent? | Inspiral PE vs Ringdown QNM |
| **Circularity Risks** | What could create circularity? | Using ringdown to compute GR reference |
| **Falsification Criterion** | What would falsify SSZ? | R_f < 1.10 at 3σ |

---

## Global Rule Statement

```
GLOBAL ANTI-CIRCULARITY RULE:

Never use the same data product both to define the prediction 
and to validate the prediction.

For every claimed test, explicitly document:
- prediction source
- reference quantity  
- measured quantity
- independence relation
- possible circularity risks
- falsification criterion

If independence cannot be shown, mark the result as 
CIRCULARITY RISK and do not use it as evidence for SSZ.
```

---

## SSZ/LIGO Specific Application

### QNM Frequency Test

| Aspect | Safe (Anti-Circular) | Unsafe (Circular) |
|--------|---------------------|-------------------|
| Prediction | r* = 1.387 r_s from SSZ metric | "We expect some shift" |
| Reference | f_GR from inspiral M_final, χ_final | f_GR from ringdown fit |
| Measured | f_QNM from ringdown posterior | Same as reference |
| Independence | Inspiral PE ≠ Ringdown QNM | Using same measurement |

### Phase Evolution Test (Future)

| Aspect | Safe | Unsafe |
|--------|------|--------|
| Prediction | δΨ_SSZ(f) from SSZ metric | Fitting δΨ to match data |
| Reference | GR waveform template | GR + fitted correction |
| Measured | Phase residual | Same as fitted |

### Residual Template Test (Future)

| Aspect | Safe | Unsafe |
|--------|------|--------|
| Prediction | r_SSZ(t) from theory | Template fitted to residuals |
| Reference | GR-only residual | GR + template match |
| Measured | Actual residual | Same as template source |

---

## Risk Assessment

### High Risk (Reject as Evidence)
```
- Same dataset for prediction and validation
- Derived quantity used as its own reference
- Post-hoc threshold adjustment
- Mode selection after seeing data
```

### Medium Risk (Document Carefully)
```
- Shared calibration between measurements
- Common systematic uncertainties
- Partial overlap in analysis pipelines
```

### Low Risk (Accept with Documentation)
```
- Completely independent measurements
- Different physics (inspiral vs ringdown)
- Different detectors (H1 vs L1)
- Pre-registered predictions
```

---

## Enforcement

### For Every SSZ Claim
```
Mandatory check:
□ Prediction documented BEFORE data
□ Reference independent of measurement
□ No circular derivation possible
□ Falsification pre-defined
□ No post-hoc changes

If any check fails → MARK AS CIRCULARITY RISK
```

### Consequence of Violation
```
Result may be:
- Exploratory finding (not confirmation)
- Hypothesis generator (not test)
- Methodological note (not evidence)

Never:
- SSZ confirmation
- SSZ validation
- SSZ support claim
```

---

## Summary

**The Golden Rule:**
```
Anti-zirkulär oder gar nicht als Bestätigung zählen.

Anti-circular or do not count as confirmation at all.
```

**For SSZ/LIGO:**
- ✅ Hypothesis pre-registered (39% QNM shift)
- ✅ R_f defined independently
- ✅ Mode fixed (l=m=2,n=0)
- ✅ Falsifier pre-defined (R_f < 1.10)
- ✅ Anti-HARKing rules in place
- ✅ Anti-circularity: Inspiral PE ≠ Ringdown QNM
- ⏳ Verification pending in QNM_RF_TEST_READINESS_REPORT.md

**Status:** Protocol established, awaiting data validation.
