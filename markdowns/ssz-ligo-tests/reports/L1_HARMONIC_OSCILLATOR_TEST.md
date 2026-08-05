# L1 Harmonic Oscillator / Resonance Test

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 01:32:12

## Configuration
- Band: 20.0–210.0 Hz
- Trigger window: 4.0s
- Peak threshold: +6.0 dB above local median
- Harmonic tolerance: ±3.0 Hz

## Results

### L1 [TRIGGER]
- Status: **POSSIBLE_HARMONIC_PAIR**
- Peaks: [26.0, 36.0, 41.0, 53.0, 60.0, 120.0]
- Best f0: 26.0 Hz
- Harmonics matched: 2
- Envelope decay: γ=1.764/s  R²=0.604  WEAK_DECAY_HINT

### H1 [TRIGGER]
- Status: **MULTIPLE_PEAKS_NO_HARMONIC_PATTERN**
- Peaks: [22.0, 28.0, 40.0]
- Best f0: 22.0 Hz
- Harmonics matched: 1
- Envelope decay: γ=0.983/s  R²=0.261  NO_CLEAR_DECAY

### L1 [OFF_SOURCE]
- Status: **MULTIPLE_PEAKS_NO_HARMONIC_PATTERN**
- Peaks: [27.0, 41.0, 60.0]
- Best f0: 27.0 Hz
- Harmonics matched: 1
- Envelope decay: γ=0.041/s  R²=0.013  NO_CLEAR_DECAY

### H1 [OFF_SOURCE]
- Status: **MULTIPLE_PEAKS_NO_HARMONIC_PATTERN**
- Peaks: [24.0, 32.0]
- Best f0: 24.0 Hz
- Harmonics matched: 1
- Envelope decay: γ=0.079/s  R²=0.063  NO_CLEAR_DECAY

## Cross-Detector
- L1 trigger peaks: [26, 36, 41, 53, 60, 120]
- H1 trigger peaks: [22, 28, 40]
- Shared: []
- L1-only: [26, 36, 41, 53, 60, 120]
- L1 off-source peaks: [27, 41, 60]
- Peaks also in off-source: [41, 60]

## OVERALL STATUS: RESONANCE_IN_OFF_SOURCE_TOO

## Anti-Circularity
- No SSZ parameters used
- No posterior data used
- No claim made
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
