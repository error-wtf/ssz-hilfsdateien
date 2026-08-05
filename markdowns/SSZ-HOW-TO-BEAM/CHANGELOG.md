# Changelog

All notable changes to the BEAM-SSZ project are documented in this file.

## [0.6.0] - 2026-06-08

### Core New Solution: SSZ Bridge Metric

The v0.6 release introduces the **SSZ Bridge Metric** as the central mathematical solution for real-beaming:

- **Problem**: Traditional approaches (scanning, copying, teleportation) violate fundamental theorems or create identity discontinuities.
- **Solution**: Model points A and B as two boundary surfaces of a common bridge metric, with movement along a continuous worldline in the bridge channel (coordinate u ∈ [-1, 1]).
- **Key Insight**: L_bridge ≪ L_normal through different effective distance, not superluminal speed.

#### Bridge Metric Module (`src/beam_ssz/bridge_metric.py`)
- `SSZBridgeMetric` class implementing the bridge coordinate system
- Bridge segment density: Ξ_B(u) = (1-w(u))Ξ_A + w(u)Ξ_B + λ·q(u)
- Metric: ds² = -D_B²c²dt² + s_B²du² + R_B²dΩ²
- Complete candidate evaluation: regularity, worldline norm, distance reduction, tidal safety, causality, energy classification
- `create_canonical_bridge()` convenience factory
- `test_bridge_candidate()` testing utility

### New Modules

#### Experimental Xi Playground (`experimental_xi.py`)
- Alternative Xi formula testing framework
- Comparison against canonical SSZ
- Status labeling: CANONICAL, EXPERIMENTAL, DEPRECATED_TEST_ONLY, TOY_MODEL
- Forbidden formula detection (Ξ = (r_s/r)² exp(-r/r_φ))

#### No-Go Filters (`no_go_filters.py`)
- Mathematical consistency checks (not moral prohibitions)
- Filters for:
  - No-cloning theorem violations
  - Identity continuity breaks (scan/copy + identity claims)
  - Destructive reconstruction
  - Faster-than-light signals
  - NEC violation classification
  - Biological experiment readiness gates
- `NoGoFilterResult`: PASS, WARNING, NON_CANONICAL, EXOTIC, FAIL

#### Metric Bridge Search (`metric_bridge.py`)
- Bridge candidate parameter evaluation
- Effective distance calculations with coupling
- CTC detection proxy
- Singularity checks
- Tidal acceleration estimates

#### Candidate Classification (`candidate_classifier.py`)
- Classification matrix:
  - `SSZ_CANONICAL_PASS/FAIL`
  - `SSZ_EXTENSION_PASS/FAIL`
  - `GR_EXOTIC_PASS/FAIL`
  - `TOY_MODEL_PASS/FAIL`
  - `INCONSISTENT`
- Full no-go filter integration
- Classification reports with reasons and warnings

#### Search Space (`search_space.py`)
- Parameter space definitions
- Linear and logarithmic grids
- Random sampling
- Search point iteration

#### Experiment Ladder (`experiment_ladder.py`)
- 6-level staged progression:
  1. LEVEL_0_FOUNDATIONAL - Mathematical consistency only
  2. LEVEL_1_PHOTON - Photon/frequency phase tests
  3. LEVEL_2_ATOMIC_CLOCK - Atomic clock/interferometer tests
  4. LEVEL_3_COLD_ATOM - Cold atom coherence tests
  5. LEVEL_4_MESOSCOPIC - Mesoscopic system tests
  6. LEVEL_5_MACROSCOPIC_INERT - Macroscopic inert matter only
  7. LEVEL_6_BIOLOGICAL_FORBIDDEN - Explicitly forbidden until all prior levels validated
- Progression checks and level validation

#### Real-Beam Readiness Score (`real_beam_readiness_score.py`)
- Strict readiness assessment (not marketing)
- Multi-axis scoring:
  - Mathematical consistency
  - SSZ guardrails
  - No-go compliance
  - Energy conditions
  - Causality
  - Tidal safety
  - Experimental ladder
  - Reproducibility
