# SSZ Forward Model Clarity Test — Phase 10 Report

**Date:** 2026-05-20
**Phase:** 10 — SSZ_FORWARD_MODEL_CLARITY_TEST
**Status:** COMPLETE
**No LIGO Runs:** YES
**No New Claims:** YES

---

## 1. Executive Summary

**h_SSZ(f) is a DERIVED_V1 inspiral-only scalar phase+amplitude correction applied to a GR template. It is NOT a complete SSZ strain waveform, NOT a full IMR template, and NOT ready for claim-level LIGO comparison.**

### What h_SSZ(f) ACTUALLY is

```
h_SSZ_V0(f) = h_GR_TaylorF2_0PN(f) * (1 + deltaA_V0(f)) * exp(i * deltaPsi_V0(f))

where:
  deltaA_V0(f)  = D(r(f))² − 1                    [amplitude suppression, D≤1]
  deltaPsi_V0(f) = [Ω/|rdot_GR|] * [(1+Ξ)⁶−1] * |dr/df|  [phase accumulation]
  r(f)          = (GM/(πf)²)^(1/3)                 [Newtonian Kepler proxy]
```

### What h_SSZ(f) is NOT

| Missing Component | Status |
|-------------------|--------|
| Full IMR (inspiral-merger-ringdown) template | NOT IMPLEMENTED |
| Ch.31 Hamilton-Jacobi S_r(r) phase integral | NOT IMPLEMENTED (Kepler-Approx used) |
| Merger phase model | NOT IMPLEMENTED |
| Ringdown / epsilon_220 | BLOCKED_CONFLICT |
| Detector antenna projection (F+/Fx) | PLACEHOLDER (hardcoded 0.5) |
| Source-to-detector propagation through SSZ metric | NOT IMPLEMENTED |
| Twist/polarization rotation from spin connection | CONCEPTUAL ONLY |
| Multi-detector coherent analysis (H1/L1/V1) | NOT IMPLEMENTED |
| PN corrections beyond 0PN | NOT IMPLEMENTED |
| Spin effects | NOT IMPLEMENTED |

---

## 2. Forward Model Architecture

### 2.1 Two Implementations Exist

The codebase contains two forward model implementations:

| Implementation | File | Status | Used in Pipeline? |
|---------------|------|--------|-------------------|
| `derived_waveform.py` | `apply_ssz_v0_to_frequency_waveform()` | `DERIVED_V1` (documented, dimensionally verified) | Available but not the main pipeline path |
| `run_strain_pipeline.py` Step D | Inline V0 proxy | `V0_PROXY` (kappa=1.0 locked, exploratory) | YES — this is what the pipeline runs |

**Critical distinction:** The pipeline runs a SIMPLER V0 proxy (`dPsi = kappa * (1-D(xi))` with kappa=1.0 locked), NOT the full `derived_waveform.py` implementation. Both are inspiral-only and 0PN. Neither is LOCKED_FINAL.

### 2.2 deltaPsi_V0(f) — Phase Component

```
Source: rdot_SSZ (Ch.31 Z.18700, AUTHORIZED_CH31)

Derivation chain:
  rdot_SSZ = rdot_GR * D²/s⁴ = rdot_GR / s⁶  [CH31 AUTHORIZED]
  → dphi/dr_SSZ = dphi/dr_GR * s⁶             [algebraic]
  → d(deltaPsi)/dr = dphi/dr_GR * (s⁶−1)      [difference]
  → deltaPsi_V0(f) = ∫ (dphi/dr_GR)(s⁶−1) dr  [integration along inspiral]

Implementation: Python code in derived_phase.py
- Newtonian omega(r) = sqrt(GM/r³)
- 0PN rdot_GR from Peters (1964)
- Kepler r(f) = (GM/(πf)²)^(1/3)
- Numerical gradient dr/df

Status: DERIVED_V1
- Source equation AUTHORIZED_CH31 ✓
- Derivation chain documented ✓
- Dimensional analysis verified ✓
- Zero fitted parameters ✓
- HJ integral NOT implemented ✗
- 0PN only, no spin ✗
```

### 2.3 deltaA_V0(f) — Amplitude Component

```
Source: P_GW_SSZ (Ch.31 Z.18696, AUTHORIZED_CH31)

Derivation chain:
  P_GW_SSZ = P_GW_GR * D²/s²          [CH31 AUTHORIZED]
  A ∝ sqrt(P)                         [standard relation]
  → A_SSZ/A_GR = D/s = D²             [since s=1/D]
  → deltaA = D² − 1                   [algebraic, bounded in (−1, 0]]

Status: DERIVED_V1
- Source equation AUTHORIZED_CH31 ✓
- Derivation algebraically exact ✓
- Bounds check: deltaA ∈ (−1, 0] → amplitude suppression only ✓
- Inspiral-only (h∝√(P) valid for inspiral) ✓
- Ringdown amplitude NOT derived ✗
```

### 2.4 h_SSZ_V0(f) — Constructed Waveform

