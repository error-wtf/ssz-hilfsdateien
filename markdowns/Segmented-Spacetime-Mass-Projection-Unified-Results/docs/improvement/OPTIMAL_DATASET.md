# Optimal Dataset Specification for SEG Paired Tests

## 1. Objectives
- Achieve ≥90% SEG win rate in paired tests by ensuring input observations are high-quality and consistent.
- Provide reproducible criteria for curating emission-line datasets.
- Identify authoritative data sources and acquisition workflows.

## 2. Applicable Target Classes
- **Class A (Galactic Center):** Sgr A* and fast-moving S-stars (current clean dataset).
- **Class B (Nearby Massive Black Holes):** e.g., NGC 4258 (H2O masers), M87* emission-line knots, providing relativistic environments with reliable VLBI/maser measurements.
- **Class C (Compact Binary Systems):** systems with precise spectroscopic orbits (e.g., X-ray binaries, microquasars) where relativistic redshift components are measurable.

Each class must meet the quality requirements below and supply class-specific metadata (instrument, source catalog, reduction pipeline).

## 3. Quality Requirements
- **Completeness:** No missing values in critical columns: `M_solar`, `r_emit_m`, `z`, `v_los_mps`, `v_tot_mps`, `lambda_emit_nm`, `lambda_obs_nm`, `T0_year`, `f_true_deg`, `N0`, `z_geom_hint`.
- **Physical validity:** All numeric fields must be finite and strictly positive where required (mass, radius, wavelengths, velocities, `N0`).
- **Reliable geometry hint:** `z_geom_hint` must be derived from vetted relativistic models (e.g., GRAVITY collaboration orbital fits) and never left at zero.
- **Instrument traceability:** Each row shall include `instrument`, `pipeline`, and `data_release` references.
- **Temporal consistency:** Observations should be calibrated to a unified epoch model (e.g., IAU SOFA standards) with `T0_year` documented.

## 4. Recommended Data Sources
- **GRAVITY (VLTI) collaboration:** High-precision infrared spectroscopy and astrometry around Sgr A*. *(Primary source for 2017–2024 observations.)*
- **Keck/NIRC2 & NIRSPEC:** Complementary Sgr A* data with long baseline coverage; ensure the latest calibration pipeline is applied.
- **ESO Science Archive:** Access to raw + pipeline products for GRAVITY and SINFONI datasets; use Phase 3 products with certified reductions.
- **Publications:** Cross-validate with peer-reviewed orbital solutions (e.g., Gravity Collaboration 2022, Parsa et al. 2017) for `z_geom_hint` inputs.

Additional sources for Classes B/C:
- **VLBI/ALMA archives:** Provide M87* jet emission-line measurements and maser-based rotation curves (e.g., via NRAO archive).
- **NASA/IPAC Extragalactic Database (NED):** Curated spectroscopic catalogs for nearby AGN with emission-line velocities.
- **Chandra/XMM-Newton archives:** Spectroscopic observations of compact binaries; use dedicated pipelines to extract relativistic line shifts.

## 5. Acquisition Workflow
1. Query ESO/Keck archives for emission-line spectra near the Galactic Center.
2. Download calibrated spectra (FITS) and associated metadata.
3. Derive `z`, `v_tot_mps`, and `v_los_mps` from spectral lines using instrument-provided wavelength solutions.
4. Compute `r_emit_m` from astrometric offsets using latest distance to Sgr A* (8.178 kpc).
5. Generate `z_geom_hint` via segmented-spacetime solver (e.g., `segspace_all_in_one_extended.py --mode hint-only`).
6. Assemble rows into CSV, verifying quality constraints.

## 6. Validation Steps
- Run `python scripts/clean_real_data_emission_lines.py` and confirm zero rows removed.
- Execute `python perfect_paired_test.py --csv data/real_data_emission_lines_clean.csv` and verify ≥90% win rate.
- Document dataset version, source archives, and reduction pipeline in `data/README.md`.

## 7. Future Enhancements
- Extend the cleaning script to detect and tag target classes automatically using (`object_name`, `instrument`) metadata.
- Add fetch automation for GRAVITY data using ESO TAP queries.
- Integrate automatic `z_geom_hint` computation with uncertainty estimates.
- Extend criteria to other targets (e.g., NGC 4258) once high-quality data are available.
