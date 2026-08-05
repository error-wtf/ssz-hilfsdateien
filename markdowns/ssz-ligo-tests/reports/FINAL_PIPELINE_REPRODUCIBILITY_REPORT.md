# Final Pipeline Reproducibility Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-18
Version: EXPLORATORY_V0_PROXY_ONLY
Source-Truth: AUDITED (see SOURCE_TRUTH_VERIFICATION.md)

---

## File Paths

| Role | Path |
|------|------|
| H1 Strain | E:\clone\ligo-gw240925-gw250207-release\18600070\GW240925-C00-Strain\GW240925-C00-Strain\O4b4DiscC00_4KHZ_R1\STRAIN_HDF\H1\1410334720\H-H1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5 |
| Metafile | E:\clone\ligo-gw240925-gw250207-release\18600070\GW240925_combinedPHM_envcalC01_metafile.hdf5 |
| Pipeline script | E:\clone\ssz-ligo-tests\scripts\run_strain_pipeline.py |

## Dataset Paths (within HDF5)

| Dataset | Path |
|---------|------|
| Strain | strain/Strain |
| GPS start | meta/GPSstart |
| Duration | meta/Duration |

## Time Window

| Parameter | Value |
|-----------|-------|
| Trigger GPS | 1411261107.984 |
| Analysis window | ±2s around trigger (4s total) |
| File GPS start | 1411260416 |
| File duration | 4096s |
| Sample rate | 4096 Hz |

## PSD Method

| Parameter | Value |
|-----------|-------|
| Method | Welch (scipy.signal.welch) |
| Segment | Off-source (first 512s of file) |
| NFFT | 4096 |
| Anti-circularity | PSD from strain, not from posterior/metafile |

## GR Control Template

| Parameter | Value |
|-----------|-------|
| Type | TaylorF2 0PN (analytic) |
| Label | CONTROL_TEMPLATE_ONLY |
| Mc | 8.9 M_sun |
| eta | 0.25 |
| f_low | 20 Hz |
| f_high | 800 Hz |
| Source | No posterior used |

## SSZ V0 Proxy

| Parameter | Value |
|-----------|-------|
| Label | SSZ_FORWARD_V0_PROXY |
| Xi form | xi_weak = rs/(2r) in LIGO band |
| D(r) | 1/(1+Xi) |
| deltaPsi | kappa * (1 - D(r_orbit(f))) |
| kappa | 1.0 |
| h_SSZ | h_GR * exp(i * deltaPsi) |
| Forward model | V0 proxy only — complete derivation NOT IN CORPUS |

## SSZ Constants (Source-Locked)

| Constant | Value | Source |
|----------|-------|--------|
| phi | (1+sqrt(5))/2 ≈ 1.618 | formula_compendium.md |
| Xi_max | 1-exp(-phi) ≈ 0.802 | formula_compendium.md |
| D_min | 1/(1+Xi_max) ≈ 0.555 | formula_compendium.md |
| BLEND_START | 1.8 r/rs | regime_and_formula_domain_clarification.md |
| BLEND_END | 2.2 r/rs | regime_and_formula_domain_clarification.md |

## Branch Choices

| Choice | Selection | Status |
|--------|-----------|--------|
| Xi_strong form | decay (historic) → saturation (canonical fixed) | CANONICAL_OPERATIONAL now |
| epsilon_220 | None | BLOCKED_CONFLICTING |
| Ringdown | not used | BLOCKED |
| Posterior data | not used | INVALID_FOR_SSZ |

## Blocked Equations

| Equation | Reason |
|----------|--------|
| h_SSZ(f) exact | not derived in corpus (known_limitations.md §3) |
| epsilon_220 | three conflicting sources (3%/31%/39%) |
| Xi_strong old decay | superseded by saturation form |
| Xi deprecated | (rs/r)^2 * exp(-r/r_phi) — FORBIDDEN |

## Pipeline Results (Exploratory)

| Metric | Value |
|--------|-------|
| lnL_GR | ≈ -3.237e7 |
| lnL_SSZ | ≈ -3.237e7 |
| Delta lnL | ≈ -4.47e-8 |
| MF-SNR GR | ≈ 39.92 |
| MF-SNR SSZ | ≈ 40.27 |
| deltaPsi_max | ≈ 0.286 rad |
| Residual max | ≈ 8.5e-22 |

## Final Gate

```
PIPELINE_STATUS:               PASS_EXPLORATORY_STRAIN_PIPELINE_RAN
READY_FOR_REAL_SSZ_CLAIM:      NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
POSTERIOR_RF_TEST:             INVALID_FOR_SSZ
RINGDOWN_TEST:                 PARTIAL_EXPLORATORY_OR_BLOCKED_UNTIL_EPSILON_220_LOCKED
REAL_STRAIN_TEST:              EXPLORATORY_V0_PROXY_ONLY
```
