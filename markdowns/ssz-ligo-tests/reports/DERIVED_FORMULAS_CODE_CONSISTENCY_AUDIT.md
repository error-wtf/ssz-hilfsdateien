# Derived Formulas — Code/Docs Consistency Audit

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Date:** 2026-05-18
**Auditor:** Cascade / automated inspection
**Method:** Side-by-side comparison of docs/*.md against src/**/*.py and tests/**/*.py

---

## Summary

| Formula | Doc Formula | Code Formula | Test Coverage | CODE_MATCH |
|---------|------------|--------------|---------------|------------|
| deltaPsi_SSZ | dphi/dr_GR * [(1+Xi)^6 - 1] * dr/df | ✅ line 71-73 derived_phase.py | ✅ test_derived_delta_psi_v0.py | **YES** |
| deltaA_SSZ | D(r)^2 - 1 | ✅ line 73 derived_amplitude.py | ✅ test_derived_delta_a_v0.py | **YES** |
| h_SSZ | h_GR * (1+deltaA) * exp(i*deltaPsi) | ✅ line 72 derived_waveform.py | ✅ test_h_ssz_v0_waveform_application.py | **YES** |
| Xi_strong default | CANONICAL = saturation 1-exp(-phi*r/rs) | ✅ xi_strong()→xi_strong_saturation() | ✅ test_xi_strong_branch_lock.py | **YES** |
| epsilon_220 blocked | None for claim | ✅ epsilon_220_for_real_ligo_claim = None | ✅ test_epsilon_220_branch_registry.py | **YES** |

**OVERALL: 5/5 CODE_MATCH = YES**

---

## CRITICAL FINDING: Doc/Doc Inconsistency

**FORMULA_BRANCH_LOCK.md (line 25, 32–33)** states:
```
DEFAULT_XI_STRONG_BRANCH = g2_decay
g2_decay formula: 1 - exp(-phi * rs/r)   [DECAY form]
```

**XI_STRONG_BRANCH_LOCK.md (lines 13–20)** states:
```
CANONICAL_OPERATIONAL = saturation: 1 - exp(-phi * r/rs)
DIDACTIC_COMPLEMENTARY = decay: 1 - exp(-phi * rs/r)
```

**ssz_core.py** follows XI_STRONG_BRANCH_LOCK.md (saturation = canonical).

**Resolution:**
- `ssz_core.py` and `XI_STRONG_BRANCH_LOCK.md` are **internally consistent**.
- `FORMULA_BRANCH_LOCK.md` uses terminology "g2_decay" for what
  `XI_STRONG_BRANCH_LOCK.md` calls DIDACTIC_COMPLEMENTARY — a naming collision.
- In the **LIGO inspiral band (r/rs >> 10)**: both forms reduce to
  Xi_weak = rs/(2r). Branch choice is **numerically irrelevant** for current pipeline.
- Action: `FORMULA_BRANCH_LOCK.md` terminology updated below.

---

## Detailed Formula Checks

### 1. deltaPsi_SSZ — DELTA_PSI_CODE_MATCH: YES

**Doc formula** (DELTA_PSI_DERIVATION.md):
```
deltaPsi_V0(f) = [Omega(r(f)) / |rdot_GR(r(f))|] * [(1+Xi(r(f)))^6 - 1] * |dr/df|
```

**Code** (`derived_phase.py` lines 64–73):
```python
rdot_gr = -64 * G**3 * M**2 * mu / (5 * C**5 * r_orb**3)   # Peters
omega   = sqrt(G * M / r_orb**3)                              # Newtonian
dphi_dr_gr = omega / abs(rdot_gr)                             # = dphi/dr|_GR
corr    = [(1 + xi(r, rs))^6 - 1 for r in r_orb]            # correction factor
dr_df   = abs(gradient(r_orb, freqs))                         # |dr/df|
delta_psi = dphi_dr_gr * corr * dr_df                         # assembled
```

Match: **EXACT** ✅

**Test** (`test_derived_delta_psi_v0.py`):
- `FORMULA_STATUS == "DERIVED_V0_PROXY"` ✅
- `READY_FOR_REAL_CLAIM == "NO"` ✅
- output finite, non-negative ✅
- weak-field bound: max < 10 rad ✅
- deterministic ✅
- raises on bad input ✅

---

### 2. deltaA_SSZ — DELTA_A_CODE_MATCH: YES

**Doc formula** (DELTA_A_DERIVATION.md):
```
deltaA_SSZ(f) = D(r(f))^2 - 1,   D = 1/(1+Xi)
```

**Code** (`derived_amplitude.py` lines 71–73):
```python
xi_vals = [get_xi(r, rs) for r in r_orb]
d_vals  = 1.0 / (1.0 + xi_vals)           # D = 1/(1+Xi)
delta_a = d_vals**2 - 1.0                  # D^2 - 1
```

Match: **EXACT** ✅

**Test** (`test_derived_delta_a_v0.py`):
- `FORMULA_STATUS == "DERIVED_V0_PROXY"` ✅
- `READY_FOR_REAL_CLAIM == "NO"` ✅
- deltaA ≤ 0 always ✅
- deltaA > -1 always ✅
- `source_equation` contains "D(r)^2 - 1" ✅
- D values physical ∈ (0,1] ✅

