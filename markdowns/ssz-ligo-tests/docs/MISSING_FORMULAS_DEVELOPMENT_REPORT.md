# Missing Formulas Development Report

**Generated:** 2026-05-18  
**Repo:** E:\clone\ssz-ligo-tests  
**Task:** SSZ_LIGO_DERIVE_MISSING_FORWARD_EQUATIONS_FROM_SOURCES  
**Status:** PHASES 1–7 COMPLETE | PHASE 8 (this report)

---

## Summary

All eight phases of the SSZ LIGO Missing Formulas derivation task are complete.
No physics claims were made. No posterior data was used. No LIGO data was fit.

---

## Phase Status

| Phase | Deliverable | Status |
|-------|-------------|--------|
| P1 | `docs/FORMULA_BRANCH_LOCK.md` — Xi_strong + regime boundaries | COMPLETE |
| P2 | `derived_phase.py` + `DELTA_PSI_DERIVATION.md` | COMPLETE |
| P3 | `derived_amplitude.py` + `DELTA_A_DERIVATION.md` | COMPLETE |
| P4 | `derived_waveform.py` + `H_SSZ_V0_DERIVATION.md` | COMPLETE |
| P5 | `epsilon_220_registry.py` | COMPLETE (BLOCKED status) |
| P6 | 6 new validation test files | COMPLETE (61 new tests) |
| P7 | `run_derived_v0_pipeline.py` + report | COMPLETE |
| P8 | This report | COMPLETE |

---

## Derived Formulas

### deltaPsi_SSZ(f) — DERIVED_V0_PROXY

**Source:** SSZ Book Ch.31, formula_compendium.md §C.1  
**Derivation:**

```
r(f)     = (G*M / (pi*f)^2)^(1/3)        [Kepler 3rd law, circular orbit]
s(r)     = 1 + Xi(r)                       [RSG scaling: radial_scaling.md]
D(r)     = 1/s(r)                          [time dilation factor]
rdot_SSZ = rdot_GR * D^2 / s^4            [locked: formula_compendium.md §C.1]
rdot_GR  = -(64/5) * G^3 * M^2 * mu / (c^5 * r^3)

deltaPsi  = integral over r: [Omega_SSZ(r') - Omega_GR(r')] * dt/dr dr'
V0 proxy: substituting rdot_SSZ:

deltaPsi_V0(f) = integral_{r(f_max)}^{r(f)} [1/D(r') - 1] * Omega(r') / rdot_GR(r') dr'
```

**Regime:** r/rs >> 1 for LIGO band (20–800 Hz, 8.9 Msun binary: r/rs ≈ 100–1000)  
**Branch:** g2_decay (operative per FORMULA_BRANCH_LOCK.md)  
**Dimensional check:** [1/D - 1] = dimensionless, [Omega/rdot_GR] = rad/m → result in rad ✓  
**READY_FOR_REAL_CLAIM:** NO  

### deltaA_SSZ(f) — DERIVED_V0_PROXY

**Source:** formula_compendium.md §B.4, ssz_inspiral.py  
**Derivation:**

```
P_GW_SSZ = P_GW_GR * D^2 / s^2           [locked: formula_compendium.md §B.4]
amplitude ~ sqrt(P_GW) => A_SSZ/A_GR = D(r(f))
deltaA(f) = D(r(f))^2 - 1                 [via power ratio, squared amplitude]
```

**Result:** deltaA in (-1, 0], monotonically decreasing as f increases (r decreases)  
**READY_FOR_REAL_CLAIM:** NO  

### h_SSZ(f) — DERIVED_V0_PROXY

```
h_SSZ(f) = h_GR(f) * [1 + deltaA(f)] * exp(i * deltaPsi(f))
```

**Construction:** h_GR is an analytic TaylorF2 0PN control template only  
**READY_FOR_REAL_CLAIM:** NO  

---

## epsilon_220 / eta_220 Registry — BLOCKED

Three conflicting branches found in corpus:

