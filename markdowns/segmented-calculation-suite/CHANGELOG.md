# Changelog

All notable changes to the SSZ Calculation Suite.

## [1.0.0] - 2025-01-17

### 🚨 CRITICAL FIX: SSZ Redshift Formula

**Before (WRONG):**
```python
z_ssz = 1/D_ssz - 1 = Ξ  # Gave +350% deviation from GR!
```

**After (CORRECT):**
```python
z_ssz = z_GR × (1 + Δ(M)/100)  # Only ~1-2% deviation
```

This fix was derived from the "Dual Velocities in Segmented Spacetime" paper:
> "In the segmented model γ_s is matched identical, therefore z(r) is identical"

### Added
- Google Colab notebook (`SSZ_Calculation_Suite.ipynb`)
- Δ(M) φ-correction with parameters A=98.01, α=2.7177e4, B=1.96
- Extended regime classification: `very_close`, `photon_sphere`, `strong`, `weak`
- Full documentation in `docs/WEAK_STRONG_FIELD_SPEC.md`
- Validation alignment docs in `docs/UNIFIED_RESULTS_ALIGNMENT.md`

### Changed
- `z_ssz()` now uses GR-based redshift with small Δ(M) correction
- D_ssz is now only used for time dilation, NOT for redshift
- Updated neutron star prediction tests to expect ~1-3% SSZ increase (not 100-200%)
- README updated with correct physics formulas and Colab badge

### Fixed
- Neutron star redshift now matches papers (~1.25% higher than GR, not 350%)
- Test `test_ssz_predicts_higher_redshift` corrected for actual physics
- All 53 tests now passing

### Validated Against
- GPS time correction: 45.7 μs/day ✅
- Pound-Rebka experiment: 2.46×10⁻¹⁵ ✅
- 47 ESO spectroscopy measurements: 97.9% accuracy ✅
- Ξ(r_s) = 0.802, D_SSZ(r_s) = 0.555 ✅

---

## [0.9.0] - 2025-01-16

### Added
- Initial calculation suite with CLI and Gradio web UI
- Xi regime system (weak/strong/blend)
- Power law energy normalization
- PPN methods for lensing and Shapiro delay
- 17 compact object dataset
- 8 NICER-validated neutron star dataset

---

© 2025 Carmen Wrede & Lino Casu
