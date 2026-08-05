# HamTools - Amateur Radio Calculator with SSZ Extension

**Version:** 1.0.0  
**Authors:** Carmen Wrede & Lino Casu  
**License:** Anti-Capitalist Software License v1.4

---

## Overview

HamTools is a practical toolkit for amateur radio operators, integrated into the SSZ/Schumann repository. It provides everyday calculations for:

- **Frequency/Wavelength** conversions
- **Antenna dimensions** (dipole, vertical, Yagi)
- **Feedline loss** calculations
- **ERP/EIRP** calculations
- **HF propagation** (MUF, skip distance)
- **Field strength** estimation

Additionally, HamTools includes an **SSZ Expert Mode** that shows how Segmented Spacetime theory would modify classical results.

---

## Installation

HamTools is part of the ssz-schuhman-experiment repository. No separate installation needed.

```bash
# From the repository root
cd ssz-schuhman-experiment

# Run CLI
python -m hamtools.cli freq --mhz 7.1

# Or use as Python module
python -c "from hamtools import core; print(core.freq_mhz_to_lambda(7.1))"
```

---

## Quick Start

### Python API

```python
from hamtools import core, antennas, feedline, ssz_extension

# Frequency/Wavelength
wavelength = core.freq_mhz_to_lambda(7.1)  # 42.22 m

# Dipole length
dipole = antennas.dipole_length_halfwave(7.1)  # 20.06 m

# Feedline loss
loss = feedline.total_loss_db(14.2, "RG-58", 30)  # 4.56 dB

# SSZ comparison
result = ssz_extension.compare_lambda_with_ssz(7.1, 0.01)
print(f"Classical: {result.classical_value:.2f} m")
print(f"SSZ:       {result.ssz_value:.2f} m")
print(f"Diff:      {result.difference_percent:.2f}%")
```

### Command Line

```bash
# Frequency to wavelength
hamtool freq --mhz 7.1

# With SSZ expert mode
hamtool freq --mhz 7.1 --ssz 0.01

# Dipole calculation
hamtool antenna dipole --mhz 7.1

# Feedline loss
hamtool feedline loss --mhz 14.2 --cable RG-58 --length 30

# MUF calculation
hamtool muf --fof2 5.0 --distance 3000 --height 300
```

---

## Modules

### core.py - Fundamental Calculations

| Function | Description |
|----------|-------------|
| `freq_to_lambda(f_hz)` | Frequency (Hz) → Wavelength (m) |
| `lambda_to_freq(lambda_m)` | Wavelength (m) → Frequency (Hz) |
| `freq_mhz_to_lambda(f_mhz)` | Frequency (MHz) → Wavelength (m) |
| `db_from_ratio(ratio)` | Power ratio → dB |
| `ratio_from_db(db)` | dB → Power ratio |
| `erp_watt(P_tx, gain_dBd, loss_db)` | Calculate ERP |
| `eirp_watt(P_tx, gain_dBi, loss_db)` | Calculate EIRP |

### antennas.py - Antenna Calculations

| Function | Description |
|----------|-------------|
| `dipole_length_halfwave(f_mhz, k)` | Half-wave dipole length |
| `vertical_quarterwave(f_mhz, k)` | Quarter-wave vertical length |
| `estimate_yagi_gain(elements, boom_m)` | Yagi gain estimate (dBd) |

### feedline.py - Cable Loss

| Function | Description |
|----------|-------------|
| `attenuation_db_per_100m(f_mhz, cable)` | Attenuation per 100m |
| `total_loss_db(f_mhz, cable, length_m)` | Total feedline loss |
| `power_at_antenna(P_tx, f_mhz, cable, length)` | Power reaching antenna |

**Supported cables:** RG-58, RG-213, RG-8, AIRCELL-7, ECOFLEX-10, ECOFLEX-15, LMR-400, H-2000

### propagation.py - HF Propagation

| Function | Description |
|----------|-------------|
| `critical_freq_fof2(N_max)` | Critical frequency from electron density |
| `muf_single_hop(foF2, distance_km, height_km)` | Maximum Usable Frequency |
| `skip_distance_km(freq_mhz, foF2, height_km)` | Skip zone distance |

### ssz_extension.py - SSZ Expert Mode

| Function | Description |
|----------|-------------|
| `d_ssz_from_delta(delta_seg)` | D_SSZ = 1 + δ_seg |
| `effective_c_from_ssz(c, delta_seg)` | c_eff = c / D_SSZ |
| `compare_lambda_with_ssz(f_mhz, delta_seg)` | Classical vs SSZ wavelength |

---

## SSZ Expert Mode

The SSZ (Segmented Spacetime) expert mode shows how spacetime segmentation would affect radio wave propagation.

### Theory

In SSZ theory, spacetime is segmented, causing an effective modification to the speed of light:

```
D_SSZ = 1 + δ_seg
c_eff = c / D_SSZ
```

This results in a slightly shorter effective wavelength:

```
λ_SSZ = c_eff / f = λ_classical / D_SSZ
```

### Typical δ_seg Values

| Value | Description |
|-------|-------------|
| 0.001 (0.1%) | Barely detectable |
| 0.01 (1%) | Small but measurable |
| 0.02 (2%) | Moderate SSZ signature |
| 0.03 (3%) | Strong SSZ signature |

