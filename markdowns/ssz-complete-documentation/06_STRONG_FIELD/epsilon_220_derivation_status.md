# epsilon_220 — Derivation Status

**FORMULA_STATUS:** BLOCKED_BRANCH_CONFLICT
**READY_FOR_REAL_CLAIM:** NO
**Implementation:** `ssz-ligo-tests/src/ssz_ligo_tests/epsilon_220_registry.py`
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES — Phase 5
**Cross-ref:** `ssz-ligo-tests/docs/EPSILON_220_DERIVATION_STATUS.md`

---

## Definition

`epsilon_220` parametrizes the SSZ modification to the (2,2,0) ringdown QNM:

```
f_220_SSZ = f_220_GR * (1 + epsilon_220_freq)
A_220_SSZ = A_220_GR * (1 + epsilon_220_amp)
tau_220_SSZ = tau_220_GR * (1 + epsilon_220_tau)
```

Three corpus values exist — they measure **different physical quantities**.

---

## Branch Classification

| Branch | Value | Source | Observable | LIGO-compatible? | Status |
|--------|-------|--------|-----------|-----------------|--------|
| v51_ch30 | ~3% | SSZ Book V51 Ch.30 | QNM freq shift (exploratory) | NO | PARTIAL_EXPLORATORY |
| dmin_squared | ~31% | formula_compendium §B.7 | Amplitude at r=r_s | NO (amplitude, not freq) | SUPERSEDED/DIFFERENT_REGIME |
| photon_sphere | ~39% | qnm_spectrum.md, r*=1.387 rs | Source-frame QNM freq ratio | NO (wrong observable) | DISCARDED_FOR_LIGO_STRAIN |

---

## Key Clarification: Why 3 Values ≠ 3 Contradictions

All three values are physically plausible within their own definitions.
The conflict is in their **labeling** — all called `epsilon_220` but measuring different things:

- 3%: frequency shift from SSZ QNM perturbation (exploratory)
- 31%: amplitude suppression factor at r_s (different observable type)
- 39%: source-frame QNM frequency ratio at photon sphere — **NOT the LIGO strain observable**

The 39% requires conversion via Strong→Weak RSG propagation before it could
enter the LIGO strain. That derivation does not exist yet.

---

## Why Pipeline Sees delta_lnL ~ 0

- epsilon_220 BLOCKED → no ringdown correction applied
- inspiral-only V0 corrections in weak field → tiny effect (r/rs ~ 100–1000)
- delta_lnL ~ 0 is **not a falsification** of any epsilon_220 branch
- it shows only: inspiral V0 proxy in weak field is indistinguishable from GR

---

## Final Status

```
epsilon_220_for_real_ligo_claim = None
FORMULA_STATUS:                   BLOCKED_BRANCH_CONFLICT
CANONICAL_VALUE:                  NONE — Author decision required
CATEGORY_ERROR_WARNING:           39% is source-frame QNM freq ratio,
                                  NOT the LIGO strain observable
```

## To Unblock

1. Author defines canonical `epsilon_220` observable (freq / amplitude / damping)
2. Full QNM derivation from SSZ metric boundary conditions
3. Strong→Weak RSG propagation factor for ringdown signal
4. Re-label all three corpus values with correct observable names
5. Pre-register selected branch before any LIGO comparison
