# H1/L1 LONG-BASELINE XCORR EXECUTION REPORT

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

**Generated: 2026-05-19 16:14:02.675242**

## EXECUTED TESTS (With Logs)

### Test 1: Long-Baseline Cross-Correlation
- Status: DONE
- Input: data_manifest/h1_l1_delay_scan.csv (2208 rows)
- Output: data_manifest/h1_l1_long_baseline_xcorr.csv
- Key Finding: max(|corr|) values per window/band computed

### Test 2: Trigger Excess Analysis  
- Status: DONE
- Method: Trigger |corr| minus OFF_m500 |corr|
- Output: data_manifest/h1_l1_trigger_excess.csv
- Critical Finding:
  * 20-40 Hz: +2.09e-05 excess (TRIGGER_SPECIFIC)
  * All other bands: NEGATIVE excess (higher correlation off-source!)

### Test 3: Time-Shift Null Test
- Status: DONE
- Method: Physical delay (|dt|<=10ms) vs Unphysical (|dt|>10ms)
- Output: data_manifest/time_shift_null_test.csv
- Finding: Physical delay preferred by ~0.5 correlation units
- CRITICAL: Both TRIGGER and OFF_m500 show identical pattern

## BLOCKED / INCOMPLETE

### Extended Off-Source Baseline
- Required: 50-100 windows from -1000s to +1000s
- Available: Only 1 window (OFF_m500)
- Status: BLOCKED - insufficient data
- Action needed: Load more GWOSC HDF5 files

### Phase Coherence Analysis
- Status: BLOCKED - phase data not available in current CSV

### Notch-Filter Test
- Status: BLOCKED - requires raw strain access for filtering

## CLASSIFICATION

H1_L1_XCORR_STATUS:             COHERENT_PHYSICAL_DELAY
PHYSICAL_DELAY_PREFERRED:       YES (delta ~0.5)
TRIGGER_SPECIFIC:               NO (both windows identical)
PERSISTENT_COMMON_MODE:         PLAUSIBLE
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO

## INTERPRETATION

The strong H1/L1 anti-correlation (|corr| ~ 0.999) is:
1. Real (not random - disappears with unphysical delays)
2. Not trigger-specific (identical in OFF_m500 window)
3. Likely common-mode environmental noise (Schumann, 60Hz, etc.)

Only 20-40 Hz shows positive trigger excess, but this is based on N=1 off-source comparison.

## NEXT STEPS (If Data Available)

1. Load extended GWOSC baseline (-1000s to +1000s)
2. Build statistical background distribution (50+ windows)
3. Compute proper Z-scores with sigma from distribution
4. Run notch-filter comparison (50/60/100/120/150/180 Hz)
5. Phase-randomization null test

## FILES GENERATED

- data_manifest/h1_l1_long_baseline_xcorr.csv
- data_manifest/h1_l1_trigger_excess.csv
- data_manifest/time_shift_null_test.csv
- GitHub commits: e43657a, 41558f5

## NO CLAIMS MADE

- SSZ support: NO
- SSZ falsification: NO
- LIGO data integrity challenged: NO
- Physical signal detection: NO

Status: Pipeline functional, data quality limited, claims blocked.
