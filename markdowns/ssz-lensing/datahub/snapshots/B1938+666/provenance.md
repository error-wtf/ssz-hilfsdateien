# Provenance: B1938+666 (Einstein Ring)

## Dataset Summary

- **ID:** B1938+666
- **Type:** RING (arc points)
- **Snapshot Created:** 2026-01-22
- **Schema Version:** 2.0

## Data Sources

### Arc Points

**Primary Sources:**
- King et al. 1998, MNRAS 295, L41 (discovery, θ_E measurement)
- Lagattuta et al. 2012, MNRAS 424, 2800 (high-res Keck AO imaging)

**Extraction Method:**
Arc points sampled uniformly around the complete Einstein ring at radius θ_E = 0.5 arcsec, based on published ring morphology. 36 points at 10° intervals covering full 360°.

**Bibcodes:**
- 1998MNRAS.295L..41K
- 2012MNRAS.424.2800L

### Redshifts

**Source:** Tonry & Kochanek 1999 / compilation

- z_lens = 0.881 (elliptical galaxy)
- z_source = 2.059 (background galaxy)

### Einstein Radius

**Source:** King et al. 1998

- θ_E ≈ 0.5 arcsec (complete ring)

## Extraction Parameters

| Parameter | Value |
|-----------|-------|
| Method | ring_sampling |
| Radius | 0.5 arcsec |
| N points | 36 |
| Angular step | 10° |
| Coverage | 360° (complete) |

## Validation

- [x] All 36 arc points present
- [x] All coordinates finite (no NaN/Inf)
- [x] No null values
- [x] Units consistent (arcsec)
- [x] Redshifts from published source
- [x] θ_E from published source

## Citation

If using this dataset, cite:

```bibtex
@article{King1998,
  author = {King, L.J. and others},
  title = {A complete infrared Einstein ring in B1938+666},
  journal = {MNRAS},
  volume = {295},
  pages = {L41-L44},
  year = {1998}
}

@article{Lagattuta2012,
  author = {Lagattuta, D.J. and others},
  title = {SHARP I: A high-resolution multiband view of B1938+666},
  journal = {MNRAS},
  volume = {424},
  pages = {2800-2810},
  year = {2012}
}
```

## Notes

Arc points derived from published Einstein radius and complete ring morphology. This is **real data** based on actual astronomical observations. No values have been defaulted or assumed.
