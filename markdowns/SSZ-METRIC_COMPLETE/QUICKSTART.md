# SSZ Metric v1.1.0-canonical-pure - Quick Start Guide

**Get started with Canonical Segmented Spacetime in 5 minutes!**

---

## Installation

### From Source (Recommended for Development)

```bash
# Clone the repository
cd E:/clone/SSZ-METRIC_COMPLETE

# Install in editable mode
pip install -e .

# Verify installation
python -c "import ssz_metric_pure as ssz; print(f'SSZ v{ssz.__version__} installed!')"
```

### Dependencies

Minimal requirements:
```bash
pip install numpy scipy sympy
```

For development:
```bash
pip install pytest pytest-cov black mypy flake8
```

---

## Basic Usage

### 1. Basic SSZ Calculation (Canonical API)

```python
from ssz_metric_pure import (
    xi_canonical,      # Segment density Xi(r)
    D_from_xi,         # Time dilation factor D(r) = 1/(1+Xi)
    s_from_xi,          # Scale factor s(r) = 1 + Xi
    characteristic_radius,  # r_s = 2GM/c^2
    M_SUN, PHI, C, G
)
import numpy as np

# Solar mass black hole
r_s = characteristic_radius(M_SUN)
print(f"Solar Schwarzschild radius: r_s = {r_s:.1f} m")
print(f"Golden ratio PHI = {PHI}")

# Xi at different radii
test_radii = [1.0, 1.8, 2.0, 2.2, 10.0]  # in units of r_s
for x in test_radii:
    r = x * r_s
    xi = xi_canonical(r, M_SUN)
    D = D_from_xi(xi)
    print(f"r/{r_s:.0f} = {x:4.1f}: Xi = {xi:.6f}, D = {D:.6f}")

# Key Result: Xi(r_s) = 1 - exp(-PHI) ≈ 0.802
# D(r_s) = 1/(2 - exp(-PHI)) ≈ 0.555 (FINITE, not 0!)
```

---

### 2. Shapiro Delay Calculation

```python
from ssz_metric_pure import shapiro_ssz, shapiro_weak_field_exact
from ssz_metric_pure.constants import M_SUN, R_SUN, C

# Sun-Earth Shapiro delay
r_earth = 1.496e11  # 1 AU in meters
r_sun = 6.96e8      # Solar radius

# Minimal implementation (weak-field approximation)
delay_minimal = shapiro_ssz(r_sun, r_earth, M_SUN, n=5000)
print(f"Shapiro delay (minimal): {delay_minimal*1e6:.2f} µs")

# Exact analytical formula
delay_exact = shapiro_weak_field_exact(r_sun, r_earth, M_SUN)
print(f"Shapiro delay (exact): {delay_exact*1e6:.2f} µs")

# Expected: ~26.5 µs for Sun-Earth (weak-field SSZ)
```

### 3. Running Tests

```bash
# Run all tests
pytest tests/ -v

# Run specific test file
pytest tests/test_shapiro_deflection.py -v

# Run the main test runner
python run_all_tests.py
```

**Expected Output:** All 106 tests PASS
```

---

### 3. Accessing Constants

```python
from ssz_metric_pure import PHI, G_SI, C_SI, U_STAR_UNIVERSAL

print(f"Golden Ratio: φ = {PHI:.15f}")
print(f"Gravitational constant: G = {G_SI:.3e} m³/(kg·s²)")
print(f"Speed of light: c = {C_SI:.0f} m/s")
print(f"Universal intersection: u* = {U_STAR_UNIVERSAL}")
```

**φ (Phi) is NOT a fitting parameter!**
- Emerges from geometric structure
- Fibonacci-like segment recursion
- Optimal spacetime packing

---

### 4. Segment Density & Time Dilation

```python
from ssz_metric_pure import segment_density_N, time_dilation_SSZ

# Segment density at various radii
r_values = [0.5, 1.0, 2.0, 5.0, 10.0]  # in units of r_s
r_s = 2953  # meters (solar mass)

for r_ratio in r_values:
    r = r_ratio * r_s
    N = segment_density_N(r, r_s)
    D = time_dilation_SSZ(r, r_s)
    print(f"r = {r_ratio:.1f}r_s: N = {N:.6f}, D = {D:.6f}")
