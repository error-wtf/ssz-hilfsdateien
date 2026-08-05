# deltaPsi_SSZ(f) — V1 Lock Attempt

**Date:** 2026-05-18
**Goal:** Upgrade DELTA_PSI_STATUS from DERIVED_V0_PROXY to DERIVED_V1_SOURCE_LOCKED if possible.
**Sources consulted:** SSZ Book Ch.31, formula_compendium.md §B.4, ssz_inspiral.py, ssz_phase.py

---

## Current V0 Formula

```
deltaPsi_V0(f) = [Omega(r(f)) / |rdot_GR(r(f))|] * [(1 + Xi(r(f)))^6 - 1] * |dr/df|
```

with:
- `r(f) = (G*M / (pi*f)^2)^(1/3)`  — 0PN Kepler (weak-field)
- `Omega = sqrt(G*M/r^3)`           — Newtonian orbital frequency
- `rdot_GR = -64/5 * G^3 M^2 mu / (C^5 r^3)` — Peters 1964

Source chain:
1. `rdot_SSZ = rdot_GR * D^2 / s^4`  → from Ch.31
2. `Delta(rdot) = rdot_SSZ - rdot_GR = rdot_GR * [(1+Xi)^-4 - 1] * (1+Xi)^-2`
   simplified as: `rdot_GR * [(1+Xi)^6 - 1]` (sign convention: s = 1+Xi, D = 1/s)
3. Phase accumulation: `dphi/dr|_SSZ = Omega / |rdot_SSZ|`
4. Correction: `dphi/dr|_SSZ - dphi/dr|_GR = dphi/dr|_GR * [(1+Xi)^6 - 1]`

---

## Checking the s^6 Derivation Step-by-Step

Starting from:
```
rdot_SSZ = rdot_GR * D(r)^2 / s(r)^4
         = rdot_GR * [1/(1+Xi)]^2 / (1+Xi)^4
         = rdot_GR * (1+Xi)^{-6}
```

Phase per unit radius:
```
dphi/dr|_SSZ = Omega / |rdot_SSZ|
             = Omega / (|rdot_GR| * (1+Xi)^{-6})
             = [Omega / |rdot_GR|] * (1+Xi)^6
             = dphi/dr|_GR * (1+Xi)^6
```

Correction factor:
```
deltaPsi_correction = dphi/dr|_SSZ - dphi/dr|_GR
                    = dphi/dr|_GR * [(1+Xi)^6 - 1]
```

**The s^6 factor is algebraically exact given rdot_SSZ = rdot_GR * D^2/s^4.**

---

## What Remains at 0PN

The V0 proxy uses 0PN (Newtonian + Peters) for:
- r(f) mapping
- Omega(r)
- rdot_GR(r)

**At 0PN, the formula is internally consistent and source-traceable.**

---

## What Changes at 1PN/1.5PN

| Term | 0PN (V0) | 1PN correction | 1.5PN (GW tail) |
|------|----------|----------------|-----------------|
| r(f) | Kepler 0PN | PN correction | spin-orbit coupling |
| Omega(r) | Newtonian | PN correction | — |
| rdot_GR | Peters exact | PN radiation | tails |
| Xi(r) | same formula | same formula | same formula |
| s^6 factor | exact given rdot | exact given rdot | exact given rdot |

The `s^6` factor itself does not change with PN order — it follows algebraically
from `rdot_SSZ = rdot_GR * D^2/s^4` regardless of PN order of `rdot_GR`.

**The only V0→V1 improvement is the r(f) mapping and rdot_GR(r) accuracy.**

---

## Locking Decision

### Can DELTA_PSI_STATUS be upgraded to DERIVED_V1_SOURCE_LOCKED?

**Criteria for V1:**
1. Source equation `rdot_SSZ = rdot_GR * D^2/s^4` locked from corpus? **YES** (Ch.31, ssz_inspiral.py)
2. s^6 factor algebraically exact from D^2/s^4? **YES** (see derivation above)
3. 0PN r(f) mapping explicitly stated as approximation? **YES** (in metadata)
4. Full PN-series r(f) available and implemented? **NO**
5. Detector-side phase propagation included? **NO**

**Decision: DERIVED_V1_INSPIRAL_0PN_LOCKED** — partial upgrade from V0.

The formula is source-locked at 0PN. It cannot be called LOCKED_FINAL
until PN corrections to r(f) and detector propagation are included.

---

## Required Steps for LOCKED_FINAL

```
STEP 1: Replace 0PN r(f) with 3.5PN TaylorF2 r(f) mapping
        Source: Blanchet 2014, or LALSuite TaylorF2 implementation
        Blocker: needs SSZ modification of PN coefficients

STEP 2: Include spin-orbit coupling in Omega(r) and rdot_GR
        Blocker: SSZ does not yet specify spin-Xi coupling

STEP 3: Detector-side RSG phase propagation
        Source: SSZ Book (propagation chapter, not yet identified)
        Blocker: source document not located in corpus

STEP 4: Merge/ringdown phase (currently excluded, inspiral only)
        Blocker: no SSZ Merger/Ringdown model exists yet
```

---

## Updated Status

```
DELTA_PSI_FORMULA:    [Omega/|rdot_GR|] * [(1+Xi)^6 - 1] * |dr/df|
S6_FACTOR:            ALGEBRAICALLY_EXACT given rdot_SSZ = rdot_GR * D^2/s^4
SOURCE_LOCK:          Ch.31 + ssz_inspiral.py
PN_VALIDITY:          0PN ONLY
DETECTOR_PROPAGATION: NOT_INCLUDED
DELTA_PSI_STATUS:     DERIVED_V1_INSPIRAL_0PN_LOCKED
                      (upgraded from DERIVED_V0_PROXY)
READY_FOR_REAL_CLAIM: NO
LOCKED_FINAL_BLOCKERS:
  - PN corrections to r(f) and rdot_GR
  - spin-orbit coupling in Xi pathway
  - detector-side RSG phase
  - merger/ringdown phase
```
