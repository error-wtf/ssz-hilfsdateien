# ⚠️ CRITICAL WARNINGS: External Data Integration

**Date:** 2025-10-19  
**Audience:** Researchers integrating external datasets  
**Priority:** 🔴 **CRITICAL - READ BEFORE INTEGRATING DATA**

---

## 🚨 **EXECUTIVE SUMMARY**

Integrating external datasets into the SSZ Suite requires **EXTREME CARE**. The pipeline consists of interconnected scripts that expect **specific column structures** and **data consistency**. Failure to properly validate and merge data can lead to:

- ❌ Silent failures (NaN propagation)
- ❌ Incorrect scientific results
- ❌ Test suite crashes
- ❌ Data inconsistencies across debug files

**GOLDEN RULE:** When in doubt, validate **three times**. Then validate again.

---

## 📊 **THREE LEVELS OF INTEGRATION COMPLEXITY**

### **Level 1: Single Script Integration** 🟢 SAFE

**Scenario:** You want to run **ONE** test script with your own data.

**Risk Level:** 🟢 **LOW** - Individual scripts have isolated requirements

**Example:**
```bash
# Run single test with custom data
python scripts/tests/test_horizon_hawking_predictions.py --custom-data my_data.csv
```

**Requirements:**
- ✅ Only needs columns required by THAT script
- ✅ Script-specific validation (e.g., `z_obs` for Hawking test)
- ✅ NaN gaps OK if script filters them out

