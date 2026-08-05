# SSZ-LIGO Observable Branch Matrix

**Version:** 1.0  
**Date:** 2026-05-18  
**Status:** CANONICAL REFERENCE  

---

## Motivation

The three values 3%, 31%, 39% are **not three estimates of the same quantity**.
They are three different observables in three different regimes, described by different
source paths. They must never be collapsed into a single "epsilon_220 = X%" test.

This document defines every possible SSZ observable branch as a separate testable hypothesis.

**Rule:** A branch is "tested" only when:
1. A formula exists that maps it to h(f) or a strain residual
2. That formula was applied to real or synthetic LIGO strain
3. A likelihood or SNR comparison was computed
4. The result was documented without physics claim

---

## Branch 1: INSPIRAL_PHASE_RSG

| Field | Value |
|-------|-------|
| **Name** | INSPIRAL_PHASE_RSG |
| **Formula** | `delta_psi_SSZ(f) = [Omega(r)/|rdot_GR(r)|] * [(1+Xi)^6 - 1] * |dr/df|` |
| **Source path** | `rdot_SSZ = rdot_GR * D(r)^2 / s(r)^4` → `dφ/dr = Omega/rdot` → `delta_psi(f)` |
| **Derivation doc** | `docs/DELTA_PSI_DERIVATION.md`, `docs/DELTA_PSI_V1_LOCK_ATTEMPT.md` |
| **Formula status** | `DERIVED_V1_INSPIRAL_0PN_LOCKED` |
| **Observable type** | Phase deformation in h(f) |
| **Regime** | Inspiral only (r/rs >> 1, weak-field Xi = rs/2r) |
| **Enters h(f)** | YES: `h_SSZ(f) = h_GR(f) * exp(i * delta_psi)` |
| **Inspiral/Merger/Ringdown** | INSPIRAL only (0PN, valid below f_ISCO) |
| **F_HIGH cap** | 210 Hz (f_ISCO ~ 215 Hz for M~20 Msun) |
| **Required data** | H1/L1 calibrated strain, off-source PSD |
| **Anti-circularity** | VALID: no posterior, GR control = analytic 0PN only |
| **Test type** | Strain residual + noise-weighted lnL |
| **Current readiness** | `YES_EXPLORATORY` |
| **Already run** | YES — H1: delta_lnL = 5.3e-06, L1: -4.4e-05 (pipeline diagnostic) |
| **What would support it** | delta_lnL >> 0 consistently across detectors after noise issues resolved |
| **What would falsify it** | delta_lnL consistent with 0 at higher PN order with improved template |
| **Blocker** | 0PN only → need 3.5PN r(f) for meaningful sensitivity |

---

## Branch 2: INSPIRAL_AMPLITUDE_POWER

| Field | Value |
|-------|-------|
| **Name** | INSPIRAL_AMPLITUDE_POWER |
| **Formula** | `delta_a_SSZ(f) = D(r(f))^2 - 1` |
| **Source path** | `P_GW_SSZ / P_GW_GR = D^2/s^2` → `|h_SSZ|/|h_GR| = D(r)` → `delta_a = D^2 - 1` |
| **Derivation doc** | `docs/DELTA_A_DERIVATION.md` |
| **Formula status** | `DERIVED_V0_INSPIRAL_ONLY` |
| **Observable type** | Amplitude envelope deformation in h(f) |
| **Regime** | Inspiral only — NOT ringdown amplitude |
| **Enters h(f)** | YES: `h_SSZ(f) = h_GR(f) * (1 + delta_a)` |
| **Inspiral/Merger/Ringdown** | INSPIRAL only — scope explicitly limited |
| **Required data** | H1/L1 strain, calibration envelope knowledge |
| **Anti-circularity** | VALID |
| **Test type** | Calibration sensitivity: is |delta_a| > calibration uncertainty? |
| **Current readiness** | `PARTIAL` |
| **Already run** | YES — SSZ_EFFECT_ABOVE_CALIBRATION: YES (6.3e-06 > cal_spread 7.1e-08) |
| **Caveat** | Effect is stable against calibration, but absolute magnitude tiny |
| **What would support it** | Consistent amplitude suppression across H1/L1 in well-characterised band |
| **What would falsify it** | No systematic amplitude deviation at higher PN + better PSD |
| **Blocker** | Scope: amplitude formula not yet scoped to merger onset |

---

## Branch 3: QNM_FREQ_3PCT_BRANCH

| Field | Value |
|-------|-------|
| **Name** | QNM_FREQ_3PCT_BRANCH |
| **Formula** | `f_220_SSZ = f_220_GR * (1 + epsilon_220)` with `epsilon_220 ~ 0.03` |
| **Source path** | SSZ Book V51 Ch.30 — text says "ca. 3%" relative to GR QNM |
| **Derivation doc** | `docs/EPSILON_220_DERIVATION_STATUS.md` |
| **Formula status** | `PARTIAL_EXPLORATORY — not derived from first principles` |
| **Observable type** | Ringdown frequency shift — appears in post-merger h(t) |
| **Regime** | Ringdown (r ~ r_s, strong field) |
| **Enters h(f)** | NOT YET — requires ringdown strain model: `h_rd(t) = A*exp(-t/tau)*cos(2*pi*f_220*t)` |
| **Inspiral/Merger/Ringdown** | RINGDOWN only |
| **Required data** | Ringdown-only strain window (post-merger), clean ringdown SNR |
| **Anti-circularity** | MUST NOT use posterior f_220 as reference — only GR prediction from M_f, chi_f |
| **Test type** | Ringdown injection sensitivity: would a 3% shift be detectable at GW240925 SNR? |
| **Current readiness** | `NO` — ringdown strain observable not yet built |
| **Already run** | NO |
| **Blocking issue** | epsilon_220 is a text statement, not a derived formula |
| **Next step** | Build synthetic ringdown injection sensitivity (Test C) |
| **What would support it** | Ringdown SNR sufficient to resolve 3% frequency shift |
| **What would falsify it** | Sensitivity test shows 3% indistinguishable from GR at GW240925 SNR |

