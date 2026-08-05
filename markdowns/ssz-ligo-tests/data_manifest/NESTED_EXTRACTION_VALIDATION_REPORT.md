# Nested Archive Extraction Validation Report

**Generated:** 2026-05-14  
**Source:** E:\clone\ligo-gw240925-gw250207-release\18600070  
**Status:** PASS (User Confirmed)

---

## Summary Table

| Archive | Status | Files | Size (MB) | Critical |
|---------|--------|-------|-----------|----------|
| combined_samples.tar.gz | PASS | User Confirmed | ~10 | ✅ |
| calibration.tar.gz | PASS | User Confirmed | ~0.5 | ✅ |
| cal_env.tar.gz | PASS | User Confirmed | ~0.01 | ✅ |
| ringdown.tar.gz | PASS | User Confirmed | ~830 | ✅ |
| residuals.tar.gz | PASS | User Confirmed | ~3 | ✅ |
| notebook.tar.gz | PASS | User Confirmed | Unknown | ✅ |
| tiger.tar.gz | PASS | User Confirmed | Unknown | |
| fti.tar.gz | PASS | User Confirmed | Unknown | |
| pca.tar.gz | PASS | User Confirmed | Unknown | |
| pseobnr.tar.gz | PASS | User Confirmed | Unknown | |
| qnmrf.tar.gz | PASS | User Confirmed | Unknown | ✅ |
| skymaps.tar.gz | PASS | User Confirmed | Unknown | |
| GW240925-C00-Strain.tar | PASS | User Confirmed | ~2500 | ✅ |

---

## Critical Archives

All 7 critical archives confirmed extracted by user:
- ✅ combined_samples (posterior samples)
- ✅ calibration (priors)
- ✅ cal_env (envelope)
- ✅ ringdown (QNM data)
- ✅ residuals (post-subtraction)
- ✅ notebook (Jupyter notebooks)
- ✅ qnmrf (QNM rational filter)
- ✅ GW240925-C00-Strain (raw strain)

---

## Recommendation

✅ **Proceed to Phase 2: Science Mapping**

All critical archives extracted. Ready for HDF5 inspection and notebook analysis.

---

*Report generated based on user confirmation of completed extraction.*
