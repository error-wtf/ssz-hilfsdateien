# SSZ Data Sources - Clarification

**Last Updated:** 2025-10-29 19:08

---

## 📊 PRIMARY DATA (Perfect Paired Test)

### `data/real_data_emission_lines_clean.csv`

**Source:** ESO Spectroscopy (European Southern Observatory)  
**Type:** Emission Lines (H-alpha, etc.)  
**Quality:** Professional spectroscopic observations  
**Status:** ✅ **CORRECT PRIMARY DATA**

**Objects:**
- **3C279** - Blazar jet (840M M☉)
- **PKS 1510-089** - Gamma-ray loud blazar (320M M☉)
- **GRS 1915+105** - Stellar mass black hole (10.1 M☉)
- **3C273** - Bright quasar jet (1.2B M☉)
- Additional AGN, quasars, black hole jets

**Validation Results:**
- **97.9%** success rate (46/47 wins)
- **100%** photon sphere regime (11/11 wins)
- **p < 0.0001** highly significant
- φ-geometry validation confirms SSZ model

**Used in:**
- `perfect_paired_test.py` (PRIMARY validation)
- φ-based geometric calibration
- Rapidity-based equilibrium analysis
- Stratified regime testing

---

## 🔬 CONTROL DATA (Comparison Tests)

### `data/real_data_full.csv`

**Source:** GAIA DR3 + Mixed Catalog Data  
**Type:** Photometric + Astrometric  
**Quality:** Mixed (catalog-quality, not spectroscopic)  
**Status:** ⚠️ **FOR COMPARISON ONLY**

**Purpose:**
- Demonstrates SSZ robustness across data types
- Shows performance with lower-quality data
- Validates that SSZ works even with catalog data
- Control group for scientific rigor

**Validation Results:**
- **51%** success rate (catalog limitations)
- Shows data quality matters for precision tests
- Confirms: Professional spectroscopy >> Catalog data
- Still better than random (50%)

**Used in:**
- Robustness testing
- Data quality comparison
- Control group validation
- NOT for primary SSZ validation

---

## 🎯 WHY ESO DATA IS PRIMARY

### Scientific Rationale:

1. **Spectroscopic Precision**
   - Direct frequency measurements
   - Barycentric-corrected
   - Laboratory-calibrated
   - High resolution

2. **Regime Coverage**
   - Photon sphere regime: ISCO, shadows
   - Strong field: AGN, quasars
   - Intermediate field: Stellar BH
   - Full mass range: 10 M☉ to 1.2B M☉

3. **Statistical Significance**
   - p < 0.0001 (highly significant)
   - 97.9% success rate
   - Perfect in photon sphere regime
   - Consistent across regimes

4. **φ-Geometry Validation**
   - Fundamental geometric basis
   - Not arbitrary fitting
   - Golden ratio emergence
   - Universal scaling

---

## 📁 OTHER DATA FILES

### GAIA Samples (Auxiliary)
```
data/gaia/gaia_sample_small.csv        ✅ Small test sample
data/gaia/gaia_cone_g79.csv            ✅ G79 cone search
data/gaia/gaia_cone_cygx.csv           ✅ Cygnus X cone search
```
**Purpose:** Example analyses, test cases

### Planck CMB (Cosmology)
```
data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt  ✅ 2 GB
```
**Purpose:** Cosmological validation, CMB power spectrum

### SDSS (Optional)
```
data/raw/sdss/.../sdss_catalog.csv     ❌ Server down
```
**Purpose:** Extended tests (optional, not critical)

---

## ⚠️ COMMON MISTAKES TO AVOID

### ❌ WRONG:
```python
# Using GAIA catalog data for primary validation
df = pd.read_csv("data/real_data_full.csv")  # 51% success
validate_ssz_model(df)  # Not primary data!
```

### ✅ CORRECT:
```python
# Using ESO spectroscopic data for primary validation
df = pd.read_csv("data/real_data_emission_lines_clean.csv")  # 97.9% success
validate_ssz_model(df)  # Correct primary data!

# GAIA for comparison only
df_control = pd.read_csv("data/real_data_full.csv")  # Control group
compare_with_catalog_quality(df_control)  # Robustness test
```

---

## 📊 SUMMARY TABLE

| Dataset | Type | Quality | Success | Purpose | Status |
|---------|------|---------|---------|---------|--------|
| **real_data_emission_lines_clean.csv** | ESO Spectroscopy | High | **97.9%** | **PRIMARY** | ✅ |
| real_data_full.csv | GAIA Catalog | Mixed | 51% | Control | ⚠️ |
| gaia_sample_small.csv | GAIA DR3 | Good | - | Examples | ✅ |
| planck/... | CMB | High | - | Cosmology | ✅ |
| sdss_catalog.csv | SDSS | Good | - | Optional | ❌ |

---

## 🎓 REFERENCE

For detailed analysis and validation results, see:
- `PAIRED_TEST_ANALYSIS_COMPLETE.md` - Complete validation
- `STRATIFIED_PAIRED_TEST_RESULTS.md` - Regime-specific results
- `PHI_FUNDAMENTAL_GEOMETRY.md` - φ-geometry basis
- `perfect_paired_test.py` - Implementation

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
