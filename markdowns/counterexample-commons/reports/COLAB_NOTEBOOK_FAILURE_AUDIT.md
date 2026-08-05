# Colab Notebook Bootstrap Failure Audit

**Date:** 2026-05-25
**Auditor:** Windsurf / Cascade

## Status Before Repair

```
COLAB_NOTEBOOKS_FUNCTIONAL_IN_FRESH_RUNTIME: FAIL
LOCAL_NBCONVERT_IN_EXISTING_CHECKOUT:        PASS
COLAB_BOOTSTRAP_REPOSITORY_INSTALLATION:    MISSING
ALL_NOTEBOOKS_USING_ROBUST_PATH_TRAVERSAL:  FALSE
```

## Root Causes

1. No notebook cloned or installed the repository — only external packages
   (`sympy`, `gradio`, etc.) were installed via `!pip install`.
2. Several notebooks used `sys.path.insert(0, "..")`, which only works when
   the CWD is `notebooks/` inside an existing checkout.
3. `00A` and `00B` used `Path(__file__).resolve()` / `globals()` heuristics
   that fail without `__file__` (standard Colab kernel).
4. Local Windows nbconvert outputs (including `E:\clone\...\.venv\...` paths)
   were committed as notebook outputs and misrepresented as Colab evidence.

## Per-Notebook Audit (Before Repair)

| Notebook | Imports project? | Clones repo? | Installs repo? | sys.path hack | Fresh Colab status |
|----------|:---:|:---:|:---:|:---:|:---:|
| 00_START_HERE_Colab | YES | NO | NO | NO | FAIL |
| 00A_Launch_Gradio_UI_in_Colab | YES | NO | NO | NO (broken heuristic) | FAIL |
| 00B_Launch_Public_Baseline_Demo_Only | YES | NO | NO | NO (broken heuristic) | FAIL |
| 01_Problem_and_Primary_Sources | NO | NO | NO | NO | CONTENT_ONLY ✅ |
| 02_Exact_Baseline_Reproduction | YES | NO | NO | `sys.path.insert(0, "..")` | FAIL |
| 03_Interactive_Unit_Distance_Explorer | YES | NO | NO | `sys.path.insert(0, "..")` | FAIL |
| 04_Controlled_AI_Construction_Experiment | YES | NO | NO | `sys.path.insert(0, "..")` | FAIL |
| 04A_Compare_Multiple_Providers | YES | NO | NO | `sys.path.insert(0, "..")` | FAIL |
| 04B_Ollama_Local_Execution_Guide | YES | NO | NO | `sys.path.insert(0, "..")` | FAIL |
| 05_Export_Validated_Report | YES | NO | NO | `sys.path.insert(0, "..")` | FAIL |

## Notebooks Repaired

All 9 notebooks importing project code were repaired with a canonical
bootstrap (see COLAB_NOTEBOOK_REPAIR_VALIDATION_REPORT.md).
`01_Problem_and_Primary_Sources` is content-only and requires no bootstrap.
