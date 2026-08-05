# Cross-Repository Boundary Incident Report

**Date:** 2026-05-25
**Written by:** Cascade (local only — NO COMMIT, NO PUSH)
**Authorised root:** E:\clone\counterexample-commons
**Reported suspect path:** E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\.venv\

---

## 1. The Alleged Incident

The user raised a concern that during the `test_repo_structure.py` secret scan failure, the error message

```
E   AssertionError: Possible API key in E:\clone\counterexample-commons\.venv\Lib\site-packages\huggingface_hub\repocard_data.py: sk-
```

might have originated from a `.venv` belonging to a different repository
(`E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results`), indicating a possible
repository boundary crossing.

---

## 2. Read-Only Verification Results

### 2a. ROOT definition

In `tests/test_repo_structure.py` line 10:

```python
ROOT = Path(__file__).resolve().parent.parent
```

At runtime, with `__file__` = `E:\clone\counterexample-commons\tests\test_repo_structure.py`:

- `parent` = `E:\clone\counterexample-commons\tests`
- `parent.parent` = `E:\clone\counterexample-commons`

**ROOT resolved to: `E:\clone\counterexample-commons` — correct.**

### 2b. rglob boundary verification

Executed in the venv of counterexample-commons:

```python
for p in ROOT.rglob("*.py"):
    if not str(p).startswith(str(ROOT)):
        outside.append(str(p))
```

**Result: 0 files outside ROOT.**

The rglob scan never left `E:\clone\counterexample-commons`.

### 2c. Search for SSZ path in all counterexample-commons files

```powershell
Select-String -Path "E:\clone\counterexample-commons\**\*" -Pattern "Segmented-Spacetime-Mass-Projection-Unified-Results" -SimpleMatch
```

**Result: 0 matches.**

The string `Segmented-Spacetime-Mass-Projection-Unified-Results` does not appear anywhere
in any file under `E:\clone\counterexample-commons`.

### 2d. The actual failing path in the original error

The actual error message was:

```
E   AssertionError: Possible API key in
    E:\clone\counterexample-commons\.venv\Lib\site-packages\huggingface_hub\repocard_data.py: sk-
```

The path begins with `E:\clone\counterexample-commons\.venv\` — this is the `.venv`
**inside counterexample-commons itself**, created by `python -m venv .venv` during Phase B.
It is NOT the `.venv` of `Segmented-Spacetime-Mass-Projection-Unified-Results`.

### 2e. SSZ repo read-only status

```
git -C "E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results" status
```

The SSZ repo shows uncommitted local changes (`M README.md`, etc.) and untracked files —
these are pre-existing modifications entirely unrelated to this session.

```
git -C "E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results" log --oneline -5
```

Most recent commit: `b68ee72` — "docs: fix broken cross-reference links in ENERGY_FRAMEWORK.md"
This predates this session. No commits were added by this session.

---

## 3. Answers to the Required Questions

| Question | Answer |
|----------|--------|
| Did any command read files outside `E:\clone\counterexample-commons`? | Yes — `git -C` read-only inspections of the SSZ repo in this investigation. No other cross-boundary reads. |
| Did any command write or modify files outside `E:\clone\counterexample-commons`? | No. |
| Did any command create, delete, install into, or alter the `.venv` of `Segmented-Spacetime-Mass-Projection-Unified-Results`? | No. |
| Why did the unrelated repository appear in a test run? | It did not. The failing path was `E:\clone\counterexample-commons\.venv\`, not the SSZ repo's `.venv`. |
| What exact value did `ROOT` have at runtime? | `E:\clone\counterexample-commons` — verified by running Python in the venv. |
| Was the `.venv` exclusion merely hiding a wrong-root bug? | No. ROOT was correct. The exclusion was the correct fix: rglob was scanning the project's own `.venv`, which is a standard exclusion pattern. |
| Which repository received commits `c190fb2` and `aa348e9`? | `counterexample-commons` only. |
| Were any files from the SSZ repository included, scanned into reports, committed, or pushed? | No. |

---

## 4. Root Cause of the Original Secret Scan Failure

The `.venv` created in Phase B (`python -m venv .venv`) inside `counterexample-commons` installed
`huggingface_hub`, which contains the literal string `sk-` in `repocard_data.py` as part of
documentation text (not an actual key). The `rglob("*.py")` without `.venv` exclusion picked
this up.

The fix — adding `".venv"` to the `excluded` set — is correct and sufficient for this case.
The root was never wrong.

---

## 5. What Was Not Wrong / What Was Wrong

- **NOT WRONG:** ROOT definition and rglob boundary.
- **NOT WRONG:** No SSZ repository was touched or scanned during the counterexample-commons work.
- **WRONG:** The `.venv` exclusion should have been in the original test from the start.
- **WRONG:** The report failed to clearly state that the triggering path was `counterexample-commons\.venv`, not a foreign repo.

---

## 6. Status

**NO COMMIT. NO PUSH. Local report only.**