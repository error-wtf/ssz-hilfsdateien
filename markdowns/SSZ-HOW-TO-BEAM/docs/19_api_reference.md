# API Reference - BEAM-SSZ v0.6

Complete API documentation for all public modules.

---

## Core Modules

### `constants`

Physical and mathematical constants.

```python
from beam_ssz.constants import PHI, C, G, HBAR, K_B

PHI = 1.618033988749895  # Golden ratio
C = 299_792_458.0  # Speed of light [m/s]
G = 6.67430e-11  # Gravitational constant [m³/kg/s²]
HBAR = 1.054571817e-34  # Reduced Planck constant [J·s]
K_B = 1.380649e-23  # Boltzmann constant [J/K]
```

### `xi` - Canonical Xi Engine

Main function: `evaluate_xi_x(x)`

```python
from beam_ssz.xi import evaluate_xi_x, XiEvaluation

result = evaluate_xi_x(2.0)
print(result.xi)  # Segment density
print(result.regime)  # Regime classification
print(result.dxi_dx)  # First derivative
```

### `bridge_metric` - Core Solution

```python
from beam_ssz.bridge_metric import SSZBridgeMetric, create_canonical_bridge

bridge = SSZBridgeMetric(
    xi_left=0.1,
    xi_right=0.2,
    lambda_bridge=0.5,
    ell0=1e-3,
    throat_radius=1e-2,
)

# Key methods
D = bridge.D(u)  # Time dilation factor
s = bridge.s(u)  # Radial scaling
l_bridge = bridge.bridge_distance()  # Effective distance
```

---

## Proof Framework

### `proof_framework`

```python
from beam_ssz.proof_framework import BeamingProofFramework

framework = BeamingProofFramework()
theorems = framework.prove_all_theorems(bridge, l_normal=1.0)
```

### `complete_proof`

```python
from beam_ssz.complete_proof import CompleteBeamingProof, is_beaming_proven

proof = CompleteBeamingProof()
result = proof.prove_all_theorems(bridge, l_normal=1.0)

# Quick check
status = is_beaming_proven(bridge)
```

---

## Analysis Modules

### `einstein_solver`

```python
from beam_ssz.einstein_solver import estimate_energy_requirements

results = estimate_energy_requirements(bridge, verbose=True)
print(results['nec_satisfied'])
print(results['classification'])
```

### `stability_analysis`

```python
from beam_ssz.stability_analysis import BridgeStabilityAnalyzer

analyzer = BridgeStabilityAnalyzer()
report = analyzer.full_stability_report(bridge)
```

### `quantum_consistency`

```python
from beam_ssz.quantum_consistency import BridgeQuantumAnalyzer

analyzer = BridgeQuantumAnalyzer()
result = analyzer.analyze_quantum_consistency(bridge)
print(result.semiclassical_valid)
```

### `thermodynamics`

```python
from beam_ssz.thermodynamics import BridgeThermodynamicAnalyzer

analyzer = BridgeThermodynamicAnalyzer()
result = analyzer.analyze_thermodynamics(bridge)
print(result.overall_feasibility)
```

---

## Classification

### `candidate_classifier`

```python
from beam_ssz.candidate_classifier import CandidateClassifier, CandidateClass

report = CandidateClassifier.classify(candidate)
print(report.candidate_class)  # SSZ_CANONICAL, GR_EXOTIC, etc.
```

### `no_go_filters`

```python
from beam_ssz.no_go_filters import NoGoFilters

reports = NoGoFilters.run_all_filters(
    scan_copy_model=False,
    nec_violation=False,
    # ... other parameters
)
```

---

## Tensor Scaffold

```python
from beam_ssz.tensor import MetricTensor, EinsteinTensor

metric = MetricTensor.compute(r=10.0, rs=1.0, theta=pi/2)
einstein = EinsteinTensor.compute(r=10.0, rs=1.0, theta=pi/2)
```

---

## Experiment Ladder

```python
from beam_ssz.experiment_ladder import ExperimentLadder, ExperimentLevel

# Get all levels
levels = ExperimentLadder.get_all_levels()

# Check specific level
stage = ExperimentLadder.get_stage(ExperimentLevel.LEVEL_1_PHOTON)
print(stage.allowed_test_systems)
```

---

## Readiness Assessment

```python
from beam_ssz.real_beam_readiness_score import RealBeamReadinessScorer

report = RealBeamReadinessScorer.assess_readiness(
    math_consistency=0.95,
    ssz_guardrails=0.95,
    no_go_compliance=0.95,
    experimental_ladder_level=1,
)
print(report.overall_level)
```

---

## Common Patterns

### Complete Analysis Pipeline

```python
from beam_ssz.bridge_metric import create_canonical_bridge
from beam_ssz.proof_framework import BeamingProofFramework
from beam_ssz.einstein_solver import estimate_energy_requirements
from beam_ssz.complete_proof import is_beaming_proven

# 1. Create bridge
bridge = create_canonical_bridge()

# 2. Basic proof
framework = BeamingProofFramework()
theorems = framework.prove_all_theorems(bridge, l_normal=1.0)

# 3. Energy analysis
energy = estimate_energy_requirements(bridge)

# 4. Complete assessment
status = is_beaming_proven(bridge)
```

---

© 2025-2026 Carmen N. Wrede, Lino P. Casu
