# deltaA_SSZ(f) — Derivation Document

**FORMULA_STATUS:** DERIVED_V0_PROXY
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `src/ssz_ligo_tests/derived_amplitude.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 3

---

## Source Equations

| Equation | Source |
|----------|--------|
| `P_GW_SSZ = P_GW_GR * D(r)^2 / s(r)^2` | SSZ Book Ch.31, formula_compendium.md §B.4 |
| `D(r) = 1/(1+Xi(r))` | SSZ metric, formula_compendium.md §A |
| `s(r) = 1/(D(r))` | SSZ metric: `s = 1+Xi = 1/D` |
| `Xi_weak = r_s/(2r)` | LOCKED |
| `r(f) = (GM/(pi*f)^2)^(1/3)` | Newtonian proxy |

---

## Derivation Steps

### Step 1 — GW Power Ratio

The locked SSZ source-side bridge gives:

```
P_GW_SSZ(r) / P_GW_GR(r) = D(r)^2 / s(r)^2
```

### Step 2 — Amplitude Ratio from Power

Gravitational wave strain amplitude scales as square root of radiated power
(for a stationary source at fixed distance, h ∝ sqrt(P_GW)):

```
A_SSZ / A_GR = sqrt(P_SSZ / P_GR) = sqrt(D^2 / s^2) = D(r) / s(r)
```

### Step 3 — Simplify Using s = 1/D

Since `s(r) = 1/D(r)`:

```
D(r) / s(r) = D(r) * D(r) = D(r)^2
```

Therefore:

```
A_SSZ / A_GR = D(r)^2
deltaA_SSZ(r) = A_SSZ/A_GR - 1 = D(r)^2 - 1
```

### Step 4 — Frequency Mapping

Map `r → f` via Newtonian Kepler:

```
r(f) = (GM/(pi*f)^2)^(1/3)
deltaA_SSZ(f) = D(r(f))^2 - 1
```

---

## Dimensional Analysis

| Quantity | Dimensions |
|----------|-----------|
| `D(r)` | dimensionless ∈ (0,1] |
| `D(r)^2` | dimensionless ∈ (0,1] |
| `deltaA = D^2 - 1` | dimensionless ∈ (-1, 0] ✓ |

**Check:** deltaA is dimensionless ✓
**Sign:** D ≤ 1 always → D^2 ≤ 1 → deltaA ≤ 0 (amplitude suppression) ✓

---

## Physical Bounds

```
D_min = 0.555  (at r = r_s)      →  deltaA_min = 0.555^2 - 1 = -0.692
D → 1  (weak field, r >> r_s)    →  deltaA → 0
```

Range: `deltaA ∈ [-0.692, 0)` in physical parameter space.

In LIGO band (weak field, r/rs >> 1): `deltaA ~ -Xi^2 ~ -(rs/2r)^2 << 1`

---

## Note on h ∝ sqrt(P) Assumption

The derivation uses `h ∝ sqrt(P_GW)`. This holds for the inspiral phase
where the waveform amplitude is set by the source luminosity and distance.
For ringdown (QNM), a separate derivation using QNM amplitude scaling applies.
This V0 formula is therefore valid **for inspiral only** and must not be
applied to the ringdown without further derivation.

---

## Assumptions

1. `h ∝ sqrt(P_GW)` — valid for inspiral phase only
2. Distance to source unchanged (no SSZ metric modification at detector)
3. Leading-order Newtonian orbit for `r(f)`
4. `s = 1/D` exactly (from SSZ metric definition)
5. **No fitted parameters**
6. **No LIGO data used**

---

## Status Classification

```
FORMULA_STATUS:         DERIVED_V0_PROXY
FITTED_PARAMETERS:      NONE
LIGO_DATA_USED:         NO
READY_FOR_REAL_CLAIM:   NO
BLOCKER:                h ∝ sqrt(P) only valid for inspiral;
                        ringdown amplitude requires separate QNM derivation;
                        detector-side amplitude (propagation in SSZ metric) not included
```

---

## What Must Change to Reach LOCKED_FINAL

1. Verify that P_GW_SSZ formula (`D^2/s^2`) is the full source-side correction
   (current source: Ch.31 — verify against full derivation)
2. Include detector-side propagation factor if SSZ metric modifies h at detector
3. Separate ringdown amplitude from inspiral: derive QNM amplitude scaling
4. Verify `h ∝ sqrt(P)` for SSZ waveform specifically (not only GR assumption)
