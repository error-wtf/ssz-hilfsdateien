# Changelog

All notable changes to Counterexample Commons will be documented in this file.

## [Unreleased]

### Fixed
- build: fix `pyproject.toml` build-backend to `setuptools.build_meta` for clean-venv compatibility
- test: exclude `.venv/` from secret scan in `test_repo_structure.py`

## [0.1.0-repair] - 2026-05-25

### integrity(Sawin)
- Downgraded `UD-SAWIN-2026-001` from `LOCALLY_REPRODUCED_NUMERICAL` to `SOURCE_DOCUMENTED`
- Replaced fake `sawin_construction.py` with honest `NotImplementedError` placeholder
- Added `rational_mesh_baseline.py` with exact finite baseline (`UD-BASE-RATIONAL-MESH-001`)
- Added 15 Sawin + 2 claim-integrity guard tests (now 231 total, 231 passing)
- Added `SAWIN_REPRODUCTION_ROADMAP.md` with realistic reproduction levels
- Added `SAWIN_CLAIM_INTEGRITY_AUDIT.md` and `SAWIN_REPAIR_IMPLEMENTATION_REPORT.md`
- Corrected README reproduction table, image caption, and false asymptotic claim
- Exposed all 6 execution modes in `run_gradio_local.py` CLI
- Added `SOURCE_DOCUMENTED` caveat to Gradio UI overview tab
- Added rational mesh row to `CLAIM_TO_SOURCE_MATRIX.md`

## [0.1.0] - UNRELEASED

### Added

- Canonical Counterexample Commons project identity.
- ACSL v1.4 licensing layer under Copyright (C) 2026 Lino Casu.
- Primary-source documentation for the 2026 unit-distance case study.
- Exact finite validation framework.
- Multi-provider AI experimentation architecture.
- Google Colab execution layer.
- Gradio main UI architecture.