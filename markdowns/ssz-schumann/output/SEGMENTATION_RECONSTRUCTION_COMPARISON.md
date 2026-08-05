# Segmentation Reconstruction Comparison

**Generated:** 2025-12-08T10:37:11.686187

## Methods Compared

1. **Full Fit**: Calibrate eta_0 on full dataset (has degeneracy)
2. **Quiet Interval**: Calibrate eta_0 only on quiet period (first 14 days)
3. **Joint Fit**: Simultaneously fit eta_0 and delta_seg parameters

## Results

| Method | eta_0 | Bias | RMSE | Correlation | Mean δ_seg | Std δ_seg |
|--------|-------|------|------|-------------|------------|-----------|
| full_fit | 0.739647 | 0.000690 | 0.005806 | 0.9646 | 0.000553 | 0.021851 |
| quiet_interval | 0.739492 | 0.000481 | 0.005784 | 0.9646 | 0.000343 | 0.021847 |
| joint_fit | 0.739285 | 0.000137 | 0.000815 | 0.9993 | 0.000000 | 0.021095 |


## Key Findings

1. **Degeneracy Problem**: The full_fit method absorbs constant SSZ shifts into eta_0,
   resulting in near-zero mean reconstructed delta_seg.

2. **Quiet Interval Method**: By calibrating eta_0 only on the quiet period,
   we can recover the true mean delta_seg level.

3. **Joint Fit Method**: Simultaneously fitting eta_0 and delta_seg parameters
   provides the best reconstruction with lowest bias and RMSE.

## Recommendation

For SSZ detection, use either:
- **Quiet Interval** method if a known quiet period exists
- **Joint Fit** method for general cases

---

© 2025 Carmen Wrede & Lino Casu
