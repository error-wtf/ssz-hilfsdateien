# Implementation Alignment Test — Report

**Date:** 2026-05-20
**Phase:** IMPLEMENTATION_ALIGNMENT_TEST
**No LIGO Runs:** YES
**No New Claims:** YES

---

## 1. Finding: IMPLEMENTATION_MISMATCH

**The pipeline (`run_strain_pipeline.py` Step D) was using a V0 proxy, not the DERIVED_V1 implementation.**

### What the pipeline was running (PRE-PATCH):
```python
# V0 PROXY — inline formula, not derived_waveform.py
xi = xi_weak(r, rs_m)              # only weak-field Xi!
dpsi[i] = 1.0 * (1.0 - d_ssz(xi)) # kappa=1.0 locked, NO derivation
h_ssz = h_gr * np.exp(1j * dpsi)   # NO amplitude correction!
```

Missing from V0 proxy:
- No deltaA (amplitude suppression)
- No get_xi() blend zone
- No rdot_SSZ chain
- No (1+Xi)^6 factor
- Hardcoded kappa=1.0

### What DERIVED_V1 provides (POST-PATCH):
```python
# derived_waveform.py → derived_phase.py + derived_amplitude.py
deltaA = D(r)^2 - 1               # from P_GW_SSZ Ch.31 Z.18696
deltaPsi via rdot_SSZ chain       # from rdot_SSZ Ch.31 Z.18700
# Uses get_xi() with blend zone via Hermite C²
h_SSZ = h_GR * (1+deltaA) * exp(i*deltaPsi)
```

---

## 2. Patches Applied

| File | Change | Lines |
|------|--------|-------|
| `run_strain_pipeline.py` Step D | Replaced V0 proxy with `derived_waveform.py` call | 218-290 |
| `run_strain_pipeline.py` Step D fallback | Preserved old V0 proxy as `_step_D_v0_fallback()` | 291-307 |
| `run_strain_pipeline.py` Report D | Updated from SSZ_FORWARD_V0_PROXY to SSZ_FORWARD_DERIVED_V1 | 456-504 |
| `run_strain_pipeline.py` Report E | Updated from "SSZ V0-proxy" to "SSZ DERIVED_V1" | 515-527 |

### Fallback preserved
If `derived_waveform.py` throws an exception, the pipeline falls back to V0 proxy with a clear warning:
```
WARNING: This uses a simplified formula, NOT the DERIVED_V1 implementation.
dPsi(f) = 1.0 * (1 - D(xi_weak(r))) — NO amplitude correction.
```

---

## 3. What Changed

| Metric | Before (V0 Proxy) | After (DERIVED_V1) |
|--------|-------------------|---------------------|
| Amplitude correction | None (h_SSZ = h_GR * exp(i*dPsi)) | deltaA = D²−1 → amplitude suppressed |
| Phase derivation | kappa=1.0 * (1-D(xi)) — heuristic | (1+Ξ)^6 via rdot_SSZ chain — derived |
| Xi regime | xi_weak only (rs/(2r)) | get_xi() with blend zone |
| Source equations | Not cited | Ch.31 Z.18696, Z.18700 |
| FORMULA_STATUS | V0_PROXY | DERIVED_V1 |

### Expected impact on delta_lnL
In weak-field LIGO band (r/rs >> 1), both corrections are tiny. The delta_lnL result should remain INDISTINGUISHABLE from GR — but now for the right reason (DERIVED_V1 corrections are physically correct but weak-field-suppressed), not the wrong reason (kappa=1.0 locked by fiat).

---

## 4. What Remains UNCHANGED

| Component | Status | Reason |
|-----------|--------|--------|
| GR control | 0PN TaylorF2 only (GR_CONTROL_TEMPLATE_LIMITED) | Not upgraded — needs separate Phase 9 |
| epsilon_220 | BLOCKED_CONFLICT | Author decision required |
| Merger | NOT IMPLEMENTED | No SSZ merger model exists |
| Ringdown | NOT IMPLEMENTED | Blocked by epsilon_220 |
| Detector projection | PLACEHOLDER (0.5/0.5) | Not used in H1 pipeline |
| Twist | CONCEPTUAL | Not used in pipeline |
| Propagation | NOT IMPLEMENTED | Source-only corrections |

---

## 5. Alignment Score

| Component | Aligned? |
|-----------|----------|
| deltaA implementation | ✅ ALIGNED (was MISMATCH) |
| deltaPsi implementation | ✅ ALIGNED (was MISMATCH) |
| h_SSZ construction | ✅ ALIGNED (was MISMATCH) |
| Xi branch selection | ✅ ALIGNED (was PARTIAL) |
| Report labels | ✅ ALIGNED (were MISMATCH) |
| epsilon_220 exclusion | ✅ ALIGNED |
| Merger/ringdown exclusion | ✅ ALIGNED |
| Detector projection | ✅ ALIGNED (both use implicit H1) |
| Twist exclusion | ✅ ALIGNED |
| Propagation exclusion | ✅ ALIGNED |

**Result: 10/10 components aligned. 4 IMPLEMENTATION_MISMATCHES patched.**

---

## 6. Mandatory Statements

```
READY_FOR_REAL_SSZ_CLAIM:      NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
IMPLEMENTATION_ALIGNED:        YES (DERIVED_V1 now used in pipeline)
NOT_LOCKED_FINAL:              YES (HJ integral, epsilon_220, merger missing)
```

---

## 7. Next Steps After This

1. **Run pipeline** to verify DERIVED_V1 output is numerically stable
2. **Phase 4: MINIMAL VERIFIED CORE PIPELINE** — reproduce with new implementation
3. **Phase 9: GR_CONTROL_UPGRADE** — beyond 0PN TaylorF2

---

## 8. Outputs

- `data_manifest/implementation_alignment_matrix.csv` — 14 components tracked
- `reports/progress/IMPLEMENTATION_ALIGNMENT_TEST.md` — this report
- `logs/implementation_alignment_test.log` — execution log
