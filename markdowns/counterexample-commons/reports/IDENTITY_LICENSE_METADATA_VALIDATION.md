# Identity, License and Metadata Validation Report

**Date:** 2026-05-23
**Validator:** Cascade (Windsurf AI)
**Project:** Counterexample Commons v0.1.0
**Test Suite:** 132/132 passed, 0 warnings, 0 flake8 errors

## Validation Matrix

| # | Check | Result |
|---|-------|--------|
| 1 | Canonical project name is Counterexample Commons | PASS |
| 2 | Repository slug is counterexample-commons | PASS |
| 3 | Project does not use OpenAI branding as its identity | PASS |
| 4 | README accurately describes the 2026 mathematical result | PASS |
| 5 | README distinguishes source-documented and locally reproduced claims | PASS |
| 6 | README contains political and scientific mission | PASS |
| 7 | README identifies project as source-available under ACSL v1.4 | PASS |
| 8 | LICENSE contains exact ACSL v1.4 text with Copyright (c) 2026 Lino Casu | PASS |
| 9 | External sources are not relicensed under ACSL | PASS |
| 10 | THIRD_PARTY_SOURCES_AND_LICENSES.md exists | PASS |
| 11 | NOTICE.md exists | PASS |
| 12 | CITATION.cff exists and validates as YAML | PASS |
| 13 | references.bib exists with all verified primary sources | PASS |
| 14 | CLAIM_TO_SOURCE_MATRIX.md exists | PASS |
| 15 | GitHub topics list exists and excludes open-source | PASS |
| 16 | Social preview brief exists without corporate branding | PASS |
| 17 | No unsupported affiliation claim exists | PASS |
| 18 | No unsupported theorem-reproduction claim exists | PASS |
| 19 | No live deployment or publication was performed | PASS |
| 20 | .zenodo.json validates as JSON | PASS |
| 21 | pyproject.toml validates as TOML | PASS |
| 22 | All 132 unit/integration/structure tests pass | PASS |
| 23 | No unused imports in Python source (flake8 0 errors) | PASS |
| 24 | No Gradio deprecation warnings (-W error::UserWarning) | PASS |
| 25 | case_studies/erdos_unit_distance_2026/ has README | PASS |
| 26 | Claim registry consistency (status matches locally_validated) | PASS |
| 27 | All 42 required files exist and are non-empty | PASS |
| 28 | No API keys or secrets in Python source | PASS |
| 29 | CITATION.cff author is Casu | PASS |
| 30 | .zenodo.json creator is Casu, Lino | PASS |
| 31 | .gitignore covers .env and __pycache__ | PASS |
| 32 | Repository topics exclude open-source | PASS |
| 33 | Edge case + stress tests (negative n, k=1, grid 10x10, line 200) | PASS |
| 34 | Squared distance exact arithmetic verified | PASS |

**Result: 34/34 PASS**

## Placeholders Requiring Replacement Before Publication

| Placeholder | Location | Replace With |
|-------------|----------|-------------|
| REPOSITORY_URL_PLACEHOLDER | CITATION.cff | https://github.com/OWNER/counterexample-commons |
| PROJECT_URL_PLACEHOLDER | CITATION.cff | Project homepage or repo URL |
| RELEASE_DATE_PLACEHOLDER | CITATION.cff | Actual release date (YYYY-MM-DD) |
| OWNER | docs/GRADIO_LOCAL_EXECUTION.md | GitHub username (error-wtf) |

## Git Initialization Commands

```bash
cd E:\clone\counterexample-commons
git init
git add -A
git commit -m "feat: initial Counterexample Commons repository — identity, licensing, exact validators, Gradio UI, full test suite"
```

## Summary

| Item | Value |
|------|-------|
| Project name | Counterexample Commons |
| Version | 0.1.0 |
| License | Anti-Capitalist Software License (v 1.4) |
| Copyright | 2026 Lino Casu |
| Python package | counterexample_commons |
| Test suite | 132 tests across 6 modules |
| Flake8 | 0 errors (all Python code) |
| Files created | 42+ |
| Forbidden actions verified | No push, no deploy, no DOI, no OpenAI branding, no open-source label |
