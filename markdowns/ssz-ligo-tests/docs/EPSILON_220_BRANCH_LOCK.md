# Epsilon_220 Branch Lock
Status: LOCKED_CONFLICT_DOCUMENTATION
Generated: 2026-05-18
Source: ssz-complete-documentation/06_STRONG_FIELD/qnm_spectrum.md
Source: ssz-complete-documentation/03_FORMULAS/formula_compendium.md §B.7
Source: ssz-ligo-tests/src/ssz_ligo_tests/ssz_ringdown.py (existing audit)

---

## Branch Classification

### Branch A — V51 / Chapter 30 Estimate
- **Value:** ~3% (epsilon_220 ≈ 0.03)
- **Origin:** SSZ_BOOK_DE_CLEAN.md Ch.30, V51 PDF
- **Context:** Fundamental QNM mode shift for inspiral/ringdown
- **LIGO relevance:** Below single-event precision; stacking or ET/CE required
- **Classification:** CANONICAL_RINGDOWN_NOTE_EXPLORATORY
- **Status:** PARTIAL_EXPLORATORY — exact derivation not yet locked

### Branch B — D_min² Scaling
- **Value:** ~31% (1 - D_min² = 1 - 0.555² ≈ 0.692, or D_min² ≈ 0.308)
- **Origin:** Older "proportional to D_min²" interpretation
- **Context:** Possibly different regime or physical quantity
- **Classification:** SUPERSEDED_OR_DIFFERENT_REGIME
- **Status:** NOT used for LIGO claim

### Branch C — Photon Sphere / QNM Spectrum
- **Value:** ~39% (f_SSZ/f_GR ≈ 1.39)
- **Origin:** qnm_spectrum.md, formula: 1/D(r*) at r* = 1.387 rs, D(r*) = 0.72
- **Context:** Raw strong-field frequency ratio at photon sphere
- **Why this is NOT the LIGO observable:**
  LIGO measures calibrated strain, not emitted-frame QNM frequency.
  The 39% is a source-frame strong-field ratio.
  The correct LIGO chain is: strong-field → RSG phase accounting → weak-field propagation → deltaPsi(f) → strain.
- **Classification:** HISTORICAL_PHOTON_SPHERE_OR_QNM_SPECTRUM_BRANCH
- **Status:** DISCARDED_FOR_LIGO_STRAIN_TEST

---

## Model History Statement

```
HISTORICAL_APPROXIMATION:
  39% photon-sphere / qnm_spectrum branch
  Source: qnm_spectrum.md, 1/D(r*)
  Not locked for LIGO strain prediction
  Discarded: DISCARDED_FOR_LIGO_STRAIN_TEST
  Reason: wrong observable chain for interferometer

CANONICAL_RINGDOWN_NOTE:
  ~3% fundamental mode (V51 / Ch.30)
  Below current single-event precision
  Testable via stacking or ET/CE
  Status: PARTIAL_EXPLORATORY

CURRENT_FORWARD_MODEL:
  Strong-field → Radial Scaling Gauge → weak-field propagation
  deltaPsi_SSZ(f) / deltaA_SSZ(f)
  h_SSZ(f) — full derivation NOT YET IN CORPUS
  Current pipeline: V0_PROXY only
```

---

## Implementation Requirement

```python
# epsilon_220 is None by default — no real ringdown claim allowed
EPSILON_220_LOCKED = None  # Requires author resolution

# Branch record
EPSILON_220_BRANCHES = {
    "A_v51_ch30":        {"value": 0.03,  "status": "PARTIAL_EXPLORATORY"},
    "B_dmin_squared":    {"value": 0.308, "status": "SUPERSEDED_OR_DIFFERENT_REGIME"},
    "C_photon_sphere":   {"value": 0.39,  "status": "DISCARDED_FOR_LIGO_STRAIN_TEST"},
}
```

Tests must verify:
- Branches A, B, C are NOT interchangeable
- No ringdown claim if epsilon_220 is None
- Branch C raises or is explicitly marked DISCARDED_FOR_LIGO_STRAIN_TEST

---

## What "Smaller than 39%" Means

If the RSG strain pipeline yields deltaPsi << 39%:
- This is EXPECTED, not a failure
- 39% was a source-frame ratio, not a strain prediction
- Smaller strain effect = correct physics: RSG phase accounting in weak-field propagation
- This is MODEL_REFINEMENT, not goalpost-moving
- Claim status remains: READY_FOR_REAL_SSZ_CLAIM = NO

---
© 2026 SSZ-LIGO Test Suite
