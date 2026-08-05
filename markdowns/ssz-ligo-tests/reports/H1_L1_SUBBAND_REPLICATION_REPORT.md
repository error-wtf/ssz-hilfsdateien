# H1/L1 Subband Abs-Correlation Replication Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Generated:** 2026-05-19
**Event:** GW240925 (GPS 1411261107.984)
**Status:** PENDING — subband run not yet executed

---

## Purpose

Determine whether the H1/L1 full-band coherence (abs(corr)=0.991 at dt=0 ms)
extends to all subbands, or whether the 20-40 Hz L1 excess is a detector-local
component not coherent with H1.

---

## Required Analysis

For each subband, run: peak_tau = argmax(|C(tau)|), peak_corr = C(peak_tau)

Scan range: tau = -10 ms to +10 ms
Physical limit: |tau| <= 10.012 ms (H1/L1 light-travel time)

| Subband | f_lo | f_hi | Target |
|---------|------|------|--------|
| 20-40 Hz | 20 | 40 | Is this L1-local or H1-coherent? |
| 40-80 Hz | 40 | 80 | Expected coherent |
| 80-120 Hz | 80 | 120 | Expected coherent |
| 120-160 Hz | 120 | 160 | Expected coherent |
| 160-210 Hz | 160 | 210 | Expected coherent |
| 20-210 Hz | 20 | 210 | Full band reference |

---

## Results Placeholder

Results will populate data_manifest/h1_l1_subband_abs_corr.csv when run is complete.

| Subband | Window | abs_corr | peak_tau_ms | verdict |
|---------|--------|----------|-------------|---------|
| 20-40 Hz | TRIGGER | PENDING | PENDING | PENDING |
| 20-40 Hz | OFF_m500 | PENDING | PENDING | PENDING |
| 40-80 Hz | TRIGGER | PENDING | PENDING | PENDING |
| 40-80 Hz | OFF_m500 | PENDING | PENDING | PENDING |
| 80-120 Hz | TRIGGER | PENDING | PENDING | PENDING |
| 80-120 Hz | OFF_m500 | PENDING | PENDING | PENDING |
| 120-160 Hz | TRIGGER | PENDING | PENDING | PENDING |
| 120-160 Hz | OFF_m500 | PENDING | PENDING | PENDING |
| 160-210 Hz | TRIGGER | PENDING | PENDING | PENDING |
| 160-210 Hz | OFF_m500 | PENDING | PENDING | PENDING |
| 20-210 Hz | TRIGGER | 0.991 | 0.0 | COHERENT_SIGN_FLIP |
| 20-210 Hz | OFF_m500 | 0.9999 | 0.0 | COHERENT_SIGN_FLIP |

---

## Decision Logic

The decisive check for each subband is:

```text
Is abs_corr_trigger significantly HIGHER than abs_corr_off_source?
```

Interpretation:

```text
abs_corr_trigger >> abs_corr_off_source:
    -> event-specific coherence
    -> subband_verdict = TRIGGER_SPECIFIC_COHERENT
    -> the signal in this band is triggered by the event

abs_corr_trigger approximately equals abs_corr_off_source:
    -> stationary coupling / common noise mode
    -> subband_verdict = PERSISTENT_COMMON_MODE
    -> not event-specific; cannot support signal claim

abs_corr_trigger < 0.3 AND abs_corr_off_source < 0.3:
    -> no H1 coherence in this band
    -> subband_verdict = L1_LOCAL
```

Note: The full-band comparison already shows TRIGGER approximately equals OFF_m500
(0.991 vs 0.9999), which suggests a stationary coupling mode dominates the full band.
Subband analysis is critical to find whether any band is trigger-specific.

**Key gate for 20-40 Hz:**

```text
If 20-40 Hz is TRIGGER_SPECIFIC_COHERENT:
    The L1 20-40 Hz excess is part of the coherent event signal.
    Gaussianity gate may be revisited with event-context.

If 20-40 Hz is PERSISTENT_COMMON_MODE:
    The excess is a stationary environmental coupling.
    Not event-specific. Does not block or support SSZ claim.
    DQ/Omicron/iDQ context required for further interpretation.
    L1_20_40_STATUS: PERSISTENT_COMMON_MODE

If 20-40 Hz is L1_LOCAL:
    The excess is detector-local, not H1-coherent.
    L1_20_40_STATUS: DQ_CONTEXT_REQUIRED
```

---

## Current Gate Status

```text
SUBBAND_RUN_COMPLETE:          NO
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```
