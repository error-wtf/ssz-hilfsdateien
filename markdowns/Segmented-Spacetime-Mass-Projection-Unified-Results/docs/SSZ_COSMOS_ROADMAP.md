# SSZ Cosmological Simulation Coding Roadmap

This roadmap expands on `docs/SSZ_COSMOS_PLAN.md` and lays out concrete implementation tasks, milestones, and deliverables for building the GAIA-driven SSZ cosmological suite.

---

## Phase 0 – Preparation

- **[P0-1] Repository hygiene**
  - Verify current virtual environment (`.venv/`) is active (Python ≥ 3.10).
  - Update `requirements.txt` if new dependencies are introduced (e.g., `pydantic`, `scipy>=1.11`, `plotly>=5`).
  - Ensure `docs/`, `ssz_cosmos/`, and `data/` directories exist (create `data/` and `ssz_cosmos/` if necessary).

- **[P0-2] Data acquisition**
  - Gather sample GAIA ephemeris exports (CSV/JSON) for Sun + planets (or use JPL Horizons data and convert to barycentric coordinates).
  - Store raw files under `data/raw/gaia/` and converted standardized sets under `data/processed/`.

- **[P0-3] Testing framework**
  - Confirm `pytest` (or `unittest`) setup works (`pip install -r requirements.txt`, `pytest -k SSZ`).
  - Create placeholder test package `tests/cosmos/`.

Deliverable: Clean repository with data stubs and test scaffolding ready.

---

## Phase 1 – Core Modules Skeleton

Implement scaffolding with docstrings, type hints, and TODO markers. No heavy logic yet.

1. **`ssz_cosmos/bodies.py`**
   - Define `BodyDefinition` dataclass: attributes `name`, `mass_kg`, `radius_m`, `kappa`, `alpha`, optional metadata.
   - Implement `BodyCatalog` to load bodies from JSON/CSV, handle unit normalization, and provide lookup by name.
   - Add validation helpers (e.g., ensure mass > 0).

2. **`ssz_cosmos/ephemerides.py`**
   - Implement `EphemerisSeries` dataclass storing `body_name`, `frame`, `origin`, `dates`, `positions`, optional `velocities`.
   - Build `EphemerisLoader` with methods `from_gaia_csv`, `from_horizons_csv`, `interpolate(jd)`.
   - Integrate frame conversion functions from `ssz_cosmos/constants.py` (e.g., `to_barycentric`).

3. **`ssz_cosmos/field.py`**
   - Create `MultiBodyField` class that wraps `SSZCore` and superposes σ/τ/n over arrays of positions.
   - Provide APIs: `sigma_at(points, epoch)`, `tau_at(...)`, `n_at(...)`.
   - Include placeholders for φ/2 blending and β coupling.

4. **`ssz_cosmos/simulation.py`**
   - Implement `SSZCosmicSimulator` orchestrating steps: load catalog, load ephemerides, iterate epochs, compute fields, store outputs.
   - Provide hooks for calibration (`calibrate_beta`), diagnostics, and export (JSON/NetCDF).

5. **Documentation**
   - Update docstrings referencing relevant papers from `Segmented_md/`.
   - Prepare developer notes in `docs/SSZ_COSMOS_PLAN.md` referencing new modules.

Deliverable: Skeleton modules with structured APIs and rich docstrings ready for implementation.

---

## Phase 2 – Field Computations & Ephemerides

1. **Ephemeris ingestion**
   - Parse GAIA barycentric CSV (columns: `JD`, `X`, `Y`, `Z`, optional `VX`, `VY`, `VZ`).
   - Parse JPL Horizons heliocentric exports (apply conversion via `to_barycentric`).
   - Implement interpolation (recommended: cubic Hermite for position, optional velocity support).
   - Add unit tests verifying interpolation accuracy, barycentric conversion, and edge cases.

2. **Multi-body field logic**
   - Extend `MultiBodyField` to compute `sigma_total = Σ_i gamma_i * K(|x - r_i|)`, using existing kernels (reuse from `Field.segmentDensity` or adapt logic).
   - Implement `tau_total = φ^(-α_eff * sigma_total)` and `n_total = 1 + κ_eff * sigma_total`.
   - Introduce α/κ per-body scaling, defaulting to global constants.
   - Add tests comparing single-body output to `SSZCore` for regression.