| Branch | Value | Source | Status |
|--------|-------|--------|--------|
| v51_ch30_3_percent | 0.03 | SSZ Book V51 Ch.30 | PARTIAL_EXPLORATORY |
| dmin_squared_scale | D_min^2 = 0.308 (~31%) | formula_compendium §B.7 | SUPERSEDED_OR_DIFFERENT_REGIME |
| photon_sphere_39_percent | 0.39 | qnm_spectrum.md r/rs=1.387 | DISCARDED_FOR_LIGO_STRAIN |

**Resolution:** BLOCKED until canonical branch is selected by authors.  
**Note:** The 39% is a source-frame QNM ratio, not the LIGO strain observable.

---

## Pipeline Run Results (GW240925, H1, 2026-05-18)

| Item | Value |
|------|-------|
| Strain source | GWOSC LIGO HDF5 (anti-circularity: VALID_INDEPENDENT) |
| Formula | DERIVED_V0_PROXY (g2_decay branch) |
| deltaPsi band 20-800 Hz | min=5.98e-02, max=1.08e+01 rad |
| deltaA band 20-800 Hz | min=-0.692, max=-0.065 |
| lnL GR control | -3.24e+07 |
| lnL SSZ V0 | -3.24e+07 |
| delta_lnL | 6.34e-06 |
| Interpretation | INDISTINGUISHABLE — delta_lnL < 1 |
| MF-SNR GR | 39.92 |
| MF-SNR SSZ | 14.23 (V0 proxy not optimized) |

**SSZ_SUPPORT_CLAIM_MADE:** NO  
**SSZ_FALSIFICATION_CLAIM_MADE:** NO  
**READY_FOR_REAL_LIGO_SSZ_CLAIM:** NO  

---

## Test Suite Summary

| Test File | Tests | Result |
|-----------|-------|--------|
| test_derived_delta_psi_v0.py | 13 | 13/13 PASS |
| test_derived_delta_a_v0.py | 11 | 11/11 PASS |
| test_h_ssz_v0_waveform_application.py | 13 | 13/13 PASS |
| test_epsilon_220_branch_registry.py | 11 | 11/11 PASS |
| test_no_data_fitting.py | 13 | 13/13 PASS |
| **All (full suite)** | **330** | **330 PASS, 1 xfail (expected)** |

---

## Open Issues / Blocked Items

1. **BLOCKED_MISSING_EQUATION — deltaPsi exact:**  
   SSZ Book Ch.31 RSG phase integral not yet unlocked as final locked formula.  
   Current V0 uses Kepler + rdot_SSZ ratio, which is approximate.

2. **BLOCKED_BRANCH_CONFLICT — epsilon_220:**  
   Three conflicting values (3%, 31%, 39%) from three source locations.  
   No canonical branch selected. Real LIGO ringdown test is BLOCKED.

3. **GR control template limited:**  
   TaylorF2 0PN only — no spin, no higher modes, no merger, no ringdown.  
   Real SSZ claim requires full IMR waveform as GR control.

---

## Anti-Circularity Gate

| Observable | Classification | Used |
|------------|---------------|------|
| H1 GWOSC strain | VALID_INDEPENDENT | YES |
| Off-source PSD (Welch) | VALID_INDEPENDENT | YES |
| TaylorF2 analytic | ANALYTIC_CONTROL | YES |
| SSZ V0 proxy | SSZ_FORWARD_V0_PROXY | YES |
| Posterior samples | INVALID | NO |
| PE-PSD | CIRCULARITY_RISK | NO |
| pSEOBNR | INVALID | NO |
| epsilon_220 | BLOCKED_CONFLICTING | NO |

---

## Absolute Rules Compliance

1. No fitting to LIGO data: **CONFIRMED**
2. No tuning to improve SSZ appearance: **CONFIRMED**
3. No posterior f, m, chi as verdict: **CONFIRMED**
4. No SSZ support/falsification claims: **CONFIRMED**
5. No silent Kerr/GR substitution: **CONFIRMED**
6. No source changes or deletions: **CONFIRMED**
7. Every formula states source, derivation, assumptions, dimensional check, status: **CONFIRMED**
8. Blocked formulas marked BLOCKED: **CONFIRMED** (epsilon_220)
9. Source conflicts preserved without silent choice: **CONFIRMED** (epsilon_220 registry)
