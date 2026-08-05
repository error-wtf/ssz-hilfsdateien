# deltaPsi_SSZ(f) — Derivation Document

**FORMULA_STATUS:** DERIVED_V0_PROXY
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `ssz-ligo-tests/src/ssz_ligo_tests/derived_phase.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 2
**Cross-ref:** `ssz-ligo-tests/docs/DELTA_PSI_DERIVATION.md`

---

## Source Equations

| Equation | Source |
|----------|--------|
| `rdot_SSZ = rdot_GR * D(r)^2 / s(r)^4` | SSZ Book Ch.31, ssz_inspiral.py |
| `P_GW_SSZ = P_GW_GR * D(r)^2 / s(r)^2` | SSZ Book Ch.31, formula_compendium.md §C.1 |
| `D(r) = 1/(1+Xi(r))`, `s(r) = 1+Xi(r)` | SSZ metric core, formula_compendium.md §A |
| `Xi_weak = r_s/(2r)` | LOCKED — formula_compendium.md §A.2 |
| `Xi_strong = 1 - exp(-phi*r_s/r)` (g2_decay) | LOCKED — FORMULA_BRANCH_LOCK.md |
| `r(f) = (GM/(pi*f)^2)^(1/3)` | Newtonian Kepler proxy |
| `rdot_GR = -64G^3 M^2 mu / (5 c^5 r^3)` | GR Peters formula (Peters 1964) |

---

## Derivation Steps

### Step 1 — Orbital Phase Accumulation Rate (GR)

```
dphi/dr|_GR = Omega(r) / |rdot_GR(r)|
```

where `Omega(r) = sqrt(GM/r^3)` is the Newtonian angular velocity.

### Step 2 — SSZ Radial Decay Rate

```
rdot_SSZ(r) = rdot_GR(r) * D(r)^2 / s(r)^4 = rdot_GR / s(r)^6
```

(since D=1/s: D^2/s^4 = s^{-2}/s^4 = s^{-6})

### Step 3 — Phase Accumulation Ratio

```
dphi/dr|_SSZ = dphi/dr|_GR * s(r)^6 = dphi/dr|_GR * (1+Xi(r))^6
```

### Step 4 — Phase Difference

```
d(deltaPsi)/dr = dphi/dr|_GR * [(1+Xi(r))^6 - 1]
```

### Step 5 — Frequency-Domain Formula

```
deltaPsi_V0(f) = [Omega(r(f)) / |rdot_GR(r(f))|] * [(1+Xi(r(f)))^6 - 1] * |dr/df|
r(f) = (GM/(pi*f)^2)^(1/3)
```

---

## Dimensional Analysis

`[rad/m] * [1] * [m·s] * [1/s]` → **[rad]** ✓

---

## Weak-Field Limit (LIGO band)

For r/rs >> 1: `(1+Xi)^6 - 1 ~ 6*Xi = 3*rs/r` → correction ~ rs/r, very small.
At 20 Hz (GW240925): r/rs ~ 100–1000 → deltaPsi ~ small. **Consistent with pipeline.**

---

## Status

```
FORMULA_STATUS:         DERIVED_V0_PROXY
FITTED_PARAMETERS:      NONE
LIGO_DATA_USED:         NO
READY_FOR_REAL_CLAIM:   NO
BLOCKER:                SSZ Book Ch.31 RSG phase integral not final
```

## Assumptions

- Leading-order Newtonian orbit, no spin, 0PN Peters rdot_GR
- No fitted parameters, no LIGO data in derivation
- Blend handled by Hermite-C² in Xi(r)

## To Reach LOCKED_FINAL

1. Author locks exact RSG phase integral from Ch.31
2. PN corrections to rdot_GR and r(f)
3. Xi_strong branch decision for ringdown
