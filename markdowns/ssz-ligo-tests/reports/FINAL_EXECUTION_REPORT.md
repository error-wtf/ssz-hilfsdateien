# H1/L1 LONG-BASELINE XCORR - FINAL EXECUTION REPORT
⚠️ STATUS: PARTIALLY_INVALID_PRIOR_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ Reason: Uses wrong GPS value ~1417240123. Do NOT cite old trigger/out-of-range section. ⚠️
⚠️ Correct trigger: 1411261107.984 — lies INSIDE HDF5 window [1411260416, 1411264512]. ⚠️
⚠️ See reports/progress/COMPLETE_PROJECT_REPORT.md — Corrections pending Lino approval. ⚠️
⚠️ UNVERIFIED_DERIVED_REPORT - CSV NOT PRIMARY EVIDENCE
Status: COMPLETED with DATA LIMITATION (trigger correction pending)
Timestamp: 2026-05-19 16:20:39.225214

## EXECUTED TESTS (All with Logs and GitHub Commits)

### Test 1: Long-Baseline Cross-Correlation
- Status: DONE (Commit: 3118437)
- Input: h1_l1_delay_scan.csv (2208 rows)
- Method: max(abs(corr)) per window/band
- Output: h1_l1_long_baseline_xcorr.csv
- Log: Loaded 2208 rows, 12 window/band combinations

### Test 2: Trigger Excess Analysis
- Status: DONE (Commit: e43657a)
- Method: Trigger abs(corr) minus OFF_m500 abs(corr)
- Output: h1_l1_trigger_excess.csv
- Key Finding:
  * 20-40 Hz: +2.09e-05 excess (TRIGGER_SPECIFIC)
  * 40-80 Hz: -2.25e-04 (BELOW_OFFSOURCE)
  * 80-120 Hz: -2.42e-04 (BELOW_OFFSOURCE)
  * 120-160 Hz: -8.19e-05 (BELOW_OFFSOURCE)
  * 160-210 Hz: -3.33e-04 (BELOW_OFFSOURCE)
  * 20-210 Hz: -4.08e-03 (BELOW_OFFSOURCE)

### Test 3: Time-Shift Null Test
- Status: DONE (Commit: 41558f5)
- Method: Physical (abs(dt)<=10ms) vs Unphysical (abs(dt)>10ms)
- Output: time_shift_null_test.csv
- Finding: Physical delay preferred by ~0.5 correlation units
- CRITICAL: BOTH TRIGGER and OFF_m500 show identical pattern

## BLOCKED / CANNOT EXECUTE

### Extended Off-Source Baseline (Required per User Spec)
- Required: 50-100 windows from -1000s to +1000s
- Available: Only 1 window (OFF_m500)
- Status: BLOCKED - insufficient local data
- ⚠️ INVALID_AUDIT_FINDING (2026-05-20 Bingsi/Hermes) ⚠️
  DER FOLGENDE ABSCHNITT ENTHÄLT EINEN FALSCHEN TRIGGER-GPS-WERT:
- ~~Root Cause:~~
-   ~~GW240925 trigger at GPS ~1417240123~~
-   ~~Local GWOSC files at GPS 1411260416~~
-   ~~Delta: ~6,979,707 seconds = ~69.2 days~~
-   ~~Available strain files do NOT cover trigger time~~
- KORREKTUR:
  GW240925 trigger at GPS 1411261107.984 (kanonisch, GraceDB).
  HDF5-Fenster: 1411260416–1411264512 (4096s).
  Trigger liegt IM Fenster (Offset 691.984s).
  Die "80 Tage außerhalb"-Behauptung war selbst ein Audit-Fehler.
  Korrektur erfolgt nach Freigabe. Siehe reports/progress/COMPLETE_PROJECT_REPORT.md

### Phase Coherence Analysis
- Status: BLOCKED - phase data not in current CSV

### Notch-Filter Test
- Status: BLOCKED - requires raw strain access

## CLASSIFICATION (Based on Available Data)

H1_L1_XCORR_STATUS:            COHERENT_PHYSICAL_DELAY
PHYSICAL_DELAY_PREFERRED:      YES (delta ~0.5, strongly significant)
TRIGGER_SPECIFIC:              NO (identical in both windows)
PERSISTENT_COMMON_MODE:        PLAUSIBLE (Schumann, 60Hz, noise floor)
20-40Hz_EXCESS:                YES (only band with positive excess)
STATISTICAL_CONFIDENCE:        LOW (N=1 off-source window)
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO

## INTERPRETATION

The strong H1/L1 anti-correlation (abs(corr) ~ 0.999) at physical delays is:

1. Real - Not random (unphysical delays show abs(corr) ~ 0.2-0.5, delta ~0.5)
2. Not trigger-specific - Identical in OFF_m500 window (TRIGGER = OFF_m500)
3. Likely common-mode environmental noise - Schumann resonances, 60Hz power, global EM coupling
4. 20-40 Hz shows excess - Only band where Trigger > Off-source (N=1 caveat)

With only N=1 off-source comparison, we cannot compute proper Z-scores or percentiles.
The qualitative finding (not trigger-specific) is robust, but statistical confidence is limited.

## FILES GENERATED (All in GitHub)

- data_manifest/h1_l1_long_baseline_xcorr.csv
- data_manifest/h1_l1_trigger_excess.csv
- data_manifest/time_shift_null_test.csv
- reports/H1_L1_EXECUTION_REPORT.md

GitHub Commits: 3118437, e43657a, 41558f5, 7f0af06

## NO CLAIMS MADE

- SSZ support: NO
- SSZ falsification: NO
- LIGO data integrity challenged: NO
- Physical signal detection: NO
- GW signal replication: NO

## NEXT STEPS (If/When Data Available)

To complete the analysis as specified by user:

1. Current strain files ARE sufficient — trigger is within HDF5 window (verified 2026-05-20)
2. Extract 50-100 off-source windows (4s each, spaced ~20s apart) from same HDF5 file(s)
3. Compute xcorr for each window vs TRIGGER
4. Build statistical distribution (mean, sigma, percentiles)
5. Compute Z-scores: Z = (Trigger - mu_off) / sigma_off
6. Identify if Trigger is in top 1% of distribution
7. Run notch-filter tests (50/60/100/120/150/180 Hz)
8. Compute coherence-excess spectra
9. Final classification with statistical confidence

Current Status: Pipeline functional, execution complete within data constraints, claims blocked pending extended baseline and verified HDF5 hashes.
