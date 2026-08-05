# SSZ-LIGO Tests — Repository Findings

**Repository:** `E:\clone\ssz-ligo-tests`  
**GitHub:** error-wtf/ssz-ligo-tests  
**Last Updated:** 2026-05-19  
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES  
**Status:** PHASES 1–9 COMPLETE

---

## Overview

This repository implements an **anti-circular, exploratory SSZ strain pipeline** for GW240925.
No physics claims are made. All formulas are source-locked or explicitly marked BLOCKED.

---

## Derived V0 Formulas

### deltaPsi_SSZ(f) — DERIVED_V0_PROXY

**Source:** formula_compendium.md §C.1, SSZ Book Ch.31, ssz_inspiral.py

```
r(f)     = (G*M / (pi*f)^2)^(1/3)       [Kepler 3rd law]
rdot_SSZ = rdot_GR * D^2 / s^4          [locked: formula_compendium §C.1]
deltaPsi_V0 = integral [1/D(r') - 1] * Omega(r') / rdot_GR(r') dr'
```

**Regime LIGO band (20–800 Hz, 8.9 Msun):** r/rs ≈ 100–1000 (weak field)  
**Branch:** g2_decay (operative per FORMULA_BRANCH_LOCK.md)  
**FORMULA_STATUS:** DERIVED_V0_PROXY  
**Implementation:** `src/ssz_ligo_tests/derived_phase.py`

### deltaA_SSZ(f) — DERIVED_V0_PROXY

**Source:** formula_compendium.md §B.4

```
P_GW_SSZ = P_GW_GR * D^2 / s^2
deltaA(f) = D(r(f))^2 - 1   in (-1, 0]
```

**Implementation:** `src/ssz_ligo_tests/derived_amplitude.py`

### h_SSZ(f) — DERIVED_V0_PROXY

```
h_SSZ(f) = h_GR(f) * [1 + deltaA(f)] * exp(i * deltaPsi(f))
```

**Implementation:** `src/ssz_ligo_tests/derived_waveform.py`

---

## epsilon_220 Registry — BLOCKED

Three conflicting branches from corpus. No canonical branch selected.

| Branch | Value | Source | Status |
|--------|-------|--------|--------|
| v51_ch30_3_percent | 0.03 | SSZ Book V51 Ch.30 | PARTIAL_EXPLORATORY |
| dmin_squared_scale | 0.308 | formula_compendium §B.7 | SUPERSEDED_OR_DIFFERENT_REGIME |
| photon_sphere_39_percent | 0.39 | qnm_spectrum.md (r*/rs=1.387) | DISCARDED_FOR_LIGO_STRAIN |

**Note:** The 39% value is a source-frame QNM *frequency* ratio from `qnm_spectrum.md`, not a LIGO strain amplitude observable. Using it as a strain observable is a category error.  
**Implementation:** `src/ssz_ligo_tests/epsilon_220_registry.py`  
**FORMULA_STATUS:** BLOCKED_BRANCH_CONFLICT

---

## Pipeline Run Results (GW240925, H1, 2026-05-18)

| Item | Value |
|------|-------|
| Strain source | GWOSC LIGO HDF5 |
| Anti-circularity | VALID_INDEPENDENT |
| deltaPsi band (20–800 Hz) | min=5.98e-02, max=1.08e+01 rad |
| deltaA band (20–800 Hz) | min=−0.692, max=−0.065 |
| lnL GR control (0PN) | −3.24e+07 |
| lnL SSZ V0-proxy | −3.24e+07 |
| delta_lnL | +6.34e-06 |
| Interpretation | INDISTINGUISHABLE (delta_lnL < 1) |
| MF-SNR GR | 39.92 |
| MF-SNR SSZ | 14.23 (V0 proxy not amplitude-matched) |

**SSZ_SUPPORT_CLAIM_MADE:** NO  
**SSZ_FALSIFICATION_CLAIM_MADE:** NO  
**READY_FOR_REAL_LIGO_SSZ_CLAIM:** NO

---

## Test Suite

