# ROADMAP: Full Parity Implementation

**Date:** 2025-01-16  
**Target:** 100% Parity with Source Repos  
**Benchmark:** ssz-qubits (74/74), Unified-Results (31/31), ssz-metric-pure (12+/12+)

---

## Milestone Overview

| Milestone | Description | Status | DoD |
|-----------|-------------|--------|-----|
| M0 | Restore all tabs/features | ✅ DONE | 6/6 tabs |
| M1 | Inventory & Mapping | ✅ DONE | 5 files |
| M2 | Core Parity | 🔄 IN PROGRESS | All methods callable |
| M3 | Test Parity | ⏳ PENDING | 100% pass |
| M4 | Plot Parity | ⏳ PENDING | All plots render |
| M5 | Run Bundles | ✅ DONE | Complete bundles |
| M6 | UI Finalization | ⏳ PENDING | No placeholders |

---

## M0: Restore (COMPLETE)

### Definition of Done
- [x] Single Object tab functional
- [x] Data tab functional  
- [x] Batch Calculate tab functional
- [x] Compare tab functional
- [x] Theory Plots tab functional
- [x] Reference tab functional

### Deliverables
- All 6 tabs present and clickable
- No removed features

---

## M1: Inventory & Mapping (COMPLETE)

### Definition of Done
- [x] INVENTORY_METHODS.json created
- [x] INVENTORY_TESTS.json created
- [x] INVENTORY_PLOTS.json created
- [x] METHOD_TEST_PLOT_MAP.md created
- [x] GAPS.md created
- [x] PARITY_PROGRESS.md created

### Additional Docs (COMPLETE)
- [x] WEAK_STRONG_FIELD_SPEC.md
- [x] MD_INDEX.md
- [x] PROOF_OF_READING.md
- [x] TRACEABILITY_MATRIX.md
- [x] PARITY_GATES.md
- [x] ROADMAP.md (this file)

---

## M2: Core Parity (IN PROGRESS)

### Definition of Done
- [x] All P1 methods implemented
- [x] All P2 methods implemented
- [ ] Regime selection matches source exactly
- [ ] Constants match source exactly
- [ ] No placeholders

### Methods Status

#### P1 Core (REQUIRED)
| method_id | Status | File |
|-----------|--------|------|
| schwarzschild_radius | ✅ | core.py |
| xi_weak | ✅ | xi.py |
| xi_strong | ✅ | xi.py |
| xi_blended | ✅ | xi.py |
| xi_auto | ✅ | xi.py |
| D_ssz | ✅ | dilation.py |
| D_gr | ✅ | dilation.py |
| z_gravitational | ✅ | redshift.py |
| z_combined | ✅ | redshift.py |
| z_ssz | ✅ | redshift.py |
| power_law_prediction | ✅ | power_law.py |

#### P2 Extended (REQUIRED)
| method_id | Status | File |
|-----------|--------|------|
| delta_M | ✅ | unified.py |
| r_phi | ✅ | unified.py |
| sigma | ✅ | unified.py |
| tau | ✅ | unified.py |
| n_index | ✅ | unified.py |
| dual_velocity | ✅ | unified.py |
| euler_spiral | ✅ | unified.py |

### Remaining Work
1. Fix regime boundary to match source (90/110 blend)
2. Verify all constants match exactly
3. Add missing error handling

---

## M3: Test Parity (PENDING)

### Definition of Done
- [ ] All 30+ tests pass
- [ ] Pass rate = 100%
- [ ] Skipped = 0
- [ ] Tolerances match source

### Current Status
```
TOTAL:   30
PASSED:  26
FAILED:  4
RATE:    86.7%
```

### Failed Tests - Fix Plan

| Test | Issue | Fix |
|------|-------|-----|
| test_ns_psr_j0740 | Expected deviation wrong | Recalculate from source |
| test_ns_psr_j0348 | Expected deviation wrong | Recalculate from source |
| test_ns_psr_j0030 | Expected deviation wrong | Recalculate from source |
| test_negative_mass | No error raised | Add validation |

### Action Items
1. Review NS deviation calculation in source
2. Match expected values from Unified-Results
3. Add negative mass validation to schwarzschild_radius

---

## M4: Plot Parity (PENDING)

### Definition of Done
- [ ] All 15 required plots render
- [ ] No crashes
- [ ] Saved to bundle
- [ ] Visual match to source

### Plot Status
| plot_id | Status |
|---------|--------|
| dilation_profile | ✅ |
| xi_profile | ✅ |
| redshift_breakdown | ✅ |
| gr_vs_ssz | ⏳ |
| universal_intersection | ⏳ |
| regime_zones | ⏳ |
| power_law | ⏳ |
| comparison_scatter | ✅ |
| residuals | ✅ |

### Action Items
1. Implement missing theory plots
2. Add paper plots from ssz-paper-plots
3. Ensure all plots saved to bundle

---

## M5: Run Bundles (COMPLETE)

### Definition of Done
- [x] params.json generated
- [x] data_input.csv saved
- [x] results.csv complete
- [x] report.md readable
- [x] plots/ directory populated
- [x] ZIP download works
- [x] Run-ID displayed (no paths)

### Deliverables
- RunBundle class in core/run_bundle.py
- Integration with Single Object tab
- Integration with Batch Calculate tab

---

## M6: UI Finalization (PENDING)

### Definition of Done
- [ ] All tabs real pipelines
- [ ] No placeholder outputs
- [ ] Clear error messages
- [ ] Template downloads work
- [ ] Presets work (5 objects)
- [ ] Online deployable

### Tab Checklist

#### Single Object ✅
- [x] 5 presets (Sun, Sirius B, NS, Sgr A*, M87*)
- [x] Calculate button
- [x] 3 plots
- [x] Results table
- [x] Download bundle

#### Data ✅
- [x] Upload CSV
- [x] Template download
- [x] Fetch from URL
- [x] Preview table
- [x] Validation messages

#### Batch Calculate ✅
- [x] Run button
- [x] Summary statistics
- [x] Results table
- [x] Download bundle

#### Compare ✅
- [x] Object selection
- [x] z_obs comparison
- [x] SSZ vs GR×SR
- [x] Residuals display

#### Theory Plots ⏳
- [x] Plot selection
- [ ] Additional plots needed
- [ ] Paper plots integration

#### Reference ✅
- [x] Constants display
- [x] Formula reference
- [x] Regime rules
- [ ] Dynamic content (current run)

---

## Timeline

| Date | Milestone | Deliverable |
|------|-----------|-------------|
| 2025-01-16 | M0, M1 | Docs complete |
| 2025-01-16 | M2 | Methods complete |
| 2025-01-16 | M3 | Tests 100% |
| 2025-01-17 | M4 | Plots complete |
| 2025-01-17 | M5, M6 | UI polish |
| 2025-01-17 | FINAL | 100% parity |

---

## Blockers

| Blocker | Impact | Resolution |
|---------|--------|------------|
| NS deviation values | M3 | Check source calculation |
| Advanced tensors | M2 | Defer (not core) |

---

## Success Criteria

**DONE when:**
1. All gates in PARITY_GATES.md are GREEN
2. Test pass rate = 100%
3. All plots render without error
4. UI fully functional
5. Deploy works (Docker)
6. PARITY_REPORT.md shows compliance

---

**Next Action:** Fix the 4 failing tests to achieve M3.
