# OFFSOURCE_BACKGROUND_TEST — SSZ-LIGO AUDIT
**Date:** 2026-05-21

## Metadata
- **SSZ_FORWARD_MODE:** DERIVED_V1
- **V0_FALLBACK_USED:** NO
- **Trigger GPS:** 1411261107.984
- **Number of Off-source Windows:** 50 (excl. $\pm 64$ s buffer around trigger)

## Background Distribution Stats

| Det | Trigger SNR GR (Pct) | Trigger SNR SSZ (Percentile) | Offsource SNR GR (Max) | Offsource SNR SSZ (Max) |
|-----|----------------------|------------------------------|------------------------|-------------------------|
| H1  | 39.45 (6.5%)         | 12.72 (19.4%)                | 712.33 (1714.76)       | 75.14 (194.22)          |
| L1  | 653.95 (56.0%)       | 16.09 (56.0%)                | 616.95 (2160.13)       | 18.69 (71.25)           |
| V1  | 19.25 (56.0%)        | 55.93 (46.0%)                | 22.86 (109.71)         | 92.87 (400.05)          |

## Subband Diagnostics (L1 Anomalies)

Livingston (L1) sub-band background metrics verify that its extremely high trigger SNR is **not trigger-specific**, but rather a persistent feature of the noise floor and whitening calibration in O4b:

- **L1 20-100 Hz (Low-Frequency Noise):**
  - Trigger SSZ SNR: 436.96
  - Offsource SSZ Mean (Max): 437.13 (1482.36)
- **L1 400-800 Hz (HF Noise / Calibration):**
  - Trigger SSZ SNR: 4417.03
  - Offsource SSZ Mean (Max): 4066.61 (14422.00)

## Scientific Verdict

> **The off-source background test shows that the extreme L1 SSZ-SNR metric in the 20–100 Hz band is not trigger-specific. The trigger value lies at the off-source background mean. Therefore, this L1 metric is DQ-blocked for any physical SSZ interpretation.**
>
> *Der Off-source-Hintergrundtest zeigt, dass die extreme L1-SSZ-SNR-Metrik im 20–100-Hz-Band nicht trigger-spezifisch ist. Der Triggerwert liegt praktisch auf dem Off-source-Hintergrundmittel. Daher ist diese L1-Metrik für jede physikalische SSZ-Interpretation DQ-blockiert.*

## Diagnostic Decisions

- **OFFSOURCE_BACKGROUND_STATUS:** PASS
- **H1_TRIGGER_SPECIFIC:** NO
- **L1_TRIGGER_SPECIFIC:** NO
- **V1_TRIGGER_SPECIFIC:** NO
- **L1_PERSISTENT_NOISE:** YES (High background SNRs confirm persistent non-Gaussianities)
- **DQ_CONTEXT_REQUIRED:** YES (Any interpretation is blocked without complete detector DQ data)
- **CLAIM_LEVEL_LIGO:** NO