**Validation Needed:** Basic (check script's column requirements)

---

### **Level 2: Partial Pipeline Integration** 🟡 MODERATE

**Scenario:** You want to run **MULTIPLE** related scripts (e.g., all prediction tests).

**Risk Level:** 🟡 **MODERATE** - Scripts share intermediate files

**Example:**
```bash
# Run test suite (multiple scripts)
python run_full_suite.py --custom-data my_data.csv
```

**Requirements:**
- ⚠️ Shared debug files (`out/phi_step_debug_full.csv`, `out/_enhanced_debug.csv`)
- ⚠️ Each script may expect different columns from same file
- ⚠️ NaN in one file can break downstream scripts

**Validation Needed:** Moderate (check all used scripts' requirements + consistency)

---

### **Level 3: Full Pipeline Integration** 🔴 CRITICAL

**Scenario:** You want to run the **COMPLETE SSZ SUITE** (`run_all_ssz_terminal.py`) with your data.

**Risk Level:** 🔴 **CRITICAL** - Multiple interdependent scripts, shared state

**Pipeline Flow:**
```
real_data_full.csv (input)
    ↓
phi_test.py → out/phi_step_debug_full.csv
    ↓
segspace_enhanced_test_better_final.py → out/_enhanced_debug.csv
    ↓
test_horizon_hawking_predictions.py (reads both files!)
    ↓
test_hawking_spectrum_continuum.py (reads both files!)
    ↓
... (more scripts)
```

**CRITICAL ISSUES:**

1. **Column Propagation**
   - ❌ Missing column in `real_data_full.csv` → Missing in ALL downstream files
   - ❌ NaN in source → NaN propagates through entire pipeline
   - ❌ One script's filter → Inconsistent row counts downstream

2. **Cross-Script Dependencies**
   - Script A generates `phi_step_debug_full.csv` with 24 columns
   - Script B reads it and expects column X
   - Script C reads it and expects column Y (≠ X)
   - **IF X or Y missing:** Silent failure or crash

3. **Merge Hell**
   - Different scripts merge data from different sources
   - Manual merges can create:
     - ❌ Duplicate rows
     - ❌ Misaligned indices
     - ❌ Inconsistent source names
     - ❌ NaN gaps where data should exist

**Validation Needed:** 🔴 **EXTREME** (triple/quadruple checks mandatory)

---

## 🔍 **CRITICAL VALIDATION WORKFLOW**

### **Step 1: Pre-Integration Validation** 

**BEFORE adding ANY external data to `real_data_full.csv`:**

```bash
# 1. Validate structure
python scripts/data_generators/validate_dataset.py

# 2. Check column completeness
python check_column_completeness.py

# 3. Check critical columns
python -c "
import pandas as pd
df = pd.read_csv('real_data_full.csv')

CRITICAL = ['source', 'f_emit_Hz', 'f_obs_Hz', 'r_emit_m', 'M_solar', 'z']
for col in CRITICAL:
    nan_count = df[col].isna().sum()
    print(f'{col}: {nan_count} NaN / {len(df)} rows')
    if nan_count > 0:
        print(f'  ⚠️ WARNING: {col} has NaN gaps!')
"
```

**MANDATORY CHECKS:**

| Check | Tool | Failure Action |
|-------|------|----------------|
| All critical columns present | `validate_dataset.py` | ❌ STOP - Add missing columns |
| No NaN in critical columns | Manual check above | ❌ STOP - Fill or remove rows |
| Source names consistent | Visual inspection | ❌ STOP - Standardize names |
| Frequency values positive | `validate_dataset.py` | ❌ STOP - Fix or remove |
| Mass values reasonable | `validate_dataset.py` | ⚠️ WARN - Review |

---

### **Step 2: Integration with Validation**

**USE OUR INTEGRATION TOOL** (has built-in validation):

```bash
# ✅ RECOMMENDED: Use our validator
python scripts/data_generators/integrate_ned_spectrum.py \
    --ned-file your_data.csv \
    --source-name "Your Source" \
    --mass-solar 1e6 \
    --validate  # ← CRITICAL FLAG
```

**What it checks:**
- ✅ Column structure matches `real_data_full.csv`
- ✅ No duplicate rows added
- ✅ All critical columns filled (no NaN)
- ✅ Frequency/mass values reasonable
- ✅ Creates backup before merging

**❌ DO NOT manually append to CSV without validation!**

---

### **Step 3: Post-Integration Validation**

**AFTER adding data, verify EVERYTHING:**

```bash
# 1. Validate merged dataset
python scripts/data_generators/validate_dataset.py

# 2. Count rows (should increase correctly)
python -c "
import pandas as pd
df = pd.read_csv('real_data_full.csv')
print(f'Total rows: {len(df)}')
print(f'Unique sources: {df[\"source\"].nunique()}')
print(f'Expected: [YOUR CALCULATION]')
"

# 3. Check for duplicates
python -c "
import pandas as pd
df = pd.read_csv('real_data_full.csv')
dupes = df.duplicated(subset=['source', 'f_emit_Hz'], keep=False)
print(f'Duplicate rows: {dupes.sum()}')
if dupes.sum() > 0:
    print('⚠️ WARNING: Duplicates found!')
    print(df[dupes][['source', 'f_emit_Hz']])
"

# 4. Run pipeline to regenerate debug files
python run_all_ssz_terminal.py

# 5. Verify debug files consistency
python check_column_completeness.py
```

---

## 🧩 **NaN GAPS: WHEN ACCEPTABLE, WHEN FATAL**

### **✅ ACCEPTABLE NaN** (Expected, Scientifically Valid)

| Column | Acceptable NaN | Reason |
|--------|---------------|---------|
| `a_m`, `e`, `P_year` | ✅ YES | Continuum spectra have no orbits |
| `z_geom_hint`, `N0`, `n_star` | ✅ YES | Optional analysis parameters |
| `lambda_emit_nm`, `lambda_obs_nm` | ✅ YES | Redundant with frequency |
| `v_los_mps`, `v_tot_mps` | ✅ YES | Stationary sources have no velocity |

**Example:** M87 NED continuum spectrum (139 rows) - ALL have NaN for orbital parameters. **This is CORRECT.**

---

### **❌ FATAL NaN** (Will Break Tests)

| Column | Fatal if NaN | Breaks |
|--------|-------------|---------|
| `source` | ❌ FATAL | All scripts - can't group data |
| `f_emit_Hz` | ❌ FATAL | All frequency-based tests |
| `f_obs_Hz` | ❌ FATAL | All redshift calculations |
| `r_emit_m` | ❌ FATAL | All horizon/radius tests |
| `M_solar` | ❌ FATAL | All Schwarzschild radius calculations |
| `z` | ❌ FATAL | Most cosmological tests |
| `z_obs` (in enhanced) | ❌ FATAL | Hawking radiation test (chi calculation) |

**If ANY of these have NaN:**
1. ❌ DO NOT proceed with integration
2. ❌ Either fill with scientific estimate OR remove rows
3. ❌ Document your filling method in `DATA_FILLING_METHODS.md`

---

## 🔬 **SCIENTIFIC DATA FILLING** (Last Resort Only!)

**⚠️ WARNING:** Filling missing data can introduce bias. **AVOID if possible.**

### **When Filling is Acceptable:**

1. **Redundant Calculations**
   ```python
   # z and z_obs are usually identical for most sources
   if df['z_obs'].isna().any():
       df['z_obs'] = df['z_obs'].fillna(df['z'])
       # Document: "Assumed z_obs ≈ z for stationary sources"
   ```

2. **Conservative Estimates**
   ```python
   # Emission radius from simplified luminosity distance
   # ONLY if actual radius unknown
   df['r_emit_m'] = estimate_radius_from_luminosity(df)
   # Document: "r_emit estimated via L = 4πr²F (simplified)"
   ```

3. **Standard Values**
   ```python
   # Eccentricity for circular orbits
   df['e'] = df['e'].fillna(0.0)
   # Document: "e=0 assumed for circular orbits (conservative)"
   ```

### **⚠️ MANDATORY when Filling:**

1. **Document EVERYTHING:**
   - Create `DATA_FILLING_LOG.md`
   - Record: What filled, Why, Method, Uncertainty
   - Example:
     ```markdown
     ## M87 NED Spectrum (2025-10-19)
     - Filled: r_emit_m (139 rows)
     - Method: Simplified luminosity distance (D_L ≈ 16.7 Mpc)
     - Uncertainty: ±30% (no proper r measurement for continuum)
     - Citation: Akiyama et al. 2019 (M87 distance)
     ```

2. **Add Warning Flags:**
   ```python
   df['data_quality_flag'] = 'FILLED'  # Mark filled rows
   df['filling_method'] = 'luminosity_distance_estimate'
   ```

3. **Validate Scientifically:**
   - Compare filled values to literature
   - Check if results change significantly
   - Run sensitivity analysis

---

## 🛠️ **OUR CONSISTENCY CHECK SCRIPTS**

We've developed multiple validation layers to catch inconsistencies:

### **1. `scripts/data_generators/validate_dataset.py`**

**Purpose:** Pre-integration validation of `real_data_full.csv`

**Checks:**
- ✅ All critical columns present (100% filled)
- ✅ Frequency values positive and reasonable
- ✅ Mass values within physical limits
- ✅ No duplicate source+frequency combinations
- ✅ Redshift values scientifically acceptable

**Usage:**
```bash
python scripts/data_generators/validate_dataset.py
# Output: PASSED / FAILED with detailed report
```

**Our Safeguards:**
- Checks 7 critical columns for 100% completeness
- Validates 4 blueshift sources are scientifically correct
- Reports percentage filled for optional columns
- Exits with error code if critical issues found

---

### **2. `check_column_completeness.py`**

**Purpose:** Cross-check consistency between pipeline files

**Checks:**
- ✅ `real_data_full.csv` has all source columns
- ✅ `out/phi_step_debug_full.csv` has phi-related columns
- ✅ `out/_enhanced_debug.csv` has enhanced columns (z_obs, deltaM, etc.)
- ⚠️ Identifies missing columns needed by tests
- ⚠️ Reports NaN gaps in critical columns

**Usage:**
```bash
python check_column_completeness.py
# Output: Reports missing columns and NaN counts
```

**Our Safeguards:**
- Compares 3 pipeline files for consistency
- Lists columns that `_enhanced_debug.csv` has but `phi_step` doesn't
- Identifies which test needs which column
- Suggests merge strategy if columns missing

---

### **3. `check_data_availability.py`**

**Purpose:** Verify test-specific data requirements

**Checks:**
- ✅ Multi-frequency sources (for Jacobian test) - Need 3+ freq
- ✅ Near-horizon data (for kappa_seg test) - Need r < 3 r_s
- ✅ Continuum spectra (for Hawking spectrum test)
- ✅ Source-specific coverage (M87, Sgr A*, S2, etc.)

**Usage:**
```bash
python check_data_availability.py
# Output: Reports data coverage for each test requirement
```

**Our Safeguards:**
- Checks 5 multi-frequency sources exist
- Validates 181 near-horizon observations (r < 3 r_s)
- Reports frequency range (9+ orders of magnitude)
- Identifies which tests will have "Insufficient data" warnings

---

### **4. `scripts/data_generators/integrate_ned_spectrum.py`**

**Purpose:** Safe external data integration with validation

**Built-in Checks:**
- ✅ Column structure match before merge
- ✅ No duplicate rows added
- ✅ Critical columns 100% filled in new data
- ✅ Source name consistency
- ✅ Creates timestamped backup before merge

**Usage:**
```bash
python scripts/data_generators/integrate_ned_spectrum.py \
    --ned-file data.csv \
    --source-name "Source" \
    --mass-solar 1e6 \
    --validate
```

**Our Safeguards:**
- Validates BEFORE writing to `real_data_full.csv`
- Shows preview of what will be added
- Backs up original file (`real_data_full.backup_YYYYMMDD_HHMMSS.csv`)
- Verifies row count increase matches expected
- Reports detailed statistics post-merge

---

## 🔄 **RECOMMENDED INTEGRATION WORKFLOW**

```
Step 1: Prepare External Data
  ↓
  [Manual] Clean source data (remove duplicates, standardize names)
  ↓
Step 2: Pre-Validation
  ↓
  [Auto] python scripts/data_generators/validate_dataset.py
  ↓
  ✅ PASSED? → Continue
  ❌ FAILED? → Fix issues, repeat Step 2
  ↓
Step 3: Integration
  ↓
  [Auto] python scripts/data_generators/integrate_ned_spectrum.py --validate
  ↓
  Review preview, confirm merge
  ↓
Step 4: Post-Validation (CRITICAL!)
  ↓
  [Auto] python scripts/data_generators/validate_dataset.py  # Re-validate merged data
  [Auto] python check_column_completeness.py                # Check all files
  [Auto] python check_data_availability.py                  # Check test coverage
  ↓
  ✅ ALL PASSED? → Continue to Step 5
  ❌ ANY FAILED? → Restore backup, debug, repeat Step 3
  ↓
Step 5: Pipeline Regeneration
  ↓
  [Auto] python run_all_ssz_terminal.py  # Regenerate ALL debug files
  ↓
  Wait for completion (~10-15 min)
  ↓
Step 6: Final Verification
  ↓
  [Auto] python check_column_completeness.py  # Verify debug files updated
  [Manual] Check test outputs for new data
  ↓
Step 7: Test Suite
  ↓
  [Auto] python run_full_suite.py --quick
  ↓
  ✅ ALL TESTS PASSED? → Integration complete! 🎉
  ❌ TESTS FAILED? → Review errors, check logs, debug
```

---

## 🚫 **COMMON MISTAKES** (DON'T DO THESE!)

### ❌ **Mistake 1: Manual CSV Append**

```python
# ❌ WRONG!
df_old = pd.read_csv('real_data_full.csv')
df_new = pd.read_csv('my_data.csv')
df_merged = pd.concat([df_old, df_new])
df_merged.to_csv('real_data_full.csv', index=False)  # NO VALIDATION!
```

**Why bad:** No validation, no duplicate check, no backup, no column match verification

**✅ CORRECT:** Use `integrate_ned_spectrum.py` with `--validate` flag

---

### ❌ **Mistake 2: Ignoring NaN in Critical Columns**

```python
# ❌ WRONG!
df = pd.read_csv('real_data_full.csv')
# "Oh, z_obs has 50 NaN? I'll just keep going..."
# → CRASH in test_horizon_hawking_predictions.py later!
```

**✅ CORRECT:** Fix or fill NaN BEFORE merging, document method

---

### ❌ **Mistake 3: Not Regenerating Debug Files**

```python
# ❌ WRONG!
# Add data to real_data_full.csv
# Run test_horizon_hawking_predictions.py directly
# → Uses OLD phi_step_debug_full.csv (143 rows)
# → New data (427 rows) not in debug files!
# → Test says "Insufficient data" even though data exists
```

**✅ CORRECT:** ALWAYS run `python run_all_ssz_terminal.py` after data changes

---

### ❌ **Mistake 4: Assuming All Scripts Use Same File**

```python
# ❌ WRONG ASSUMPTION!
# "I updated real_data_full.csv, so ALL tests will use it"
# 
# Reality:
# - Some tests read real_data_full.csv
# - Some tests read out/phi_step_debug_full.csv
# - Some tests read out/_enhanced_debug.csv
# → Inconsistent data across tests!
```

**✅ CORRECT:** Regenerate ALL debug files after merging

---

## 📝 **INTEGRATION CHECKLIST**

Before integrating external data, check ALL boxes:

### Pre-Integration
- [ ] External data has ALL critical columns (source, f_emit_Hz, f_obs_Hz, r_emit_m, M_solar, z)
- [ ] Source names standardized (no "M87" vs "m87" vs "M 87")
- [ ] No duplicate source+frequency combinations
- [ ] Frequency values positive and reasonable (> 1e6 Hz, < 1e20 Hz)
- [ ] Mass values reasonable (> 1e-10 M_sun, < 1e12 M_sun)
- [ ] Created backup of `real_data_full.csv`

### Integration
- [ ] Used `integrate_ned_spectrum.py` with `--validate` flag
- [ ] Reviewed integration preview before confirming
- [ ] Integration reported success (no errors)
- [ ] Row count increased by expected amount

### Post-Integration
- [ ] Ran `validate_dataset.py` - PASSED
- [ ] Ran `check_column_completeness.py` - No missing critical columns
- [ ] Ran `check_data_availability.py` - Data coverage acceptable
- [ ] Checked for duplicates (zero found)
- [ ] Verified no NaN in critical columns

### Pipeline Regeneration
- [ ] Ran `python run_all_ssz_terminal.py` - Completed successfully
- [ ] Checked `out/phi_step_debug_full.csv` row count (should match `real_data_full.csv`)
- [ ] Checked `out/_enhanced_debug.csv` has `z_obs` column (0 NaN)
- [ ] Re-ran `check_column_completeness.py` - All debug files consistent

### Final Verification
- [ ] Ran `python run_full_suite.py --quick` - All tests passed
- [ ] Reviewed test outputs for warnings (acceptable vs critical)
- [ ] Documented integration in `NED_SPECTRUM_INTEGRATION_YYYY-MM-DD.md`
- [ ] If filled any data: Created `DATA_FILLING_LOG.md` with methods

### Documentation
- [ ] Updated `README.md` with new row count
- [ ] Updated `DATA_COLUMNS_README.md` if column structure changed
- [ ] Created integration summary document
- [ ] Committed changes with descriptive message

---

## 🎯 **SUMMARY: THREE GOLDEN RULES**

1. **VALIDATE THREE TIMES**
   - Before integration
   - After integration
   - After pipeline regeneration

2. **NEVER SKIP DEBUG FILE REGENERATION**
   - Always run `python run_all_ssz_terminal.py` after data changes
   - Always verify debug files with `check_column_completeness.py`

3. **DOCUMENT EVERYTHING**
   - What data added
   - Where it came from
   - How it was processed
   - What was filled (if anything)
   - Why it's scientifically valid

---

## 📞 **CONTACT & SUPPORT**

**If you encounter integration issues:**

1. **Check validation output:**
   ```bash
   python scripts/data_generators/validate_dataset.py 2>&1 | tee validation.log
   ```

2. **Review our integration examples:**
   - `NED_SPECTRUM_INTEGRATION_2025-10-19.md` - Full NED integration
   - `EXTERNAL_DATASETS_GUIDE.md` - General guidelines

3. **Common error solutions:**
   - "Column X missing" → Add to source data before merging
   - "NaN in critical column" → Fill or remove rows
   - "Test says insufficient data" → Regenerate debug files
   - "Duplicate rows found" → Check source name consistency

4. **Open issue on GitHub:**
   - Include validation output
   - Include `check_column_completeness.py` output
   - Include sample of your data (first 10 rows)

---

## ⚠️ **FINAL WARNING**

**Data integration for full pipeline runs is HARD.** 

If you're unsure, **start with Level 1** (single script) and work your way up. Don't attempt full pipeline integration on your first try.

**When in doubt:** Validate three times. Then validate again. 🎯

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
