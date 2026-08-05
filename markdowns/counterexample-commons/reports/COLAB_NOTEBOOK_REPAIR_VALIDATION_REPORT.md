# Colab Notebook Repair Validation Report

**Date:** 2026-05-25
**Auditor:** Windsurf / Cascade

## Initial Status (Before Repair)

```
COLAB_NOTEBOOKS_FUNCTIONAL_IN_FRESH_RUNTIME: FAIL
LOCAL_NBCONVERT_IN_EXISTING_CHECKOUT:        PASS
COLAB_BOOTSTRAP_REPOSITORY_INSTALLATION:    MISSING
ALL_NOTEBOOKS_USING_ROBUST_PATH_TRAVERSAL:  FALSE
```

## Root Causes (Confirmed)

- Repository was not cloned or installed in any notebook's Colab bootstrap.
- Local Windows nbconvert outputs (containing `E:\clone\..\.venv\...` paths)
  were committed to notebooks and misrepresented as Colab functionality.
- App was built locally but never launched; output `App built successfully`
  was confused with Colab Gradio launch.
- Legacy `sys.path.insert(0, "..")` remained in 5 notebooks after previous
  partial fix attempt.

## Bootstrap Pattern Implemented

All 9 notebooks importing project code now use one canonical bootstrap:

```python
import os, sys, subprocess
from pathlib import Path

IN_COLAB = "google.colab" in sys.modules
REPO_URL = "https://github.com/error-wtf/counterexample-commons.git"
REPO_DIR = Path("/content/counterexample-commons")

if IN_COLAB:
    if not REPO_DIR.exists():
        subprocess.run(["git", "clone", "--depth", "1", REPO_URL, str(REPO_DIR)], check=True)
    subprocess.run([sys.executable, "-m", "pip", "install", "-q", "-e", str(REPO_DIR)], check=True)
    os.chdir(REPO_DIR)
    if str(REPO_DIR) not in sys.path:
        sys.path.insert(0, str(REPO_DIR))
else:
    _here = Path.cwd().resolve()
    _repo_root = next(
        (p for p in [_here, *_here.parents]
         if (p / "counterexample_commons").is_dir() and (p / "pyproject.toml").exists()),
        None,
    )
    if _repo_root is None:
        raise RuntimeError("Repository root not found. Run from inside cloned repo.")
    os.chdir(_repo_root)
    if str(_repo_root) not in sys.path:
        sys.path.insert(0, str(_repo_root))
```

## Notebooks Modified

- `notebooks/00_START_HERE_Colab.ipynb`
- `notebooks/00A_Launch_Gradio_UI_in_Colab.ipynb`
- `notebooks/00B_Launch_Public_Baseline_Demo_Only.ipynb`
- `notebooks/02_Exact_Baseline_Reproduction.ipynb`
- `notebooks/03_Interactive_Unit_Distance_Explorer.ipynb`
- `notebooks/04_Controlled_AI_Construction_Experiment.ipynb`
- `notebooks/04A_Compare_Multiple_Providers.ipynb`
- `notebooks/04B_Ollama_Local_Execution_Guide.ipynb`
- `notebooks/05_Export_Validated_Report.ipynb`

## Notebook Outputs Cleared

- `notebooks/00A_Launch_Gradio_UI_in_Colab.ipynb` (contained `.venv` Windows path)
- `notebooks/00B_Launch_Public_Baseline_Demo_Only.ipynb` (contained `.venv` Windows path)

## Legacy sys.path Hacks Remaining

NONE — all `sys.path.insert(0, "..")` removed.

## README Updated

- Removed claim "10 ready-to-use Google Colab notebooks".
- Added honest wording: "locally validated after bootstrap repair; fresh Colab runtime verification still pending".
- Added Open-in-Colab badge links for all 6 safe public notebooks.
- Labelled AI/provider notebooks as optional private/manual use only.

## Local Validation Results

```
LOCAL_NBCONVERT_AFTER_REPAIR:              PASS (10/10)
FRESH_COLAB_RUNTIME_EXECUTION:             NOT_YET_VERIFIED
PUBLIC_NOTEBOOK_OUTPUTS_CLEAN:             PASS
LOCAL_WINDOWS_PATHS_REMOVED_FROM_OUTPUTS: PASS
LIVE_PROVIDER_CALLS_DURING_LOCAL_TEST:     NO
PYTEST:                                    PASS (232/232)
FLAKE8:                                    PASS (clean)
SECRETS_EXPOSED:                           NO
```
