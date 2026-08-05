# Real Data SSZ Schumann Analysis

**Analysis Date:** 2025-12-08 04:18:54

## Data Summary

- **Period:** 2016-01-01 to 2016-03-30
- **Data Points:** 2,160
- **Calibrated eta_0:** 0.739275

## SSZ Signature Analysis

| Metric | Value |
|--------|-------|
| SSZ Score | 0.1059 |
| Mode Correlation | 0.0108 |
| Mean Spread | 8.4425% |
| Consistent | No |

## Model Fit Results

### Global SSZ Model

- **R²:** 0.0130
- **RMSE:** 0.002132
- **beta_0:** -0.046317
- **beta_1 (F10.7):** -0.000222

### Proxy Correlations

| Proxy | Correlation |
|-------|-------------|
| F107_norm | -0.1095 |
| Kp_norm | -0.0534 |

## Interpretation

```
============================================================
SSZ ANALYSIS INTERPRETATION
============================================================

1. MODE CONSISTENCY (SSZ Signature Test)
----------------------------------------
   Weak mode correlation: 0.011
   -> No clear SSZ signature
   SSZ Score: 0.1059
   Mean spread across modes: 8.443%

2. SEGMENTATION MAGNITUDE
----------------------------------------
   Mean delta_seg: -4.6317%
   Std delta_seg:  0.2147%
   -> Significant segmentation effect (> 1%)

3. IONOSPHERIC PROXY CORRELATIONS
----------------------------------------
   F107_norm: r = -0.1095 (weak)
   Kp_norm: r = -0.0534 (weak)

4. MODEL FIT QUALITY
----------------------------------------
   Global SSZ model R²: 0.0130
   Layered SSZ model R²: 0.0130
   -> Proxies explain little variance

5. CONCLUSION
----------------------------------------
   Results CONSISTENT WITH ZERO SSZ within current sensitivity.
   No significant mode-independent shifts or proxy correlations
   detected at the current measurement precision.

============================================================
```

## Figures

- `fig_real_timeseries.png` - Observed vs classical frequencies
- `fig_real_delta_seg_vs_mode.png` - Delta_seg time series per mode
- `fig_real_mode_consistency.png` - Mode consistency scatter plots
- `fig_real_delta_vs_f107_kp.png` - Delta_seg vs ionospheric proxies
- `fig_real_summary.png` - Summary panel
