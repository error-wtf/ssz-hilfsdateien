# SSZ Calculation Suite - Fix Plan

**Version:** 1.0.0  
**Created:** 2025-01-16  
**Status:** PHASE 0 Complete → Starting PHASE 1

---

## Priority Order

| Priority | Phase | Component | Effort | Status |
|----------|-------|-----------|--------|--------|
| P1 | 1 | DataModel + CSV Schema | Medium | 🔄 IN PROGRESS |
| P2 | 2 | Single Object Pipeline | Low | ⏳ PENDING |
| P3 | 2 | Batch Calculate Pipeline | Low | ⏳ PENDING |
| P4 | 3 | Compare Pipeline | Medium | ⏳ PENDING |
| P5 | 4 | Run Bundles + Downloads | Medium | ⏳ PENDING |
| P6 | 5 | Dynamic Reference Tab | Low | ⏳ PENDING |
| P7 | - | Deployment (Dockerfile) | Medium | ⏳ PENDING |

---

## PHASE 1: DataModel & CSV Schemas

### 1.1 Central DataModel ✅ DONE
- [x] DataFrame + metadata structure
- [x] Units: M_Msun (solar masses), R_km (kilometers), v_kms (km/s)
- [x] Optional columns with defaults: v_kms=0, z_obs=NaN

### 1.2 CSV Upload Validator ✅ DONE
- [x] Schema detection (OBJECT_LIST vs RING_DATA)
- [x] Column aliases (M_msun, r_m, etc.)
- [x] Clear error messages with line/column info
- [x] r_m → R_km conversion (meters to km)
- [x] Auto-generate names if missing

### 1.3 Template Download ✅ DONE
- [x] Template CSV button
- [x] Correct column format

### 1.4 Preview Table ✅ DONE
- [x] Real data preview (not dummy)
- [x] Shows first 15 rows

---

## PHASE 2: Single Object & Batch

### 2.1 Single Object Tab
- [x] Preset buttons (Sun, NS, WD)
- [x] Manual input fields
- [x] Calculate button
- [x] Numeric results display
- [x] Time Dilation plot (D_SSZ vs D_GR)
- [x] Xi profile plot
- [x] Redshift breakdown plot
- [ ] **TODO:** Run Bundle download button
- [ ] **TODO:** Copy Run-ID button

### 2.2 Batch Calculate Tab
- [x] Uses Data tab dataset
- [x] Results table
- [x] Summary statistics
- [x] 4 visualization plots
- [x] Export results CSV
- [ ] **TODO:** Run Bundle download (.zip)

---

## PHASE 3: Compare Pipeline

### 3.1 Compare Tab
- [x] Object dropdown
- [x] Refresh button
- [x] Comparison output
- [x] Plots
- [ ] **TODO:** Check z_obs presence
- [ ] **TODO:** Show "disabled: missing z_obs" when appropriate
- [ ] **TODO:** Scatter + residuals when z_obs present

---

## PHASE 4: Run Bundles

### 4.1 Bundle Contents
- [ ] params.json (phi, xi_max, constants, regime rules, version)
- [ ] data_input.csv (normalized)
- [ ] results.csv
- [ ] report.md
- [ ] plots/*.png
- [ ] errors.log (if any)

### 4.2 UI Components
- [ ] Download Run Bundle (.zip) button
- [ ] Copy Run-ID button
- [ ] Show Run Summary (no local paths!)

### 4.3 Storage
- [ ] Server-side Run-ID based storage
- [ ] Ephemeral or SQLite + object storage
- [ ] Never show file paths in UI

---

## PHASE 5: Dynamic Reference Tab

### 5.1 Current Run Parameters
- [ ] Show phi, xi_max from current config
- [ ] Show regime thresholds
- [ ] Show method IDs

### 5.2 Formulas
- [x] Xi formulas (weak/strong/blend)
- [x] D_SSZ, D_GR formulas
- [x] Redshift formulas
- [ ] **TODO:** LaTeX rendering

### 5.3 Assumptions Section
- [ ] Regime selection rules
- [ ] Units and frames
- [ ] Data sources

### 5.4 Document References
- [ ] Use doc-id format (no local paths, no web links)
- [ ] Reference to repo documents

---

## Deployment

### Dockerfile
- [ ] Python 3.10+ base
- [ ] Install requirements
- [ ] Expose port 7860
- [ ] Health endpoint /health
- [ ] Entrypoint: gradio/uvicorn

### Requirements
- [x] requirements.txt exists
- [ ] Pin versions for reproducibility

### CI/CD
- [ ] Basic test runner
- [ ] Lint check (optional)

---

## Critical Fixes Required

### 1. Remove Local Paths from UI
**Location:** `app_v3.py` footer
**Current:** Shows `./reports/<run_id>/`
**Fix:** Remove or replace with "Download Run Bundle"

### 2. Run Bundle Implementation
**Files needed:**
- `segcalc/core/run_bundle.py` - Bundle creation
- Update `app_v3.py` - Download buttons

### 3. Compare Tab z_obs Check
**Location:** `app_v3.py` Compare tab
**Fix:** Add check for z_obs, show disabled message

### 4. Dockerfile
**Create:** `Dockerfile` in root
**Contents:** See deployment section

---

## Acceptance Criteria Checklist

- [x] All tabs visible (9 tabs present)
- [x] No placeholder tables/plots
- [x] Sun preset → Calculate produces real numbers
- [x] CSV wrong schema → clear error + template
- [x] CSV correct → preview works
- [ ] Compare with z_obs → scatter + residuals + table
- [ ] Compare without z_obs → disabled message
- [ ] Run Bundle contains all required files
- [ ] App deployable via Docker
- [ ] No local paths in UI

---

## Next Immediate Actions

1. ~~Create FEATURE_MATRIX.md~~ ✅
2. ~~Create FIX_PLAN.md~~ ✅
3. Remove local paths from footer
4. Create run_bundle.py module
5. Add Download Bundle buttons
6. Fix Compare tab z_obs handling
7. Create Dockerfile
8. Test deployment

---

**Estimated Completion:** 2-3 hours for full implementation
