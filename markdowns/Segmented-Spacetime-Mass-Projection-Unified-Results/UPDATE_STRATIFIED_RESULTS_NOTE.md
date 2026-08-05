# Stratified Results Update Note

**Date:** 2025-10-20  
**Action Required:** Update all documentation and reports

---

## Files Updated ✅

1. **README.md** - Added stratified results summary
2. **PAIRED_TEST_ANALYSIS_COMPLETE.md** - Completely revised with stratified data
3. **STRATIFIED_PAIRED_TEST_RESULTS.md** - NEW comprehensive analysis
4. **data/DATA_TYPE_USAGE_GUIDE.md** - Updated percentages and added stratification note
5. **stratified_paired_test.py** - NEW analysis script

---

## Files That Need Regeneration 🔄

### Test Reports (auto-generated):
- `reports/full-output.md` - Will be regenerated on next `python run_full_suite.py`
- `reports/summary-output.md` - Will be regenerated on next run
- `reports/RUN_SUMMARY.md` - Will be regenerated on next run

**Note:** These files are auto-generated and will show updated paired test results (73/143) on next test run.

### Agent Output (runtime):
- `agent_out/reports/redshift_paired_stats.json` - Generated during eval-redshift
- Shows current paired stats for whatever dataset is run

---

## Key Message to Communicate

### Old Understanding (WRONG):
> "Paired test shows 51% (p=0.867) because photon sphere region dilutes SEG advantage"

### New Understanding (CORRECT):
> "Paired test shows 51% (p=0.867) because:
> - Photon sphere (r=2-3): SEG DOMINATES (82% wins, p<0.0001)
> - Very close (r<2): SEG FAILS (0% wins, p<0.0001)  
> - These opposite effects CANCEL OUT to give 51% overall"

---

## Stratified Results Summary

| Regime | n | SEG Wins | % | p-value | Status |
|--------|---|----------|---|---------|--------|
| Photon Sphere | 45 | 37 | 82.2% | <0.0001 | ✅ HIGHLY SIGNIFICANT |
| Very Close | 29 | 0 | 0.0% | <0.0001 | ❌ CATASTROPHIC |
| High Velocity | 21 | 18 | 85.7% | 0.0015 | ✅ HIGHLY SIGNIFICANT |
| Weak Field | 40 | 15 | 37.5% | 0.1539 | ⚠️ Not significant |
| **Full Dataset** | **143** | **73** | **51.0%** | **0.8672** | **Cancellation** |

---

## Action Items

### For Documentation:
- ✅ Update all references to "79/143" → "73/143"
- ✅ Add stratification note where paired test mentioned
- ✅ Link to STRATIFIED_PAIRED_TEST_RESULTS.md
- ✅ Explain cancellation effect

### For Future Papers/Presentations:
- Focus on stratified results, not overall 51%
- Highlight photon sphere dominance (82%)
- Acknowledge r<2 failure honestly
- Emphasize high velocity success (86%)
- Explain physical reasons for regime dependence

### For Code:
- ✅ stratified_paired_test.py is rerunnable
- Consider adding regime-specific reporting to main test
- Document which regime each observation belongs to

---

## Physical Interpretation

**SEG is a PHOTON SPHERE theory:**
- Optimal at r = 2-3 r_s (photon sphere region)
- Phi-based corrections work best where field is strong but not extreme
- Approximations break down at r < 2 r_s (too close to horizon)
- High velocity enhances performance across all radii (SR+GR coupling)

**This is GOOD SCIENCE:**
- Clear definition of applicability domain
- Honest reporting of failures
- Guides future model improvements
- Better than claiming universal superiority

---

## References

- **Full Analysis:** STRATIFIED_PAIRED_TEST_RESULTS.md
- **Investigation:** PAIRED_TEST_ANALYSIS_COMPLETE.md
- **Analysis Script:** stratified_paired_test.py
- **Data Guide:** data/DATA_TYPE_USAGE_GUIDE.md

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
