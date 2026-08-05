# SSZ Schumann - API Reference

**Complete API documentation for the ssz_schumann package**

---

## Table of Contents

1. [Configuration](#1-configuration)
2. [Data I/O](#2-data-io)
3. [Classical Model](#3-classical-model)
4. [SSZ Correction](#4-ssz-correction)
5. [Layered SSZ Model](#5-layered-ssz-model)
6. [Analysis Functions](#6-analysis-functions)

---

## 1. Configuration

### Module: `ssz_schumann.config`

Physical constants used throughout the package.

```python
from ssz_schumann.config import PHI, C_LIGHT, EARTH_RADIUS, ETA_0_DEFAULT
```

| Constant | Value | Description |
|----------|-------|-------------|
| `PHI` | 1.618034 | Golden ratio (1+sqrt(5))/2 |
| `C_LIGHT` | 299792458 | Speed of light (m/s) |
| `EARTH_RADIUS` | 6.371e6 | Earth radius (m) |
| `ETA_0_DEFAULT` | 0.74 | Default slowdown factor |

---

## 2. Data I/O

### Module: `ssz_schumann.data_io`

#### 2.1 Schumann Data

```python
from ssz_schumann.data_io.schumann_sierra_nevada import (
    load_sierra_nevada_data,
    create_synthetic_schumann_data,
)
```

##### `create_synthetic_schumann_data`

Generate synthetic Schumann resonance data for testing.

```python
def create_synthetic_schumann_data(
    start: str = "2016-01-01",
    end: str = "2016-12-31",
    freq: str = "1h",
    eta_0: float = 0.74,
    delta_seg_amplitude: float = 0.02,
    noise_level: float = 0.01,
) -> xr.Dataset:
```

**Parameters:**
- `start`: Start date (ISO format)
- `end`: End date (ISO format)
- `freq`: Time resolution (pandas freq string)
- `eta_0`: Classical slowdown factor
- `delta_seg_amplitude`: Amplitude of SSZ variation
- `noise_level`: Gaussian noise level

**Returns:** xarray Dataset with f1, f2, f3 time series

**Example:**
```python
ds = create_synthetic_schumann_data(
    start="2016-01-01",
    end="2016-06-30",
    delta_seg_amplitude=0.015,
    noise_level=0.008,
)
```

#### 2.2 Space Weather Data

```python
from ssz_schumann.data_io.space_weather_noaa import (
    load_f107_noaa,
    load_kp_gfz,
    create_synthetic_space_weather,
)
```

##### `create_synthetic_space_weather`

Generate synthetic F10.7 and Kp data.

```python
def create_synthetic_space_weather(
    start: str,
    end: str,
) -> Tuple[pd.Series, pd.Series]:
```

**Returns:** Tuple of (f107_series, kp_series)

#### 2.3 Data Merging

```python
from ssz_schumann.data_io.merge import merge_all
```

##### `merge_all`

Merge Schumann, F10.7, and Kp data onto common time grid.

```python
def merge_all(
    schumann_ds: xr.Dataset,
    f107: pd.Series,
    kp: pd.Series,
    time_resolution: str = "1h",
) -> xr.Dataset:
```

**Returns:** Merged xarray Dataset with all variables

---

## 3. Classical Model

### Module: `ssz_schumann.models.classical_schumann`

```python
from ssz_schumann.models.classical_schumann import (
    f_n_classical,
    f_n_classical_timeseries,
    compute_eta0_from_mean_f1,
    schumann_mode_factor,
)
```

#### `f_n_classical`

Calculate classical Schumann frequency for mode n.

```python
def f_n_classical(
    n: int,
    eta: float = ETA_0_DEFAULT,
    R: float = EARTH_RADIUS,
    c: float = C_LIGHT,
) -> float:
```

**Parameters:**
- `n`: Mode number (1, 2, 3, ...)
- `eta`: Slowdown factor
- `R`: Earth radius (m)
- `c`: Speed of light (m/s)

**Returns:** Frequency in Hz

**Example:**
```python
f1 = f_n_classical(1)  # 7.83 Hz
f2 = f_n_classical(2)  # 13.56 Hz
```

#### `compute_eta0_from_mean_f1`

Calibrate eta from observed mean f1.

```python
def compute_eta0_from_mean_f1(f1_mean: float) -> float:
```

**Example:**
```python
eta = compute_eta0_from_mean_f1(7.85)  # ~0.742
```

#### `schumann_mode_factor`

Calculate sqrt(n*(n+1)) for mode n.

```python
def schumann_mode_factor(n: int) -> float:
```

---

## 4. SSZ Correction

### Module: `ssz_schumann.models.ssz_correction`

```python
from ssz_schumann.models.ssz_correction import (
    D_SSZ,
    delta_seg_from_observed,
    check_mode_consistency,
    fit_delta_seg_simple,
    f_n_ssz_model,
)
```

#### `D_SSZ`

Calculate SSZ correction factor.

```python
def D_SSZ(delta_seg: ArrayLike) -> ArrayLike:
    """D_SSZ = 1 + delta_seg"""
```

#### `delta_seg_from_observed`

Extract delta_seg from observed frequencies.

```python
def delta_seg_from_observed(
    f_obs: ArrayLike,
    f_classical: ArrayLike,
) -> ArrayLike:
    """delta_seg = f_classical / f_obs - 1"""
```

**Example:**
```python
delta_seg = delta_seg_from_observed(7.80, 7.83)  # ~0.0038
```

#### `check_mode_consistency`

Check if delta_seg is consistent across modes (SSZ signature).

```python
def check_mode_consistency(
    delta_seg_dict: Dict[int, ArrayLike],
    tolerance: float = 0.01,
) -> Dict[str, float]:
```

**Returns:** Dictionary with:
- `mean_delta_seg`: Mean across all modes
- `std_delta_seg`: Std across modes
- `mean_correlation`: Average correlation between modes
- `ssz_score`: SSZ signature score (0-1)
- `is_consistent`: Boolean

**Example:**
```python
result = check_mode_consistency({1: ds1, 2: ds2, 3: ds3})
print(f"SSZ score: {result['ssz_score']:.3f}")
```

#### `f_n_ssz_model`

Calculate SSZ-corrected frequency.

```python
def f_n_ssz_model(
    f_n_classical: ArrayLike,
    delta_seg: ArrayLike,
) -> ArrayLike:
```

---

## 5. Layered SSZ Model

### Module: `ssz_schumann.models.layered_ssz`

```python
from ssz_schumann.models.layered_ssz import (
    LayerConfig,
    LayeredSSZConfig,
    D_SSZ_layered,
    D_SSZ_from_sigmas,
    f_n_classical,
    f_n_ssz_layered,
    compute_all_modes,
    sigma_from_phi_ratio,
    phi_segment_density,
    create_phi_based_config,
    sigma_iono_from_proxy,
    f_n_ssz_timeseries,
    fit_layered_ssz,
    frequency_shift_estimate,
    print_frequency_table,
)
```

#### `LayerConfig`

Configuration for a single atmospheric layer.

```python
@dataclass
class LayerConfig:
    name: str
    weight: float      # w_j: contribution to wave propagation
    sigma: float = 0.0 # sigma_j: segmentation parameter
    height_km: float = 0.0
```

#### `LayeredSSZConfig`

Configuration for the complete layered model.

```python
@dataclass
class LayeredSSZConfig:
    ground: LayerConfig      # w=0.0
    atmosphere: LayerConfig  # w=0.2
    ionosphere: LayerConfig  # w=0.8
    eta_0: float = 0.74
    f1_ref: float = 7.83
```

**Example:**
```python
config = LayeredSSZConfig()
config.ionosphere.sigma = 0.01  # 1% segmentation
```

#### `D_SSZ_layered`

Calculate layered SSZ correction factor.

```python
def D_SSZ_layered(config: LayeredSSZConfig) -> float:
    """D_SSZ = 1 + sum_j(w_j * sigma_j)"""
```

#### `D_SSZ_from_sigmas`

Convenience function for D_SSZ calculation.

```python
def D_SSZ_from_sigmas(
    sigma_ground: float = 0.0,
    sigma_atm: float = 0.0,
    sigma_iono: float = 0.0,
    w_ground: float = 0.0,
    w_atm: float = 0.2,
    w_iono: float = 0.8,
) -> float:
```

#### `f_n_ssz_layered`

Calculate SSZ-corrected frequency with layered model.

```python
def f_n_ssz_layered(
    n: int,
    config: LayeredSSZConfig,
) -> float:
```

**Example:**
```python
config = LayeredSSZConfig()
config.ionosphere.sigma = 0.01
f1 = f_n_ssz_layered(1, config)  # ~7.77 Hz
```

#### `compute_all_modes`

Compute frequencies for all modes at once.

```python
def compute_all_modes(
    config: LayeredSSZConfig,
    modes: List[int] = [1, 2, 3],
) -> Dict[int, Dict[str, float]]:
```

**Returns:** Dictionary with f_classical, f_ssz, delta_f, relative_shift for each mode

#### `sigma_iono_from_proxy`

Calculate ionosphere sigma from proxy.

```python
def sigma_iono_from_proxy(
    F_iono: ArrayLike,
    beta_0: float = 0.0,
    beta_1: float = 0.01,
) -> ArrayLike:
    """sigma_iono = beta_0 + beta_1 * F_iono"""
```

#### `f_n_ssz_timeseries`

Calculate frequency time series.

```python
def f_n_ssz_timeseries(
    n: int,
    sigma_iono_t: ArrayLike,
    sigma_atm: float = 0.0,
    w_atm: float = 0.2,
    w_iono: float = 0.8,
    f1_ref: float = 7.83,
) -> ArrayLike:
```

#### `frequency_shift_estimate`

Estimate frequency shifts for given delta_seg.

```python
def frequency_shift_estimate(
    delta_seg_eff: float,
    f_ref: float = 7.83,
) -> Dict[str, float]:
```

**Returns:** Dictionary with f1_classical, f1_ssz, delta_f1, etc.

#### `print_frequency_table`

Print formatted frequency shift table.

```python
def print_frequency_table(
    delta_seg_values: List[float] = [0.0, 0.005, 0.01, 0.02],
    f_ref: float = 7.83,
):
```

---

## 6. Analysis Functions

### Module: `ssz_schumann.analysis`

```python
from ssz_schumann.analysis.compute_deltas import compute_all_deltas
from ssz_schumann.analysis.correlation_plots import create_correlation_plots
from ssz_schumann.analysis.regression_models import fit_regression_model
```

#### `compute_all_deltas`

Compute delta_seg for all modes in dataset.

```python
def compute_all_deltas(
    ds: xr.Dataset,
    eta_0: float = None,
) -> xr.Dataset:
```

**Returns:** Dataset with added delta_seg_1, delta_seg_2, delta_seg_3 variables

---

## Quick Reference

### Frequency Calculation

```python
# Classical
f1 = f_n_classical(1)  # 7.83 Hz

# SSZ (simple)
f1_ssz = f1 / D_SSZ(0.01)  # ~7.75 Hz

# SSZ (layered)
config = LayeredSSZConfig()
config.ionosphere.sigma = 0.01
f1_ssz = f_n_ssz_layered(1, config)  # ~7.77 Hz
```

### SSZ Signature Check

```python
# Extract delta_seg from observations
delta_seg = {
    1: delta_seg_from_observed(f1_obs, f1_class),
    2: delta_seg_from_observed(f2_obs, f2_class),
    3: delta_seg_from_observed(f3_obs, f3_class),
}

# Check consistency
result = check_mode_consistency(delta_seg)
if result['ssz_score'] > 0.7:
    print("Strong SSZ signature!")
```

### Frequency Shift Estimation

```python
# 1% segmentation
result = frequency_shift_estimate(0.01)
print(f"f1: {result['f1_classical']:.2f} -> {result['f1_ssz']:.2f} Hz")
print(f"Shift: {result['delta_f1']:.3f} Hz")
```

---

**© 2025 Carmen Wrede & Lino Casu**
