# SSZ Schumann Experiment - Complete Validation Report

**Generated:** 2025-12-08T10:44:55.895525

---

## Executive Summary

This report presents the complete validation of the SSZ (Segmented Spacetime) analysis
pipeline for Schumann resonance data.

### Key Findings

| Metric | Value | Status |
|--------|-------|--------|
| Detection Threshold (95% power) | 1.0% | ✓ |
| Preferred Model | Classical | ✓ |
| Evidence Strength | Weak evidence against | ✓ |
| Mean Mode Coherence | 0.0157 | ✓ |
| Phase Locking Value | 0.8791 | ✓ |

---

## 1. Sensitivity Analysis

The sensitivity analysis determines the minimum detectable SSZ amplitude.

### Results

| Amplitude | Detection Rate | Mean T_SSZ |
|-----------|----------------|------------|
| 0.0% | 5% | 0.0825 |
| 1.0% | 100% | 0.3562 |
| 2.0% | 100% | 0.6418 |
| 3.0% | 100% | 0.7797 |
| 4.0% | 100% | 0.8493 |
| 5.0% | 100% | 0.8887 |


### Detection Statement

**With the current method and 1-year time series, SSZ amplitudes below 1.0% are 
statistically undetectable at 95% confidence (noise level = 1%).**

---

## 2. Multi-Layer SSZ Model

The multi-layer model accounts for different ionospheric layers (D, E, F).

### Fitted Parameters

| Parameter | Value |
|-----------|-------|
| σ₀ (base amplitude) | 0.038894132090154 |
| RMSE | 0.3031 Hz |
| R² | 0.9958 |

---

## 3. Bayesian Model Comparison

### Posterior Probabilities

| Model | Probability |
|-------|-------------|
| Classical | 0.0% |
| SSZ | nan% |
| Layered_SSZ | nan% |


**Preferred Model:** Classical
**Evidence Strength:** Weak evidence against

---

## 4. Spectral Coherence Analysis

### Results

| Metric | Value | Interpretation |
|--------|-------|----------------|
| Mean Mode Coherence | 0.0157 | Low |
| Phase Locking Value | 0.8791 | Strong |

**SSZ Interpretation:** Weak/partial SSZ signature

---

## 5. Reconstruction Method Comparison

| method         |    eta_0 |        bias |        rmse |   correlation |   mean_delta_seg |   std_delta_seg |   amplitude_A |   amplitude_B |
|:---------------|---------:|------------:|------------:|--------------:|-----------------:|----------------:|--------------:|--------------:|
| full_fit       | 0.740431 | 0.000661025 | 0.00578209  |      0.965185 |      0.000523591 |       0.0219604 |   nan         |           nan |
| quiet_interval | 0.740135 | 0.000261008 | 0.00574783  |      0.965185 |      0.000123574 |       0.0219516 |   nan         |           nan |
| joint_fit      | 0.740111 | 0.000137485 | 0.000810025 |      0.999291 |      5.14304e-08 |       0.021172  |     0.0299314 |             0 |

### Recommendation

For SSZ detection, use either:
- **Quiet Interval** method if a known quiet period exists
- **Joint Fit** method for general cases

---

## 6. Conclusions

1. **Detection Capability:** The pipeline can reliably detect SSZ signals above the threshold
2. **Model Selection:** Bayesian comparison identifies the best-fitting model
3. **Coherence Analysis:** Spectral coherence provides additional validation
4. **Reconstruction:** Joint fit provides the most accurate δ_seg reconstruction

---

## Next Steps

1. Apply to real Schumann data from Sierra Nevada station
2. Extend analysis to multiple years
3. Compare with other ELF observatories
4. Prepare publication-ready figures

---

© 2025 Carmen Wrede & Lino Casu
Licensed under the Anti-Capitalist Software License v1.4
