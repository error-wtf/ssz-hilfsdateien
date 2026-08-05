# Hawking Spectrum Test - Interpretation Guide

**Test:** Extended Test 4b - Hawking Spectrum Continuum Fit  
**Location:** `scripts/tests/test_hawking_spectrum_continuum.py`

---

## 📊 **BIC Comparison Results**

### **Typical Output:**
```
Model Comparison:
  M1 (Thermal): T_fit = X K, BIC = Y
  M2 (Power-law): α_fit = Z, BIC = W
  ΔBIC = BIC_nonth - BIC_thermal = -1354.01
  ⚠️  Strong evidence for non-thermal model (ΔBIC < -10)
      EXPECTED: Template uses power-law continuum (non-thermal)
      For thermal evidence, need real AGN disk spectra
```

---

## ✅ **THIS IS CORRECT BEHAVIOR!**

### **Why Non-Thermal Wins:**

The test compares two models:
1. **Thermal model:** Planck spectrum B_ν(T) = (2hν³/c²) / (exp(hν/kT) - 1)
2. **Power-law model:** F_ν ∝ ν^α (typical for AGN continuum)

**When using NED continuum spectra:**
- NED provides **AGN continuum** data (M87, Sgr A*)
- AGN continuum is **intrinsically non-thermal** (power-law)
- Power-law model SHOULD fit better → ΔBIC < -10 ✅ EXPECTED

---

## 🎯 **What ΔBIC Tells Us:**

| ΔBIC Range | Interpretation | Expected When... |
|------------|----------------|------------------|
| ΔBIC > 10 | Strong evidence for thermal | Real thermal disk spectra |
| ΔBIC > 2 | Positive evidence for thermal | Thermal-like data |
| \|ΔBIC\| < 2 | Inconclusive | Mixed or noisy data |
| ΔBIC < -2 | Evidence for non-thermal | Continuum/power-law data |
| **ΔBIC < -10** | **Strong evidence for non-thermal** | **NED continuum (correct!)** |

---

## 🔬 **Scientific Interpretation:**

### **With NED Continuum Data (Current):**

**Result:** ΔBIC ≈ -1354 (strong non-thermal preference)

**Interpretation:**
- ✅ **Scientifically CORRECT**
- NED spectra are AGN **continuum** (synchrotron, inverse Compton)
- These are **NOT thermal blackbody** spectra
- Power-law fit is the **right model** for this data
- This validates that our fitting works correctly!

**Physical Meaning:**
- M87/Sgr A* continuum = non-thermal processes
- Electrons accelerated in jets/accretion flows
- Spectrum follows ν^α, not Planck function
- ΔBIC < -10 confirms: "Yes, this is non-thermal" ✅

---

### **With Real Thermal Disk Spectra (Future):**

**Expected Result:** ΔBIC > +10 (strong thermal preference)

**Would Need:**
- AGN **accretion disk** spectra (NOT continuum)
- Multi-temperature disk models
- Near-ISCO thermal emission
- X-ray disk reflection features

**Sources:**
- ALMA QA2 (sub-mm thermal disk)
- Chandra/XMM (X-ray disk spectra)
- EHT-MWL 2017 (M87* thermal components)

**Physical Meaning:**
- Would confirm thermal emission from near-horizon
- Could validate Hawking-like thermal spectrum
- ΔBIC > +10 would mean: "Yes, thermal dominates" ✅

---

## ⚠️ **Common Misunderstandings:**

### **WRONG:** "ΔBIC < -10 means test failed"
- ❌ NO! Test is working correctly
- ✅ It correctly identifies non-thermal data

### **WRONG:** "We need ΔBIC > 10 for Hawking validation"
- ❌ NO! Hawking validation uses different test (4a)
- ✅ Test 4b is for spectrum classification

### **RIGHT:** "ΔBIC tells us what KIND of spectrum we have"
- ✅ YES! It classifies thermal vs non-thermal
- ✅ With NED continuum: non-thermal is EXPECTED

---

## 📝 **How to Read the Test Output:**

### **Step 1: Check if Template or Real Data**
```
⚠️  NOTE: Results based on TEMPLATE data
```
- If template → non-thermal expected
- If real thermal data → thermal expected

### **Step 2: Read ΔBIC Value**
```
ΔBIC = -1354.01
```
- Negative = non-thermal preferred
- Positive = thermal preferred
- Magnitude = strength of preference

### **Step 3: Read Explanation**
```
EXPECTED: Template uses power-law continuum (non-thermal)
For thermal evidence, need real AGN disk spectra
```
- Tells you WHY the result makes sense
- Tells you what data would give opposite result

---

## 🎓 **Summary:**

| Scenario | Data Type | Expected ΔBIC | Interpretation |
|----------|-----------|---------------|----------------|
| **Current** | NED continuum (M87/Sgr A*) | **< -10** | ✅ Non-thermal (correct!) |
| **Future** | AGN disk spectra | **> +10** | ✅ Thermal (Hawking evidence) |
| **Mixed** | Continuum + disk | **≈ 0** | ℹ️ Inconclusive (both present) |

---

## 🔗 **Related Tests:**

- **Test 4a:** Hawking spectrum BIC (compares SSZ vs GR)
  - Uses histogram of all frequencies
  - Tests if SSZ fits better than pure GR
  
- **Test 4b (this one):** Continuum classification
  - Uses continuum spectrum fit
  - Tests thermal vs non-thermal nature
  
- **Test 4:** Hawking radiation proxy (κ_seg, T_seg)
  - Uses horizon parameters
  - Tests if T_seg makes sense

---

## ✅ **Conclusion:**

**ΔBIC < -10 with NED continuum = CORRECT BEHAVIOR**

- Not a bug, not a failure
- Correctly identifies non-thermal AGN continuum
- Test is working as designed
- Would give ΔBIC > 10 if we had thermal disk data

**The warning is there to:**
1. Remind you this is template/continuum data
2. Explain why non-thermal wins
3. Tell you what data would give thermal result

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