```
Construction:
  h_SSZ_V0(f) = h_GR_control(f) * [1 + deltaA_V0(f)] * exp(i * deltaPsi_V0(f))

  h_GR_control = analytic TaylorF2 0PN template (GR_CONTROL_TEMPLATE_LIMITED)

Status: DERIVED_V1 (constructed from DERIVED_V1 components)
- Weak-field limit: h_SSZ → h_GR ✓
- Units preserved ✓
- Finite values verified ✓
- Pipeline result: delta_lnL ~ 6e-6 → INDISTINGUISHABLE (inspiral weak-field)
  [This is expected — r/rs >> 1 in LIGO band, SSZ corrections are tiny]
```

---

## 3. What Is MISSING for Claim-Level LIGO Test

### 3.1 Phase: Hamilton-Jacobi Integral Not Implemented

The authoritative GW phase method from Ch.31 Z.18677:

```
S_r(r) = ∫ s(r)/D(r) * sqrt[E²/(D²c⁴) − L²/(r²s²) − ε/s²] dr
```

This is the general-orbit phase integral. The V0 Kepler-Approx is a circular, Newtonian special case. The HJ integral would provide:
- Correct PN expansion
- Eccentric orbit handling
- Proper strong-field behavior near ISCO
- Connection to RSG phase accounting

**Without this, deltaPsi remains DERIVED_V1, not LOCKED_FINAL.**

### 3.2 Merger: No SSZ Merger Model

The 0PN TaylorF2 template has NO merger phase. An SSZ-specific merger model would require:
- SSZ metric evolution through the last orbits
- Non-perturbative dynamics near r*
- Transition from inspiral to merger regime
- This does not exist in the codebase anywhere.

### 3.3 Ringdown: BLOCKED_CONFLICT

epsilon_220 has three corpus values (3%, 31%, 39%) measuring different observables:
- 3%: exploratory QNM shift (Ch.30, below detector precision)
- 31%: D_min² amplitude factor (different observable type)
- 39%: source-frame QNM frequency ratio = 1/D(r*) (NOT LIGO strain)

`ssz_ringdown.py` EXPLICITLY REFUSES TO RUN:
```python
check_ringdown_usable() → (False, "CONFLICTING_SSZ_SOURCES")
```

The forward_model.py class requires explicit `lock_epsilon_220()` before any ringdown call. It is never called in the current pipeline.

### 3.4 Detector Projection: Not Applied

`detector_response.py` exists but:
- `antenna_pattern_h1()` returns hardcoded (0.5, 0.5) — PLACEHOLDER
- `antenna_pattern_l1()` returns hardcoded (0.5, 0.5) — PLACEHOLDER
- NOT used in `run_strain_pipeline.py`
- The pipeline treats H1 as if optimally aligned (implicit F+=1, Fx=0)

For multi-detector analysis, proper GW sky position and polarization angle are needed.

### 3.5 Propagation: Source-Only, No Detector-Side

Current model applies SSZ corrections at the source orbital radius r(f) only. The GW signal propagates through SSZ-modified spacetime:
- The metric D(r), s(r) varies along the propagation path
- No path integral from source to detector
- This is a NON-TRIVIAL derivation gap

### 3.6 Twist/Polarization: Conceptual Only

`ssz_twist.py` exists but:
- `twist_angle_v0()` uses theta ~ Xi(r_char) * phi_geom with phi_geom=1.0
- Status: `DERIVED_V0_CONCEPTUAL`
- Derivation from SSZ metric spin connection NOT done
- Christoffel → spin connection → holonomy → SO(2) rotation path documented but not implemented
- `twist_sensitivity_scan()` exists but runs on synthetic data only

### 3.7 GR Control: 0PN Only

The TaylorF2 0PN template is:
- Labeled `GR_CONTROL_TEMPLATE_LIMITED` in pipeline
- No spin corrections
- No higher modes
- No merger
- Compared against: SSZ V0-proxy corrections on same 0PN template
- **Both sides of the comparison are limited.** A fair comparison would require a stronger GR baseline.

---

## 4. Method Assignment Audit

### What IS Correctly Assigned

| Observable | Method | Formula | Status |
|-----------|--------|---------|--------|
| GW Power (source) | QUADRUPOLE_POWER | P_GW_SSZ = P_GW_GR * D²/s² | AUTHORIZED_CH31 ✓ |
| Inspiral rate | ENERGY_BALANCE | rdot_SSZ = rdot_GR * D²/s⁴ | AUTHORIZED_CH31 ✓ |
| Amplitude suppression | POWER_SCALING | deltaA = D²−1 | DERIVED_V1 (correctly derived) |
| Phase accumulation | KEPLER_APPROX | deltaPsi_V0(f) | DERIVED_V1 (HJ not implemented) |

### Method Assignment Gaps

