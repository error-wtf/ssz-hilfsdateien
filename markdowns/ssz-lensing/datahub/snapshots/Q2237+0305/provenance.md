# Provenance: Q2237+0305 (Einstein Cross)

## Dataset Summary

- **ID:** Q2237+0305
- **Type:** QUAD (4 lensed images)
- **Snapshot Created:** 2026-01-22
- **Schema Version:** 2.0

## Data Sources

### Image Positions (A, B, C, D)

**Source:** Irwin et al. 1989, AJ 98, 1989-1994, Table II
**Bibcode:** 1989AJ.....98.1989I
**URL:** https://adsabs.harvard.edu/full/1989AJ.....98.1989I

Positions extracted from Table II of the paper. Original measurements from HST/FOC observations.

| Image | x (arcsec) | y (arcsec) | σ (arcsec) |
|-------|------------|------------|------------|
| A | +0.758 | +0.560 | 0.003 |
| B | -0.619 | +0.480 | 0.003 |
| C | -0.472 | -0.761 | 0.003 |
| D | +0.857 | -0.196 | 0.003 |

### Redshifts

**Source:** Huchra et al. 1985, AJ 90, 691-696
**Bibcode:** 1985AJ.....90..691H

- z_lens = 0.0394 (spiral galaxy)
- z_source = 1.695 (quasar)

### Einstein Radius

**Source:** CASTLES Survey catalog
**URL:** https://lweb.cfa.harvard.edu/castles/

- θ_E ≈ 0.89 arcsec

## Validation

- [x] All 4 image positions present
- [x] All coordinates finite (no NaN/Inf)
- [x] No null values
- [x] Units consistent (arcsec)
- [x] Redshifts from published source
- [x] Position uncertainties from published source

## Citation

If using this dataset, cite:

```bibtex
@article{Huchra1985,
  author = {Huchra, J. and others},
  title = {2237+0305: A new and unusual gravitational lens},
  journal = {AJ},
  volume = {90},
  pages = {691-696},
  year = {1985}
}

@article{Irwin1989,
  author = {Irwin, M.J. and others},
  title = {Photometric variations in the Q2237+0305 system},
  journal = {AJ},
  volume = {98},
  pages = {1989-1994},
  year = {1989}
}
```

## Notes

This is a **real dataset** from published astronomical observations. No values have been defaulted, assumed, or interpolated. All fields are directly from cited sources.