- Readiness levels: NOT_READY, FOUNDATIONAL_ONLY, PHOTON_TEST_READY, ATOMIC_TEST_READY, MESOSCOPIC_TEST_READY, MACROSCOPIC_INERT_TEST_READY, HUMAN_TRANSFER_NOT_ALLOWED
- Blocker identification and recommendations

#### Tensor Scaffold (`tensor/` package)
Complete tensor calculation modules:
- `metric_tensor.py` - SSZ metric components
- `inverse_metric.py` - Inverse metric
- `christoffel.py` - Christoffel symbols (finite difference)
- `riemann.py` - Riemann tensor
- `ricci.py` - Ricci tensor
- `ricci_scalar.py` - Ricci scalar
- `einstein.py` - Einstein tensor
- `stress_energy.py` - Stress-energy tensor from Einstein
- `invariants.py` - Curvature invariants (Kretschmann scalar)

#### Additional Modules
- `derivatives.py` - Centralized derivative calculations for Xi, D, s
- `light_travel_time.py` - Null geodesic light travel time calculations

### New Documentation
- `docs/17_bridge_metric_spec.md` - Complete bridge metric mathematical specification

### New Simulations (011-016)
- `011_bridge_metric_demo.py` - Bridge metric demonstration
- `012_energy_class_scan.py` - Energy condition classification parameter scan
- `013_no_go_filter_demo.py` - No-go theorem filters demonstration
- `014_experimental_xi_demo.py` - Experimental Xi formulas playground
- `015_readiness_assessment.py` - Real-beam readiness scoring
- `016_full_pipeline_demo.py` - Complete pipeline integration test

### New Tests
- `test_bridge_metric.py` - Core bridge metric tests (20+ tests)
- `test_no_go_filters.py` - No-go filter tests (15+ tests)
- `test_experimental_xi.py` - Experimental Xi tests (10+ tests)
- `test_readiness_score.py` - Readiness scoring tests (15+ tests)
- `test_tensor_scaffold.py` - Tensor calculation tests (20+ tests)

### Statistics
- Total modules: 30+ (from 21 in v0.4)
- Total documentation: 17 files
- Total simulations: 16 (from 10 in v0.4)
- Total tests: 18+ files, 60+ individual test functions
- Total lines of code: ~15,000+ (estimated)

### Dependencies
- Added: numpy >= 1.24.0, scipy >= 1.10.0

### Project Metadata
- Updated README with bridge metric solution
- Added LICENSE (MIT with disclaimer)
- Added CITATION.cff
- Added pyproject.toml with full project configuration
- Added CHANGELOG.md (this file)

---

## [0.4.0] - 2026-05-XX

### Features
- Canonical Xi/regime engine
- SSZ metric object
- Geodesic utilities for timelike radial motion
- Effective potential helpers
- Radial scaling coordinate `rho`, with `d rho = s(r) dr`
- Radial null-geodesic light travel time
- Wave operator chain rule guardrail
- Static closed-loop holonomy invariant
- First radial geodesic-deviation/tidal proxy
- Reproducibility and validation level documentation
- 10 simulations
- 40+ tests

---

## [0.3.0] - 2026-05-XX (Pre-release)

### Features
- Initial Xi/regime engine
- Basic metric calculations
- Early geodesic implementations

---

## Project Philosophy

BEAM-SSZ follows these principles:

1. **Mathematical Rigor**: All formulas must be mathematically consistent
2. **Canonical SSZ**: Where applicable, use canonical SSZ formulas
3. **Classification, Not Prohibition**: Exotic cases are classified (GR_EXOTIC, TOY_MODEL), not forbidden
4. **Safety First**: No-go filters enforce mathematical/physical consistency
5. **Experimental Ladder**: Harmless test systems first, biological systems last (and forbidden until fully validated)
6. **No False Claims**: Explicitly not a device blueprint, not claiming human teleportation is possible

---

© 2025-2026 Carmen N. Wrede, Lino P. Casu
