# Phase 5C: R_f Computation Report

**Generated:** 2026-05-14  
**Task ID:** LIGO_PHASE_5_PREREGISTERED_QNM_RF_TEST  
**Status:** BLOCKED - GR Reference Computation

---

## Attempted Computation

### Preregistered Formula
```
R_f := f_QNM,measured / f_QNM,GR(reference)
```

### Available Data

| Component | Source | Status |
|-----------|--------|--------|
| f_QNM,measured | ringdown/H1_only/f | ✅ Available |
| f_QNM,measured | ringdown/L1_only/f | ✅ Available |
| final_mass | combinedPHM/priors/samples | ✅ Available |
| final_spin | combinedPHM/priors/samples | ✅ Available |
| **f_QNM,GR(reference)** | **Requires computation from M, χ** | **❌ BLOCKED** |

---

## Blockage Reason

### Missing Component: GR QNM Frequency Computation

To compute f_QNM,GR(reference) from final_mass and final_spin, a reliable GR/Kerr QNM calculation method is required.

**Preregistered Protocol Requirement:**
> "If GR reference is not explicitly provided: compute f_QNM,GR(reference) from final mass and final spin posterior **only if a documented GR/Kerr QNM formula or library is available locally and cited in the report**. If **no reliable local formula/library exists, do NOT invent one**. Mark GR reference computation BLOCKED."

### Current Situation

| Requirement | Status |
|-------------|--------|
| Local QNM library (qnm, kerrgeodesic, etc.) | ❌ Not installed in .venv-ligo |
| Analytic GR QNM formula implementation | ❌ Not available locally |
| Pre-computed f_QNM,GR in HDF5 files | ❌ Not found in ringdown or metafiles |
| Validated external reference | ❌ Not verified |

### GR QNM Physics Background

For a Kerr BH, the l=m=2, n=0 QNM frequency depends on both mass M and dimensionless spin χ:

```
f_QNM = (1/2π) × ω_QNM(M, χ)
```

Where ω_QNM is the complex frequency from the Kerr QNM eigenvalue problem. This requires:
- Numerical solution of Teukolsky equation
- Or tabulated fits (e.g., from Berti et al. 2009)
- Or specialized libraries (qnm, pykerr, etc.)

**The relationship is non-trivial and cannot be approximated safely without validated code.**

---

## Attempted Workarounds (All Rejected)

| Workaround | Status | Reason |
|------------|--------|--------|
| Approximate with ω ≈ (0.3737 - 0.0846χ) × (M/M_sun)^-1 | ❌ REJECTED | Not preregistered, no validation |
| Use pykerr/qnm if available | ❌ REJECTED | Not in local venv |
| Extract from ringdown file directly | ❌ FAILED | No pre-computed GR reference found |
| Use formula from literature | ❌ REJECTED | Requires implementation verification |

---

## What Was Found

### Measured QNM Data (Available)
```python
# From rd_GW250207_Kerr220_8M_singleIFO_prod_2048Hz_evol_20Ksamps.hdf5
H1_only/f: median = 243.2 Hz, samples = 20,000
L1_only/f: median = 243.8 Hz, samples = 20,000
```

### Remnant Parameters (Available)
```python
# From GW250207_combinedPHM_cal_metafile.hdf5 (various approximants)
final_mass: ~60-80 M_sun (varies by approximant)
final_spin: ~0.6-0.8 (varies by approximant)
```

### Missing: GR Prediction
```python
# Would require:
f_GR = qnm_frequency(final_mass, final_spin, mode=(2,2,0))
# Result expected: ~240-260 Hz for GW250207-like remnant
```

---

## Safety Compliance

| Rule | Status |
|------|--------|
| Do not invent formulas | ✅ COMPLIED - Blocked instead of approximating |
| Do not compute without library | ✅ COMPLIED - No qnm/pykerr available |
| Mark BLOCKED if no reliable method | ✅ COMPLIED - This report |
| Document what is missing | ✅ COMPLIED - GR reference computation |

---

## Alternative Path Forward

### Option 1: Install QNM Library (Future)
```bash
pip install qnm
# or
pip install pykerr
```

Then re-run Phase 5C with validated GR QNM computation.

### Option 2: Use Tabulated Reference (Future)
Obtain pre-computed GR QNM frequency for GW250207 from:
- LIGO/Virgo parameter estimation release
- Academic literature with GW250207 analysis
- QNMRF product if it contains GR reference (currently blocked)

### Option 3: Exploratory Calculation (Explicitly Labeled)
Use published fitting formula from Berti et al. (2009) with clear citation:
```
ω ≈ 0.3737 - 0.0846χ - 0.0260χ² + ... (for l=m=2, n=0)
```

**But this would require:**
- Implementation verification
- Uncertainty propagation
- Explicit "exploratory only" label
- No definitive SSZ claims

---

## Conclusion

**R_f computation BLOCKED at Phase 5C.**

The blockage is due to missing local capability to compute GR-predicted QNM frequency from final_mass and final_spin. This is a **technical blocker**, not a fundamental physics issue.

### What Exists
- ✅ Measured QNM frequencies (ringdown analysis)
- ✅ Remnant mass/spin posteriors (combinedPHM metafiles)
- ✅ Anti-circularity assessment (PARTIALLY_COUPLED)

### What Is Missing
- ❌ GR QNM computation library/formula (locally validated)
- ❌ Pre-computed GR reference values in HDF5 products

### Recommendation

**Next step:** Install validated QNM library (e.g., `qnm` package) and re-run Phase 5C, OR obtain pre-computed GR QNM reference from LIGO/Virgo documentation.

**Do not proceed with unvalidated approximations.**

---

*This blockage follows the preregistered protocol's safety requirements: when GR reference cannot be computed reliably, mark BLOCKED rather than invent methods.*
