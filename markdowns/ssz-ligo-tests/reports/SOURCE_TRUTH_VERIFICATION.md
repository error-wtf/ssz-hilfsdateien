# SOURCE-OF-TRUTH VERIFICATION REPORT

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18
Status: CANONICAL AUDIT COMPLETE

---

## Sources Read Before Any Test

| # | Source | Path | Key Finding |
|---|--------|------|-------------|
| 1 | formula_compendium.md | ssz-complete-documentation/03_FORMULAS/ | CANONICAL formula list |
| 2 | regime_and_formula_domain_clarification.md | ssz-complete-documentation/02_FOUNDATIONS/ | Two Xi forms: saturation vs. decay |
| 3 | qnm_spectrum.md | ssz-complete-documentation/06_STRONG_FIELD/ | QNM: ~39% shift (1/D(r*)) |
| 4 | known_limitations.md | ssz-complete-documentation/08_FALSIFICATION/ | GW waveform: NOT yet complete in SSZ |
| 5 | falsification_criteria.md | ssz-complete-documentation/08_FALSIFICATION/ | Hard falsification conditions |
| 6 | forbidden_formulas.md | ssz-complete-documentation/03_FORMULAS/ | Deprecated formulas (BANNED) |
| 7 | radial_scaling.md | ssz-complete-documentation/05_ELECTROMAGNETISM/ | RSG: s(r) = 1 + Xi = 1/D |

---

## LOCKED CORE EQUATIONS (Source-Confirmed)

### Xi Formulas — Two Forms, Both Source-Confirmed

| Form | Formula | Status | Domain |
|------|---------|--------|--------|
| **g2 / Saturation (CANONICAL)** | Xi = min(1 - exp(-phi * r/rs), Xi_max) | OPERATIVE | r/rs < 1.8 |
| **Decay (didactic only)** | Xi = 1 - exp(-phi * rs/r) | COMPLEMENTARY | same r=rs value |
| DEPRECATED (BANNED) | Xi = (rs/r)^2 * exp(-r/r_phi) | FORBIDDEN | — |

Source: `formula_compendium.md` §B.1, `regime_and_formula_domain_clarification.md` §Saturation vs Decay

**CRITICAL FINDING:**
`ssz_core.py` uses `xi = 1 - exp(-phi * rs/r)` — this is the **DECAY form** (didactic/complementary).
The CANONICAL g2 form is `1 - exp(-phi * r/rs)`.
Both give identical values at r = rs (Xi = 0.802) but differ elsewhere.
This is a formula-form inconsistency. Status: MISMATCH_DECAY_NOT_CANONICAL

### Regime Boundaries (Source-Confirmed)

| Boundary | Value (r/rs) | Source |
|----------|-------------|--------|
| g2 / very_close | < 1.8 | regime_and_formula_domain_clarification.md |
| blend | 1.8 – 2.2 | formula_compendium.md §B.2 |
| g1 / photon_sphere | 2.2 – 3.0 | regime_and_formula_domain_clarification.md |
| g1 / strong | 3.0 – 10.0 | regime_and_formula_domain_clarification.md |
| g1 / weak | > 10.0 | regime_and_formula_domain_clarification.md |

**NOTE:** ssz_core.py uses boundaries 1.0 and 2.2 — NOT matching canonical 1.8/2.2.
Status: REGIME_BOUNDARY_MISMATCH (lower boundary 1.0 vs canonical 1.8)

### Special Values (Source-Confirmed)

| Value | Canonical | ssz_core.py | Match |
|-------|-----------|-------------|-------|
| Xi(rs) | 0.80171 | 0.80171 | YES (both forms agree at r=rs) |
| D(rs) | 0.55503 | 0.55503 | YES |
| Xi_max | 1 - exp(-phi) ≈ 0.802 | same | YES |
| D_min | 1/(1 + Xi_max) ≈ 0.555 | same | YES |

---

## EPSILON_220 RINGDOWN — CONFLICT AUDIT

| Source | Value | Formula/Context |
|--------|-------|----------------|
| qnm_spectrum.md | **~39%** | 1/D(r*) at r* = 1.387 rs, D(r*) = 0.72 |
| formula_compendium.md §B.7 | D_intersection depends on Xi-form | r*/rs = 1.595 (decay) or 1.387 (saturation) |
| V51 Book Ch.30 | **~3%** | Referenced in test suite ringdown model |
| D_min^2 argument | **~31%** | 1 - D_min^2 = 1 - 0.555^2 |

**STATUS: CONFLICTING_SSZ_SOURCES — epsilon_220 NOT LOCKED**
**ACTION REQUIRED: Author decision on which source is canonical for QNM**

---

## GW FORWARD MODEL — SOURCE STATUS

From `known_limitations.md` §3 (CANONICAL):
> "SSZ modifies the metric → gravitational wave propagation is affected
>  But a complete GW waveform calculation in SSZ is not yet available"

**CONSEQUENCE:**
- delta_psi_SSZ(f): V0 PROXY only — no locked corpus equation
- h_SSZ(f): NOT DERIVED in any source
- REAL_LIGO_NUMERICAL_CLAIM: BLOCKED by canonical known_limitations.md

RSG bridge (from `radial_scaling.md`):
- s(r) = 1 + Xi(r) = 1/D(r) — LOCKED
- Phase accumulation via dρ = s(r) dr — LOCKED concept
- Full interferometer forward equation: NOT YET IN CORPUS

---

## FORBIDDEN CHECKS (from forbidden_formulas.md)

These patterns are BANNED:

| Pattern | Status |
|---------|--------|
| Xi = (rs/r)^2 * exp(-r/r_phi) | BANNED |
| D(r) = 1 - (1+gamma)*rs/(2r) | BANNED |
| rs = GM/c^2 (missing factor 2) | BANNED |
| D = 1/(1+2*Xi) | BANNED |
| Using 90/110 as regime boundaries | BANNED |

---

## FINAL MANDATORY GATE

```
POSTERIOR_RF_TEST:                         INVALID_FOR_SSZ
RINGDOWN_TEST:                             PARTIAL_EXPLORATORY_OR_BLOCKED_UNTIL_EPSILON_220_LOCKED
REAL_STRAIN_TEST:                          BLOCKED_UNTIL_HSSZ_FORWARD_MODEL_AND_CALIBRATION_SAFE_ADAPTER_EXIST
READY_FOR_REAL_LIGO_NUMERICAL_CLAIM:       NO
SSZ_SUPPORT_CLAIM_MADE:                    NO
SSZ_FALSIFICATION_CLAIM_MADE:             NO
XI_STRONG_FORM_IN_SSZ_CORE:               MISMATCH_DECAY_NOT_CANONICAL_G2
REGIME_BOUNDARIES_IN_SSZ_CORE:            MISMATCH_LOWER_1.0_NOT_1.8
PIPELINE_STATUS:                           PASS_EXPLORATORY_STRAIN_PIPELINE_RAN
```

---

## WHAT NEEDS AUTHOR DECISION

1. **Xi_strong form:** Is decay form `1-exp(-phi*rs/r)` acceptable for the LIGO test suite,
   or must it be replaced with canonical g2 `1-exp(-phi*r/rs)`?
   (Both give same D_min at r=rs, but differ at other radii)

2. **epsilon_220:** Which source is authoritative?
   - qnm_spectrum.md: 39% (1/D(r*))
   - V51 Ch.30: ~3%
   - D_min^2: ~31%

3. **h_SSZ(f):** Is there a corpus derivation somewhere not yet found,
   or is the full GW waveform explicitly deferred to future work?

---
© 2026 SSZ-LIGO Test Suite | Source-Truth-Locked Report
