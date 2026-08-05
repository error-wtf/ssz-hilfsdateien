# DQ State-Vector Bit Provenance Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 23:39:25  
Event: GW240925 (trigger GPS 1411261107.984)  
File segment: GPS 1411260416 -- 1411264512 (4096 s)

## Methodology

All bit names and descriptions were extracted **directly from the HDF5 files**
using `DQShortnames`, `DQDescriptions`, `InjShortnames`, `InjDescriptions`
datasets inside the `quality/` group. No names were hardcoded.

Name source for all bits below: **VERIFIED_FROM_HDF5**

---

## H1 DQ Bit Provenance

| Bit | Name | Source | At Trigger | % Set (file) | Constant? | Description |
|-----|------|--------|-----------|-------------|-----------|-------------|
| 0 | DATA | VERIFIED_FROM_HDF5 | 1 | 41.6% | False | data present |
| 1 | CBC_CAT1 | VERIFIED_FROM_HDF5 | 1 | 41.6% | False | passes the cbc CAT1 test |
| 2 | CBC_CAT2 | VERIFIED_FROM_HDF5 | 1 | 41.6% | False | passes cbc CAT2 test |
| 3 | CBC_CAT3 | VERIFIED_FROM_HDF5 | 1 | 41.6% | False | passes cbc CAT3 test |
| 4 | BURST_CAT1 | VERIFIED_FROM_HDF5 | 1 | 41.6% | False | passes burst CAT1 test |
| 5 | BURST_CAT2 | VERIFIED_FROM_HDF5 | 1 | 41.5% | False | passes burst CAT2 test |
| 6 | BURST_CAT3 | VERIFIED_FROM_HDF5 | 1 | 41.5% | False | passes burst CAT3 test |
| 7 | STOCH_CAT1 | VERIFIED_FROM_HDF5 | 1 | 41.6% | False | passes stoch CAT1 test |
| 8 | CW_CAT1 | VERIFIED_FROM_HDF5 | 0 | 0.0% | True | passes cw CAT1 test |

### H1 Injection Bit Provenance

| Bit | Name | Source | At Trigger | % Set (file) | Constant? | Description |
|-----|------|--------|-----------|-------------|-----------|-------------|
| 0 | NO_CBC_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no cbc injection |
| 1 | NO_BURST_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no burst injections |
| 2 | NO_DETCHAR_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no detchar injections |
| 3 | NO_CW_HW_INJ | VERIFIED_FROM_HDF5 | 0 | 0.0% | True | no continuous wave injections |
| 4 | NO_STOCH_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no stoch injections |

---

## L1 DQ Bit Provenance

| Bit | Name | Source | At Trigger | % Set (file) | Constant? | Description |
|-----|------|--------|-----------|-------------|-----------|-------------|
| 0 | DATA | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | data present |
| 1 | CBC_CAT1 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes the cbc CAT1 test |
| 2 | CBC_CAT2 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes cbc CAT2 test |
| 3 | CBC_CAT3 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes cbc CAT3 test |
| 4 | BURST_CAT1 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes burst CAT1 test |
| 5 | BURST_CAT2 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes burst CAT2 test |
| 6 | BURST_CAT3 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes burst CAT3 test |
| 7 | STOCH_CAT1 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes stoch CAT1 test |
| 8 | CW_CAT1 | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | passes cw CAT1 test |

### L1 Injection Bit Provenance

| Bit | Name | Source | At Trigger | % Set (file) | Constant? | Description |
|-----|------|--------|-----------|-------------|-----------|-------------|
| 0 | NO_CBC_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no cbc injection |
| 1 | NO_BURST_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no burst injections |
| 2 | NO_DETCHAR_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no detchar injections |
| 3 | NO_CW_HW_INJ | VERIFIED_FROM_HDF5 | 0 | 0.0% | True | no continuous wave injections |
| 4 | NO_STOCH_HW_INJ | VERIFIED_FROM_HDF5 | 1 | 100.0% | True | no stoch injections |

---

## H1 / L1 Comparison

### DQ Bits

| Bit | Name | H1 trigger | L1 trigger | H1 % file | L1 % file | Status |
|-----|------|-----------|-----------|-----------|-----------|--------|
| 0 | DATA | 1 | 1 | 41.58% | 100.0% | AGREE |
| 1 | CBC_CAT1 | 1 | 1 | 41.58% | 100.0% | AGREE |
| 2 | CBC_CAT2 | 1 | 1 | 41.58% | 100.0% | AGREE |
| 3 | CBC_CAT3 | 1 | 1 | 41.58% | 100.0% | AGREE |
| 4 | BURST_CAT1 | 1 | 1 | 41.58% | 100.0% | AGREE |
| 5 | BURST_CAT2 | 1 | 1 | 41.46% | 100.0% | AGREE |
| 6 | BURST_CAT3 | 1 | 1 | 41.46% | 100.0% | AGREE |
| 7 | STOCH_CAT1 | 1 | 1 | 41.58% | 100.0% | AGREE |
| 8 | CW_CAT1 | 0 | 1 | 0.0% | 100.0% | DIFFER |

