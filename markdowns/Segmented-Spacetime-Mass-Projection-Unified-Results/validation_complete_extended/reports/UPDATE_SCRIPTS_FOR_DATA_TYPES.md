# Update Scripts for Data Type Separation

**Created:** 2025-10-19  
**Purpose:** Update analysis scripts to use appropriate data files

---

## Changes Required

### 1. Paired Test Scripts → Use `data/real_data_emission_lines.csv`

**Files to update:**

#### `segspace_all_in_one_extended.py`
```python
# BEFORE (Line 497):
sp.add_argument("--csv", type=Path, default=Path("./real_data_full.csv"))

# AFTER:
sp.add_argument("--csv", type=Path, default=Path("./data/real_data_emission_lines.csv"))

# BEFORE (Line 561):
csv_path=Path("./real_data_full.csv")

# AFTER:
csv_path=Path("./data/real_data_emission_lines.csv")
```

**Why:** Paired test compares predictions to observations. Only emission-line data has compatible z_obs.

---

### 2. Spectrum Analysis Scripts → Use `data/real_data_continuum.csv`

**Files to update:**

#### `scripts/tests/test_hawking_spectrum_continuum.py`
```python
# Should use continuum data for spectrum analysis
```

---

### 3. Multi-Purpose Scripts → Use `data/real_data_full_typed.csv` + Filter

**Files to update:**

#### Scripts that need BOTH types:
- Information Preservation tests
- Jacobian Reconstruction
- General analysis

**Example filtering:**
```python
import pandas as pd

df = pd.read_csv('data/real_data_full_typed.csv')

# For paired test
emission = df[df['data_type'] == 'emission_line']

# For spectrum analysis
continuum = df[df['data_type'] == 'continuum']
```

---

## Update Strategy

### Option A: Automatic Update Script
Create script to update all occurrences automatically.

### Option B: Manual Updates (RECOMMENDED)
Update key scripts one-by-one with testing:
1. `segspace_all_in_one_extended.py` (MAIN)
2. Test after each change
3. Document in commit

### Option C: Keep Backward Compatible
Add new parameter `--data-type` to scripts:
```python
parser.add_argument('--data-type', choices=['emission', 'continuum', 'all'], 
                   default='emission',
                   help='Which data type to use')
```

Then load appropriate file based on choice.

---

## Recommended Changes

### PRIORITY 1: Main Analysis Script

**File:** `segspace_all_in_one_extended.py`

**Change Lines 497 & 561:**
```python
# Update default paths to use emission_lines for paired test
default_csv = Path("./data/real_data_emission_lines.csv")
```

**Add comment:**
```python
# Using emission-line data for paired test (compatible z_obs)
# See data/DATA_TYPE_USAGE_GUIDE.md for details
```

---

### PRIORITY 2: Documentation in Scripts

Add header comment to all scripts:
```python
"""
DATA FILE USAGE:
- This script uses: data/real_data_emission_lines.csv
- Reason: Paired test requires emission-line redshifts
- See: data/DATA_TYPE_USAGE_GUIDE.md
"""
```

---

## Implementation Plan

1. **Test Current State**
   ```bash
   python segspace_all_in_one_extended.py eval-redshift
   ```

2. **Update Main Script**
   - Change default CSV paths
   - Add documentation
   - Keep backward compatible via --csv flag

3. **Test Updated State**
   ```bash
   python segspace_all_in_one_extended.py eval-redshift
   ```

4. **Verify Results**
   - Check paired test uses 143 rows
   - Verify output makes sense

5. **Document Changes**
   - Commit message
   - Update README if needed

---

## Scripts That DON'T Need Changes

**Keep using `real_data_full.csv`:**
- Data generation scripts (source of truth)
- Validation scripts (check complete dataset)
- Backup/migration tools

**These can stay as-is:**
- `scripts/data_generators/*.py` (work on full dataset)
- `investigate_paired_test.py` (analysis script, not production)
- Build/package scripts

---

## Testing Checklist

After updates:
- [ ] Paired test runs with 143 rows
- [ ] Results make sense (79/143, 55%)
- [ ] No errors about missing columns
- [ ] Backward compatible (can still specify --csv)
- [ ] Documentation updated

---

## Rollback Plan

If issues:
```bash
git checkout HEAD -- segspace_all_in_one_extended.py
```

Or keep both paths:
```python
# Try new path first, fall back to old
new_path = Path("data/real_data_emission_lines.csv")
old_path = Path("real_data_full.csv")
csv_path = new_path if new_path.exists() else old_path
```

---

© 2025 Carmen Wrede, Lino Casu
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
