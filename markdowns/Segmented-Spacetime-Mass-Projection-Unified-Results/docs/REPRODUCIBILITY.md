# Reproducibility Guide

This guide explains how to reproduce runs of the Segmented Spacetime (SSZ) cosmology pipeline.

## 1. Environment Setup

1. Create a virtual environment inside the repository:
   ```bash
   python -m venv .venv
   .\.venv\Scripts\activate  # Windows PowerShell
   pip install --upgrade pip wheel setuptools
   ```
2. Install dependencies (placeholder until requirements are consolidated):
   ```bash
   pip install numpy scipy pandas astropy astroquery pyvo pyerfa pyproj healpy pyarrow fastparquet tqdm loguru pydantic rich matplotlib plotly kaleido
   ```
3. Configure credentials by copying `.env.example` to `.env` and filling GAIA login details and data paths.

## 2. Directory Layout

All outputs are organized by run identifier (`RUN_ID`), e.g., `2025-10-17_gaia_ssz_v1`:
- Raw GAIA dumps: `data/raw/gaia/<RUN_ID>/`
- Interim cleaned catalogues: `data/interim/gaia/<RUN_ID>/`
- Processed cosmology fields: `models/cosmology/<RUN_ID>/`
- Solar system projections: `models/solar_system/<RUN_ID>/`
- Experiment artefacts: `experiments/<RUN_ID>/qa/`, `experiments/<RUN_ID>/viz/`
- Logs: `data/logs/`
- Backups/Snapshots: `backups/`

## 3. Typical Workflow

1. **Fetch GAIA data**
   ```bash
   python scripts/gaia/fetch_gaia_adql.py --adql queries/gaia_dr3_core.sql --limit 200000 --out data/raw/gaia/<RUN_ID>/ --cache data/cache/astro/ --run-id <RUN_ID>
   python scripts/gaia/fetch_gaia_conesearch.py --config configs/gaia_cones.json --out data/raw/gaia/<RUN_ID>/ --cache data/cache/astro/ --run-id <RUN_ID>
   ```
2. **Preprocess**
   ```bash
   python scripts/preprocess/gaia_clean_map.py --run-id <RUN_ID>
   python scripts/preprocess/gaia_frame_transform.py --run-id <RUN_ID>
   ```
3. **Build SSZ cosmology field**
   ```bash
   python scripts/SSZ/build_ssz_model.py --run-id <RUN_ID>
   ```
4. **Solar system embedding**
   ```bash
   python scripts/SSZ/build_solar_system_model.py --run-id <RUN_ID>
   ```
5. **Visualization**
   ```bash
   python scripts/viz/plot_ssz_maps.py --run-id <RUN_ID>
   ```
6. **End-to-end runner (planned)**
   ```bash
   python run_gaia_ssz_pipeline.py --run-id <RUN_ID> ...
   ```

## 4. Manifest Generation

Each pipeline run should create `experiments/<RUN_ID>/MANIFEST.json` capturing:
- Start/finish timestamps.
- Input data fingerprints (SHA256).
- Output artefact hashes.
- Environment snapshot (`pip freeze` or lock file hash).
- Git commit hash (if repository is versioned).

## 5. Validation

Planned validation components:
- `scripts/tests/test_ssz_invariants.py` (segment counts, natural boundary checks).
- `notebooks/qa/qa_checks.ipynb` for exploratory verification.
- QA plots saved to `experiments/<RUN_ID>/qa/`.

## 6. Notes

- All scripts avoid overwriting inputs; new files are time-fragmented (`__partNN_timestamp`).
- GAIA service usage must comply with rate limits.
- Update configurations in `configs/` to reflect new data sources or parameter choices.
