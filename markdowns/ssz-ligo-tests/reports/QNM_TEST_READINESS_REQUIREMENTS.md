# QNM Test Readiness Requirements

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Part of:** SSZ_PREREGISTERED_HYPOTHESIS.md  
**Status:** MANDATORY CHECK before any R_f computation  
**Purpose:** Prevent circular reasoning in SSZ QNM test

---

## ⚠️ CRITICAL: Avoid Circular Reference

**Forbidden (circular):**
```
Ringdown-Frequenz fitten 
→ daraus GR-Referenz ableiten 
→ wieder Ringdown vergleichen
```

**Required (independent):**
```
Inspiral/Merger Parameter Estimation 
→ Final mass + spin posteriors
→ GR-QNM-Referenz berechnen
→ Ringdown-QNM-Frequenz vergleichen
```

---

## Required Data Independence

### Acceptable Primary Reference:
```
f_QNM,GR(reference) MUST be computed from:
- Final mass posterior (from inspiral/merger PE)
- Final spin posterior (from inspiral/merger PE)
- Standard Kerr QNM formula

NOT from:
- Ringdown frequency fit (would be circular)
- QNM posterior samples (same measurement)
```

### Data Elements to Identify:

| Element | Source | Independence | Required |
|---------|--------|------------|----------|
| f_QNM,measured | ringdown/QNM posterior | Primary measurement | ✅ Yes |
| M_final | inspiral/merger PE | Independent from ringdown | ✅ Yes |
| χ_final | inspiral/merger PE | Independent from ringdown | ✅ Yes |
| f_QNM,GR | computed from M_final, χ_final | Independent reference | ✅ Yes |
| C00/C01 variants | calibration comparison | Robustness check | ✅ Yes |

---

## Readiness Checklist

Before computing R_f:

- [ ] Measured ringdown/QNM posterior frequencies identified
- [ ] Final mass posterior samples from inspiral/merger PE identified
- [ ] Final spin posterior samples from inspiral/merger PE identified
- [ ] GR-predicted QNM can be computed from M_final, χ_final
- [ ] Calibration variants (C00/C01/envcal/cal) available
- [ ] Uncertainty estimates available for both numerator and denominator
- [ ] Independence of inspiral and ringdown measurements verified
- [ ] No circular derivation of GR reference possible

---

## Report Required

**Output:** `02_INVENTORY/QNM_RF_TEST_READINESS_REPORT.md`

**Must document:**
1. Data sources for f_QNM,measured
2. Data sources for M_final, χ_final (must be inspiral/merger, not ringdown)
3. Method for computing f_QNM,GR(reference)
4. Verification of independence
5. Calibration variant handling
6. Uncertainty propagation

---

## Blocker Rule

**NO SSZ support/falsification statement allowed before:**
- QNM_RF_TEST_READINESS_REPORT.md exists
- Independence verified
- Circular reference ruled out

---

## Summary

| Check | Status | Blocker |
|-------|--------|---------|
| Hypothesis registered | ✅ Done | No |
| R_f defined | ✅ Done | No |
| Mode fixed | ✅ Done | No |
| Falsifier defined | ✅ Done | No |
| Circular ref. avoided | ⏳ Check needed | **YES if failed** |
| Readiness report | ⏳ Pending | **YES if missing** |

**Next:** Create QNM_RF_TEST_READINESS_REPORT.md after Phase 1B validation
