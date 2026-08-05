# LIGO GW240925 — SSZ V0-Proxy Pipeline Validation

**Run date:** 2026-05-18  
**Event:** GW240925 (GWOSC O4b, H1 detector)  
**Trigger GPS:** 1411261107.984  
**Chirp mass:** 8.9 Msun (public alert estimate)  
**Pipeline:** `ssz-ligo-tests/scripts/run_derived_v0_pipeline.py`  
**Formula status:** DERIVED_V0_PROXY  
**Claim status:** NO CLAIM

---

## Purpose

This is an **exploratory, anti-circular technical validation** of the derived SSZ V0
forward model formulas against real LIGO strain data. It demonstrates that the
pipeline runs without error and that the derived formulas produce finite,
physically-bounded outputs. It does **not** constitute a physics test of SSZ.

---

## Data Sources

| Source | Type | Anti-Circularity |
|--------|------|-----------------|
| H1 GWOSC strain HDF5 | calibrated strain | VALID_INDEPENDENT |
| Off-source Welch PSD | estimated from raw strain | VALID_INDEPENDENT |
| TaylorF2 0PN template | analytic GR control | ANALYTIC_CONTROL |
| SSZ V0 proxy | derived from locked sources | SSZ_FORWARD_V0_PROXY |
| Posterior samples | NOT USED | BLOCKED |
| PE-derived PSD | NOT USED | BLOCKED (circularity risk) |

---

## Derived Formula Application

```
r(f)     = (G*M / (pi*f)^2)^(1/3)
Xi(r)    = Xi_decay(r)  [g2_decay branch, r/rs in weak-field LIGO regime]
D(r)     = 1/(1+Xi(r))
deltaPsi = integral [1/D(r') - 1] * Omega(r') / rdot_GR(r') dr'
deltaA   = D(r)^2 - 1
h_SSZ(f) = h_GR(f) * [1 + deltaA(f)] * exp(i * deltaPsi(f))
```

---

## Numerical Results

### Phase Correction (deltaPsi), band 20–800 Hz

| Statistic | Value |
|-----------|-------|
| minimum | 5.98e-02 rad |
| maximum | 1.08e+01 rad |
| median | 1.72e-01 rad |

**Physical interpretation:** r/rs at 20 Hz ≈ 1000 (deep weak field), at 800 Hz ≈ 100.
Correction is small at low frequencies, grows toward ISCO. Capped at ISCO (r/rs = 3).

### Amplitude Correction (deltaA), band 20–800 Hz

| Statistic | Value |
|-----------|-------|
| minimum | −0.692 |
| maximum | −0.065 |
| median | −0.602 |

**Physical interpretation:** D^2 - 1 ∈ (-1, 0]. Amplitude is suppressed.
Large corrections at high f (small r) consistent with D approaching D_min.

### Log-Likelihood Comparison

| Model | lnL | MF-SNR |
|-------|-----|--------|
| GR control (TaylorF2 0PN) | −3.24e+07 | 39.92 |
| SSZ V0-proxy | −3.24e+07 | 14.23 |
| delta_lnL (SSZ − GR) | +6.34e-06 | — |

**Interpretation:** delta_lnL = 6.34e-06 < 1 → **INDISTINGUISHABLE**.

The low SSZ MF-SNR (14.23 vs 39.92) reflects that the V0 proxy amplitude
deformation (up to −69%) is **not** amplitude-matched to data. This is expected
and does not constitute a falsification.

---

## Epistemological Status

```
PIPELINE_STATUS:                PASS_DERIVED_V0_PIPELINE
FORMULA_STATUS:                 DERIVED_V0_PROXY
EPSILON_220_STATUS:             BLOCKED_BRANCH_CONFLICT
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
ANTI_CIRCULARITY_GATE:         CLEAR
```

---

## Blockers Before Real SSZ LIGO Test

1. **deltaPsi exact formula** — SSZ Book Ch.31 RSG phase integral not yet locked
2. **epsilon_220 ringdown** — 3 conflicting values (3%/31%/39%), no canonical branch
3. **Full IMR waveform** — GR control template must include spin + merger + ringdown
4. **Amplitude matching** — V0 amplitude proxy needs physical justification for claim
5. **Calibration uncertainty** — systematic calibration envelope not yet included

---

## Relation to All-Tests Snapshot

This pipeline validation is **separate** from the 1296/1296 all-tests snapshot
(`07_VALIDATION/all_tests_2026-05-07.md`). The all-tests snapshot covers
SSZ core theory implementations. This document covers the LIGO-specific
exploratory strain pipeline only.

The 330/330 ssz-ligo-tests result (including 61 new V0 tests from 2026-05-18)
will be incorporated into the next all-tests snapshot run.
