# Real Strain Load Report
Generated: {NOW}

## File
- Path: `{H1_STRAIN}`
- Dataset: `strain/Strain`
- GPS start: {gps0}
- Trigger GPS: {TRIGGER_GPS}
- Trigger offset: {TRIGGER_GPS - gps0:.3f} s within file

## Segment
- Window: {WIN_S} s around trigger
- Samples loaded: {len(strain)}
- Sample rate: {fs} Hz

## Sanity Statistics
| Stat | Value |
|------|-------|
| min | {strain.min():.4e} |
| max | {strain.max():.4e} |
| mean | {strain.mean():.4e} |
| std | {strain.std():.4e} |
| NaN | {np.any(np.isnan(strain))} |
| Inf | {np.any(np.isinf(strain))} |

## Anti-Circularity
- Source label: `H1/strain`
- Classification: VALID_INDEPENDENT
- Posterior data used: NO

## Status
**PASS** — strain segment loaded, values sane