### Example

```bash
$ hamtool freq --mhz 7.1 --ssz 0.01

==================================================
Frequency / Wavelength Calculation
==================================================
Frequency: 7.1000 MHz (7100000 Hz)
Wavelength: 42.2242 m
Period: 1.408451e-07 s

==================================================
SSZ Expert Mode (δ_seg = 0.0100)
==================================================
Classical λ:  42.2242 m
SSZ λ:        41.8061 m
Difference:   -0.9901%

Interpretation: SSZ segmentation slightly reduces
the effective wave speed, shortening wavelength.
```

### Consistency with Schumann Analysis

The SSZ extension uses the same notation and formulas as the Schumann resonance analysis:

- `δ_seg` - Segmentation parameter
- `D_SSZ = 1 + δ_seg` - Time dilation factor
- `c_eff = c / D_SSZ` - Effective speed of light

See `docs/SSZ_FORMULAS.md` for the complete mathematical framework.

---

## CLI Reference

### freq - Frequency/Wavelength

```bash
hamtool freq --mhz 7.1           # MHz input
hamtool freq --khz 7100          # kHz input
hamtool freq --hz 7100000        # Hz input
hamtool freq --mhz 7.1 --ssz 0.01  # With SSZ mode
```

### lambda - Wavelength to Frequency

```bash
hamtool lambda --m 40            # 40m → frequency
```

### antenna - Antenna Calculations

```bash
hamtool antenna dipole --mhz 7.1
hamtool antenna dipole --mhz 7.1 --k 0.93  # Custom shortening factor
hamtool antenna vertical --mhz 14.2
hamtool antenna yagi --mhz 14.2 --elements 5 --boom 6.5
hamtool antenna dipole --mhz 7.1 --ssz 0.01  # With SSZ mode
```

### feedline - Cable Loss

```bash
hamtool feedline loss --mhz 14.2 --cable RG-58 --length 30
hamtool feedline loss --mhz 14.2 --cable ECOFLEX-10 --length 30 --p-in-watt 100
hamtool feedline compare --mhz 14.2 --length 30
hamtool feedline cables  # List available cables
```

### erp - ERP/EIRP

```bash
hamtool erp --p-tx 100 --gain-dbd 3 --loss-db 2
```

### db - dB Calculator

```bash
hamtool db --ratio 2    # 2× → dB
hamtool db --db 3       # 3 dB → ratio
```

### muf - Maximum Usable Frequency

```bash
hamtool muf --fof2 5.0 --distance 3000 --height 300
hamtool muf --fof2 5.0 --distance 3000 --ssz 0.01  # With SSZ mode
```

### field - Field Strength

```bash
hamtool field --p-tx 100 --gain-dbi 6 --km 1 --mhz 14.2
```

### ssz - SSZ Expert Mode

```bash
hamtool ssz --mhz 7.1 --delta 0.01
hamtool ssz --mhz 7.1 --info  # Show typical values
```

---

## Examples

### Calculate Dipole for 40m Band

```python
from hamtools import antennas

result = antennas.calculate_dipole(7.1)
print(result)
# Half-Wave Dipole for 7.100 MHz
# ========================================
# Wavelength:        42.22 m
# Shortening factor: 0.95
# Total length:      20.06 m
# Each leg:          10.03 m
```

### Compare Feedline Options

```python
from hamtools import feedline

result = feedline.compare_cables(14.2, 30, 100)
print(result)
# Cable Comparison at 14.2 MHz, 30m
# ============================================================
# Cable           Loss (dB)    Power Out    Efficiency  
# ------------------------------------------------------------
# ECOFLEX-15      0.70         85.1         85.1%
# ECOFLEX-10      1.02         79.1         79.1%
# ...
# RG-58           4.56         35.0         35.0%
```

### SSZ Effect on Antenna Design

```python
from hamtools import ssz_extension

# Compare classical vs SSZ dipole
result = ssz_extension.compare_antenna_length_with_ssz(
    f_mhz=7.1,
    delta_seg=0.02,  # 2% SSZ
    antenna_type="dipole"
)

print(f"Classical: {result.classical_value:.2f} m")
print(f"SSZ:       {result.ssz_value:.2f} m")
print(f"Diff:      {result.difference_percent:.2f}%")
# Classical: 20.06 m
# SSZ:       19.66 m
# Diff:      -1.98%
```

---

## Integration with Schumann Analysis

HamTools integrates with the existing Schumann resonance analysis:

```python
# Use Schumann-derived δ_seg for ham calculations
from ssz_schumann.config import Config

config = Config()
delta_seg = config.ssz.amplitude_A  # From Schumann analysis

from hamtools import ssz_extension
result = ssz_extension.compare_lambda_with_ssz(7.1, delta_seg)
```

---

## References

- `docs/SSZ_FORMULAS.md` - SSZ mathematical framework
- `docs/Antennen_Basics.md` - Antenna theory
- `docs/Daempfung_dB_EMV.md` - dB calculations
- `docs/Wellen_Ionosphaere.md` - Ionospheric propagation
- `docs/Glossar_Funktechnik.md` - Radio terminology

---

## License

Anti-Capitalist Software License v1.4

© 2025 Carmen Wrede & Lino Casu