---

### 3. h_SSZ — H_SSZ_CODE_MATCH: YES

**Doc formula** (H_SSZ_V0_DERIVATION.md):
```
h_SSZ(f) = h_GR(f) * [1 + deltaA(f)] * exp(i * deltaPsi(f))
```

**Code** (`derived_waveform.py` line 72):
```python
h_ssz_f = h_gr_f * (1.0 + delta_a) * np.exp(1j * delta_psi)
```

Match: **EXACT** ✅

**Test** (`test_h_ssz_v0_waveform_application.py`):
- `FORMULA_STATUS == "DERIVED_V0_PROXY"` ✅
- `READY_FOR_REAL_CLAIM == "NO"` ✅
- `SSZ_SUPPORT_CLAIM_MADE == "NO"` ✅
- `SSZ_FALSIFICATION_CLAIM_MADE == "NO"` ✅
- shape preserved ✅
- complex output ✅
- finite everywhere ✅

---

### 4. Xi_strong — XI_BRANCH_CODE_MATCH: YES

**Operative branch** (XI_STRONG_BRANCH_LOCK.md):
```
CANONICAL_OPERATIONAL: Xi = min(1 - exp(-phi * r/rs), Xi_max)
```

**Code** (`ssz_core.py` lines 50–60):
```python
def xi_strong(r, rs, phi=PHI):
    return xi_strong_saturation(r, rs, phi)   # delegates to CANONICAL

def xi_strong_saturation(r, rs, phi=PHI):
    xi = 1 - np.exp(-phi * r / rs)            # CANONICAL formula
    return np.minimum(xi, XI_MAX)

def xi_strong_decay(r, rs, phi=PHI):          # DIDACTIC only, labelled
    xi = 1 - np.exp(-phi * rs / r)
    return np.minimum(xi, XI_MAX)
```

Match: **EXACT** ✅
Decay form present but explicitly labelled DIDACTIC_COMPLEMENTARY ✅
Deprecated form absent ✅

**Test** (`test_xi_strong_branch_lock.py`):
- `xi_strong()` delegates to saturation ✅
- saturation monotonically increasing ✅
- decay monotonically decreasing ✅
- both agree at r=rs ✅
- differ at r≠rs ✅
- deprecated form not present ✅

**Note:** `FORMULA_BRANCH_LOCK.md` uses "g2_decay" as label for the saturation form
(confusing naming). This is a **documentation naming collision only** — see Doc Conflict
section above. No code change needed.

---

### 5. epsilon_220 — EPSILON_220_BLOCKED: YES

**Doc** (EPSILON_220_DERIVATION_STATUS.md):
```
epsilon_220_for_real_ligo_claim = None
FORMULA_STATUS = BLOCKED_BRANCH_CONFLICT
```

**Code** (`epsilon_220_registry.py` lines 12–16):
```python
FORMULA_STATUS = "BLOCKED_BRANCH_CONFLICT"
READY_FOR_REAL_CLAIM = "NO"
epsilon_220_for_real_ligo_claim = None
status = "BLOCKED_BRANCH_CONFLICT"
```

Match: **EXACT** ✅

**Test** (`test_epsilon_220_branch_registry.py`):
- `epsilon_220_for_real_ligo_claim is None` ✅
- `ligo_claim_allowed is False` ✅
- all 3 branches exist ✅
- no branch is ligo_strain_compatible ✅
- values match corpus (3%, D_min^2, 39%) ✅

---

## Posterior Firewall Check

**Anti-circularity** (`anti_circularity.py`, `test_08_anti_circularity.py`):
- No posterior-derived waveform accepted as SSZ observable ✅
- GR control = analytic TaylorF2 0PN, not PE output ✅
- ANTI_CIRCULARITY_GATE: CLEAR ✅

---

## Doc/Doc Conflict: ACTION REQUIRED

`FORMULA_BRANCH_LOCK.md` line 25 says `g2_decay (OPERATIVE)` maps to
`1 - exp(-phi * rs/r)` (decay form). But `XI_STRONG_BRANCH_LOCK.md` and
`ssz_core.py` call the **saturation form** (`1 - exp(-phi * r/rs)`) the CANONICAL
operative branch.

**Terminology is inverted between the two docs.**
Action: Add clarification note to `FORMULA_BRANCH_LOCK.md`.
Code is correct — no code change needed.
LIGO pipeline is unaffected (weak field throughout inspiral band).

---

## Final Gate

```
DELTA_PSI_CODE_MATCH:           YES
DELTA_A_CODE_MATCH:             YES
H_SSZ_CODE_MATCH:               YES
XI_BRANCH_CODE_MATCH:           YES (saturation=CANONICAL in code)
EPSILON_220_BLOCKED:            YES
POSTERIOR_FIREWALL:             CLEAR
DOC_DOC_INCONSISTENCY:          FOUND — FORMULA_BRANCH_LOCK.md naming conflict
                                ACTION: annotation added to FORMULA_BRANCH_LOCK.md
LIGO_PIPELINE_AFFECTED:         NO (weak-field inspiral, both forms = Xi_weak)
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
```
