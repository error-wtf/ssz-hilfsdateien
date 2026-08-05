# SSZ Schumann Experiment

**Segmented Spacetime (SSZ) Analysis of Schumann Resonances**

[![Tests](https://img.shields.io/badge/tests-94%20passed-brightgreen)]()
[![Python](https://img.shields.io/badge/python-3.10+-blue)]()
[![License](https://img.shields.io/badge/license-Anti--Capitalist-red)]()

A Python package for testing the Segmented Spacetime (SSZ) theory using
Earth-based Schumann resonance measurements.

## Documentation

- **[Quick Start Guide](docs/QUICKSTART.md)** - Get started in 5 minutes
- **[Final Report](docs/FINAL_REPORT.md)** - Complete analysis results
- **[API Reference](docs/API_REFERENCE.md)** - Full API documentation
- **[Theory](docs/THEORY.md)** - Theoretical background
- **[Test Report](docs/TEST_REPORT.md)** - Test results and validation

## Overview

This project applies the SSZ framework to Schumann resonances - electromagnetic
resonances in the Earth-ionosphere cavity. The key SSZ prediction is that
spacetime segmentation introduces a **uniform relative frequency shift** across
all resonance modes, distinct from classical dispersive effects.

### Physical Background

**Classical Schumann Resonances:**
```
f_n = η × c / (2πR) × √(n(n+1))
```
where:
- `n` = mode number (1, 2, 3, ...)
- `η` ≈ 0.74 = effective slowdown factor (due to finite conductivity)
- `c` = speed of light
- `R` = Earth radius

**SSZ Modification:**
```
f_n_SSZ = f_n_classical / D_SSZ
D_SSZ = 1 + δ_seg(t)
```

The **SSZ signature** is that `δ_seg(t)` produces the **same relative shift**
for all modes:
```
Δf_n / f_n ≈ -δ_seg(t)  for all n
```

This is testable: if the relative frequency shifts are consistent across modes
and correlate with ionospheric conditions, it supports the SSZ hypothesis.

## Installation

```bash
# Clone the repository
git clone https://github.com/error-wtf/ssz-schuhman-experiment.git
cd ssz-schuhman-experiment

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
# or: .venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt

# Install package in development mode
pip install -e .
```

## Quick Start

### 1. Run with Synthetic Data

```bash
python scripts/run_schumann_ssz_analysis.py --synthetic
```

This creates synthetic Schumann data with a known SSZ signature and
demonstrates that the analysis pipeline can recover it.

### 2. Fetch Real Data

```bash
python scripts/fetch_data.py --all
```

This creates info files with instructions for downloading:
- Schumann data from Zenodo (Sierra Nevada ELF station)
- F10.7 solar flux from NOAA
- Kp/Ap indices from GFZ Potsdam

### 3. Run Analysis on Real Data

```bash
python scripts/run_schumann_ssz_analysis.py \
    --schumann-path data/schumann/2016/data.csv \
    --f107-path data/space_weather/f107_noaa.csv \
    --kp-path data/space_weather/kp_ap.csv
```

## Project Structure

```
ssz-schuhman-experiment/
├── ssz_schumann/              # Main package
│   ├── config.py              # Configuration and constants
│   ├── data_io/               # Data loading modules
│   │   ├── schumann_sierra_nevada.py
│   │   ├── schumann_real.py
│   │   ├── space_weather_noaa.py
│   │   ├── lightning_wwlln.py
│   │   └── merge.py
│   ├── models/                # Physical models
│   │   ├── classical_schumann.py
│   │   ├── ssz_correction.py
│   │   ├── layered_ssz.py
│   │   ├── maxwell_schumann.py
│   │   ├── physical_ssz.py
│   │   └── fit_wrappers.py
│   └── analysis/              # Analysis pipeline
│       ├── compute_deltas.py
│       ├── correlation_plots.py
│       ├── regression_models.py
│       ├── spectral_coherence.py
│       ├── model_comparison.py
│       └── model_fits.py
├── tests/                     # Unit tests (94 tests)
├── scripts/                   # CLI scripts
│   ├── run_complete_analysis.py
│   ├── run_full_validation.py
│   ├── run_sensitivity_scan.py
│   └── fetch_zenodo_schumann.py
├── docs/                      # Documentation
└── output/                    # Analysis output
```

## Data Sources

### Schumann Resonance Data
- **Source:** Sierra Nevada ELF Station (Salinas et al., 2022)
- **DOI:** [10.5281/zenodo.6348930](https://doi.org/10.5281/zenodo.6348930)
- **Period:** March 2013 - February 2017
- **Resolution:** 10-minute intervals
- **Parameters:** f1, f2, f3 (frequencies), widths, amplitudes

### Space Weather Data
- **F10.7 Solar Flux:** NOAA SWPC
- **Kp/Ap Index:** GFZ Potsdam

## Key Results

The analysis produces:

1. **Mode Consistency Score:** Measures how well δ_seg is consistent across modes
   - Score > 0.7: Strong SSZ signature
   - Score < 0.3: No SSZ signature detected

2. **Model Comparison:** Classical vs. SSZ model
   - ΔR²: Improvement in explained variance
   - ΔAIC/BIC: Information criteria comparison

3. **Correlation Analysis:** δ_seg vs. ionospheric proxies
   - F10.7 (solar activity)
   - Kp (geomagnetic activity)

## Running Tests

```bash
# Run all tests (94 tests)
pytest tests/ -v

# Run full validation suite
python scripts/run_full_validation.py

# Run complete analysis with synthetic data
python scripts/run_complete_analysis.py --synthetic --delta-seg-amp 0.03

# Run sensitivity scan
python scripts/run_sensitivity_scan.py --amplitudes 0.0 0.01 0.02 0.05 --plot
```

## Validation Results

| Phase | Status |
|-------|--------|
| Unit Tests | **94 passed** |
| Synthetic Validation | PASS |
| Model Comparison | PASS |
| Physical Model | PASS |
| Sensitivity Analysis | PASS |

### Model Comparison (Synthetic Data with 2% SSZ Signal)

| Metric | Classical | SSZ |
|--------|-----------|-----|
| RMSE | 1.05 Hz | **0.44 Hz** |
| R² | 0.96 | **0.99** |
| AIC | 20298 | **7103** |
| BIC | 20305 | **7129** |

**Delta BIC: +13176** -> Very strong evidence for SSZ model

## References

### SSZ Theory
- Wrede, C. & Casu, L. (2025). Segmented Spacetime Theory.
- [SSZ Metric Pure Repository](https://github.com/error-wtf/ssz-metric-pure)
- [SSZ Unified Results](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results)

### Schumann Resonances
- Schumann, W.O. (1952). Über die strahlungslosen Eigenschwingungen einer
  leitenden Kugel, die von einer Luftschicht und einer Ionosphärenhülle
  umgeben ist. Z. Naturforsch., 7a, 149-154.
- Salinas, A. et al. (2022). Schumann resonance data processing programs and
  four-year measurements from Sierra Nevada ELF station. Computers &
  Geosciences, 165, 105148.

## License

Anti-Capitalist Software License v1.4

© 2025 Carmen Wrede & Lino Casu
