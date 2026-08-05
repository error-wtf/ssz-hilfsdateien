# NEXT PROMPT - LIGO Phase 1B Extraction Validation

**DO NOT EXECUTE UNTIL EXTRACTION IS COMPLETE**
**WAIT FOR USER CONFIRMATION**

---

## Execution Trigger

Run this prompt only when:
- User confirms extraction is complete
- Or after checking that nested/ directory has content
- And no extraction process is running

---

## Prompt Text (Copy to Chat)

```
You are working in:

E:\clone\ligo-gw240925-gw250207-release

TASK ID:
LIGO_PHASE_1B_EXTRACTION_VALIDATION_BEFORE_ANALYSIS

STRICT RULES:
1. Do not run scientific analysis yet.
2. Do not open large HDF5 datasets fully.
3. Do not run notebooks yet.
4. Do not modify raw archives.
5. Do not delete anything.
6. Do not claim extraction success until all expected archive folders exist and contain files.
7. Every finding must be written to a report.

EXPECTED NESTED ARCHIVES:
- combined_samples.tar.gz
- calibration.tar.gz
- cal_env.tar.gz
- ringdown.tar.gz
- residuals.tar.gz
- notebook.tar.gz
- tiger.tar.gz
- fti.tar.gz
- pca.tar.gz
- pseobnr.tar.gz
- qnmrf.tar.gz
- skymaps.tar.gz
- GW240925-C00-Strain.tar

EXPECTED NESTED EXTRACTION ROOT:
E:\clone\ligo-gw240925-gw250207-release\01_EXTRACTED\nested

OBJECTIVE:
Validate that nested archive extraction completed safely and completely before any scientific inspection.

REQUIRED ACTIONS:
1. Inspect:
   E:\clone\ligo-gw240925-gw250207-release\01_EXTRACTED\nested

2. For each expected archive, determine:
   - extraction folder exists: YES/NO
   - number of files
   - total extracted size
   - largest files
   - file extensions present
   - obvious empty/corrupt result: YES/NO
   - extraction status: PASS/FAIL/BLOCKED/UNKNOWN

3. Compare extracted folders against expected archive names.

4. Look for:
   - empty folders
   - partial extraction artifacts
   - zero-byte files
   - duplicate extraction folders
   - error logs
   - unfinished temp files
   - suspiciously small outputs

5. Generate a complete recursive manifest:
   E:\clone\ligo-gw240925-gw250207-release\02_INVENTORY\NESTED_EXTRACTION_MANIFEST.csv

CSV columns:
archive_name, extraction_folder, full_path, filename, extension, size_bytes, last_modified

6. Generate a validation report:
   E:\clone\ligo-gw240925-gw250207-release\02_INVENTORY\NESTED_EXTRACTION_VALIDATION_REPORT.md

The report must include:
- summary table for all 13 expected archives
- PASS/FAIL/BLOCKED/UNKNOWN status per archive
- total extracted size
- total file count
- warnings
- incomplete or suspicious folders
- recommendation whether Phase 2 may start

7. Generate a log:
   E:\clone\ligo-gw240925-gw250207-release\06_WINDSURF_LOGS\PHASE_1B_EXTRACTION_VALIDATION_LOG.md

PASS CRITERIA:
PASS only if:
- all 13 expected archive extraction folders exist
- all folders contain files
- no zero-byte critical files are found
- no extraction errors are found
- manifest exists
- validation report exists
- log exists

FAIL CRITERIA:
FAIL if:
- one or more archive folders are missing
- extraction clearly failed
- important folders are empty
- corrupt/zero-byte critical files are detected

BLOCKED CRITERIA:
BLOCKED if:
- extraction is still running
- files are locked
- nested directory is inaccessible

FINAL RESPONSE FORMAT:
STATUS: PASS/FAIL/BLOCKED/PARTIAL
REPORT: <path>
MANIFEST: <path>
LOG: <path>
ARCHIVES_OK: <number>/13
WARNINGS:
- <warning 1>
- <warning 2>
NEXT:
<one precise recommendation>
```

---

## After Validation PASS

**Phase 2 Prompt (Science Mapping):**

```
TASK ID: LIGO_PHASE_2_SCIENCE_MAPPING

STRICT RULES:
1. Do not run scientific analysis yet.
2. Do not open large HDF5 datasets fully (only structure).
3. Do not run notebooks yet.
4. Do not modify any files.
5. Focus: inventory and mapping only.

OBJECTIVE:
Map extracted LIGO data to scientific categories without interpretation.

REQUIRED ACTIONS:
1. HDF5 structure inspection (headers only, not loading data)
2. Notebook dependency analysis (imports, requirements)
3. File categorization:
   - GW240925 vs GW250207
   - C00 vs C01 vs envcal
   - Strain / Posterior / Ringdown / Residual / GR-Test
4. Generate mapping reports
5. Document all outputs

OUTPUTS:
- 02_INVENTORY/HDF5_STRUCTURE_REPORT.md
- 02_INVENTORY/NOTEBOOK_DEPENDENCY_REPORT.md
- 02_INVENTORY/LIGO_RELEASE_SCIENCE_MAP.md
- 06_WINDSURF_LOGS/PHASE_2_SCIENCE_MAPPING_LOG.md
```

---

## Checkpoint Summary

**Current Status:**
- Phase 1 (Evidence Inventory): ✅ COMPLETE
- Phase 1B (Nested Extraction): ⏳ RUNNING (do not disturb)
- Phase 1B Validation: ⏳ READY (prompt prepared)
- Phase 2 (Science Mapping): ⏳ PENDING

**Prepared Documents:**
- ✅ SSZ_LIGO_TEST_FRAMEWORK.md
- ✅ PHYSICS_FOUNDATIONS.md
- ✅ NOTEBOOK_REPRODUCTION_PLAN.md
- ✅ CALIBRATION_COMPARISON_PLAN.md
- ✅ POSTERIOR_COMPARISON_PLAN.md
- ✅ GR_TEST_AND_RINGDOWN_COMPARISON_PLAN.md
- ✅ THIS_PROMPT.md (ready for execution)

**Next Action:**
WAIT for extraction completion, then execute THIS_PROMPT.md