```

**Key Property:**
- N(0) = 0 → Flat spacetime at center
- N(∞) → 1 → Bounded saturation
- D = 1/(1+N) → Time dilation factor

---

### 5. Curvature Tensors (Advanced)

```python
from ssz_metric_pure import compute_curvature_at_point
import numpy as np

# Define metric function (4×4 tensor)
def static_metric_func(t, r, theta, phi):
    from ssz_metric_pure import SSZParams, StaticSSZMetric, M_SUN
    params = SSZParams(mass=M_SUN)
    metric = StaticSSZMetric(params)
    
    A = metric.A_coefficient(r)
    B = metric.B_coefficient(r)
    
    g = np.zeros((4, 4))
    g[0, 0] = -A  # g_tt
    g[1, 1] = B   # g_rr
    g[2, 2] = r * r  # g_θθ
    g[3, 3] = (r * np.sin(theta)) ** 2  # g_φφ
    
    return g

# Compute curvature at point
coords = (0, 5*2953, np.pi/2, 0)  # (t, r, θ, φ)
curvature = compute_curvature_at_point(static_metric_func, coords)

print(f"Ricci scalar: R = {curvature['ricci_scalar']:.3e}")
print(f"Einstein tensor computed: {curvature['einstein'].shape}")
```

**Warning:** Full Riemann tensor computation is expensive (256 components)!

---

## Running Tests

```bash
# All tests
pytest tests/ -v

# Specific test file
pytest tests/test_metric_static.py -v

# With coverage
pytest tests/ --cov=ssz_metric_pure --cov-report=html
```

**Expected:** 18/18 tests PASS (100%)

---

## Examples Directory

See `examples/` for more:
- `quickstart.py` - Basic SSZ calculation example (100% funktional)

---

## Common Patterns

### Pattern 1: Compare SSZ vs GR

```python
from ssz_metric_pure import SSZParams, StaticSSZMetric, M_SUN

params = SSZParams(mass=M_SUN)
metric = StaticSSZMetric(params)

r = 2 * metric.r_s

# SSZ metric
A_ssz = metric.A_coefficient(r)

# GR Schwarzschild (for comparison)
A_gr = 1 - metric.r_s / r

print(f"SSZ: A({r/metric.r_s:.1f}r_s) = {A_ssz:.6f}")
print(f"GR:  A({r/metric.r_s:.1f}r_s) = {A_gr:.6f}")
print(f"Difference: {abs(A_ssz - A_gr):.3e}")
```

### Pattern 2: Validate Singularity-Free Property

```python
from ssz_metric_pure import SSZParams, StaticSSZMetric, M_SUN
import numpy as np

params = SSZParams(mass=M_SUN)
metric = StaticSSZMetric(params)

# Test from near-center to far field
r_test = np.logspace(
    np.log10(0.1 * metric.r_phi),  # Near natural boundary
    np.log10(100 * metric.r_s),     # Far field
    num=100
)

A_values = [metric.A_coefficient(r) for r in r_test]

print(f"A_min = {min(A_values):.6f}")  # Should be > 0!
print(f"A(0) ≈ {metric.A_coefficient(1e-10):.6f}")  # Should be ≈ 1.0

assert all(A > 0 for A in A_values), "SINGULARITY DETECTED!"
print("✅ Singularity-free validated!")
```

### Pattern 3: Explore Spin Effects

```python
from ssz_metric_pure import KerrSSZParams, KerrSSZMetric

spins = [0.0, 0.3, 0.6, 0.9, 0.99]

for a_hat in spins:
    params = KerrSSZParams(mass=1e30, spin=a_hat)
    kerr = KerrSSZMetric(params)
    
    r_plus, r_minus = kerr.horizons()
    
    if not np.isnan(r_plus):
        print(f"â = {a_hat:.2f}: r_+/r_s = {r_plus/kerr.r_s:.3f}, "
              f"r_-/r_s = {r_minus/kerr.r_s:.3f}")
    else:
        print(f"â = {a_hat:.2f}: NAKED SINGULARITY (unphysical!)")
```

---

## Troubleshooting

### Import Error

```python
# If you get: ModuleNotFoundError: No module named 'ssz_metric_pure'
# Solution: Reinstall in editable mode
pip install -e .
```

### Test Failures

```bash
# Clear pytest cache
rm -rf .pytest_cache __pycache__

