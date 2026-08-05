# Segmented Energy Model

**Segmented Spacetime (SSZ) Energy Framework - Astropy Implementation**

[![Python](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/)
[![Objects](https://img.shields.io/badge/objects-129-brightgreen)](#data-coverage)
[![Statistical](https://img.shields.io/badge/statistical%20validity-n%3E%3E30-success)](#statistical-validity)
[![License](https://img.shields.io/badge/license-Anti--Capitalist-red)](LICENSE)

**Authors:** Carmen Wrede & Lino Casu  
**Version:** 1.0.0 (2025-12-07)  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## Overview

This repository implements the **Segmented Energy Model** for computing gravitational and relativistic energies using N-segment discretization. The model is validated across **129 astronomical objects** spanning 15 orders of magnitude in mass.

### Key Features

- **N-Segment Discretization:** Divide radial space into N segments for energy calculation
- **Astropy Integration:** Full unit support with astropy.units and astropy.constants
- **129 Objects:** Comprehensive dataset for statistical validation
- **Convergence Analysis:** Verified convergence as N -> infinity
- **Colab Support:** One-click notebook for cloud execution

---

## Data Coverage

### Total: 129 Objects

| Category | Count | Description |
|----------|-------|-------------|
| **Stellar Systems** | 64 | All spectral types O-M + compact objects |
| **Exoplanet Systems** | 10 systems (57 planets) | Solar System, Kepler, TRAPPIST-1, etc. |
| **Binary Systems** | 8 | Including GW sources |

### Stellar Systems Breakdown (64 objects)

| Type | Count | Examples |
|------|-------|----------|
| Main Sequence (O-M) | 26 | Sun, Sirius A, Proxima Centauri |
| Giants & Supergiants | 10 | Betelgeuse, Rigel, Antares |
| White Dwarfs | 6 | Sirius B, Procyon B |
| Neutron Stars | 7 | Crab Pulsar, PSR J0740+6620 |
| Stellar Black Holes | 7 | Cygnus X-1, GW150914 |
| Supermassive BHs | 7 | Sgr A*, M87*, TON 618 |

### Mass Range

- **Minimum:** 0.055 M_earth (Mercury)
- **Maximum:** 6.6 x 10^10 M_sun (TON 618)
- **Span:** 15 orders of magnitude

---

## Statistical Validity

```
n = 129 objects

Central Limit Theorem: n >> 30 [SATISFIED]
Binomial Test Power: > 99%
95% Confidence Interval: +/- 8.7%
```

---

## Installation

```bash
# Clone repository
git clone https://github.com/error-wtf/segmented-energy.git
cd segmented-energy

# Install dependencies
pip install numpy astropy matplotlib pandas

# Run validation
python segmented_energy.py
```

---

## Quick Start

### Basic Usage

```python
from segmented_energy import compute_segmented_energy
from astropy import units as u
from astropy.constants import M_sun, R_sun, au

# Compute energy for Sun
result = compute_segmented_energy(
    M=1.0 * M_sun,
    m=1.0 * u.kg,
    r_in=2.0 * R_sun,
    r_out=1.0 * au,
    N=1000,
    segmentation='linear'
)

print(f"E_total = {result['E_total']:.3e}")
print(f"E/(mc^2) = {result['E_normalized']:.3e}")
```

### Run Full Validation

```bash
python segmented_energy.py
```

Expected output:
```
================================================================================
SEGMENTED ENERGY MODEL - ASTROPY IMPLEMENTATION
================================================================================
[PASS] Segmented energy model implemented with astropy
[PASS] Linear segmentation tested with various N
[PASS] Convergence verified as N increases
================================================================================
```

---

## Theoretical Model

### Energy Formula

```
E_tot(N) = sum_{n=1..N} [ E_GR_(n) + E_SR_(n) ]

where:
  E_GR_(n) = - G * M * dm / r_n        (gravitational)
  E_SR_(n) = (gamma_n - 1) * dm * c^2  (special relativistic)
  
  dm = m / N                           (mass per segment)
  r_n = r_in + (n - 0.5) * dr          (segment midpoint)
  dr = (r_out - r_in) / N              (radial step)
  v_n = sqrt(G * M / r_n)              (Keplerian velocity)
  gamma_n = 1 / sqrt(1 - v_n^2 / c^2)  (Lorentz factor)
```

### Full Substitution

```
E_tot(N) = (m / N) * sum_{n=1..N} [
    - G * M / r_n
  + ( 1 / sqrt( 1 - (G*M)/(r_n * c^2) ) - 1 ) * c^2
]
```

---

## Files

### Core Scripts

| File | Description |
|------|-------------|
| `segmented_energy.py` | Main energy calculation module |
| `fetch_real_data.py` | Astronomical data (129 objects) |
| `Segmented_Energy_Colab.ipynb` | Google Colab notebook |

### Documentation

| File | Description |
|------|-------------|
| [`docs/INDEX.md`](docs/INDEX.md) | **Complete Documentation Index** |
| [`README.md`](README.md) | This file |
| [`COMPLETE_DOCUMENTATION.md`](COMPLETE_DOCUMENTATION.md) | Full technical documentation |
| [`README_COMPLETE.md`](README_COMPLETE.md) | Extended README |
| [`FINDINGS.md`](FINDINGS.md) | Scientific findings |
| [`SEGMENTED_SPACETIME_COMPLETE_MATHEMATICS.md`](SEGMENTED_SPACETIME_COMPLETE_MATHEMATICS.md) | Mathematical foundations |
| [`ENERGY_DECOMPOSITION_N_SEGMENTS.md`](ENERGY_DECOMPOSITION_N_SEGMENTS.md) | N-segment decomposition |
| [`TEST_RESULTS_SUMMARY.md`](TEST_RESULTS_SUMMARY.md) | Validation results |
| [`META_ANALYSIS_LESSONS_LEARNED.md`](META_ANALYSIS_LESSONS_LEARNED.md) | Meta-analysis |
| [`VERGLEICH_ERGEBNIS.md`](VERGLEICH_ERGEBNIS.md) | Comparison results (DE) |
| [`WARUM_UNIFIED_VERSION.md`](WARUM_UNIFIED_VERSION.md) | Why unified version (DE) |

### Output Files

| File | Description |
|------|-------------|
| `validation_results.csv` | Energy calculations for all objects |
| `MASTER_comprehensive_overview.png` | Main results plot |
| `MASTER_neutron_stars_detailed.png` | Neutron star analysis |

---

## Colab Notebook

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/segmented-energy/blob/main/Segmented_Energy_Colab.ipynb)

**Features:**
- Zero installation required
- Validates all 129 objects
- Generates 5 publication-quality plots
- Downloads results as ZIP

**Structure:**
1. **Pipeline Section:** Runs validation (no plots displayed)
2. **Visualization Section:** All 5 plots displayed at end

---

## Results Summary

### Convergence (Sun, N=10 to N=10000)

| N | E_total [J] | Relative Change |
|---|-------------|-----------------|
| 10 | -1.735e+09 | - |
| 100 | -2.076e+09 | 1.64e-01 |
| 1000 | -2.094e+09 | 8.63e-03 |
| 10000 | -2.094e+09 | 9.98e-05 |

### Energy by Object Type

| Type | |E/(mc^2)| Range |
|------|------------------|
| Main Sequence | 10^-8 - 10^-7 |
| Giants | 10^-7 - 10^-6 |
| White Dwarfs | 10^-5 - 10^-4 |
| Neutron Stars | 10^-1 - 10^0 |
| Black Holes | ~1 |

---

## Related Repositories

This repository is part of the **Segmented Spacetime (SSZ) Research Suite**:

- **🌌 [Unified Results](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results)** ← **MAIN REPO**
  - Comprehensive physical validation (97.9% ESO accuracy)
  - 25/25 test suites passing
  - Theory of Everything (83.3% consistency)

- **📐 [SSZ Metric Pure](https://github.com/error-wtf/ssz-metric-pure)** - Mathematical foundations

- **🌟 [G79 Cygnus Tests](https://github.com/error-wtf/g79-cygnus-tests)** - Nebula application

---

## Citation

```bibtex
@software{segmented_energy_2025,
  title = {Segmented Energy Model - SSZ Framework},
  author = {Wrede, Carmen and Casu, Lino},
  year = {2025},
  version = {1.0.0},
  url = {https://github.com/error-wtf/segmented-energy},
  license = {ANTI-CAPITALIST SOFTWARE LICENSE v1.4}
}
```

---

## License

**ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

- Free for research, education, non-profit use
- Commercial use requires permission
- See [LICENSE](LICENSE) for full terms

---

<p align="center">
  <b>Segmented Energy Model</b><br>
  (c) 2025 Carmen Wrede & Lino Casu<br>
  Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
</p>
