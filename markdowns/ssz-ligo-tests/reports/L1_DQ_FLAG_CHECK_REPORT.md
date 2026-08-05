# L1 DQ Flag Check Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 23:21:51  
Event: GW240925 (trigger GPS 1411261107.984)  
Window: +/- 2.0s around trigger  
Band: 20.0--210.0 Hz

## Summary

| Status | Value |
|--------|-------|
| L1_DQ_STATUS | FLAGGED_CW_HW_INJ_ACTIVE |
| COHERENCE_STATUS | PARTIAL_L1_ANOMALY |
| READY_FOR_REAL_LIGO_SSZ_CLAIM | NO |
| SSZ_SUPPORT_CLAIM_MADE | NO |
| SSZ_FALSIFICATION_CLAIM_MADE | NO |

## H1 DQ Flags in Trigger Window

| Flag | Set? | Meaning |
|------|------|---------|
| DATA | YES | pass/active |
| CBC_CAT1 | YES | pass/active |
| CBC_CAT2 | YES | pass/active |
| CBC_CAT3 | YES | pass/active |
| BURST_CAT1 | YES | pass/active |
| BURST_CAT2 | YES | pass/active |
| BURST_CAT3 | YES | pass/active |
| STOCH_CAT1 | YES | pass/active |
| CW_CAT1 | NO | FAIL/inactive |

### H1 Injection Flags

| Flag | Value | Meaning |
|------|-------|---------|
| NO_CBC_HW_INJ | CLEAN | no injection |
| NO_BURST_HW_INJ | CLEAN | no injection |
| NO_DETCHAR_HW_INJ | CLEAN | no injection |
| NO_CW_HW_INJ | INJ_PRESENT | INJECTION ACTIVE |
| NO_STOCH_HW_INJ | CLEAN | no injection |

H1 band power ratio (trigger/off-200s): 0.76

## L1 DQ Flags in Trigger Window

| Flag | Set? | Meaning |
|------|------|---------|
| DATA | YES | pass/active |
| CBC_CAT1 | YES | pass/active |
| CBC_CAT2 | YES | pass/active |
| CBC_CAT3 | YES | pass/active |
| BURST_CAT1 | YES | pass/active |
| BURST_CAT2 | YES | pass/active |
| BURST_CAT3 | YES | pass/active |
| STOCH_CAT1 | YES | pass/active |
| CW_CAT1 | YES | pass/active |

### L1 Injection Flags

| Flag | Value | Meaning |
|------|-------|---------|
| NO_CBC_HW_INJ | CLEAN | no injection |
| NO_BURST_HW_INJ | CLEAN | no injection |
| NO_DETCHAR_HW_INJ | CLEAN | no injection |
| NO_CW_HW_INJ | INJ_PRESENT | INJECTION ACTIVE |
| NO_STOCH_HW_INJ | CLEAN | no injection |

L1 band power ratio (trigger/off-200s): 2.28

## H1 / L1 Flag Differences

Flags that differ between H1 and L1: **['CW_CAT1']**

| Flag | H1 | L1 | Status |
|------|----|----|--------|
| CW_CAT1 | False | True | DIFFER |
| NO_CW_HW_INJ | INJ_PRESENT | INJ_PRESENT | SAME |

## Key Finding: CW Hardware Injection

```
NO_CW_HW_INJ flag is NOT SET for BOTH H1 and L1.
This means a CW (continuous wave) hardware injection was ACTIVE
at the time of the GW240925 trigger at both detectors.
```

**What this means:**

A hardware injection injects a simulated signal directly into the
detector actuation system. CW injections are continuous sinusoidal
signals used for calibration and detector characterization. They are
NOT GW signals.

If a CW hardware injection was active in the 20-210 Hz band at
trigger time, it would:
- Add a narrow spectral line to the data
- NOT explain a broadband power excess like the L1 anomaly
- Be present in both H1 and L1 simultaneously (consistent with both
  being flagged)

**However:** The CW injection line would be at a single known frequency,
not broadband. The L1 power excess across the full 20-210 Hz band
is **not explained** by a CW hardware injection alone.

## Critical Flags: CBC_CAT2 / CBC_CAT3

| Flag | H1 | L1 |
|------|----|----|
| CBC_CAT2 | SET | SET |
| CBC_CAT3 | SET | SET |

Both H1 and L1 pass CBC_CAT2 and CBC_CAT3 in the trigger window.
The L1 power excess is therefore **not due to a known vetoed glitch**
in the GWOSC release DQ flags.

## Interpretation

The L1 in-band power anomaly:

1. **Is NOT due to a CAT2/CAT3 flagged glitch** (both flags pass)
2. **Is NOT explained by DATA quality failure** (DATA flag set = good)
3. **Has a CW HW injection present** (same for H1 and L1) — cannot
   explain broadband excess
4. **CW_CAT1 differs**: H1 fails CW_CAT1, L1 passes — this means
   H1 was flagged for CW analysis quality, not L1

**Conclusion:** The L1 broadband power excess in the trigger window
is **not explained by any GWOSC release DQ flag**. The source of the
anomaly remains unresolved. Possible explanations:

- A non-stationary noise transient not captured by 1Hz DQ masks
- Environmental coupling not listed in simple DQ products
- An actual astrophysical signal in L1 (the event GW240925 itself)
- A non-glitch excess that requires LIGO offline DQ tools

## Question to LIGO (if needed)

```
We observe an L1-specific broadband power excess in the 20-210 Hz band
at the GW240925 trigger time (GPS 1411261107.984) after robust
multi-window PSD checks (4 off-source windows from -500s to +300s).

The GWOSC DQ flags CBC_CAT2/CAT3 are set (passing), DATA is set, and
we note NO_CW_HW_INJ is not set (CW injection active).

Questions:
1. Are offline DQ / glitch characterization products (omicron, iDQ,
   hveto outputs) available for this release?
2. Is the L1 trigger window in GW240925 known to be affected by any
   non-stationarity or environmental coupling not in the simple DQ mask?
3. Is there a recommended off-source window strategy for L1 in this event?
```

## Gate Status

```
L1_DQ_STATUS:                   FLAGGED_CW_HW_INJ_ACTIVE
H1_DQ_STATUS:                   PASS_NO_CRITICAL_FLAG
CBC_CAT2_BOTH:                  PASS
CBC_CAT3_BOTH:                  PASS
DATA_BOTH:                      PASS
CW_HW_INJ_BOTH_DETECTORS:       ACTIVE (broadband effect: NO)
CW_CAT1_ASYMMETRY:              H1 FAILS, L1 PASSES
L1_BROADBAND_EXCESS_EXPLAINED:  NO
COHERENCE_STATUS:               PARTIAL_L1_ANOMALY
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```
