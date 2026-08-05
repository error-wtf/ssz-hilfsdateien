# L1/H1 Gaussianity Test

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️

Generated: 2026-05-19 01:34:31

## Configuration
- Trigger GPS: 1411261107.984
- Window: 4.0s
- PSD source: -500.0s x 64.0s
- Band tested: 20.0-210.0 Hz
- Whitening: divide FFT by sqrt(PSD*fs/2)

## Results

| H1 | TRIGGER | FULLBAND | sigma=1.000 | ex_kurt=-1.268 | |z|>4: 0 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(-1.27),AD_FAIL,KS_FAI |
| H1 | TRIGGER | 20.0-210.0Hz | sigma=1.000 | ex_kurt=+2.605 | |z|>4: 36 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(+2.61),EXCESS_OUTLIER |
| H1 | OFF_m500 | FULLBAND | sigma=1.000 | ex_kurt=-1.409 | |z|>4: 0 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(-1.41),AD_FAIL,KS_FAI |
| H1 | OFF_m500 | 20.0-210.0Hz | sigma=1.000 | ex_kurt=+6.375 | |z|>4: 91 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(+6.37),EXCESS_OUTLIER |
| H1 | OFF_m300 | FULLBAND | sigma=1.000 | ex_kurt=-1.408 | |z|>4: 0 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(-1.41),AD_FAIL,KS_FAI |
| H1 | OFF_m300 | 20.0-210.0Hz | sigma=1.000 | ex_kurt=+6.334 | |z|>4: 91 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(+6.33),EXCESS_OUTLIER |
| L1 | TRIGGER | FULLBAND | sigma=1.000 | ex_kurt=+0.618 | |z|>4: 6 (exp 1) | AD: FAIL | NON_GAUSSIAN:EXCESS_OUTLIERS_4s(6vs1),AD_FAIL,KS_F |
| L1 | TRIGGER | 20.0-210.0Hz | sigma=1.000 | ex_kurt=+4.582 | |z|>4: 74 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(+4.58),EXCESS_OUTLIER |
| L1 | OFF_m500 | FULLBAND | sigma=1.000 | ex_kurt=+0.585 | |z|>4: 4 (exp 1) | AD: FAIL | NON_GAUSSIAN:EXCESS_OUTLIERS_4s(4vs1),AD_FAIL,KS_F |
| L1 | OFF_m500 | 20.0-210.0Hz | sigma=1.000 | ex_kurt=+2.856 | |z|>4: 66 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(+2.86),EXCESS_OUTLIER |
| L1 | OFF_m300 | FULLBAND | sigma=1.000 | ex_kurt=+0.617 | |z|>4: 6 (exp 1) | AD: FAIL | NON_GAUSSIAN:EXCESS_OUTLIERS_4s(6vs1),AD_FAIL,KS_F |
| L1 | OFF_m300 | 20.0-210.0Hz | sigma=1.000 | ex_kurt=+4.560 | |z|>4: 75 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(+4.56),EXCESS_OUTLIER |
| L1 | OFF_m100 | FULLBAND | sigma=1.000 | ex_kurt=+0.609 | |z|>4: 6 (exp 1) | AD: FAIL | NON_GAUSSIAN:EXCESS_OUTLIERS_4s(6vs1),AD_FAIL,KS_F |
| L1 | OFF_m100 | 20.0-210.0Hz | sigma=1.000 | ex_kurt=+4.524 | |z|>4: 69 (exp 1) | AD: FAIL | NON_GAUSSIAN:KURTOSIS_EXCESS(+4.52),EXCESS_OUTLIER |

## Anti-Circularity
- No SSZ parameters fitted
- No posterior data used
- READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