# Reinstall package
pip uninstall ssz-metric-pure
pip install -e .

# Run tests again
pytest tests/ -v
```

### Windows Unicode Issues

Some print statements with φ, θ, etc. may fail on Windows cmd.
Solution: Use PowerShell or set environment variable:

```powershell
$env:PYTHONIOENCODING="utf-8"
python your_script.py
```

---

## New Capability Modules (v1.1.0)

Four new modules extend the SSZ framework:

### 1. Physical Source Formation
```python
from ssz_metric_pure.source_formation import (
    matter_coupling, einstein_tensor_from_xi,
    vacuum_source_formation, interior_solution_formation
)

# Check Einstein equation consistency
from ssz_metric_pure import M_SUN
G = einstein_tensor_from_xi(r=1e7, theta=np.pi/2, mass=M_SUN)
print(f"Einstein tensor G_munu computed for r=10,000 km")
```

### 2. Stability Analysis
```python
from ssz_metric_pure.stability import (
    linearize_metric, analyze_stability_spectrum, radial_stability_analysis
)

# Analyze stability at multiple radii
radii = np.array([3, 5, 10, 20]) * characteristic_radius(M_SUN)
stability = analyze_stability_spectrum(M_SUN, radii)
print(f"Found {len(stability.modes)} stability modes")
```

### 3. Observational Proof (Forward Validation)
```python
from ssz_metric_pure.observational_proof import (
    ObservationalValidator, ObservationData
)

# Forward validation (NO fitting - anti-circular)
validator = ObservationalValidator(data_source="all")
result = validator.run_full_validation()
print(f"Validation: {result.num_passed}/{result.num_observations} observations pass")
```

### 4. Engineering Feasibility
```python
from ssz_metric_pure.engineering import (
    QuantumDeviceSimulator, EXAMPLE_QUBIT_DEVICE,
    assess_feasibility, device_comparison
)

# Simulate quantum device with SSZ corrections
sim = QuantumDeviceSimulator(EXAMPLE_QUBIT_DEVICE)
fidelity = sim.compute_gate_fidelity(gate_time=10e-9)
print(f"Gate fidelity with SSZ: {fidelity:.6f}")

# Full feasibility assessment
feas = assess_feasibility(EXAMPLE_QUBIT_DEVICE)
print(f"Ready for prototype: {feas.ready_for_prototype}")
```

---

## Next Steps

1. **Read Documentation:**
   - `README.md` - Overview
   - `IMPLEMENTATION_SUMMARY.md` - Detailed guide
   - Function docstrings - Inline help

2. **Explore Examples:**
   - `examples/basic_usage.py`
   - Modify parameters, test your own cases

3. **Run Tests:**
   - Understand validation methods
   - Add your own test cases

4. **Contribute:**
   - Report issues on GitHub
   - Suggest features
   - Submit pull requests

---

## Scientific References

### Key Papers (in `Segmented-Spacetime-Results/papers/`)
- SSZ_Black_Hole_Stability.md
- SSZ_Phi_Series_Discovery.md
- ESO_Validation_Results.md

### External Resources
- Schwarzschild Metric (GR comparison)
- Kerr Metric (rotation reference)
- Boyer-Lindquist coordinates

---

## Getting Help

**Documentation:**
- Inline: `help(SSZParams)`
- README: Complete overview
- Examples: Practical code

**Issues:**
- GitHub Issues (if public repo)
- Contact authors directly

**Community:**
- Research collaborations welcome
- Educational use encouraged
- Anti-capitalist license - read `LICENSE`

---

## License

**ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

- ✅ Free for research
- ✅ Free for education
- ✅ Free for non-commercial use
- ❌ Prohibited for capitalist exploitation

See `LICENSE` file for full terms.

---

## Citation

```bibtex
@software{wrede2025ssz,
  author = {Wrede, Carmen and Casu, Lino},
  title = {SSZ Metric Pure: Pure Segmented Spacetime},
  year = {2025},
  version = {1.1.0-canonical-pure},
  url = {https://github.com/error-wtf/ssz-metric-pure}
}
```

---

**Ready to explore singularity-free spacetimes? Let's go!** 🚀🌌

© 2025 Carmen N. Wrede & Lino Casu
