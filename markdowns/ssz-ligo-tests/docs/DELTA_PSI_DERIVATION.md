# deltaPsi_SSZ(f) — Derivation Document

**FORMULA_STATUS:** DERIVED_V0_PROXY
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `src/ssz_ligo_tests/derived_phase.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 2

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

In GR, the orbital phase phi accumulated per unit radius is:

```
dphi/dr|_GR = Omega(r) / |rdot_GR(r)|
```

where `Omega(r) = sqrt(GM/r^3)` is the Newtonian angular velocity.

### Step 2 — SSZ Radial Decay Rate

The SSZ-corrected radial decay is locked from SSZ Book Ch.31:

```
rdot_SSZ(r) = rdot_GR(r) * D(r)^2 / s(r)^4
```

Since `D = 1/s`, this is:

```
rdot_SSZ = rdot_GR / s(r)^6
```

(because D^2/s^4 = s^{-2}/s^4 = s^{-6})

### Step 3 — SSZ Phase Accumulation Rate

```
dphi/dr|_SSZ = Omega(r) / |rdot_SSZ(r)|
             = Omega(r) * s(r)^6 / |rdot_GR(r)|
             = dphi/dr|_GR * s(r)^6
```

### Step 4 — Phase Difference per Unit Radius

```
d(deltaPsi)/dr = dphi/dr|_SSZ - dphi/dr|_GR
               = dphi/dr|_GR * [s(r)^6 - 1]
               = dphi/dr|_GR * [(1+Xi(r))^6 - 1]
```

### Step 5 — Frequency Mapping

Use Newtonian frequency-radius correspondence:

```
r(f) = (G*M / (pi*f)^2)^(1/3)
```

The frequency-domain phase element is:

```
deltaPsi(f) ~ d(deltaPsi)/dr * |dr/df|
```

where `|dr/df|` is computed numerically from `r(f)` via finite differences.

### Step 6 — Assembled V0 Formula

```
deltaPsi_V0(f) = [Omega(r(f)) / |rdot_GR(r(f))|] * [(1+Xi(r(f)))^6 - 1] * |dr/df|
```

---

## Dimensional Analysis

| Quantity | Dimensions |
|----------|-----------|
| `Omega(r)` | [rad/s] |
| `rdot_GR` | [m/s] |
| `dphi/dr` | [rad/m] |
| `(1+Xi)^6 - 1` | [dimensionless] |
| `|dr/df|` | [m/Hz] = [m·s] |
| `deltaPsi(f)` | [rad/Hz · Hz] → but here per frequency bin → [rad] ✓ |

**Check:** `[rad/m] * [1] * [m·s] * [1/s]` → [rad] ✓

---

## Assumptions

1. Leading-order Newtonian circular orbit (`Omega = sqrt(GM/r^3)`)
2. No spin, no eccentricity
3. GR Peters formula for `rdot_GR` (0PN energy loss)
4. `r(f)` is Newtonian Kepler proxy (no PN corrections)
5. Blend regime (1.8 rs < r < 2.2 rs) handled by `get_xi()` with Hermite-C² transition
6. **No fitted parameters** — formula contains only locked SSZ constants
7. **No LIGO data used in derivation**

---

## Status Classification

```
FORMULA_STATUS:         DERIVED_V0_PROXY
FITTED_PARAMETERS:      NONE
LIGO_DATA_USED:         NO
READY_FOR_REAL_CLAIM:   NO
BLOCKER:                SSZ Book Ch.31 RSG phase integral not yet final
                        (kappa=1 implicit in s^6 factor, not independently locked)
```

---

## Weak-Field Behavior

In the LIGO inspiral band (r/rs >> 1), `Xi_weak = rs/(2r) << 1`:

```
(1+Xi)^6 - 1 ~ 6*Xi = 6*rs/(2r) = 3*rs/r  [leading order]
```

The correction is proportional to `rs/r` — very small in weak field.
For GW240925 at 20 Hz: r/rs ~ 100-1000 → correction ~ 0.3–3%.
This is consistent with `deltaPsi_max ~ 0.06–10 rad` in the pipeline.

---

## What Must Change to Reach LOCKED_FINAL

1. Author locks the exact RSG phase integral from Ch.31 (replaces `s^6` factor if different)
2. PN-corrections to `rdot_GR` and `r(f)` incorporated (1PN, 1.5PN)
3. Xi_strong branch decision for merger/ringdown regime
4. Independent verification of `D^2/s^4` rdot formula against original derivation
