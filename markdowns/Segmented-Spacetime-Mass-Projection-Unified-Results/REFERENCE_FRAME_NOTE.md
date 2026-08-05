# Note on Laboratory Reference Frames

⚠️ **Critical Scientific Consideration**

The "rest wavelength" (e.g. λ₀ = 656.281 nm for H-alpha) used in spectroscopic datasets is **not a universal constant** but a **laboratory-defined reference value**. 

Each observatory measures within its own local gravitational potential and time standard, so the observed frequency f_obs inherently depends on the laboratory frame. 

**Therefore:** Any formula or comparison involving f_obs must be performed within the **same reference frame** or after proper barycentric (or equivalent) correction.

---

## ⚠️ Critical Implications for Model Testing:

Because the observed frequency f_obs is defined relative to each laboratory's local reference frame, **all comparisons or formula evaluations involving f_obs must use identical laboratory calibration values**.

**Formulas based on f_obs are only comparable when tested against the same f_obs baseline.**

Since laboratory reference conditions (gravitational potential, time standard, motion) can differ by orders of magnitude, **cross-lab tests without proper correction may yield physically impossible values** — making **correct models appear wrong** and **wrong models appear correct**.

### Example of Systematic Error:

```
Lab A (Sea level):    f_obs_A = 4.5682×10¹⁴ Hz (H-alpha)
Lab B (ISS orbit):    f_obs_B = 4.5683×10¹⁴ Hz (same line!)
                      ───────────────────────────────────
Apparent shift:       Δf/f ≈ 2×10⁻⁵ (≈ 6 km/s)
                      
TRUE cause: Gravitational + kinematic frame difference
WRONG interpretation: Source motion or gravitational redshift
```

**Without barycentric correction:** A physically correct model tested on Lab A data vs. Lab B predictions will show systematic 6 km/s "error" — purely from reference frame mismatch, not model failure!

**Solution:** Transform all f_obs to common barycentric frame BEFORE model comparison.

---

## Quick Facts:

- **Effect size:** ~10⁻¹² from gravity, ~10⁻⁴ from orbital motion
- **Solution:** Barycentric transformation (standard in astrophysics)
- **This dataset:** All f_obs already barycentric-corrected ✅
- **Standards:** NIST Atomic Spectra Database, CODATA 2018

---

## See Also:

- **Detailed explanation:** [LABORATORY_COMPARABILITY.md](LABORATORY_COMPARABILITY.md)
- **Paper section:** [papers/CALIBRATION_BIAS_SECTION.md](papers/CALIBRATION_BIAS_SECTION.md)
- **Data documentation:** [DATA_COLUMNS_README.md](DATA_COLUMNS_README.md) (Section: "Laborvergleichbarkeit")
- **Analysis documentation:** [COMPREHENSIVE_DATA_ANALYSIS.md](COMPREHENSIVE_DATA_ANALYSIS.md)

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