3. **φ/2 + Δ(M) + β integration**
   - Implement helper to compute `r_phi(M)` using `SSZCore` + new β parameter.
   - Ensure all field computations respect the range [r_s, r_phi] (clamp inputs outside range).
   - Provide method `set_beta(value)` and `delta_M(mass)` (reuse from `SSZCore`).
   - Add tests covering `r_phi` transitions and Δ(M) values from reference data.

Deliverable: Functional field computation across multiple bodies and epochs with validated ephemeris ingestion.

---

## Phase 3 – Simulation Workflow & Calibration

1. **Simulation runner**
   - Implement `SSZCosmicSimulator.run(start_jd, end_jd, step_days, grid_config)` that:
     - Interpolates ephemerides for each epoch.
     - Evaluates σ, τ, n on configured grids (e.g., 3D cubes, 2D slices, radial samples).
     - Stores results in memory or streaming outputs.

2. **β calibration pipeline**
   - Implement `calibrate_beta(observables)` using median residual minimization (per `Φ_2 And Β ...`).
   - Include bootstrap resampling for CI estimation and a sign test against GR baseline.
   - Add tests with synthetic data to ensure convergence and CI computation.

3. **Diagnostics & exports**
   - Provide summary statistics per epoch (max σ, τ range, n range, dual-velocity deviations).
   - Allow exports to JSON/NetCDF/CSV for WebGL/Java clients.
   - Log outputs to `out/cosmos/` with metadata (version, timestamp, configuration).

Deliverable: End-to-end cosmological simulation producing datasets ready for visualization and calibration reports.

---

## Phase 4 – Visualization & Client Integration

1. **Python Plotly dashboards (`ssz_cosmos/viz.py`)**
   - Implement `plot_slice(field_data)` for 2D slices of σ/τ/n.
   - Implement `plot_isosurface(field_data)` for 3D volume rendering.
   - Add timeline controls (Slider, Play) for epoch animation.

2. **WebGL integration**
   - Extend `segmented-solar-webgl/docs/app.js` to load exported JSON (positions, field LUTs).
   - Visualize superposed fields with instanced Icospheres or volumetric approximations.
   - Provide timeline GUI using lil-gui.

3. **Java/TeaVM client**
   - Update `segmented-solar-java` to fetch simulation data, render multiple bodies, and display fields for N/τ/n.
   - Add screenshot/export functionality for cosmological scenes.

Deliverable: Consistent visualization platform across Python, WebGL, and Java clients for the cosmological outputs.

---

## Phase 5 – Testing, Validation, Documentation

1. **Testing**
   - Expand `ssz_test_suite.py` with cosmology tests (field superposition, β calibration, GAIA ingestion). Ensure Windows console compatibility (ASCII logs).
   - Add integration tests from `tests/cosmos/` covering the full pipeline.

2. **Documentation**
   - Update `README_SSZ_COMPLETE.md` and `docs/SSZ_COSMOS_PLAN.md` with user-facing instructions.
   - Create `docs/COSMOS_USAGE.md` detailing CLI/GUI usage, data requirements, calibration workflows.

3. **Release preparations**
   - Generate reproducible datasets for the solar system and include optional Jupyter notebooks showcasing analysis.
   - Ensure GitHub Pages (WebGL + documentation) are updated.

Deliverable: Verified, documented, and release-ready cosmological SSZ suite.

---

## Milestones Summary

- **M1**: Skeleton modules and tests scaffolded (Phase 1).
- **M2**: Ephemerides ingestion + multi-body fields operational (Phase 2).
- **M3**: Simulation runner + β calibration functional (Phase 3).
- **M4**: Visualization clients integrated (Phase 4).
- **M5**: Full test suite passing, documentation updated (Phase 5).

Each milestone should include a short demo (CLI run, notebook, or visualization) plus notes on open issues.

---

## Risk & Mitigation

- **Data coverage**: GAIA data may be incomplete for some bodies. Mitigation: provide converter for JPL Horizons and allow synthetic fallback.
- **Performance**: Large grids could be expensive. Mitigation: add sampling modes, use Numba/JAX for heavy computations.
- **License compliance**: Ensure all new code carries the Anti-Capitalist Software License headers.

---

## Next Steps

1. Implement Phase 1 skeletons with docstrings referencing the relevant Markdown papers.
2. Begin Phase 2 by wiring GAIA ingestion and validating with sample data.
3. Schedule regular checkpoints (after each milestone) to review progress and adjust plan.