| Test File | Tests | Status |
|-----------|-------|--------|
| test_derived_delta_psi_v0.py | 13 | PASS |
| test_derived_delta_a_v0.py | 11 | PASS |
| test_h_ssz_v0_waveform_application.py | 13 | PASS |
| test_epsilon_220_branch_registry.py | 11 | PASS |
| test_no_data_fitting.py | 13 | PASS |
| **Full suite** | **330** | **330 PASS, 1 xfail (expected)** |

**xfail:** `test_d_min_squared_vs_3_percent` — ε₂₂₀ ambiguity (31% vs 3%) cannot be resolved without author decision.

---

## Locked Constants (from FORMULA_BRANCH_LOCK.md)

| Constant | Value | Source |
|----------|-------|--------|
| Xi_strong | 1 − exp(−φ·rs/r) [decay form] | formula_compendium.md §A.3 |
| BLEND_START | 1.8 rs | FORMULA_BRANCH_LOCK.md |
| BLEND_END | 2.2 rs | FORMULA_BRANCH_LOCK.md |
| D_min at rs | 0.555 | formula_compendium.md |
| Xi at rs | 0.802 | formula_compendium.md |
| s at rs | 1.802 | radial_scaling.md |

---

## Open Blockers

1. **BLOCKED_MISSING_EQUATION:** deltaPsi exact RSG phase integral (SSZ Book Ch.31 not yet final)
2. **BLOCKED_BRANCH_CONFLICT:** epsilon_220 (3 conflicting sources: 3%, 31%, 39%)
3. **GR_CONTROL_LIMITED:** TaylorF2 0PN only — no spin, no merger, no ringdown

---

## Phase 9 — H1/L1 Time-Delay Replication (2026-05-19)

**Script:** `scripts/run_h1_l1_time_delay_replication.py`  
**Output:** `reports/H1_L1_TIME_DELAY_REPLICATION_REPORT.md`, `data_manifest/h1_l1_delay_scan.csv` (2208 rows)

### Method

FFT cross-correlation lag scan ±50 ms coarse / ±10 ms fine. 6 subbands (20-40, 40-80, 80-120, 120-160, 160-210, 20-210 Hz). Off-source comparison window at t−500 s to detect persistent systematics. Sign-flip test for L1.

### Results

| Window | Band | Verdict | Peak xcorr |
|--------|------|---------|------------|
| TRIGGER | 20-210 Hz | PHYSICAL_DELAY_COHERENT | −0.9959 |
| TRIGGER | 20-40 Hz | PHYSICAL_DELAY_COHERENT | −0.9998 |
| OFF_m500 | 20-210 Hz | PHYSICAL_DELAY_COHERENT | −0.9999 |
| OFF_m500 | 20-40 Hz | PHYSICAL_DELAY_COHERENT | −0.9998 |

**H1_L1_REPLICATION_STATUS: COHERENT_WITH_SIGN_FLIP** (updated 2026-05-19)

The full-band trigger shows abs(xcorr) = 0.991 at dt = 0 ms. The negative sign is physically
expected (H1/L1 opposite arm orientations). The previous PERSISTENT_SYSTEMATIC classification
was a peak-detection artifact from using argmax(corr) instead of argmax(|corr|).

The L1 20–40 Hz non-Gaussianity (kurtosis +44.9) remains separately unresolved.
Subband abs-correlation run is the next required step.

### Gate

```text
H1_L1_REPLICATION_STATUS:        COHERENT_WITH_SIGN_FLIP
BEST_DELAY:                       0 ms
BEST_ABS_CORR:                    0.991
PREVIOUS_DT_MINUS_10MS_RESULT:    CLASSIFICATION_ARTIFACT
TRIGGER_SPECIFIC:                 PENDING (subband abs-corr required)
L1_20_40_STATUS:                  DQ_CONTEXT_REQUIRED
READY_FOR_REAL_LIGO_SSZ_CLAIM:    NO
SSZ_SUPPORT_CLAIM_MADE:           NO
SSZ_FALSIFICATION_CLAIM_MADE:     NO
```

---

## Absolute Rules Compliance

All 9 absolute rules confirmed: no fitting, no tuning, no posterior verdict,
no SSZ claims, no silent GR substitution, no source deletions,
all formulas documented, blocked items marked, conflicts preserved.
