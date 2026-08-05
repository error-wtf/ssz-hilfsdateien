# epsilon_220 — Derivation Status Document

**FORMULA_STATUS:** BLOCKED_BRANCH_CONFLICT
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `src/ssz_ligo_tests/epsilon_220_registry.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 5

---

## Definition

`epsilon_220` is intended to parametrize the SSZ modification to the
(2,2,0) ringdown quasi-normal mode (QNM) in the LIGO strain.

In the GR ringdown, the dominant QNM contributes:

```
h_ringdown(t) ~ A_220 * exp(-t/tau_220) * cos(2*pi*f_220*t + phi_0)
```

The SSZ modification would enter as:

```
f_220_SSZ = f_220_GR * (1 + epsilon_220_freq)   [frequency shift]
A_220_SSZ = A_220_GR * (1 + epsilon_220_amp)     [amplitude shift]
tau_220_SSZ = tau_220_GR * (1 + epsilon_220_tau) [damping time shift]
```

The question is: what are `epsilon_220_freq`, `epsilon_220_amp`, `epsilon_220_tau`
in SSZ? Three corpus values exist, but they measure different things.

---

## Branch Classification

### Branch 1: v51_ch30_3_percent

| Item | Content |
|------|---------|
| Value | ~3% |
| Source | SSZ Book V51 Ch.30, SSZ_BOOK_DE_CLEAN.md |
| Formula | Fundamental QNM frequency shift from SSZ metric modification |
| Regime | Weak perturbation of QNM at effective photon sphere |
| Observable | Frequency shift: `f_220_SSZ/f_220_GR - 1 ~ 0.03` |
| LIGO strain compatible? | **NO** — marked as partial/exploratory in source |
| Used for claim? | **NO** |
| Status | `PARTIAL_EXPLORATORY` |

**Note:** The 3% value appears in early exploratory notes in Ch.30.
It is not given a locked derivation in the corpus.

### Branch 2: dmin_squared_scale

| Item | Content |
|------|---------|
| Value | D_min^2 = 0.555^2 ≈ 0.308 → ~31% |
| Source | formula_compendium.md §B.7 |
| Formula | `epsilon_220 ~ D_min^2 - 1` |
| Regime | Strong-field amplitude suppression at r = r_s |
| Observable | Amplitude factor, NOT frequency shift |
| LIGO strain compatible? | **NO** — different observable type (amplitude, not freq) |
| Used for claim? | **NO** |
| Status | `SUPERSEDED_OR_DIFFERENT_REGIME` |

**Note:** D_min^2 is a plausible amplitude scale at the Schwarzschild radius.
But applying it as a QNM frequency observable is a category error.

### Branch 3: photon_sphere_39_percent

| Item | Content |
|------|---------|
| Value | ~39% |
| Source | qnm_spectrum.md, r* = 1.387*r_s |
| Formula | `f_SSZ/f_GR = 1/D(r*) ≈ 1.39` → `epsilon_220_freq = 0.39` |
| Regime | Source-frame QNM frequency ratio at photon sphere |
| Observable | **Source-frame QNM frequency ratio**, not LIGO strain amplitude |
| LIGO strain compatible? | **NO** — category error for LIGO strain application |
| Used for claim? | **NO** |
| Status | `DISCARDED_FOR_LIGO_STRAIN_TEST` |

**Note:** The 39% is NOT the strain amplitude observable in LIGO.
It is the ratio `f_QNM_SSZ / f_QNM_GR` at the photon sphere.
Converting this to a LIGO strain claim requires additional derivation:
- How does a source-frame QNM frequency shift appear in detector strain?
- Is the frequency shift the dominant observable or the amplitude/damping?
- What does Strong→Weak RSG mapping do to this shift at detector?

---

## Why the Three Values Are Not Mutually Exclusive

All three values are plausible **within their own regime and observable definition**:

| Branch | Observable | Regime | Compatible with others? |
|--------|-----------|--------|------------------------|
| 3% | freq shift (exploratory) | QNM near r* | Not ruled out by 39% |
| 31% | amplitude scale at r_s | strong field amplitude | Different quantity from freq |
| 39% | source QNM freq ratio | photon sphere | Not same as LIGO strain obs |

They are not mutually contradictory — they measure **different physical quantities**.
The conflict is in their labeling: all three are sometimes called `epsilon_220`
as if they were the same observable.

---

## Why the Pipeline Sees delta_lnL ~ 0

The exploratory pipeline ran **without any epsilon_220 correction** (BLOCKED).
The result delta_lnL ~ 6e-6 (effectively zero) reflects:

1. The inspiral-only V0 corrections (deltaPsi, deltaA) produce tiny effects in the
   weak-field LIGO band (r/rs ~ 100–1000 at 20–800 Hz)
2. No ringdown correction was applied
3. The V0 proxy is limited to 0PN TaylorF2 GR control

**This is not a falsification of epsilon_220.** It simply shows that the
inspiral phase correction alone is too small to distinguish in the current setup.

---

## Correct Observable Identification for LIGO Strain

To build a proper SSZ ringdown observable for LIGO strain, one must:

1. Identify where in the SSZ metric the QNM boundary conditions live
2. Derive QNM frequencies from SSZ metric (not just ratio at photon sphere)
3. Map the source-frame QNM frequency shift to detector-frame strain modification
4. Account for Strong→Weak RSG propagation between source and detector
5. Derive amplitude and damping-time shifts separately

Until these steps are completed, no `epsilon_220` value is usable for LIGO strain.

---

## Final Status

```
epsilon_220_for_real_ligo_claim = None
FORMULA_STATUS:                   BLOCKED_BRANCH_CONFLICT
READY_FOR_REAL_CLAIM:             NO
EXPLORATORY_VALUES_AVAILABLE:     3%, 31%, 39% (different observables)
CANONICAL_VALUE:                  NONE — Author decision required
CATEGORY_ERROR_WARNING:           39% is QNM freq ratio, NOT LIGO strain amplitude
```

---

## What Must Change to Unblock

1. Author selects canonical `epsilon_220` definition (freq / amplitude / damping)
2. Full QNM derivation from SSZ metric (not photon sphere approximation)
3. Strong→Weak RSG propagation factor derived for ringdown signal
4. All three corpus values re-labeled with their correct observable names
5. Pre-registration of selected branch before any LIGO comparison
