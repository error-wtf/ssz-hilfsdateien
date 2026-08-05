# L1 Excluded / Diagnostic Report — GW240925

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 23:49:58  
Detector: L1 (LIGO Livingston)  
Event: GW240925 (trigger GPS 1411261107.984)  
Status: **DQ_FLAGGED_DIAGNOSTIC_ONLY**

## Why L1 Is Diagnostic-Only

L1 passes all CBC quality flags (CAT1/2/3, DATA) according to the
GWOSC release DQ bitmask. However, a strong broadband in-band power
excess is observed (band-power ratio trigger/off-source = 2.28)
that is NOT explained by any available DQ flag.

Additionally, the CW hardware injection flag (NO_CW_HW_INJ) is not
set ("not certified injection-free") for the entire 4096-second
release segment at both detectors. This is a file-wide constant, not
a trigger-specific event, and cannot by itself explain the broadband
excess.

## L1 DQ Status (VERIFIED_FROM_HDF5)

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
| CW_CAT1 | 1 | PASS (100% over full file) |

## L1 In-Band Diagnostics

| Metric | Value |
|--------|-------|
| Band | 20.0--210.0 Hz |
| Band-power ratio (trigger/off-source) | 2.28 |
| H1 band-power ratio for comparison | 0.76 |
| H1/L1 ratio difference | 1.52 |
| Assessment | ANOMALOUS — excess not explained by GWOSC DQ |

## Possible Explanations (Unresolved)

```
1. Real GW signal in L1
   GW240925 is a confirmed event. L1 would be expected to show
   elevated in-band power. This may simply be the signal.
   -> Would require matched-filter SNR comparison vs H1.

2. Non-stationary noise transient (unvetoed glitch)
   A noise event not captured by the 1Hz DQ bitmask.
   CBC_CAT2/CAT3 only veto known, classified glitch families.
   A glitch present but not in the veto list would remain unflagged.
   -> Needs offline omicron time-frequency scan to distinguish from signal.

3. PSD estimation mismatch / non-stationarity
   Off-source window at -200s may not represent noise at trigger time.
   -> Robust multi-window PSD (already done) showed consistent excess.
   -> iDQ glitch probability at trigger time would clarify.

4. CW hardware injection contribution
   Narrow-band only — cannot explain broadband excess.
   -> Already ruled out by bandwidth argument.
```

## Why CBC_CAT2/CAT3 Clean Is Not Sufficient Here

```
CBC_CAT2/CAT3 vetoes cover known, pre-classified glitch families.
They do NOT cover:
  - Novel or uncatalogued transients
  - Excess power in frequency bands not covered by veto templates
  - Non-stationary noise not flagged by any CAT criterion

The only products that can distinguish:
  signal / unvetoed glitch / line / PSD non-stationarity
are offline tools:
  - Omicron: time-frequency excess power scan
  - iDQ:     glitch probability at specific GPS times
  - hveto:   correlation with environmental monitors
  - line-noise monitors: persistent narrow features

These are NOT included in the GWOSC release DQ bitmask.
Without them, L1 cannot be definitively assessed for our purpose.
```

## What L1 Can Be Used For

```
DIAGNOSTIC USE ONLY:
  - Qualitative comparison with H1
  - Visual inspection of spectral excess
  - Motivating LIGO DQ question

NOT USABLE FOR:
  - H1/L1 coherence-based SSZ evidence
  - Multi-detector twist amplitude claim
  - Any claim requiring clean L1 noise characterization
```

## Reinstatement Criteria

```
L1 can be reinstated as a full coherence partner when:
  1. Offline DQ (omicron/iDQ/hveto) confirms no glitch at trigger time
  OR
  2. LIGO/GWOSC confirms the L1 segment is usable for coherence tests
  OR
  3. A physically motivated explanation for the excess is found
     (e.g., confirmed matched-filter SNR consistent with the event)
```

## Gate

```
L1_STATUS:                     DQ_FLAGGED_DIAGNOSTIC_ONLY
L1_CBC_DQ:                     PASS (no vetoed glitch)
L1_BROADBAND_EXCESS:           UNEXPLAINED
L1_REINSTATEMENT:              REQUIRES_OFFLINE_DQ_OR_LIGO_CONFIRMATION
H1_L1_COHERENCE_STATUS:        BLOCKED_BY_L1_DQ
TWIST_REAL_DATA_STATUS:        BLOCKED_BY_L1_DQ
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```
