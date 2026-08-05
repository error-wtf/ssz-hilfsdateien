# GPS Gravitational Frequency Shift Validation

**Book reference:** Ch 20 (PPN Tests), Ch 21 (GPS and Atomic Clocks)  
**Test file:** `test_validation.py` (ssz-qubits), `test_gps_relativistic.py`  
**Paper:** 01 (Radial Scaling), 20 (Observational Tests)

---

## Setup

GPS satellites orbit at h = 20,200 km altitude. Their onboard atomic clocks must be corrected for two relativistic effects:

1. **Gravitational blueshift** (higher altitude = weaker gravity = faster clock): +45.7 μs/day
2. **Kinematic time dilation** (orbital velocity = slower clock): -7.1 μs/day

**Net correction: +38.4 to +38.6 μs/day**

Without this correction, GPS position errors accumulate at ~10 km/day.

## SSZ Calculation

**Earth parameters:**
```
M_earth = 5.972e24 kg
R_earth = 6,371 km = 6.371e6 m
r_s_earth = 2*G*M_earth/c^2 = 2 * 6.674e-11 * 5.972e24 / (3e8)^2 = 8.87 mm = 0.00887 m
```

**Xi at Earth's surface:**
```
Xi_surface = r_s / (2*R_earth) = 0.00887 / (2 * 6.371e6) = 6.953e-10
```

**Xi at GPS orbit altitude:**
```
R_GPS = 6371 + 20200 = 26,571 km = 2.6571e7 m
Xi_GPS = r_s / (2*R_GPS) = 0.00887 / (2 * 2.6571e7) = 1.668e-10
```

**Gravitational frequency shift (fractional):**
```
Delta_f/f = Xi_surface - Xi_GPS = 6.953e-10 - 1.668e-10 = 5.285e-10
```

**Per day:**
```
5.285e-10 * 86400 s = 45.66 μs/day   (gravitational)
```

**Kinematic correction (special relativity):**
```
v_GPS = sqrt(G*M/R_GPS) = sqrt(6.674e-11 * 5.972e24 / 2.657e7) = 3874 m/s
Delta_f/f = -v^2/(2c^2) = -(3874)^2 / (2*(3e8)^2) = -8.34e-11
Per day: -8.34e-11 * 86400 = -7.21 μs/day  (kinematic)
```

**Net SSZ prediction:**
```
+45.66 - 7.21 = +38.45 μs/day
```

## Comparison

| Source | Value [μs/day] |
|--------|---------------|
| Gravitational (SSZ) | +45.66 |
| Kinematic (SR) | -7.21 |
| **SSZ Total** | **+38.45** |
| **GPS Specification** | **+38.4** |
| GR Total | +38.4 |
| Deviation SSZ vs GR | < 0.1% |

**Result:** SSZ and GR agree with the GPS specification to <0.1%.  
This confirms SSZ in the weak-field regime (r_s/R << 1).

## Why SSZ = GR Here

For Earth, `r_s/R = 1.39e-9` (extremely weak field). Both SSZ formulas give:
```
Xi_weak = r_s/(2r)  ≈  Xi_strong = 1 - exp(-phi*r_s/r)  for r >> r_s
```

The two formulas agree to better than 1 part per million at Earth's distance.

## Physical Interpretation

The GPS clock correction demonstrates that **gravitational time dilation is real and precisely predictable**. The formula used:

```
Delta_f/f = Xi(r_surface) - Xi(r_satellite)
```

This is the **additive** form of frequency shift, directly derivable from the SSZ segment density model: clocks tick faster where segment density is lower.

## Test Code (ssz-qubits)

```python
# From test_validation.py
def test_gps_correction():
    M_earth = 5.972e24
    R_surface = 6.371e6
    R_orbit = 2.6571e7
    r_s = 2 * G * M_earth / c**2
    
    xi_surface = r_s / (2 * R_surface)
    xi_orbit = r_s / (2 * R_orbit)
    
    grav_shift_per_day = (xi_surface - xi_orbit) * 86400 * 1e6  # microseconds
    kinematic_shift_per_day = -(3874**2) / (2 * c**2) * 86400 * 1e6
    
    total = grav_shift_per_day + kinematic_shift_per_day
    assert abs(total - 38.4) < 0.5  # within 0.5 μs/day of spec
```

## Relation to Other Sections

- [Time Dilation D](../02_FOUNDATIONS/time_dilation.md) — D = 1/(1+Xi) used for redshift
- [Segment Density Xi](../02_FOUNDATIONS/segment_density.md) — Xi formula
- [Worked Examples](../03_FORMULAS/worked_examples.md) — full calculation with numbers
- [PPN Formulas](../03_FORMULAS/ppn_formulas.md) — SSZ weak-field = PPN = GR
