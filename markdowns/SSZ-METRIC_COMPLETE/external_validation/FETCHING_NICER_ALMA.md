# Fetching Public Astroquery Datasets (NICER / ALMA)

This directory implements robust, reproducible download utilities for astrophysical data.

## Installation

Ensure that you have installed the `external-data` optional group:
```bash
python -m pip install -e ".[external-data]"
```

## Workflows

All downloads follow a safe, three-step dry-run and confirmation workflow to prevent network disasters.

### 1. Dry Run / Manifest Generation
Create a manifest first without transferring any data files:
```bash
python scripts/fetch_nicer.py --target "PSR J0030+0451" --max-rows 3 --dry-run
```

### 2. Verified File Transfer
Authorize physical file downloads using explicit confirmations:
```bash
python scripts/fetch_nicer.py --manifest external_validation/manifests/nicer/nicer_manifest.json --download --confirm-download --max-gb 5
```