| Observable | Current | Should Be | Gap |
|-----------|---------|-----------|-----|
| General GW phase | Kepler-Approx (special case) | Hamilton-Jacobi S_r(r) (Ch.31 Z.18677) | HJ integral not implemented |
| Ringdown frequency | BLOCKED | epsilon_220 canonical value | Author decision needed |
| Ringdown amplitude | NOT IMPLEMENTED | QNM derivation from SSZ metric | No SSZ QNM model |
| Detector strain | Scalar correction to H1 | F+*h+(SSZ) + Fx*hx(SSZ) | Antenna patterns not applied |
| Propagation | Source-only | Path integral through SSZ metric | Not modelled |

---

## 5. What CAN and CANNOT Be Done

### CAN Be Done (Methodological Tests)

| Test | What It Means |
|------|---------------|
| H1 inspiral sanity check | Apply SSZ correction, compute delta_lnL, verify < 1 → INDISTINGUISHABLE (as expected in weak field) |
| Sensitivity analysis | How large would SSZ correction need to be to produce delta_lnL >= 8? |
| Parameter space exploration | What mass/distance/regime would make SSZ detectable? |
| Code validation | Verify weak-field limit SSZ→GR (r→∞) |
| Numerical stability | Verify finite values, no NaN/Inf, consistent derivatives |

### CANNOT Be Done (Claim-Level Tests)

| Test | Blocker |
|------|---------|
| "SSZ preferred over GR at N sigma" | deltaPsi not LOCKED_FINAL (HJ integral missing) |
| "SSZ ringdown detected" | epsilon_220 BLOCKED_CONFLICT |
| "SSZ template matches LIGO data better than GR" | No full IMR SSZ template exists |
| "H1/L1/V1 coherent SSZ detection" | No multi-detector model |
| "SSZ polarization twist observed" | Twist not derived from metric |
| Any claim involving merger | No SSZ merger model |

---

## 6. Gap Severity Assessment

| Gap | Severity | Priority | Effort | Action |
|-----|----------|----------|--------|--------|
| HJ phase integral (deltaPsi) | HIGH | 1 | Medium | Implement Ch.31 Z.18677 S_r(r) |
| epsilon_220 canonical value | BLOCKER | 1 | Low (decision) | Author chooses which observable |
| Merger model | HIGH | 2 | High | Derive from SSZ metric dynamics |
| Detector projection | MEDIUM | 2 | Low | Implement sky-position F+/Fx |
| GR control upgrade (1.5PN+) | MEDIUM | 2 | Medium | Extend TaylorF2 |
| Ringdown QNM derivation | HIGH | 3 | High | Derive from SSZ boundary conditions |
| Propagation path integral | LOW | 4 | High | Non-trivial derivation |
| Twist from spin connection | LOW | 4 | High | Christoffel→spin connection→holonomy |
| Multi-detector coherence | MEDIUM | 3 | Medium | Network analysis framework |
| PN corrections to rdot/omega | MEDIUM | 3 | Medium | 1PN, 1.5PN, 2PN terms |

---

## 7. Verdict

| Question | Answer |
|----------|--------|
| Is h_SSZ(f) a complete strain-level forward model? | **NO.** It is an inspiral-only scalar correction to a 0PN GR template. |
| Is it a derived prototype? | **YES.** DERIVED_V1 — sourced from CH31-authorized equations, documented, dimensionally verified. |
| Does it include merger/ringdown? | **NO.** 0PN template has no merger phase. epsilon_220 is BLOCKED_CONFLICT. |
| Does it include detector projection? | **NO.** H1 implicitly assumed as optimally aligned. Antenna patterns are placeholders. |
| Does it include propagation/twist? | **NO.** Twist is conceptual (DERIVED_V0_CONCEPTUAL). Propagation not modelled. |
| Can it run as methodological test against H1? | **YES.** As pipeline sanity: apply correction, compute delta_lnL, verify INDISTINGUISHABLE in weak field. |
| Can it run claim-level against LIGO? | **NO.** Marked `READY_FOR_REAL_CLAIM: NO`. Missing: HJ integral, epsilon_220, merger, ringdown, detector projection. |
| Can it run H1/L1/V1? | **NO.** Single-detector only. Antenna patterns not applied. |

---

## 8. Next Steps (Recommended Order)

1. **Implement Ch.31 Hamilton-Jacobi S_r(r) integral** → deltaPsi moves toward LOCKED_FINAL
2. **Author resolves epsilon_220** → unblocks ringdown
3. **Upgrade GR control to 1.5PN+ TaylorF2** → fair comparison baseline
4. **Implement detector antenna patterns** → enable H1/L1/V1
5. **Derive QNM amplitude from SSZ metric** → deltaA ringdown component

Phase 10 complete. No LIGO runs. No claims.

---

## 9. Outputs

- `data_manifest/ssz_forward_model_clarity_matrix.csv` — 18 components × 6 questions
- `reports/progress/SSZ_FORWARD_MODEL_CLARITY_TEST.md` — this report
- `logs/ssz_forward_model_clarity_test.log` — execution log
