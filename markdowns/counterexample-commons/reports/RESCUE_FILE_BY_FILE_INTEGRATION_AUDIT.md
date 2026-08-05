# RESCUE_FILE_BY_FILE_INTEGRATION_AUDIT.md
**Date:** 2025-05-27  
**Rescue Branch:** `rescue/integrated-complete-lab`  
**Sources Compared:**
- `origin/main` - Source of truth for README identity
- `origin/rebuild/colab-complete-lab` - Windsurf rebuild (evidence only)
- `origin/recovery/complete-gradio-lab-codex` - Codex recovery (selective code donor)

## Baseline Health Check (main)
- **Compile:** PASS
- **Pytest:** 232 passed
- **Flake8:** Minor issues only (E501, F401, W292)

## Integration Strategy

### README.md / Identity
- **Source:** `origin/main`
- **Action:** Preserve with targeted fix only
- **Fix Required:** "Sawin Lattice" → "Finite Rational Mesh Baseline"
- **REJECT:** Codex dry status memo

### Core Application Code
- **Source:** `origin/main` baseline
- **Selective import from Codex:**
  - `app/main.py` - Review for functional improvements
  - `.env.example` - If present and clean
  - `counterexample_commons/env_loader.py` - If validated
- **REJECT:** Rebuild app code (known broken)

### Claims & Source Map
- **Source:** `origin/main`
- **CRITICAL:** Must maintain:
  - Sawin: `SOURCE_DOCUMENTED` (arXiv:2605.20579)
  - **NOT** `PRIMARY_PROOF_PENDING`
  - OpenAI: `SOURCE_DOCUMENTED` (not locally reproduced)

### Documentation Images
- **From Codex (uncommitted):**
  - `docs/images/sawin_lattice.png` → `docs/images/rational_mesh_baseline.png` (rename captured)
- **Verification:** Ensure caption matches "Finite rational mesh baseline (not Sawin's construction)"

### Test Suite
- **Source:** `origin/main`
- **Verify:** All Sawin tests correctly assert `SOURCE_DOCUMENTED` status only

## Files Under Review

| File | main | rebuild | recovery/codex | Decision |
|------|------|---------|----------------|----------|
| README.md | Rich identity | WIP mix | Dry status memo | **USE main** |
| app/main.py | Baseline | Broken WIP | Gradio tabs | **AUDIT codex** |
| counterexample_commons/claims.py | Correct | N/A | Modified | **VERIFY codex** |
| docs/images/*.png | Original | N/A | Renamed | **IMPORT codex rename** |
| .env.example | May exist | N/A | May exist | **IF clean, use** |
| notebooks/Colab.ipynb | Single | Present | N/A | **RESERVE for later** |

## Scientific Provenance Invariants

These must NOT change:

```
SAWIN_EXPLICIT_EXPONENT_1_014:
  status: SOURCE_DOCUMENTED
  primary_source: arXiv:2605.20579
  primary_proof_pending: False

OPENAI_FIXED_DELTA_DISPROOF:
  status: SOURCE_DOCUMENTED
  locally_validated: False

FINITE_RATIONAL_MESH:
  status: LOCALLY_REPRODUCED_EXACT
  note: "Not Sawin's construction"
```

## Prohibited Changes
- NO removal of anti-capitalist mission statement
- NO replacement of README with status memo
- NO `PRIMARY_PROOF_PENDING` for Sawin
- NO asymptotic claims from finite validation
- NO blind import of Codex README
- NO wholesale merge of rebuild branch

## Next Steps
1. Read and compare actual file contents
2. Import Codex image rename
3. Fix Sawin title in README
4. Verify claims.py status values
5. Local commits with audit trail
6. AWAIT USER APPROVAL for any push
