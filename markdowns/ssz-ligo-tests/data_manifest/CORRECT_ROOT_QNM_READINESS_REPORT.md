# QNM R_f Test Readiness Report (Corrected)

**Generated:** 2026-05-14T13:39:55.832019

## Preregistered Test Definition

```
R_f := f_QNM,measured / f_QNM,GR(reference)

- f_QNM,measured = posterior median of observed QNM frequency
- f_QNM,GR(reference) = GR-predicted QNM from final mass/spin posterior
- mode fixed: l=m=2,n=0
```

## Data Availability Status: READY

The required data products are now confirmed accessible:

### Primary Posterior Samples

| File | Size | Items | QNM-Related Fields |
|------|------|-------|-------------------|
| GW240925_combinedPHM_envcalC01_metafile.hdf5 | 190.8 MB | 1898 | 50 |
| GW250207_combinedPHM_cal_metafile.hdf5 | 292.5 MB | 3105 | 50 |

### Strain Data

- 6 strain HDF5 files available

## R_f Computation Status

**R_f has NOT been computed yet.**

The data is now verified as accessible, but the actual R_f calculation
requires careful separation of:

1. **Independent measurement**: Ringdown frequency from posterior samples
2. **GR reference prediction**: QNM frequency from final mass/spin

Anti-circularity must be ensured before R_f computation.

## Next Steps for R_f Test

1. Extract final_mass, final_spin from metafile posteriors
2. Identify QNM frequency fields (f_220, omega_220, etc.)
3. Verify independence of measurement and prediction sources
4. Compute R_f only after anti-circularity confirmation

## Safety Declaration

- **No R_f computed yet**: YES
- **No SSZ claim made**: YES
- **Anti-circularity verified**: PENDING (to be done in next phase)
- **Data accessibility**: VERIFIED
