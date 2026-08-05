# SSZ Trajectories

**Geodesic toolkit for Segmented Spacetime (SSZ)**

Authors: Carmen N. Wrede, Lino P. Casu

---

## Overview

`ssz-trajectories` provides a pure-Python library for computing geodesics in the SSZ (Segmented Spacetime) metric:

$$ds^2 = -D^2(r)\,c^2\,dt^2 + s^2(r)\,dr^2 + r^2\,d\Omega^2$$

where $s(r) = 1 + \Xi(r)$ and $D(r) = 1/s(r)$.

### Key features

- **Four Xi variants:** `Xi_strong`, `Xi_weak`, `Xi_hard` (auto-switch at 100 r_s), `Xi_blend` (C² Hermite in [80, 120] r_s)
- **Radial geodesics:** null outgoing, timelike freefall
- **Non-radial null geodesics:** 2nd-order geodesic equation with automatic turning-point handling (no sign-switching artifacts)
- **Phi-Euler embedding:** local embedding x(r), N-level counting, cumulative embedding along orbits
- **Bridge identity:** numerical verification that dl/dt = s·dr/dt = c·D
- **Deflection analysis:** gravitational lensing angle corrected for finite starting radius

### Related SSZ repositories

| Repository | Purpose |
|------------|---------|
| [ssz-qubits](https://github.com/error-wtf/ssz-qubits) | Core SSZ functions, qubit applications (74 tests) |
| [ssz-metric-pure](https://github.com/error-wtf/ssz-metric-pure) | 4D tensor package, Einstein/Ricci curvature |
| [g79-cygnus-tests](https://github.com/error-wtf/g79-cygnus-tests) | Cygnus X-1 observational validation |
| [ssz-schumann](https://github.com/error-wtf/ssz-schumann) | Schumann resonance experiment |

---

## Installation

```bash
# From source
git clone https://github.com/error-wtf/ssz-trajectories.git
cd ssz-trajectories
pip install -e .

# With plotting support
pip install -e ".[plot]"

# With dev tools
pip install -e ".[dev]"
```

**Zero external dependencies** for the core library (pure Python + `math`).
Optional: `matplotlib` + `numpy` for plotting examples.

---

## Quick start

### Xi profile

```python
from ssz_trajectories import Xi_blend, D, s, x_local, N_level

# Metric at r = 1 r_s (Schwarzschild radius)
print(f"Xi(r_s)  = {Xi_blend(1.0):.4f}")   # 0.8024
print(f"D(r_s)   = {D(1.0, Xi_blend):.4f}")   # 0.5552
print(f"x_local  = {x_local(1.0, Xi_blend):.4f}")  # 1.22
print(f"N-level  = {N_level(1.0, Xi_blend)}")       # 1
```

### Radial null outgoing

```python
from ssz_trajectories import Xi_blend, integrate_null_radial, bridge_identity

pts = integrate_null_radial(Xi_blend, r0=1.01, tmax=2e-6, dt=2e-9)
print(f"r: {pts[0][1]:.3f} -> {pts[-1][1]:.1f} r_s")

# Bridge identity check
b = bridge_identity(Xi_blend, r=1.0)
print(f"dl/dt = {b['dl_dt']:.2f}, c*D = {b['cD']:.2f}, error = {b['relative_error']:.1e}")
```

### Non-radial null geodesic

```python
from ssz_trajectories import (
    Xi_blend, c_light,
    integrate_null_geodesic, analyze_orbit, deflection_angle,
)
import math

b = 5.0  # impact parameter in r_s
r0 = 300.0
pts = integrate_null_geodesic(Xi_blend, b, r0, r0 / c_light * 12, 2e-9)
res = analyze_orbit(Xi_blend, pts)
defl = deflection_angle(res["phi_total"], b, r0, Xi_blend)

print(f"r_min = {res['r_min']:.2f}, jumps = {res['xl_jumps']}")
print(f"deflection = {math.degrees(defl):.1f} deg")
```

---

## Theory

### The SSZ metric

In Segmented Spacetime, the line element is:

$$ds^2 = -D^2(r)\,c^2\,dt^2 \;+\; \frac{1}{D^2(r)}\,dr^2 \;+\; r^2\,d\Omega^2$$

The segment-density function $\Xi(r)$ encodes how densely spacetime is "segmented" by the gravitational field:

| Regime | Formula | Range |
|--------|---------|-------|
| **Strong** | $\Xi = 1 - e^{-\varphi r_s / r}$ | $r/r_s < 80$ |
| **Blend** | C² Hermite interpolation | $80 \le r/r_s \le 120$ |
| **Weak** | $\Xi = r_s/(2r)$ | $r/r_s > 120$ |

where $\varphi = (1+\sqrt{5})/2$ is the golden ratio.

**Key property:** $D(r_s) = 0.555 > 0$ — SSZ has **no event horizon**. The proper radial distance to $r_s$ is finite.

### Bridge identity

The coordinate velocity $dr/dt = c\,D^2$ and proper-distance velocity $d\ell/dt = c\,D$ are related by:

$$\frac{d\ell}{dt} = s(r)\,\frac{dr}{dt} = \frac{1}{D}\cdot c\,D^2 = c\,D$$

This "bridge" between coordinate and physical velocities is verified to machine precision by the test suite.

### Phi-Euler embedding

The local embedding level:

$$x(r) = \frac{\ln s(r)}{\ln \varphi}$$

maps the segment factor to a continuous real value. The integer part $N = \text{round}(x)$ counts phi-levels. For orbits penetrating the strong field ($b \lesssim 80\,r_s$), x_local crosses from $N=0$ to $N=1$ and back, yielding exactly **2 jumps**.

### Non-radial null geodesics

The 2nd-order geodesic equation (from Christoffel symbols):

$$\frac{d^2r}{d\lambda^2} = -\frac{D'c^2}{D} + \frac{D'}{D}\left(\frac{dr}{d\lambda}\right)^2 + \frac{c^2 b^2 D^2}{r^3}$$

This naturally handles turning points — no sign-switching needed. The radial velocity $v_r$ reverses smoothly at $r_{\text{tp}}$ where $r/D(r) = b$.

---

## Test suite

```bash
pytest tests/ -v
```

Tests cover:
- Xi function values, monotonicity, C² smoothness
- Embedding levels and jump counting
- RK4 integrator accuracy
- Radial geodesic monotonicity and speed bounds
- Timelike infall reaching boundary
- Non-radial turning points and deflection
- Bridge identity at all radii
- Proper length and tortoise coordinate finiteness

---

## Project structure

```
ssz-trajectories/
├── src/ssz_trajectories/
│   ├── __init__.py         # Public API
│   ├── constants.py        # PHI, c_light, blend bounds
│   ├── xi.py               # Xi_strong, Xi_weak, Xi_hard, Xi_blend, D, s
│   ├── embedding.py        # x_local, N_level, x_cumulative
│   ├── integrator.py       # RK4, radial/non-radial geodesics
│   └── analysis.py         # Orbit analysis, deflection, bridge
├── tests/
│   ├── test_xi.py
│   ├── test_embedding.py
│   ├── test_integrator.py
│   └── test_analysis.py
├── reports/
│   ├── TEST_REPORT.md      # 63/63 tests passed
│   └── test_results.xml    # JUnit XML
├── examples/
│   ├── radial_null_outgoing.py
│   ├── nonradial_deflection.py
│   └── plot_xi_profile.py
├── pyproject.toml
├── LICENSE (Anti-Capitalist Software License v1.4)
└── README.md
```

---

## License

**Anti-Capitalist Software License (v 1.4)**

Copyright (c) 2025 Carmen N. Wrede, Lino P. Casu

This is anti-capitalist software, released for free use by individuals and organizations that do not operate by capitalist principles. See [LICENSE](LICENSE) for full terms.
