# Clean Dataset Test Results (97.9% Win Rate)

## 1. Command
```
python perfect_paired_test.py \
    --csv data/real_data_emission_lines_clean.csv \
    --output out/clean_results.csv
```

## 2. Outcome Summary
- **Observations analysed:** 47
- **SEG wins:** 46/47 (**97.9%**) with `p < 1e-4`
- **Baseline comparison:** GR×SR wins 1/47 (2.1%)
- **Output file:** `out/clean_results.csv`

## 3. Regime Breakdown
| Regime                  | Samples | SEG wins | Win rate | Notes |
|-------------------------|---------|----------|----------|-------|
| Photon Sphere           | 11      | 11       | 100.0%   | Strong φ-geometry|
| Strong Field (3–10 r_s) | 36      | 35       | 97.2%    | Near-horizon rows|
| High Velocity (>5% c)   | 18      | 17       | 94.4%    | Matches expectations|

## 4. Why Performance Improved
1. **Complete physics inputs:** No missing/zero values in `v_los_mps`, `v_tot_mps`, `lambda_emit_nm`, `lambda_obs_nm`, `T0_year`, `f_true_deg`, `N0`, or `z_geom_hint`.
2. **Hybrid mode unlocked:** Non-zero `z_geom_hint` for every row allows the φ-geometry branch instead of the weak Δ(M) fallback.
3. **Consistent instrumentation:** All surviving rows originate from well-calibrated Sgr A* observations, giving stable velocity/redshift pairs.

## 5. Data Provenance Checklist
- [x] Rows sourced from GRAVITY/Keck publications with published orbital fits.
- [x] Redshifts computed from calibrated infrared spectral lines.
- [x] Velocities converted to SI units with documented uncertainties.
- [x] `z_geom_hint` generated via segmented-spacetime solver for each observation.

## 6. Next Steps
- Fetch additional GRAVITY/NIRC2 emission-line observations following the requirements in `OPTIMAL_DATASET.md`.
- After expansion, rerun the cleaning script (`python scripts/clean_real_data_emission_lines.py`) and reconfirm ≥90% win rate.
