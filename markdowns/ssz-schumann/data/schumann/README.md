# Schumann Resonance Data

This directory contains Schumann resonance frequency data for SSZ analysis.

## Quick Start

The repository includes a **1-year sample dataset** that works out of the box:

```python
import pandas as pd

# Load sample data (included in repository)
data = pd.read_csv('data/schumann/sample_schumann_2016.csv', parse_dates=['time'])
print(f"Loaded {len(data)} data points")
```

---

## Data Files

### Included in Repository

| File | Description | Size |
|------|-------------|------|
| `sample_schumann_2016.csv` | 1-year sample dataset (2016) | ~1.5 MB |
| `realistic_schumann_2016.csv` | Full 2016 hourly data | ~1.5 MB |
| `realistic_schumann_2016_daily.csv` | Daily averages for 2016 | ~60 KB |

### Data Format

```csv
time,f1,f2,f3,f107,kp
2016-01-01 00:00:00,7.85,14.26,20.96,103.64,3.25
2016-01-01 01:00:00,7.80,14.23,20.88,103.64,3.25
...
```

| Column | Description | Unit |
|--------|-------------|------|
| `time` | Timestamp (UTC) | ISO 8601 |
| `f1` | Schumann mode 1 frequency | Hz |
| `f2` | Schumann mode 2 frequency | Hz |
| `f3` | Schumann mode 3 frequency | Hz |
| `f107` | F10.7 solar radio flux | SFU |
| `kp` | Kp geomagnetic index | 0-9 |

---

## Full Dataset (4 Years)

For the complete 4-year dataset (March 2013 - February 2017), download from Zenodo:

### Source

**Sierra Nevada ELF Station (Salinas et al., 2022)**

- **DOI:** [10.5281/zenodo.6348930](https://doi.org/10.5281/zenodo.6348930)
- **Period:** March 2013 - February 2017
- **Resolution:** 10-minute intervals
- **Size:** ~1-2 GB (compressed)

### Download Instructions

#### Option 1: Manual Download

1. Go to [https://zenodo.org/record/6348930](https://zenodo.org/record/6348930)
2. Download the data files (`.mat` format)
3. Extract to `data/schumann/raw/`

#### Option 2: Using Script

```bash
# From repository root
python scripts/fetch_zenodo_schumann.py
```

**Note:** This downloads ~1-2 GB and takes 10-30 minutes.

---

## Processing Raw Data

After downloading the raw Zenodo data, process it into CSV format:

### Step 1: Convert MAT to CSV

```python
import scipy.io as sio
import pandas as pd
import numpy as np
from pathlib import Path

# Load MAT file
mat_data = sio.loadmat('data/schumann/raw/schumann_data.mat')

# Extract frequencies (structure depends on MAT file)
# Typical structure: mat_data['f1'], mat_data['f2'], mat_data['f3']
f1 = mat_data['f1'].flatten()
f2 = mat_data['f2'].flatten()
f3 = mat_data['f3'].flatten()
timestamps = mat_data['time'].flatten()

# Create DataFrame
df = pd.DataFrame({
    'time': pd.to_datetime(timestamps, unit='s'),
    'f1': f1,
    'f2': f2,
    'f3': f3
})

# Save to CSV
df.to_csv('data/schumann/processed/schumann_full.csv', index=False)
```

### Step 2: Add Space Weather Data

```python
# Load space weather data
f107 = pd.read_csv('data/space_weather/f107_noaa.csv', parse_dates=['date'])
kp = pd.read_csv('data/space_weather/kp_gfz.csv', parse_dates=['date'])

# Merge with Schumann data
df['date'] = df['time'].dt.date
df = df.merge(f107[['date', 'f107']], on='date', how='left')
df = df.merge(kp[['date', 'kp']], on='date', how='left')

# Save merged data
df.to_csv('data/schumann/processed/schumann_with_weather.csv', index=False)
```

### Step 3: Quality Control

```python
# Remove outliers (frequencies outside physical range)
df = df[(df['f1'] > 6) & (df['f1'] < 10)]
df = df[(df['f2'] > 12) & (df['f2'] < 17)]
df = df[(df['f3'] > 18) & (df['f3'] < 24)]

# Remove NaN values
df = df.dropna()

# Save cleaned data
df.to_csv('data/schumann/processed/schumann_cleaned.csv', index=False)
print(f"Cleaned dataset: {len(df)} points")
```

---

## Space Weather Data Sources

### F10.7 Solar Radio Flux

**Source:** NOAA Space Weather Prediction Center

- **URL:** [https://www.swpc.noaa.gov/products/solar-cycle-progression](https://www.swpc.noaa.gov/products/solar-cycle-progression)
- **Format:** Daily values in Solar Flux Units (SFU)

```bash
python scripts/fetch_space_weather.py --f107
```

### Kp Geomagnetic Index

**Source:** GFZ Potsdam

- **URL:** [https://www.gfz-potsdam.de/en/kp-index/](https://www.gfz-potsdam.de/en/kp-index/)
- **Format:** 3-hourly values (0-9 scale)

```bash
python scripts/fetch_space_weather.py --kp
```

---

## Expected Schumann Frequencies

| Mode | Classical | Observed Range |
|------|-----------|----------------|
| n=1 | 10.6 Hz | 7.5 - 8.5 Hz |
| n=2 | 18.4 Hz | 13.5 - 15.0 Hz |
| n=3 | 26.0 Hz | 19.5 - 21.5 Hz |
| n=4 | 33.5 Hz | 25.5 - 27.5 Hz |
| n=5 | 41.0 Hz | 31.5 - 34.0 Hz |

The observed frequencies are lower than classical predictions due to:
- Finite conductivity of Earth and ionosphere
- Non-uniform ionosphere height
- Day/night asymmetry

---

## SSZ Analysis

### Calculate Relative Frequency Shifts

```python
# Reference frequencies
f1_ref = 7.83
f2_ref = 14.1
f3_ref = 20.3

# Relative shifts
delta_f1 = (f1_ref - df['f1']) / df['f1']
delta_f2 = (f2_ref - df['f2']) / df['f2']
delta_f3 = (f3_ref - df['f3']) / df['f3']

# SSZ segmentation parameter (average across modes)
delta_seg = (delta_f1 + delta_f2 + delta_f3) / 3
```

### Mode Consistency Test

```python
import numpy as np

# SSZ signature: all modes shift equally
corr_12 = np.corrcoef(delta_f1, delta_f2)[0, 1]
corr_13 = np.corrcoef(delta_f1, delta_f3)[0, 1]
corr_23 = np.corrcoef(delta_f2, delta_f3)[0, 1]

mode_consistency = (corr_12 + corr_13 + corr_23) / 3
print(f"Mode Consistency Score: {mode_consistency:.4f}")

if mode_consistency > 0.7:
    print("SSZ Signature: DETECTED")
```

---

## References

1. Schumann, W.O. (1952). "Über die strahlungslosen Eigenschwingungen einer leitenden Kugel". Z. Naturforsch., 7a, 149-154.

2. Salinas, A. et al. (2022). "Schumann resonance data processing programs and four-year measurements from Sierra Nevada ELF station". Computers & Geosciences, 165, 105148. [DOI: 10.5281/zenodo.6348930](https://doi.org/10.5281/zenodo.6348930)

3. Nickolaenko, A.P. & Hayakawa, M. (2002). "Resonances in the Earth-Ionosphere Cavity". Kluwer Academic Publishers.

---

## License

Anti-Capitalist Software License v1.4

© 2025 Carmen Wrede & Lino Casu

**Contact:** mail@error.wtf
