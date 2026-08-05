# LIGO Physics Clarification — GW240925

**Date:** 2026-05-19 | **Cross-ref:** `ssz-ligo-tests/reports/PHYSICS_CLARIFICATION_NOTE.md`

## Canonical Statement

> We distinguish between detector measurements and model-conditioned inference products. The calibrated strain is measurement input; chirp mass, component masses, spins, and QNM parameters are GR/CBC-conditioned estimates — not metric-neutral observables.

On the L1 anomaly:
> The anomaly may be detector- or pipeline-induced. Current public GWOSC products are insufficient to decide whether the 20-40 Hz structure is instrumental, environmental, line-related, or signal-like.

## Four Precise Statements

### 1. Chirp Mass

| Statement | Verdict |
|-----------|---------|
| Chirp mass is arbitrary | NO — it is the leading GR inspiral observable |
| Chirp mass is model-free | NO — defined inside GR/CBC waveform framework |
| Valid input for anti-circular SSZ test | NO — circular: uses GR-inferred ℳ to constrain SSZ |

### 2. LIGO Posteriors

The parameters m₁, m₂, χ, ℳ, f_QNM, τ_QNM are Bayesian posteriors conditioned on GR/Kerr waveform templates — not direct measurements of physical object properties.

| Incorrect framing | Correct framing |
|-------------------|----------------|
| "GW240925 has component masses m₁=X, m₂=Y" | "Under GR/CBC templates, posterior on m₁ peaks at X M☉" |
| "The ringdown frequency proves Kerr" | "Data is consistent with Kerr QNM frequencies at stated SNR" |

### 3. L1 Anomaly

| Diagnostic | Result |
|-----------|--------|
| L1 20-40 Hz trigger ex_kurtosis | +44.9 |
| L1 20-40 Hz off-source ex_kurtosis | +1.1 |
| Δ trigger − off-source | +43.7 — trigger-specific |
| H1 20-40 Hz trigger ex_kurtosis | +3.7 — clean |

Plausible candidates: sub-threshold glitch, environmental coupling, filter/whitening artifact, calibration/line leakage. Cannot be classified without Omicron/iDQ.

### 4. SSZ Claim Status

```
SSZ_SUPPORT_CLAIM_MADE:       NO
SSZ_FALSIFICATION_CLAIM_MADE: NO
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```

A valid SSZ strain-level test requires: clean H1+L1 with verified DQ, locked h_SSZ(f) derivation, forward-model on raw strain, no GR posteriors as inputs.

## Summary Table

| Statement | Verdict |
|-----------|---------|
| LIGO posteriors are direct measurements | NO |
| L1 anomaly is a confirmed glitch | NO |
| L1 anomaly is a confirmed signal | NO |
| SSZ is supported by this analysis | NO |
| SSZ is falsified by this analysis | NO |
| The analysis pipeline is valid | YES |
| The L1 anomaly is real | YES — reproduced across methods |
| The 20-40 Hz localization is new | YES |
