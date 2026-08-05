# h_SSZ(f) V0 — Derivation Document

**FORMULA_STATUS:** DERIVED_V0_PROXY
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `ssz-ligo-tests/src/ssz_ligo_tests/derived_waveform.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 4
**Cross-ref:** `ssz-ligo-tests/docs/H_SSZ_V0_DERIVATION.md`

---

## Formula

```
h_SSZ_V0(f) = h_GR_control(f) * [1 + deltaA_V0(f)] * exp(i * deltaPsi_V0(f))
```

where:
- `deltaA_V0(f) = D(r(f))^2 - 1 ∈ (-1, 0]`  → amplitude suppression
- `deltaPsi_V0(f) = dphi/dr|_GR * [(1+Xi)^6 - 1] * |dr/df|`  → phase increase
- `r(f) = (GM/(pi*f)^2)^(1/3)`  → Newtonian Kepler proxy
- `h_GR_control` = analytic TaylorF2 0PN template (NOT a posterior waveform)

---

## Properties

| Property | Result |
|----------|--------|
| Amplitude | `|h_SSZ| = |h_GR| * D^2 ≤ |h_GR|` — suppressed |
| Phase | `arg(h_SSZ) = arg(h_GR) + deltaPsi` — increased |
| Weak-field limit | `h_SSZ → h_GR` as r/rs → ∞ ✓ |
| Units | [1/Hz] preserved ✓ |

---

## Pipeline Result (GW240925 H1, 2026-05-18)

| Metric | Value |
|--------|-------|
| delta_lnL (SSZ−GR) | ~6e-6 → INDISTINGUISHABLE |
| MF-SNR GR | 39.92 |
| MF-SNR SSZ | 14.23 (amplitude suppression + mis-matched filter) |

**The MF-SNR drop is not a falsification.** A proper SSZ test requires SSZ templates.

---

## Status

```
FORMULA_STATUS:                 DERIVED_V0_PROXY
FITTED_PARAMETERS:              NONE
LIGO_DATA_USED:                 NO
READY_FOR_REAL_CLAIM:           NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
EPSILON_220_INCLUDED:           NO (BLOCKED_BRANCH_CONFLICT)
GR_CONTROL_TYPE:                ANALYTIC_TaylorF2_0PN
```

## To Reach LOCKED_FINAL

1. Lock deltaPsi (Ch.31 RSG integral)
2. Verify h ∝ sqrt(P) chain
3. Include detector-side propagation
4. Unblock epsilon_220 (author decision)
5. Upgrade GR control to full IMR
6. Build SSZ template bank
