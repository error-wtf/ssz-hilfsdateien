# SSZ-Lensing

## Radial Scaling Gauge Validation Suite

> ### 🚀 [**Try it Online! → Launch Gradio Demo**](https://colab.research.google.com/github/error-wtf/ssz-lensing/blob/main/SSZ_Lensing_Colab.ipynb)
> 
> Run the full lensing analysis in your browser - no installation needed!

---

[![Tests](https://img.shields.io/badge/tests-28%2F28-brightgreen)](https://github.com/error-wtf/ssz-lensing)
[![Pass Rate](https://img.shields.io/badge/pass%20rate-100%25-brightgreen)](https://github.com/error-wtf/ssz-lensing)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-ACSL%201.4-orange)](LICENSE.md)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/ssz-lensing/blob/main/SSZ_Lensing_Colab.ipynb)

**Paper:** *Radial Scaling Gauge for Maxwell Fields*

**Authors:** Carmen N. Wrede & Lino P. Casu

---

## Overview

Comprehensive validation suite for the **Radial Scaling Gauge** framework from the SSZ (Segmented Spacetime) theory. This repository tests gravitational lensing, Shapiro delay, and redshift predictions against experimental data.

**Key Result: 28/28 tests pass (100%) - NO FITTING**

## Core Physics

### The Radial Scaling Gauge

Gravitational effects are described by a single scaling function:

```
s(r) = 1 + Xi(r) = 1 + r_s/(2r)
```

Where:
- `Xi(r)` = Segment density (gravitational potential proxy)
- `r_s = 2GM/c²` = Schwarzschild radius
- `s(r)` = Physical distance scaling factor

### Key Formulas

| Observable | Formula | Test |
|------------|---------|------|
| Time Dilation | `D(r) = 1/(1 + Xi)` | GPS, Pound-Rebka |
| Shapiro Delay | `dt = (r_s/c) * ln(4*r1*r2/r_min²)` | Cassini 2003 |
| Light Deflection | `delta = (1+gamma)*r_s/b` | 1919 Eclipse |
| Redshift | `z = Xi(r1) - Xi(r2)` | Tokyo Skytree |

## Test Results Summary

| Section | Tests | Status |
|---------|-------|--------|
| Section 2: Radial Scaling | 8 | PASS |
| Section 3: EM Phase | 7 | PASS |
| Appendix A.1: Shapiro Delay | 3 | PASS |
| Appendix A.2: Lensing | 3 | PASS |
| Appendix B: WKB Phase | 2 | PASS |
| Frame Consistency | 2 | PASS |
| Experimental Validation | 3 | PASS |
| **TOTAL** | **28** | **100%** |

## Experimental Validation

### Shapiro Delay (Cassini 2003)
- **Measured:** gamma = 1.000021 ± 2.3e-5
- **Our prediction:** Matches GR (gamma = 1)
- **Delay:** ~265 microseconds

### Light Deflection (Solar Limb)
- **1919 Eclipse:** 1.75 arcseconds
- **Our prediction:** 1.75 arcseconds
- **Agreement:** < 1%

### Gravitational Redshift
- **Pound-Rebka (22.5m):** 2.46e-15 ✓
- **GPS (20,200 km):** 45.7 us/day ✓
- **Tokyo Skytree (450m):** 4.9e-14 ✓

## Project Structure

```
ssz-lensing/
├── tests/
│   └── test_radial_scaling_gauge.py   # 28 comprehensive tests
├── plots/
│   ├── generate_plots.py              # Visualization generator
│   └── *.png                          # 7 plots
├── notebooks/
│   └── radial_scaling_gauge_colab.ipynb  # Interactive notebook
├── test-reports/
│   ├── RADIAL_SCALING_GAUGE_REPORT.md
│   └── radial_scaling_gauge_results.json
├── LICENSE.md                         # ACSL v1.4
└── README.md
```

## Quick Start

### Run Tests

```bash
cd tests
python test_radial_scaling_gauge.py
```

### Generate Plots

```bash
cd plots
python generate_plots.py
```

### Open in Colab

Click the Colab badge above or visit:
[Open Notebook](https://colab.research.google.com/github/error-wtf/ssz-lensing/blob/main/notebooks/radial_scaling_gauge_colab.ipynb)

## Requirements

```bash
pip install numpy matplotlib
```

## Key Insight: No Fitting Required

All experimental predictions emerge directly from:

```
Xi(r) = r_s / (2r)
```

This single formula, derived from SSZ principles, reproduces:
- Shapiro delay measurements
- Gravitational lensing angles
- Clock comparison experiments
- GPS relativistic corrections

**No free parameters. No curve fitting. Pure physics.**

## License

Anti-Capitalist Software License v1.4

See [LICENSE.md](LICENSE.md) for details.

## Authors

- **Carmen N. Wrede**
- **Lino P. Casu**

## Repository

https://github.com/error-wtf/ssz-lensing
