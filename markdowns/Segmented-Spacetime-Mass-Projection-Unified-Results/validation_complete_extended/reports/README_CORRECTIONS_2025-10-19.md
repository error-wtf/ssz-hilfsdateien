# README & Documentation Corrections - October 19, 2025

**Status:** ✅ COMPLETE  
**Reason:** After NED spectrum integration (143→427 rows), some documentation had outdated numbers

---

## 🔍 **CORRECTIONS MADE**

### **1. README.md** (3 fixes)

**Lines 55, 90-91, 132:**

| Old (❌ Incorrect) | New (✅ Correct) |
|-------------------|-----------------|
| "427 data points (143 original + 142 M87 NED + 142 Sgr A* NED)" | "427 data points from 117 unique sources" |
| "Unique sources: 119 → **123**" | "Unique sources: **117**" |
| "Multi-frequency sources: **4** (M87*, S2, PSR, AGN)" | "Multi-frequency sources: **5** (M87: 278 obs, Cyg X-1: 10, M87*: 10, S2: 10, Sgr A*: 6)" |
| "Warning 1 RESOLVED: 4 multi-frequency sources" | "Warning 1 RESOLVED: 5 multi-frequency sources" |

**Why:** Actual data has 117 unique sources and 5 multi-frequency sources (not 123 and 4)

---

### **2. Sources.md** (1 fix)

**Line 278:**

| Old (❌) | New (✅) |
|---------|---------|
| "Multi-frequency sources: 4 (M87*, S2, PSR B1937+21, NGC 4151)" | "Multi-frequency sources: 5 (M87: 278 obs, Cyg X-1: 10, M87*: 10, S2: 10, Sgr A*: 6)" |

---

### **3. COMPREHENSIVE_DATA_ANALYSIS.md** (2 fixes)

**Lines 4-6, 15-16:**

| Old (❌) | New (✅) |
|---------|---------|
| "167 real data points" | "427 real data points" |
| "123 unique astronomical objects" | "117 unique astronomical objects" |
| "4 multi-frequency sources" | "5 multi-frequency sources" |
| "167 points" (singularity resolution) | "427 points" |

**Why:** Document was from before NED integration

---

## ❌ **NOT CHANGED** (Historical Documents)

These files contain **historical documentation** of past states and should NOT be updated:

1. **DATA_CHANGELOG.md**
   - Lines 200, 404-405 mention "167 data points" and "4 multi-frequency sources"
   - **Reason:** Documents the state AFTER synthetic removal but BEFORE NED integration
   - **Keep as-is:** Historical record

2. **REPOSITORY_UPDATE_2025-10-19.md**
   - Mentions "143 rows" in commit descriptions
   - **Reason:** Git log history, immutable
   - **Keep as-is:** Historical record

3. **DATA_QUALITY_FINAL_STATUS.md**
   - Mentions "143 rows" as final status
   - **Reason:** Status report from specific point in time
   - **Keep as-is:** Historical record

---

## ✅ **VERIFIED CORRECT**

These scripts/files dynamically calculate numbers (no hardcoded values):

- ✅ `install.ps1` / `install.sh` - No hardcoded row counts
- ✅ `install_and_test.ps1` / `install_and_test.sh` - Wrapper scripts only
- ✅ `run_all_ssz_terminal.py` - Uses `len(df)`
- ✅ `run_full_suite.py` - Dynamic test counting
- ✅ `phi_test.py` - Prints actual `summary["rows_used"]`
- ✅ All test scripts - Use filters/assertions, not hardcoded counts

---

## 📊 **FACT-CHECKED NUMBERS**

| Metric | Value | Source |
|--------|-------|--------|
| **Total rows** | 427 | `check_data_composition.py` |
| **Unique sources** | 117 | `df['source'].nunique()` |
| **Multi-frequency (3+ obs)** | 5 | `groupby('source').size()` |
| **M87-related rows** | 292 | M87 (278) + M87* (10) + others (4) |
| **Sgr A*-related rows** | 8 | Sgr A* (6) + magnetar (1) + EMRI (1) |

**Multi-frequency breakdown:**
- M87: 278 observations (NED continuum spectrum)
- Cyg X-1: 10 observations
- M87*: 10 observations
- S2: 10 observations
- Sgr A*: 6 observations

---

## 🎯 **ACCURACY VERIFICATION**

All numbers now match actual dataset:

```python
import pandas as pd

df = pd.read_csv('real_data_full.csv')

assert len(df) == 427
assert df['source'].nunique() == 117

freq_counts = df.groupby('source').size()
multi = freq_counts[freq_counts >= 3]
assert len(multi) == 5

print("✅ All numbers verified correct!")
```

---

## 📝 **COMMIT MESSAGE**

```
FIX: Correct data statistics in documentation (117 sources, 5 multi-freq)

Corrections based on actual dataset analysis:
- Total rows: 427 (verified)
- Unique sources: 123 → 117 (fact-checked with check_data_composition.py)
- Multi-frequency sources: 4 → 5 (M87, Cyg X-1, M87*, S2, Sgr A*)

Updated files:
- README.md (4 corrections)
- Sources.md (1 correction)
- COMPREHENSIVE_DATA_ANALYSIS.md (2 corrections)

Historical documents (DATA_CHANGELOG.md, etc.) kept unchanged as they
document past states before NED integration.

All scripts verified to use dynamic calculations (no hardcoded counts).
```

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
