# deltaA_SSZ(f) — Derivation Document

**FORMULA_STATUS:** DERIVED_V0_PROXY
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `ssz-ligo-tests/src/ssz_ligo_tests/derived_amplitude.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 3
**Cross-ref:** `ssz-ligo-tests/docs/DELTA_A_DERIVATION.md`

---

## Source Equations

| Equation | Source |
|----------|--------|
| `P_GW_SSZ = P_GW_GR * D(r)^2 / s(r)^2` | SSZ Book Ch.31, formula_compendium.md §B.4 |
| `D(r) = 1/(1+Xi(r))`, `s(r) = 1/D(r)` | SSZ metric core |
| `Xi_weak = r_s/(2r)` | LOCKED |

---

## Derivation

```
P_SSZ / P_GR = D^2 / s^2

A_SSZ / A_GR = sqrt(P_SSZ/P_GR) = D/s = D * D = D^2   [since s=1/D]

deltaA_SSZ(r) = D(r)^2 - 1

deltaA_SSZ(f) = D(r(f))^2 - 1,   r(f) = (GM/(pi*f)^2)^(1/3)
```

---

## Physical Bounds

```
D_min = 0.555  (at r = r_s)   → deltaA_min = -0.692
D → 1  (weak field)           → deltaA → 0
deltaA ∈ (-1, 0] always       → amplitude suppression only
```

In LIGO band: `deltaA ~ -(rs/2r)^2 << 1` (very small, weak field).

---

## Status

```
FORMULA_STATUS:         DERIVED_V0_PROXY
FITTED_PARAMETERS:      NONE
LIGO_DATA_USED:         NO
READY_FOR_REAL_CLAIM:   NO
BLOCKER:                h ∝ sqrt(P) only valid for inspiral;
                        ringdown amplitude requires separate QNM derivation;
                        detector-side propagation factor not included
```

## Assumptions

- `h ∝ sqrt(P_GW)` valid for inspiral only
- Source-detector distance fixed (no SSZ propagation modification included)
- No fitted parameters, no LIGO data

## To Reach LOCKED_FINAL

1. Verify full P_GW_SSZ chain against original Ch.31 derivation
2. Include detector-side SSZ metric propagation factor
3. Derive QNM amplitude scaling separately for ringdown
