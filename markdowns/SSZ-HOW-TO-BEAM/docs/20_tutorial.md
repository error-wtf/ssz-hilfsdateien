# BEAM-SSZ Tutorial

Step-by-step guide to using BEAM-SSZ v0.6.

---

## Installation

```bash
# Clone or download
cd BEAM-SSZ-v0.6

# Run installer
bash scripts/install.sh

# Or manually
python -m venv .venv
source .venv/bin/activate
pip install numpy scipy pytest
```

## Your First Analysis

### Step 1: Basic Xi Evaluation

```python
from beam_ssz import evaluate_xi_x

# Evaluate at r = 2r_s
result = evaluate_xi_x(2.0)
print(f"Ξ = {result.xi:.4f}")
print(f"Regime: {result.regime.value}")
```

### Step 2: Create a Bridge

```python
from beam_ssz import create_canonical_bridge

bridge = create_canonical_bridge(
    xi_a=0.1,      # Xi at point A
    xi_b=0.2,      # Xi at point B
    lambda_bridge=0.5,  # Coupling strength
    ell0=1e-3,     # Bridge scale [m]
    throat_radius=1e-2,  # Throat radius [m]
)

print(f"Bridge distance: {bridge.bridge_distance():.3e} m")
```

### Step 3: Run Proof Analysis

```python
from beam_ssz import is_beaming_proven

status = is_beaming_proven(bridge, l_normal=1.0)
print(f"Status: {status['completeness']}")
print(f"Theorems proven: {status['theorems_proven']}/8")
```

### Step 4: Full Analysis

```python
from beam_ssz.einstein_solver import estimate_energy_requirements
from beam_ssz.stability_analysis import BridgeStabilityAnalyzer

# Energy analysis
energy = estimate_energy_requirements(bridge, verbose=True)

# Stability analysis
analyzer = BridgeStabilityAnalyzer()
report = analyzer.full_stability_report(bridge, verbose=True)
```

## Understanding Results

### Proof Status Levels

- **RIGOROUS**: All theorems proven
- **STRONG**: Core structure valid
- **MODERATE**: Likely possible, open issues remain
- **WEAK**: Possibly possible, significant issues
- **INSUFFICIENT**: Cannot establish feasibility

### Energy Classifications

- **SSZ_CANONICAL**: NEC satisfied, standard matter
- **GR_EXOTIC**: NEC violated, exotic matter required
- **TOY_MODEL**: Mathematical only, not physical

## Parameter Exploration

### Weak Bridge (Safe but less effective)

```python
bridge = SSZBridgeMetric(
    xi_left=0.01,
    xi_right=0.01,
    lambda_bridge=0.01,
    ell0=1e-2,
    throat_radius=1e-2,
)
```

### Strong Bridge (Effective but challenging)

```python
bridge = SSZBridgeMetric(
    xi_left=0.1,
    xi_right=0.2,
    lambda_bridge=2.0,
    ell0=5e-4,
    throat_radius=5e-3,
)
```

## Advanced Usage

### Custom Analysis Pipeline

```python
from beam_ssz import *

# 1. Define parameters
xi_a = 0.1
xi_b = 0.15
lam = 0.8

# 2. Create and analyze
bridge = SSZBridgeMetric(xi_a, xi_b, lam, 1e-3, 1e-2)

# 3. Full proof
framework = BeamingProofFramework()
theorems = framework.prove_all_theorems(bridge, 1.0)

# 4. Component analysis
energy = estimate_energy_requirements(bridge)
stability = BridgeStabilityAnalyzer().analyze_stability_proxy(bridge)
quantum = BridgeQuantumAnalyzer().analyze_quantum_consistency(bridge)
thermo = BridgeThermodynamicAnalyzer().analyze_thermodynamics(bridge)

# 5. Decision
if (all(t.conditions_satisfied for t in theorems[:2]) and
    thermo.overall_feasibility != "VIOLATION"):
    print("Candidate worth further study")
```

## Common Workflows

### Research Mode

```bash
# Run simulations
python simulations/011_bridge_metric_demo.py

# Run tests
python -m pytest tests/test_bridge_metric.py -v

# Custom analysis
python scripts/analyze_bridge.py --xi-a 0.1 --xi-b 0.2
```

### Development Mode

```bash
# Edit code
vim src/beam_ssz/your_module.py

# Test changes
python -m pytest tests/test_your_module.py -v

# Full test suite
make test
```

## Troubleshooting

### Import Errors

```bash
# Ensure virtual environment is activated
source .venv/bin/activate

# Reinstall if needed
pip install -e .
```

### Numerical Issues

- Check parameter ranges (Xi should be positive)
- Verify ell0 and radius are positive
- Try smaller lambda for numerical stability

### Understanding Output

- **η (eta)**: Distance ratio, lower is better
- **λ (lambda)**: Coupling strength, higher = more effective but harder
- **NEC**: Null Energy Condition, violation requires exotic matter

## Next Steps

1. Read `docs/18_mathematical_proof_status.md` for theory
2. Study `examples/quickstart.py` for patterns
3. Explore `simulations/` for demonstrations
4. Run full test suite to verify installation

---

Happy researching!

© 2025-2026 Carmen N. Wrede, Lino P. Casu
