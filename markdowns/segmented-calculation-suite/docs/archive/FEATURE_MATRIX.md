# SSZ Calculation Suite - Feature Matrix

**Version:** 1.0.0  
**Last Updated:** 2025-01-16  
**Status:** PHASE 0 Complete

---

## Tab/Feature Status Overview

| Tab | Status | Missing/Issues |
|-----|--------|----------------|
| 🔢 Single Object | WORKING | ✅ Run Bundle download added |
| 📁 Data | WORKING | Fetch caching not shown |
| ⚡ Batch Calculate | WORKING | ✅ Run Bundle download added |
| 📊 Compare | WORKING | ✅ z_obs check + residuals added |
| 🔴 Redshift Eval | WORKING | Minor UI improvements |
| 🌀 Regimes | WORKING | Plot auto-load issue |
| 📖 Reference | PARTIAL | Static, needs dynamic run params |
| ✅ Validation | WORKING | All 63 tests pass |
| 📈 Theory Plots | WORKING | 7 plot types available |

---

## Detailed Feature Breakdown

### 1. 🔢 Single Object Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Sun/NS/WD Presets | ✅ WORKING | Preloads realistic values |
| Manual Input | ✅ WORKING | M_Msun, R_km, v_kms, z_obs |
| Calculate Button | ✅ WORKING | Produces all SSZ quantities |
| Time Dilation Plot | ✅ WORKING | D_SSZ vs D_GR |
| Xi Profile Plot | ✅ WORKING | Ξ(r) across regimes |
| Redshift Breakdown Plot | ✅ WORKING | z components |
| Results Table | ✅ WORKING | All computed values |
| Run Bundle Download | ❌ NOT IMPLEMENTED | TODO: Add download button |
| Copy Run-ID | ❌ NOT IMPLEMENTED | TODO: Add copy button |

### 2. 📁 Data Tab

| Feature | Status | Notes |
|---------|--------|-------|
| CSV Upload | ✅ WORKING | Validates schema |
| Template Download | ✅ WORKING | Correct format CSV |
| Data Preview | ✅ WORKING | Shows loaded data |
| Fetch Dataset | ✅ WORKING | ESO, NS, WD, Template |
| Download Loaded CSV | ✅ WORKING | Exports current data |
| Cache Hit/Miss Display | ❌ NOT IMPLEMENTED | TODO: Show fetch metadata |
| Proceed to Batch | ✅ WORKING | Navigation button |

### 3. ⚡ Batch Calculate Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Run Calculation | ✅ WORKING | Processes all objects |
| Summary Statistics | ✅ WORKING | Win rates, counts |
| Results Table | ✅ WORKING | Full results |
| Comparison Scatter | ✅ WORKING | When z_obs present |
| Regime Distribution | ✅ WORKING | Pie/bar chart |
| Win Rate Chart | ✅ WORKING | SSZ vs GR×SR |
| Compactness Plot | ✅ WORKING | Power law |
| Export Results CSV | ✅ WORKING | Download button |
| Run Bundle Download | ❌ NOT IMPLEMENTED | TODO: Full bundle .zip |

### 4. 📊 Compare Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Object Dropdown | ✅ WORKING | Select from loaded data |
| Refresh Button | ✅ WORKING | Updates dropdown |
| Comparison Output | ✅ WORKING | SSZ vs GR table |
| Time Dilation Plot | ✅ WORKING | D comparison |
| Redshift Plot | ✅ WORKING | z breakdown |
| Disabled State (no z_obs) | ❌ PARTIAL | Needs clear message |

### 5. 🔴 Redshift Eval Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Input Parameters | ✅ WORKING | M, R, v, z_obs |
| Evaluate Button | ✅ WORKING | Computes redshift |
| Results Display | ✅ WORKING | Markdown output |
| Redshift Plot | ✅ WORKING | Breakdown chart |

### 6. 🌀 Regimes Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Regime Table | ✅ WORKING | Weak/Blend/Strong |
| Key Values | ✅ WORKING | φ, Ξ_max, D(r_s), r* |
| Regime Plot | ⚠️ PARTIAL | May not auto-load |

### 7. 📖 Reference Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Constants Table | ✅ WORKING | G, c, M_☉, φ |
| Formulas | ✅ WORKING | Xi, D, z equations |
| Assumptions | ❌ NOT IMPLEMENTED | TODO: Add section |
| Dynamic Run Params | ❌ NOT IMPLEMENTED | TODO: Show current config |
| Doc References | ❌ NOT IMPLEMENTED | TODO: doc-id format |

### 8. ✅ Validation Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Run Validation Button | ✅ WORKING | Executes 35 tests |
| Summary Display | ✅ WORKING | Pass/fail counts |
| Category Chart | ✅ WORKING | Visual breakdown |
| Detailed Results | ✅ WORKING | Per-test info |

### 9. 📈 Theory Plots Tab

| Feature | Status | Notes |
|---------|--------|-------|
| Plot Selector | ✅ WORKING | 7 plot types |
| Xi & Dilation | ✅ WORKING | Core physics |
| GR vs SSZ | ✅ WORKING | Comparison |
| Universal Intersection | ✅ WORKING | r*/r_s = 1.387 |
| Power Law | ✅ WORKING | E_norm scaling |
| Regime Zones | ✅ WORKING | Weak/Blend/Strong |
| Experimental Validation | ✅ WORKING | GPS, Pound-Rebka |
| NS Predictions | ✅ WORKING | +13% redshift |

---

## Cross-Cutting Features

| Feature | Status | Notes |
|---------|--------|-------|
| Run-ID Generation | ✅ WORKING | UUID per session |
| Parameter Snapshot | ❌ NOT IMPLEMENTED | TODO: params.json |
| Run Bundle (.zip) | ❌ NOT IMPLEMENTED | TODO: Full download |
| No Local Paths in UI | ⚠️ PARTIAL | Footer still shows path |
| Dockerfile | ❌ NOT IMPLEMENTED | TODO: Create |
| Health Endpoint | ❌ NOT IMPLEMENTED | TODO: /health |

---

## Summary

- **WORKING:** 35 features
- **PARTIAL:** 4 features  
- **NOT IMPLEMENTED:** 10 features

**Next Steps:** See `FIX_PLAN.md` for implementation priority.
