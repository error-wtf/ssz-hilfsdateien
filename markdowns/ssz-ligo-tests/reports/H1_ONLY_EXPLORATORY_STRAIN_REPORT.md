# H1-Only Exploratory Strain Report — GW240925

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 23:49:58  
Detector: H1 (LIGO Hanford)  
Event: GW240925 (trigger GPS 1411261107.984)  
Status: **USABLE_EXPLORATORY**

## Why H1-Only

L1 is in DQ_FLAGGED_DIAGNOSTIC_ONLY status due to unresolved broadband
power excess and CW hardware injection context (see
DQ_AWARE_FINAL_LIGO_STATUS.md). H1 passes all CBC quality flags and
has a normal in-band power profile.

## H1 DQ Status (VERIFIED_FROM_HDF5)

| Flag | Value | Status |
|------|-------|--------|
| DATA | 1 | PASS |
| CBC_CAT1 | 1 | PASS |
| CBC_CAT2 | 1 | PASS |
| CBC_CAT3 | 1 | PASS |
| BURST_CAT1 | 1 | PASS |
| BURST_CAT2 | 1 | PASS |
| BURST_CAT3 | 1 | PASS |
| STOCH_CAT1 | 1 | PASS |
| CW_CAT1 | 0 | FAILS (file-wide, not trigger-specific) |

CW_CAT1 failure is constant over the entire 4096-second file,
indicating a detector-state issue for CW analyses unrelated to the
GW240925 trigger window.

## H1 In-Band Diagnostics

| Metric | Value |
|--------|-------|
| Band | 20.0--210.0 Hz |
| Off-source window | trigger -200s, 64s duration |
| Band-power ratio (trigger/off-source) | 0.76 |
| Peak single-bin SNR proxy | 0.9 |
| Assessment | NORMAL |

## What H1 Can Test

```
USABLE FOR:
  - Single-detector scale SSZ: h_H1^SSZ = S * h_H1^GR
  - H1 MF-SNR with 2PN template
  - H1 band-power consistency check
  - H1 scale-factor scan vs theta at fixed inclination
  - Pipeline validation on a clean detector

NOT USABLE FOR (without L1):
  - H1/L1 differential response under twist
  - Coherence-based SSZ evidence
  - Multi-detector twist claim
```

## Gate

```
H1_STATUS:                     USABLE_EXPLORATORY
H1_CBC_DQ:                     PASS
H1_ANOMALY:                    NONE
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
```
