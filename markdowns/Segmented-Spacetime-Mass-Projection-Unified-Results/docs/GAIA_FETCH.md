# GAIA Fetch Layer

## Overview

This document describes how the Segmented Spacetime (SSZ) cosmology pipeline retrieves GAIA catalog data using the wrapper scripts in `scripts/gaia/`.

## Scripts

- `scripts/gaia/fetch_gaia_adql.py`
  - Executes a pre-defined ADQL query file against the GAIA TAP service using `astroquery.gaia`.
  - Supports CLI parameters:
    - `--adql`: Path to query file.
    - `--limit`: Optional row cap (applied via subquery wrapper).
    - `--out`: Output directory (new files, no overwrites).
    - `--cache`: Cache directory (placeholder for TAP caches).
    - `--format`: `parquet`, `csv`, or `fits`.
    - `--run-id`: Required identifier for filenames and logs.
    - `--log-dir`: Defaults to `data/logs`.
  - Output filenames follow `run_id__partNN_timestamp.<ext>`, ensuring non-destructive writes.
  - Logs stored in `data/logs/fetch_<run_id>.log`.

- `scripts/gaia/fetch_gaia_conesearch.py`
  - Performs cone searches defined in `configs/gaia_cones.json`.
  - CLI parameters mirror the ADQL script plus `--config` and optional `--sleep` for rate-limit spacing.
  - Each region result is saved separately (`run_id__region__partNN_timestamp.<ext>`).

## Workflow

1. Prepare a run identifier, e.g., `2025-10-17_gaia_ssz_v1`.
2. Ensure `.env` contains GAIA credentials or configure session manually.
3. Place ADQL query files under `queries/` and region configs in `configs/`.
4. Execute the ADQL wrapper to create `data/raw/gaia/<RUN_ID>/...` outputs.
5. Optionally run the cone search wrapper for complementary regions.
6. Check `data/logs/` for job status and diagnostics.

## Rate Limits & Etiquette

- Sleep of at least two seconds between queries is enforced by default.
- Respect GAIA TAP service usage policies: chunk large downloads, avoid simultaneous jobs.
- The scripts currently run sequentially; for bulk jobs, manually throttle submissions.

## Error Handling

- Network faults raise exceptions; retry logic can be added at caller level.
- Missing output directories trigger user-friendly errors.
- Table conversions use `astropy` for FITS and `pandas` for CSV/Parquet.

## Next Steps

- Integrate TAP+ authentication with `.netrc` or credential prompts.
- Add chunked retrieval for very large ADQL results.
- Store TAP job IDs alongside logs for audit trails.
