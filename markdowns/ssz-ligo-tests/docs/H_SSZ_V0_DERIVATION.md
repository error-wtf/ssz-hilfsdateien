# h_SSZ(f) V0 — Derivation Document

**FORMULA_STATUS:** DERIVED_V0_PROXY
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `src/ssz_ligo_tests/derived_waveform.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 4

---

## Source Equations

| Equation | Source |
|----------|--------|
| `deltaPsi_SSZ(f)` | DELTA_PSI_DERIVATION.md, derived_phase.py |
| `deltaA_SSZ(f)` | DELTA_A_DERIVATION.md, derived_amplitude.py |
| GW forward model construction | SSZ_LIGO_FORWARD_MODEL_SPEC.md |

---

## Construction

### Step 1 — Start from GR Control Template

```
h_GR_control(f) = analytic TaylorF2 0PN template (or other analytic GR control)
```

This is an **analytic control template only** — not a PE-fitted posterior waveform.
It is independent of any SSZ parameter choice.

**Anti-circularity:** using a posterior-derived waveform here would be circular.
The GR control must be analytic or independently specified.

### Step 2 — Apply Phase Correction

The SSZ phase correction modifies the frequency-domain phase:

```
h_phase_corrected(f) = h_GR_control(f) * exp(i * deltaPsi_SSZ_V0(f))
```

### Step 3 — Apply Amplitude Correction

The SSZ amplitude correction scales the waveform amplitude:

```
h_SSZ(f) = h_phase_corrected(f) * [1 + deltaA_SSZ_V0(f)]
         = h_GR_control(f) * [1 + deltaA_SSZ_V0(f)] * exp(i * deltaPsi_SSZ_V0(f))
```

### Step 4 — Combined Formula

```
h_SSZ_V0(f) = h_GR_control(f) * [1 + deltaA_V0(f)] * exp(i * deltaPsi_V0(f))
```

where:
- `deltaA_V0(f) = D(r(f))^2 - 1 ∈ (-1, 0]`
- `deltaPsi_V0(f) = [dphi/dr|_GR] * [(1+Xi(r))^6 - 1] * |dr/df|`
- `r(f) = (GM/(pi*f)^2)^(1/3)`

---

## Dimensional Analysis

| Quantity | Dimensions |
|----------|-----------|
| `h_GR_control(f)` | [1/Hz] (strain spectral density) |
| `1 + deltaA` | dimensionless ∈ (0, 1] |
| `exp(i*deltaPsi)` | dimensionless, unit modulus |
| `h_SSZ(f)` | [1/Hz] ✓ |

**Check:** Units preserved ✓. Modulus of h_SSZ reduced relative to h_GR (amplitude suppression).

---

## Properties

### Amplitude
```
|h_SSZ(f)| = |h_GR(f)| * [1 + deltaA(f)]
           = |h_GR(f)| * D(r(f))^2
```
Since `D ≤ 1`: `|h_SSZ| ≤ |h_GR|` always. SSZ amplitude is suppressed.

### Phase
```
arg(h_SSZ(f)) = arg(h_GR(f)) + deltaPsi(f)
```
Phase is increased (more phase accumulated in SSZ due to slower radial inspiral).

### Weak-field limit
For `r >> rs`: `Xi → 0`, `D → 1`, `deltaA → 0`, `deltaPsi → 0`
→ `h_SSZ → h_GR` ✓ (GR recovered in weak field)

---

## Pipeline Context

In the exploratory pipeline run on GW240925 H1:

| Quantity | Value | Interpretation |
|----------|-------|---------------|
| delta_lnL (SSZ-GR) | ~6e-6 | INDISTINGUISHABLE |
| MF-SNR GR | 39.92 | GR control template |
| MF-SNR SSZ | 14.23 | Amplitude suppression reduces match |

The low MF-SNR for SSZ reflects that h_SSZ has reduced amplitude
(`|h_SSZ| = D^2 * |h_GR|`, with D^2 ~ 0.3–0.9 in band).
A proper SSZ matched filter would use SSZ templates, not GR templates.
The MF-SNR drop is **not a falsification** — it is a consequence of using a
mis-matched filter.

---

## Assumptions

1. GR control template is analytic and independent of posterior
2. SSZ corrections are applied multiplicatively (linear approximation)
3. Phase and amplitude corrections are independent (valid at leading order)
4. No ringdown correction (epsilon_220 BLOCKED)
5. No spin, no merger, no eccentricity
6. **No fitted parameters anywhere in the chain**
7. **No LIGO data used in constructing deltaPsi or deltaA**

---

## Status Classification

```
FORMULA_STATUS:                 DERIVED_V0_PROXY
FITTED_PARAMETERS:              NONE
LIGO_DATA_USED:                 NO
READY_FOR_REAL_CLAIM:           NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
EPSILON_220_INCLUDED:           NO (BLOCKED_BRANCH_CONFLICT)
MERGER_INCLUDED:                NO
RINGDOWN_INCLUDED:              NO
GR_CONTROL_TYPE:                ANALYTIC_TaylorF2_0PN
```

---

## What Must Change to Reach LOCKED_FINAL

1. `deltaPsi` must be locked (see DELTA_PSI_DERIVATION.md blockers)
2. `deltaA` must verify the `h ∝ sqrt(P)` chain for SSZ specifically
3. Detector-side propagation in SSZ metric must be assessed
4. Ringdown section (epsilon_220) must be unblocked
5. GR control must be upgraded to full IMR (merger + ringdown)
6. SSZ template bank must be built for proper matched filtering
