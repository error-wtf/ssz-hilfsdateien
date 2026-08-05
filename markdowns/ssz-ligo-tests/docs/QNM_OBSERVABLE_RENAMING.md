# QNM Observable Renaming — epsilon_220 Branch Disambiguation

**Date:** 2026-05-18
**Purpose:** Prevent misuse of the three "epsilon_220" values as if they measured
the same observable. Each branch is a different physical quantity.
**Action:** Rename conceptually in docs and registry; do NOT delete old branch keys.

---

## The Problem

All three values were called "epsilon_220" as if they were competing answers
to one question. They are not. They measure different observables in different
regimes. Calling all three "epsilon_220" creates a false conflict.

---

## Renaming Map

| Old name (registry key) | New conceptual name | Physical meaning | Regime |
|------------------------|--------------------|--------------------|--------|
| `v51_ch30_3_percent` | `qnm_freq_shift_v51_exploratory` | QNM frequency shift relative to GR, from V51 Ch.30 | near-horizon, strong |
| `dmin_squared_scale` | `amplitude_scale_dmin_squared` | Amplitude correction D_min^2 = 0.308 at r=rs | strong-field max |
| `photon_sphere_39_percent` | `source_frame_qnm_ratio` | f_SSZ / f_GR source-frame frequency ratio at photon sphere | r*/rs = 1.387 |

**None of these three is a LIGO strain amplitude observable.**
**None of these three is directly comparable to the others.**

---

## Why the 39% is NOT a LIGO strain observable

The 39% comes from:
```
f_SSZ/f_GR = 1/D(r*) at r* = 1.387 rs (photon sphere, saturation branch)
D(r*) = 1/(1 + Xi(r*)) ≈ 0.72
=> ratio ≈ 1.39
```

This is a **source-frame QNM frequency ratio**. When a gravitational wave
propagates from source to detector:
- SSZ RSG phase accounting partially compensates the frequency shift
- The LIGO strain sees a propagation-corrected signal, not raw source-frame ratio
- The correct LIGO observable is deltaPsi_SSZ(f) after RSG integration

**The 39% was never the right LIGO-strain correction. It is a strong-field
source-frame quantity.**

---

## Why the 3% is NOT yet a LIGO strain observable

The 3% from V51/Ch.30 is:
- An exploratory QNM frequency shift estimate
- Derived under assumptions not yet fully documented in corpus
- Status: EXPLORATORY, not DERIVED or LOCKED

---

## Why the 31% (D_min^2) is NOT a LIGO strain observable

The 31% = 1 - D_min^2 = 1 - 0.308 = 0.692:
- Represents maximum amplitude suppression at r = rs
- This is the strong-field limit, not the inspiral-band value
- In the LIGO band (r >> rs): D^2 → 1, deltaA → 0
- D_min^2 only relevant for deep strong-field (merger/ringdown proximity)

---

## Updated epsilon_220_registry.py Keys (No Key Deletion)

Old keys preserved for backward compatibility.
New `canonical_name` field added to each branch entry.
No existing test breaks.

### Affected file: src/ssz_ligo_tests/epsilon_220_registry.py

Add `canonical_name` field to each branch dict:
- `v51_ch30_3_percent` → `canonical_name = "qnm_freq_shift_v51_exploratory"`
- `dmin_squared_scale` → `canonical_name = "amplitude_scale_dmin_squared"`
- `photon_sphere_39_percent` → `canonical_name = "source_frame_qnm_ratio"`

---

## What This Means for Book and Documentation

| Incorrect formulation (FORBIDDEN) | Correct formulation |
|-----------------------------------|---------------------|
| "epsilon_220 = 39%" | "source-frame QNM ratio at photon sphere = 39%" |
| "epsilon_220 = 3%" | "exploratory QNM freq shift V51/Ch.30 = 3%" |
| "epsilon_220 conflict: 3% vs 31% vs 39%" | "three different observables, no conflict" |
| "LIGO tests epsilon_220" | "LIGO strain pipeline tests deltaPsi/deltaA, not QNM directly" |

---

## Status

```
RENAMING_COMPLETE:             DOCS_ONLY (registry keys preserved)
EPSILON_220_STATUS:            BLOCKED_BRANCH_CONFLICT (unchanged)
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO (unchanged)
BOOK_ACTION_REQUIRED:          YES — remove all "epsilon_220 = 39%" LIGO-strain claims
```
