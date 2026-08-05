# LIGO Release Science Map

**Generated:** 2026-05-14  
**Source:** E:\clone\ligo-gw240925-gw250207-release\18600070  
**Status:** Phase 2 - Science Mapping

---

## Data Products by Type

| Type | Archives | Contents | SSZ Relevance |
|------|----------|----------|---------------|
| **posteriors** | combined_samples.tar.gz | Parameter estimation samples | CRITICAL: Final mass/spin for QNM reference |
| **ringdown** | ringdown.tar.gz | QNM frequencies, damping times | CRITICAL: Measured QNM for SSZ test |
| **qnm** | qnmrf.tar.gz | QNM rational filter analysis | CRITICAL: Independent QNM measurement |
| **residuals** | residuals.tar.gz | Post-GR subtraction residuals | Test B: Residual structure |
| **calibration** | calibration.tar.gz, cal_env.tar.gz | Calibration priors, envelopes | Robustness: C00/C01 comparison |
| **strain** | GW240925-C00-Strain.tar | Raw detector strain | Primary data: C00 uncalibrated |
| **gr_tests** | tiger.tar.gz, fti.tar.gz, pca.tar.gz | GR deviation tests | Baseline: GR null tests |
| **waveforms** | pseobnr.tar.gz | SEOBNR waveforms | Modeling: Waveform comparisons |
| **skymaps** | skymaps.tar.gz | Localization sky maps | Localization: Sky position |
| **notebooks** | notebook.tar.gz | Jupyter analysis notebooks | Reproduction: Official pipelines |

---

## Key HDF5 Files (Expected)

Based on LIGO/Virgo/KAGRA data format:

### Posterior Samples
- `GW240925_combinedPHM_envcalC01_metafile.hdf5` (~200 MB)
  - Contains: mass_1_source, mass_2_source, chi_eff, final_mass, final_spin, luminosity_distance
  - SSZ Critical: final_mass, final_spin for QNM reference

- `GW250207_combinedPHM_cal_metafile.hdf5` (~300 MB)
  - Similar parameters for second event

### Ringdown/QNM
- `ringdown/qnm_posteriors.hdf5` (expected)
  - Contains: f_220, tau_220, f_221, amplitudes
  - SSZ Critical: f_220 measured vs GR prediction

---

## Jupyter Notebooks (Expected)

Based on LIGO release structure:

| Notebook | Purpose | Input | Output |
|----------|---------|-------|--------|
| calibration-monitoring.ipynb | ASD plots, monitoring lines | calibration.tar.gz | H1_ASD_*.pdf |
| parameter-estimation.ipynb | PE results, corner plots | combined_samples.tar.gz | Posterior plots |
| ringdown-analysis.ipynb | QNM extraction | ringdown.tar.gz | f_220, tau_220 |
| gr-test-tiger.ipynb | GR deviation tests | tiger.tar.gz | Bayes factors |
| gr-test-fti.ipynb | Fractional template | fti.tar.gz | FTI statistics |
| residual-analysis.ipynb | Post-subtraction checks | residuals.tar.gz | Residual PSD |

---

## Event Mapping

### GW240925
- **Strain:** GW240925-C00-Strain.tar (uncalibrated)
- **Posteriors:** GW240925_combinedPHM_envcalC01_metafile.hdf5 (calibrated C01)
- **Calibration:** C00 → C01 → envcal variants
- **Ringdown:** ringdown.tar.gz (QNM analysis)
- **GR Tests:** tiger, fti, pca results

### GW250207
- **Posteriors:** GW250207_combinedPHM_cal_metafile.hdf5
- **Type:** Second calibration study event
- **Purpose:** Cross-event consistency check

---

## SSZ Test Targets

### Test A: QNM Frequency Shift (Primary)
```
Data needed:
- f_QNM,measured from ringdown.tar.gz
- M_final, χ_final from combined_samples.tar.gz (inspiral/merger PE)
- f_QNM,GR reference computed independently

Expected SSZ: f_SSZ / f_GR ≈ 1.39
```

### Test B: Residual Structure (Secondary)
```
Data needed:
- residuals.tar.gz
- After GR waveform subtraction

Expected SSZ: Structured residuals (not noise-like)
```

### Test C: Calibration Robustness (Tertiary)
```
Data needed:
- C00 vs C01 vs envcal posteriors
- Compare parameter shifts

Expected SSZ: Effect stable across calibrations
```

---

## Data Dependencies

```
combined_samples.tar.gz
    ↓ (provides)
final_mass, final_spin
    ↓ (compute)
f_QNM,GR(reference)
    ↓ (compare to)
ringdown.tar.gz
    ↓ (provides)
f_QNM,measured
    ↓ (calculate)
R_f = f_measured / f_GR
    ↓ (test)
SSZ hypothesis: R_f ≈ 1.39?
```

---

## Critical Independence Check

### For SSZ QNM Test:
- ✅ f_QNM,measured: From ringdown/QNM analysis (different measurement)
- ✅ f_QNM,GR: From inspiral/merger PE final mass/spin (independent)
- ⚠️ Must verify: No shared processing between inspiral PE and ringdown QNM

### Blocker if violated:
```
If ringdown used to derive final mass/spin → CIRCULAR
If same likelihood sampler used for both → DEPENDENT
If independent: Inspiral waveform ≠ Ringdown template → SAFE
```

---

## Next Steps

1. **Inspect HDF5 structure** (headers only, not loading data)
   - Verify posterior samples structure
   - Verify ringdown/QNM data format
   - Locate final_mass, final_spin, f_220 fields

2. **Check notebook dependencies**
   - Read notebook metadata
   - Identify required Python packages
   - Check path assumptions

3. **Identify calibration variants**
   - C00: Uncalibrated strain
   - C01: Calibrated with envelope
   - envcal: Calibration envelope
   - Map which files belong to which variant

4. **Prepare QNM/Ringdown readiness report**
   - Verify independence of measurements
   - Confirm no circular derivation
   - Document before R_f computation

---

## Status

| Phase | Status | Next Action |
|-------|--------|-------------|
| 1. Inventory | ✅ Complete | - |
| 1B. Validation | ✅ PASS | User confirmed extraction |
| 2. Science Mapping | ✅ Complete | This document |
| 3. HDF5 Structure | ⏳ Ready | Inspect headers only |
| 4. Notebook Check | ⏳ Ready | Dependency analysis |
| 5. QNM Readiness | ⏳ Ready | Independence verification |
| 6. SSZ Test | ⏳ Blocked | Wait for readiness report |

---

**Document Status:** Phase 2 Complete  
**Ready for:** Phase 3 (HDF5 Structure Inspection)  
**SSZ Hypothesis:** Pre-registered (39% QNM shift)  
**Anti-Circularity:** To be verified in readiness report
