# Formula Branch Lock
Status: LOCKED_DOCUMENTATION
Date: 2026-05-18

---

## CRITICAL: Xi_strong Branch Resolution

### Source of Truth: formula_compendium.md §B.1

The compendium explicitly lists **two** Xi_strong forms with different roles:

```
Inner exponential / decay form (OPERATIVE g2 branch in segcalc, r/rs < 1.8):
  Xi_strong(r) = 1 - exp(-phi * r_s / r)

Local saturation form (metric-pure / paper-local comparison):
  Xi_sat(r)    = min(1 - exp(-phi * r_s / r), Xi_max)
```

### Branch Classification

| Branch | Formula | Operative Context | Status |
|--------|---------|-------------------|--------|
| g2_decay (OPERATIVE) | 1 - exp(-phi * rs/r) | segcalc, r/rs < 1.8 | LOCKED |
| saturation | min(1-exp(-phi*r/rs), Xi_max) | metric-pure, local | PARTIAL |
| deprecated | (rs/r)^2 * exp(-r/r_phi) | old, pre-corpus | FORBIDDEN |

### DEFAULT_XI_STRONG_BRANCH

```
DEFAULT_XI_STRONG_BRANCH = g2_decay
STATUS = LOCKED (formula_compendium.md §B.1, "operative g2 branch")
```

**TERMINOLOGY NOTE (2026-05-18, Audit DERIVED_FORMULAS_CODE_CONSISTENCY_AUDIT.md):**
"g2_decay" here = `1 - exp(-phi*rs/r)` (decay-asymptotic, segcalc operative).
XI_STRONG_BRANCH_LOCK.md calls `1 - exp(-phi*r/rs)` CANONICAL_OPERATIONAL.
Both docs agree: deprecated `(rs/r)^2*exp(...)` = FORBIDDEN.
ssz_core.py follows XI_STRONG_BRANCH_LOCK.md (saturation = canonical default).
LIGO inspiral band (r/rs >> 10): both reduce to Xi_weak = rs/(2r) — numerically irrelevant.

### Behavior Comparison

| Form | r→0 | r=rs | r→∞ | Monotone |
|------|-----|------|-----|----------|
| decay | Xi→Xi_max | 0.802 | 0 | decreases |
| saturation | 0 | 0.802 | Xi_max | increases |

Both agree at r = rs: Xi(rs) = 1 - exp(-phi) = 0.80171. **This is the only point of agreement.**

For the LIGO inspiral band (r >> rs, weak field):
- Both forms converge to Xi_weak = rs/(2r) in the far field
- In the near-horizon regime (r/rs < 1.8): **decay form is operative per corpus**

### Implication for LIGO Forward Model

In the LIGO band (f ~ 20–800 Hz), r_orbit >> rs for typical binary parameters.
The orbit is in the **weak-field regime** (r/rs >> 10) throughout most of the chirp.
In this regime both forms reduce to Xi_weak = rs/(2r) anyway.
**The branch choice does not affect the LIGO inspiral band significantly.**

Near merger (r/rs ~ 3–10): decay form operative per corpus.

---

## Regime Boundaries: LOCKED

From formula_compendium.md §B.2:

| Regime | r/rs | Xi branch |
|--------|------|-----------|
| very_close | < 1.8 | g2_decay (operative) |
| blended | 1.8–2.2 | Hermite C² |
| photon_sphere | 2.2–3.0 | g1 = Xi_weak |
| strong | 3.0–10.0 | g1 = Xi_weak |
| weak | > 10.0 | Xi_weak |

```
BLEND_START = 1.8   (r/rs)  STATUS: LOCKED
BLEND_END   = 2.2   (r/rs)  STATUS: LOCKED
```

Note: the corpus uses Xi_weak (g1 formula) from r/rs = 2.2 onward.
In the LIGO band (r/rs >> 10), only Xi_weak is operative.

---

## GW Source-Side Bridge: LOCKED

From ssz_inspiral.py (sourced from SSZ Book Ch.31-32):

```
P_GW_SSZ = P_GW_GR * D(r)^2 / s(r)^2
rdot_SSZ = rdot_GR * D(r)^2 / s(r)^4
```

Status: LOCKED from corpus reference in ssz_inspiral.py.

---

## D-Intersection (r* values): LOCKED

From formula_compendium.md §B.7:

```
For Xi_decay (r*/rs = 1.595):  D_SSZ = D_GR = 0.6107
For Xi_sat   (r*/rs = 1.387):  D_SSZ = D_GR = 0.5280
```

The 39% QNM shift cited qnm_spectrum.md uses the photon sphere at r/rs ~ 1.5.
This is deep inside the strong-field region and is **not the LIGO strain observable**.

---

## Xi_strong Update Required in ssz_core.py

```
CURRENT (previous session): xi_strong() -> saturation form
CORRECT (per corpus):       xi_strong() -> decay form (g2 operative branch)
```

This must be corrected. However, the LIGO band is not affected (weak-field throughout).
The correction matters for r/rs < 1.8 regime calculations only.