**Bits that differ at trigger: ['CW_CAT1']**

### Key Finding: CW_CAT1

```
Name source:  VERIFIED_FROM_HDF5
Description:  "passes cw CAT1 test"

H1: CW_CAT1 = 0 (NOT SET) at trigger
    0.0% set over entire 4096-second file
    -> H1 never passes CW CAT1 in this segment

L1: CW_CAT1 = 1 (SET) at trigger
    100.0% set over entire 4096-second file
    -> L1 always passes CW CAT1 in this segment
```

**What CW_CAT1 means:**
This flag indicates whether the data passes the quality check for
Continuous Wave (CW) searches. It does NOT directly indicate whether
an H1-specific glitch or environmental coupling exists. H1 failing
CW_CAT1 for the entire 4096-second file segment is a file-wide
property, not a trigger-specific event.

**Critical point:**
CW_CAT1 is a quality category for CW analyses, not for CBC searches.
The CBC_CAT1, CBC_CAT2, CBC_CAT3 flags — which ARE relevant for
binary merger searches like GW240925 — are ALL SET (passing) for
BOTH H1 and L1 at the trigger.

### Key Finding: NO_CW_HW_INJ

```
Name source:     VERIFIED_FROM_HDF5
Description:     "no continuous wave injections"
H1 value:        0 (NOT SET) over entire file (0.0%)
L1 value:        0 (NOT SET) over entire file (0.0%)

Convention: SET=1 means "no injection of this type confirmed"
            NOT SET=0 means "not certified injection-free"
```

**What this means:**
Neither H1 nor L1 is certified as "no CW hardware injection" during
this 4096-second segment. This does NOT mean a CW injection was
definitely present; it means the injection-free status for CW was
not positively certified in this product.

**Important distinction:**
- The CBC injection flags (NO_CBC_HW_INJ, NO_BURST_HW_INJ,
  NO_DETCHAR_HW_INJ, NO_STOCH_HW_INJ) are ALL SET=1 (clean) for
  BOTH detectors at trigger time.
- Only NO_CW_HW_INJ is unset — and this is constant over the entire
  4096-second file, not specific to the trigger window.
- A CW hardware injection (if present) would be a narrow-band,
  continuous sinusoidal signal. It would NOT produce the broadband
  20-210 Hz power excess observed in L1.

---

## L1 Anomaly Assessment

| Question | Answer | Basis |
|----------|--------|-------|
| Does H1/L1 DQ difference coincide with trigger? | No — file-wide difference | H1 CW_CAT1=0 over full 4096s |
| Does H1 CW_CAT1=0 explain L1 broadband excess? | No — different detectors | H1 failure says nothing about L1 |
| Does unset NO_CW_HW_INJ explain L1 excess? | No — would be narrow-band | CW inj = single line, not broadband |
| Are CBC DQ flags passing for L1? | YES | CBC_CAT1/2/3 all SET |
| Is L1 broadband excess explained by DQ flags? | NO | No matching flag found |
| Is L1 DQ mapping verified? | YES | All names from HDF5 file |

---

## Final Status

```
DQ_BIT_MAPPING_STATUS:          VERIFIED_FROM_HDF5
NAMES_HARDCODED:                NO (all from HDF5 datasets)
L1_DQ_INTERPRETATION:           NO_FLAG_CONFIRMED
L1_CBC_DQ:                      PASS (CAT1/2/3 all SET)
H1_CW_CAT1:                     FAILS (0% over full file — file-level, not trigger-specific)
L1_CW_CAT1:                     PASSES (100% over full file)
INJECTION_STATUS:               NOT_CERTIFIED_INJECTION_FREE
NO_CW_HW_INJ_BOTH_DETECTORS:   NOT_CERTIFIED (constant over full 4096s — not trigger-specific)
CW_INJ_EXPLAINS_BROADBAND:      NO (CW = narrow-band, not broadband)
L1_BROADBAND_EXCESS_EXPLAINED:  NO
COHERENCE_STATUS:               PARTIAL_L1_ANOMALY
OFFLINE_DQ_NEEDED:              YES (omicron/iDQ for glitch classification)
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```

## Recommended Next Step

```
The GWOSC simple DQ products show L1 passes all CBC quality flags.
The H1/L1 CW_CAT1 difference is file-wide (not trigger-specific).
The NO_CW_HW_INJ status is constant over the entire 4096s file.
None of these explain the L1 broadband power excess.

To resolve the L1 anomaly, offline DQ products are needed:
  - Omicron glitch time-frequency scan
  - iDQ glitch probability at trigger time
  - hveto/UPV correlation with known noise lines

If these are not available in the release:
  -> Submit question to LIGO/GWOSC as documented in
     reports/L1_DQ_FLAG_CHECK_REPORT.md
```