---

## Branch 4: AMPLITUDE_DMIN2_BRANCH

| Field | Value |
|-------|-------|
| **Name** | AMPLITUDE_DMIN2_BRANCH |
| **Formula** | `scaling ~ D_min^2 = 0.3082...` |
| **Source path** | `D_min = 1/(1+Xi_max)` → amplitude damping at strong-field limit |
| **Derivation doc** | `docs/EPSILON_220_DERIVATION_STATUS.md` — "31% branch" |
| **Formula status** | `DIFFERENT_OBSERVABLE — not frequency shift` |
| **Observable type** | Strong-field amplitude/damping scale — NOT a frequency observable |
| **Enters h(f)** | NOT DIRECTLY — requires ringdown amplitude equation |
| **Inspiral/Merger/Ringdown** | MERGER/RINGDOWN strong field only |
| **Required data** | Ringdown amplitude calibration + derived damping equation |
| **Anti-circularity** | Needs independent derivation of damping → strain coupling |
| **Test type** | Only after ringdown amplitude equation is derived |
| **Current readiness** | `NO` |
| **Already run** | NO |
| **Critical note** | 31% ≠ 3% ≠ 39%. This measures amplitude damping, not frequency. |
| **Blocker** | No derived ringdown amplitude equation exists yet |

---

## Branch 5: PHOTON_SPHERE_39PCT_BRANCH

| Field | Value |
|-------|-------|
| **Name** | PHOTON_SPHERE_39PCT_BRANCH |
| **Formula** | `f_SSZ / f_GR ≈ 1/D(r*) ≈ 1.39` where r* = photon sphere radius |
| **Source path** | `docs/qnm_spectrum.md` — photon sphere orbit frequency ratio |
| **Derivation doc** | `docs/QNM_OBSERVABLE_RENAMING.md` |
| **Formula status** | `SOURCE_FRAME_QNM_RATIO — not a detector-frame observable` |
| **Observable type** | Source-frame strong-field orbital frequency ratio |
| **Enters h(f)** | NO — not directly. Requires source-frame → detector-frame mapping |
| **Inspiral/Merger/Ringdown** | STRONG FIELD / QNM vicinity only |
| **Required data** | Source-frame-to-detector-strain mapping (does not exist yet) |
| **Anti-circularity** | Cannot use posterior chi_f or M_f — would be circular |
| **Test type** | Only after detector-strain mapping is derived analytically |
| **Current readiness** | `NO` |
| **Already run** | NO |
| **Critical note** | 39% is the frequency RATIO at the source, not a LIGO strain shift |
| **Blocker** | No source-frame → h(f) mapping exists for this observable |

---

## Summary Matrix

| Branch | Formula | Status | Enters h(f) | Tested | Readiness |
|--------|---------|--------|-------------|--------|-----------|
| INSPIRAL_PHASE_RSG | delta_psi = (Omega/rdot)*(Xi^6...) | DERIVED_V1_0PN_LOCKED | YES | YES (H1/L1 run) | YES_EXPLORATORY |
| INSPIRAL_AMPLITUDE_POWER | delta_a = D^2-1 | DERIVED_V0_INSPIRAL | YES | YES (cal scan) | PARTIAL |
| QNM_FREQ_3PCT | f_220 * 1.03 | PARTIAL_EXPLORATORY | NOT YET | NO | NO — build injection |
| AMPLITUDE_DMIN2 | ~D_min^2 = 0.308 | DIFFERENT_OBSERVABLE | NOT YET | NO | NO — no equation |
| PHOTON_SPHERE_39PCT | f_SSZ/f_GR = 1/D(r*) | SOURCE_FRAME_ONLY | NO | NO | NO — no mapping |

---

## Hard Rules

```
RULE 1: Never say "epsilon_220 tested" unless a ringdown strain observable
        using that specific branch was built and run.

RULE 2: Never collapse 3% / 31% / 39% into one test.
        They are different formulas, different observables, different regimes.

RULE 3: "Inspiral tested" means only Branch 1 + Branch 2.
        It says NOTHING about ringdown.

RULE 4: A sensitivity test (can we even see it?) must come BEFORE a signal test.

RULE 5: No posterior f,m,chi in any branch test.
        GR prediction from fixed physical priors only.

READY_FOR_REAL_LIGO_SSZ_CLAIM: NO (any branch)
SSZ_SUPPORT_CLAIM_MADE: NO
SSZ_FALSIFICATION_CLAIM_MADE: NO
```

---

## Next Steps per Branch

| Branch | Immediate Next Step |
|--------|---------------------|
| INSPIRAL_PHASE_RSG | Upgrade to 3.5PN r(f) mapping |
| INSPIRAL_AMPLITUDE_POWER | Scope lock: inspiral only, define merger onset |
| QNM_FREQ_3PCT | Build synthetic ringdown injection sensitivity test |
| AMPLITUDE_DMIN2 | Derive ringdown amplitude equation from first principles |
| PHOTON_SPHERE_39PCT | Derive source-frame → detector-strain coupling |
