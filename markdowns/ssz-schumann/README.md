# SSZ-Schumann: Segmented Spacetime Analysis of Schumann Resonances

[![License: ACSL](https://img.shields.io/badge/License-Anti--Capitalist-red.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Tests: 94 passed](https://img.shields.io/badge/Tests-94%20Passed-brightgreen.svg)](tests/)
[![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-orange.svg)](CONTRIBUTING.md)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/ssz-schumann/blob/main/SSZ_Schumann_Colab.ipynb)

---

## Overview

**SSZ-Schumann** applies the Segmented Spacetime (SSZ) framework to Earth's Schumann resonances - electromagnetic standing waves in the Earth-ionosphere cavity. This project tests whether SSZ theory can explain subtle frequency variations in Schumann resonance measurements.

> **"Schumann resonances as a probe for spacetime segmentation."**

### Key Hypothesis

SSZ theory predicts that spacetime segmentation introduces a **uniform relative frequency shift** across all Schumann resonance modes:

```
Δf_n / f_n ≈ -δ_seg(t)  for all n
```

This is distinct from classical dispersive effects and provides a testable prediction.

---

## Table of Contents

1. [Physical Background](#physical-background)
2. [Installation](#installation)
3. [Data Sources](#data-sources)
4. [Quick Start](#quick-start)
5. [Analysis Pipeline](#analysis-pipeline)
6. [Key Results](#key-results)
7. [Project Structure](#project-structure)
8. [References](#references)
9. [Authors & License](#authors--license)

---

## Physical Background

### Classical Schumann Resonances

The Earth-ionosphere cavity acts as a resonant cavity for extremely low frequency (ELF) electromagnetic waves. The resonance frequencies are:

```
f_n = η × c / (2πR) × √(n(n+1))
```

where:
- `n` = mode number (1, 2, 3, ...)
- `η` ≈ 0.74 = effective slowdown factor
- `c` = speed of light
- `R` = Earth radius

**Typical frequencies:**
| Mode | Classical | Observed |
|------|-----------|----------|
| n=1 | 10.6 Hz | 7.83 Hz |
| n=2 | 18.4 Hz | 14.1 Hz |
| n=3 | 26.0 Hz | 20.3 Hz |

### SSZ Modification

In SSZ theory, the effective speed of light is modified by spacetime segmentation:

```
f_n_SSZ = f_n_classical / D_SSZ
D_SSZ = 1 + δ_seg(t)
```

The **SSZ signature** is that `δ_seg(t)` produces the **same relative shift** for all modes simultaneously. This is testable by analyzing correlations between mode frequencies.

---

## Installation

### Requirements

- Python 3.10+
- NumPy, SciPy, Pandas
- Matplotlib (for visualization)

### Setup

```bash
# Clone the repository
git clone https://github.com/error-wtf/ssz-schumann.git
cd ssz-schumann

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
# or: .venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt

# Install package in development mode
pip install -e .
```

---

## Data Sources

### ⚠️ Important: Data Not Included

Due to licensing and size constraints, **raw data is not included** in this repository. Users must download data themselves from the following sources:

### 1. Schumann Resonance Data

**Source:** Sierra Nevada ELF Station (Salinas et al., 2022)

```bash
# Download from Zenodo
python scripts/fetch_zenodo_schumann.py
```

- **DOI:** [10.5281/zenodo.6348930](https://doi.org/10.5281/zenodo.6348930)
- **Period:** March 2013 - February 2017
- **Resolution:** 10-minute intervals
- **Parameters:** f1, f2, f3 (frequencies), widths, amplitudes

### 2. Space Weather Data

**F10.7 Solar Flux (NOAA):**
```bash
python scripts/fetch_space_weather.py --f107
```
- Source: [NOAA SWPC](https://www.swpc.noaa.gov/products/solar-cycle-progression)

**Kp/Ap Geomagnetic Index (GFZ Potsdam):**
```bash
python scripts/fetch_space_weather.py --kp
```
- Source: [GFZ Potsdam](https://www.gfz-potsdam.de/en/kp-index/)

### 3. All Data at Once

```bash
python scripts/fetch_data.py --all
```

This creates info files with download instructions in `data/`.

---

## Quick Start

### 1. Run with Synthetic Data (No Download Required)

```bash
python scripts/run_schumann_ssz_analysis.py --synthetic
```

This creates synthetic Schumann data with a known SSZ signature and demonstrates that the analysis pipeline can recover it.

### 2. Run with Real Data (After Download)

```bash
python scripts/run_schumann_ssz_analysis.py \
    --schumann-path data/schumann/2016/data.csv \
    --f107-path data/space_weather/f107_noaa.csv \
    --kp-path data/space_weather/kp_ap.csv
```

### 3. Run Full Validation Suite

```bash
python scripts/run_full_validation.py
```

---

## Analysis Pipeline

### Step 1: Data Loading

```python
from ssz_schumann.data_io import load_schumann_data, load_space_weather

schumann = load_schumann_data("data/schumann/2016/")
weather = load_space_weather("data/space_weather/")
```

### Step 2: Compute Relative Frequency Shifts

```python
from ssz_schumann.analysis import compute_relative_shifts

shifts = compute_relative_shifts(schumann)
# Returns: δf_1/f_1, δf_2/f_2, δf_3/f_3
```

### Step 3: Test Mode Consistency

```python
from ssz_schumann.analysis import mode_consistency_score

score = mode_consistency_score(shifts)
# Score > 0.7: Strong SSZ signature
# Score < 0.3: No SSZ signature
```

### Step 4: Model Comparison

```python
from ssz_schumann.models import fit_classical, fit_ssz

classical_fit = fit_classical(schumann)
ssz_fit = fit_ssz(schumann)

# Compare AIC/BIC
print(f"ΔAIC: {classical_fit.aic - ssz_fit.aic}")
```

---

## Key Results

### Synthetic Data Validation

With 2% injected SSZ signal:

| Metric | Classical Model | SSZ Model |
|--------|-----------------|-----------|
| RMSE | 1.05 Hz | **0.44 Hz** |
| R² | 0.96 | **0.99** |
| AIC | 20298 | **7103** |
| BIC | 20305 | **7129** |

**ΔBIC = +13176** → Very strong evidence for SSZ model when signal is present.

### Mode Consistency

The SSZ signature is characterized by:
- High correlation between relative shifts of different modes
- Uniform δ_seg across all frequencies
- Correlation with ionospheric conditions (F10.7, Kp)

---

## Project Structure

```
ssz-schumann/
├── ssz_schumann/              # Main package
│   ├── config.py              # Configuration and constants
│   ├── data_io/               # Data loading modules
│   │   ├── schumann_sierra_nevada.py
│   │   ├── space_weather_noaa.py
│   │   └── merge.py
│   ├── models/                # Physical models
│   │   ├── classical_schumann.py
│   │   ├── ssz_correction.py
│   │   └── physical_ssz.py
│   └── analysis/              # Analysis pipeline
│       ├── compute_deltas.py
│       ├── correlation_plots.py
│       └── model_comparison.py
├── scripts/                   # CLI scripts
│   ├── fetch_data.py          # Download data
│   ├── fetch_zenodo_schumann.py
│   ├── fetch_space_weather.py
│   ├── run_schumann_ssz_analysis.py
│   └── run_full_validation.py
├── tests/                     # Unit tests (94 tests)
├── data/                      # Data directory (user downloads)
│   ├── schumann/              # Schumann resonance data
│   └── space_weather/         # F10.7, Kp indices
├── output/                    # Analysis output
├── requirements.txt           # Dependencies
├── LICENSE                    # Anti-Capitalist License v1.4
└── README.md                  # This file
```

---

## Running Tests

```bash
# Run all tests
pytest tests/ -v

# Run specific test file
pytest tests/test_models.py -v

# Run with coverage
pytest tests/ --cov=ssz_schumann
```

---

## References

### SSZ Theory

1. Wrede, C. & Casu, L. (2025). "Segmented Spacetime: A Discrete Framework for Quantum Gravity" *(in preparation)*
2. [SSZ-Qubits Repository](https://github.com/error-wtf/ssz-qubits)
3. [SSZ Metric Pure Repository](https://github.com/error-wtf/ssz-metric-pure)

### Schumann Resonances

4. Schumann, W.O. (1952). "Über die strahlungslosen Eigenschwingungen einer leitenden Kugel". Z. Naturforsch., 7a, 149-154.
5. Salinas, A. et al. (2022). "Schumann resonance data processing programs and four-year measurements from Sierra Nevada ELF station". Computers & Geosciences, 165, 105148. [DOI: 10.5281/zenodo.6348930](https://doi.org/10.5281/zenodo.6348930)

### Space Weather

6. NOAA Space Weather Prediction Center: [swpc.noaa.gov](https://www.swpc.noaa.gov/)
7. GFZ Potsdam Kp Index: [gfz-potsdam.de](https://www.gfz-potsdam.de/en/kp-index/)

---

## Authors & License

### Authors

**Carmen Wrede** - Theoretical Physics, SSZ Theory  
**Lino Casu** - Implementation, Data Analysis

### Contact

- Email: [mail@error.wtf](mailto:mail@error.wtf)
- GitHub: [github.com/error-wtf](https://github.com/error-wtf)

### License

This project is licensed under the **Anti-Capitalist Software License v1.4**.

See [LICENSE](LICENSE) for the full license text.

---

© 2025 Carmen Wrede & Lino Casu

**"Schumann resonances as a probe for spacetime segmentation."**
