# SSZ Cosmological Simulation Plan

## 1. Vision

Build a modular, data-driven simulation suite that superposes Segmented Spacetime (SSZ) fields for solar-system and extragalactic scales using real catalogs (GAIA, VizieR, JPL Horizons). The system must:

- Reproduce single-body SSZ physics (σ, τ, n, Δ(M), φ/2 natural boundary, β coupling).
- Aggregate multiple bodies via barycentric frames with precise ephemerides.
- Offer extensible APIs for Python analytics, WebGL/Three.js rendering, and Java/TeaVM clients.
- Support calibration workflows (β estimation, Δ(M) validation, dual-velocity checks) as prescribed in the reference papers.

## 2. Architecture Overview

### 2.1 Packages

- `ssz_unified_suite.py`: Existing core remains the single-body reference implementation.
- `ssz_cosmos/`: New cosmology package with the following modules:
  - `constants.py`: Shared frames, units, φ/2 helpers (already created).
  - `bodies.py`: Data classes for celestial bodies, GAIA/VizieR ingestion, unit normalization.
  - `ephemerides.py`: Load GAIA/JPL samples, interpolate positions/velocities (e.g., cubic Hermite). Handles barycentric ⇄ heliocentric transforms.
  - `field.py`: `MultiBodyField` that superposes σ/τ/n per timestep using φ/2 blending and β/Δ(M) coupling.
  - `simulation.py`: `SSZCosmicSimulator` orchestrating time loops, caching, calibration routines, and output datasets.
  - `viz.py` (optional later): Python Plotly helpers for volumetric / isosurface rendering.

### 2.2 Data Flow

1. **Catalog ingest**: JSON/CSV describing bodies (`name`, `mass_kg`, `radius`, `kappa`, `alpha`, etc.). Initial set: Sun, planets, major moons.
2. **Ephemeris ingest**: GAIA/VizieR exports (ICRS barycentric) converted to standardized format (`jd`, `x`, `y`, `z`, optional velocities). Provide converters for JPL Horizons (heliocentric) using `to_barycentric()`.
3. **Field computation**: For each epoch, evaluate σ, τ, n on requested grids or sample points. Support both full superposition and per-body diagnostics.
4. **Calibration**: Implement β estimation routines (median residual, bootstrap, sign test) referencing the procedures from `Φ_2 And Β ...`.
5. **Visualization**: Generate Plotly scenes (slices, isosurfaces, vector fields) and export to JSON for WebGL/Java clients.

## 3. Mathematical Requirements

- Natural boundary: `r_phi = (phi/2) * r_s * (1 + beta * delta(M))`.
- Segment density superposition: `sigma_total(x, t) = sum_i gamma_i * K(||x - r_i(t)||)` with existing kernel definitions from `Field`.
- Time dilation & refractive index: `tau_total = phi^(-alpha_total * sigma_total)` (alpha configurable per-body/global); `n_total = 1 + kappa_total * sigma_total`.
- Dual velocity check: Ensure `v_esc(x) * v_fall(x) ≈ c^2` across sampled points, reporting deviations.

## 4. Implementation Roadmap

### Phase 1 – Data & Physics Foundations

- Implement `BodyDefinition` and `BodyCatalog` for loading GAIA/VizieR CSV/JSON.
- Build `EphemerisLoader` supporting barycentric and heliocentric datasets, including interpolation.
- Extend `SSZCore` formulas into `MultiBodyField` with φ/2 blending and β coupling per references.
- Create unit tests for Δ(M), rφ, σ superposition, dual velocities, and ephemeris conversions.

### Phase 2 – Simulation & Calibration

- Develop `SSZCosmicSimulator` to step through epochs, query fields, and accumulate diagnostics.
- Integrate β calibration workflow (median residuals + bootstrap + sign test).
- Support export to NetCDF/JSON for sharing with WebGL/Java clients.

### Phase 3 – Visualization & Clients

- Python: Add interactive Plotly dashboards (`ssz_cosmos/viz.py`).
- WebGL: Update `segmented-solar-webgl/docs/app.js` to consume exported datasets (instanced bodies, LUT textures, timeline controls).
- Java/TeaVM: Extend `segmented-solar-java` to stream cosmology data and render multi-body fields.

### Phase 4 – Validation & Documentation

- Expand `ssz_test_suite.py` to include cosmological scenarios, calibration checks, and GAIA ingestion tests.
- Update documentation (`README_SSZ_COMPLETE.md`, new `docs/COSMOS.md`) covering pipeline usage and theory compliance.

## 5. Data Requirements

- GAIA DR3/DR4 solar-system orbits (ICRS barycentric).
- JPL Horizons fallback (requires heliocentric → barycentric conversion).
- Optional: Extragalactic datasets for future expansion.

## 6. Tooling & Standards

- Python ≥3.10 with NumPy, SciPy, pandas, Plotly.
- Numba or JAX (optional) for acceleration of large field grids.
- JSON Schema for catalog/ephemeris files to ensure cross-language compatibility.
- Follow Anti-Capitalist Software License and repo guidelines.

## 7. Next Steps

1. Finalize `bodies.py`, `ephemerides.py`, `field.py`, `simulation.py` skeletons.
2. Implement Phase 1 tasks with accompanying unit tests.
3. Iteratively integrate visualization clients and calibration routines.

Once Phase 1 skeletons are in place, we can begin coding the simulation core and integrating GAIA data.
