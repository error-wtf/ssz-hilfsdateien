# Formula-Code Mapping Report

**Generated:** 2025-10-20 01:37:14
**Formulas Mapped:** 10

---

## 📊 Summary

- **Total Formulas:** 10
- **Implemented:** 10
- **Not Found:** 0
- **Coverage:** 100.0%

`[██████████]` 100.0%

---

## ✅ Implemented Formulas

### Golden Ratio

**Formula:** `φ = (1 + √5)/2`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (70):**

- **calculation_test.py** (line 3)
  ```python
  segmented_mass_from_rphi.py  –  Extended Roundtrip Validation with Real Calculations
  ```

- **complete-math.py** (line 14)
  ```python
  phi = (D(1) + D(5).sqrt()) / D(2)  # Goldener Schnitt (dimensionslos)
  ```

- **compute_vfall_dual_files.py** (line 54)
  ```python
  PHI_DEFAULT = (1 + 5 ** 0.5) / 2  # the Golden Ratio, ≈1.618
  ```

- **compute_vfall_from_z.py** (line 33)
  ```python
  PHI_DEFAULT = (1 + 5 ** 0.5) / 2  # 1.618033988749895...
  ```

- **create_final_deb.py** (line 319)
  ```python
  PHILOSOPHY
  ```

### R Phi

**Formula:** `r_φ = φ·(GM/c²)·(1 + Δ(M)/100)`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (26):**

- **calculation_test.py** (line 7)
  ```python
  2. Computing the segmented radius r_phi from that mass.
  ```

- **complete-math.py** (line 45)
  ```python
  def r_phi_corr(M):
  ```

- **extend_all_tests.py** (line 54)
  ```python
  "result": "All r_φ > 0 (Physical boundary)"
  ```

- **final_test.py** (line 39)
  ```python
  def mass_from_rphi(r_phi: Decimal) -> Decimal:
  ```

- **further-bak.py** (line 26)
  ```python
  def r_phi(M, phi=phi):
  ```

### Schwarzschild

**Formula:** `r_s = 2GM/c²`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (101):**

- **analyze_failures.py** (line 207)
  ```python
  s_star_suggestions = [
  ```

- **bound_energy_plot_with_frequenz_shift_fix.py** (line 30)
  ```python
  r_s = Decimal(2) * G * M_kg / (c**2)
  ```

- **calculation_test.py** (line 6)
  ```python
  1. Computing the Schwarzschild radius r_s from a known mass.
  ```

- **carmen_qed_incompleteness_demo.py** (line 215)
  ```python
  lines.append("  flow explains the redshift primarily via GR×SR plus a Schwarzschild-compatible")
  ```

- **complete-math.py** (line 35)
  ```python
  r_s = D(2)*G*M/c**2
  ```

### Time Dilation

**Formula:** `τ(x) = φ^(-α·N(x))`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (19):**

- **further-bak.py** (line 18)
  ```python
  # --- Objektauswahl (nur eine Zeile aktiv lassen!)
  ```

- **segmented_full_proof.py** (line 47)
  ```python
  ("Proxima Centauri",   1.210000e-01),
  ```

- **segmented_mass.py** (line 80)
  ```python
  ("Proxima Centauri",         0.1221*M_sun),
  ```

- **ssz_interactive_gui.py** (line 137)
  ```python
  ("τ(r) - Time Dilation", "tau"),
  ```

- **ssz_test_suite.py** (line 91)
  ```python
  def test_tau_phi_scaling(self):
  ```

### Segment Density

**Formula:** `N(x) = Σ γ_i·K_i(||x - x_i||)`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (27):**

- **bound_energy_english.py** (line 13)
  ```python
  def compute_segment_density(f_emit: float, f_obs: float, N0: float = 1.000000028) -> float:
  ```

- **bound_energy_plot.py** (line 30)
  ```python
  def compute_segment_density(f_emit, f_obs, N0):
  ```

- **fetch_robust_5000.py** (line 71)
  ```python
  t = max(tlist, key=lambda x: len(x))
  ```

- **fetch_robust_5000_enhanced.py** (line 87)
  ```python
  t = max(tlist, key=lambda x: len(x))
  ```

- **run_full_suite.py** (line 10)
  ```python
  3. Scripts/tests (pytest - SSZ kernel, invariants, segmenter, cosmo)
  ```

### Refractive Index

**Formula:** `n(x) = 1 + κ·N(x)`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (105):**

- **analyze_failures.py** (line 164)
  ```python
  for category in failure_by_cat.index:
  ```

- **bound_energy.py** (line 193)
  ```python
  df.to_csv(out, index=False)
  ```

- **bound_energy_english.py** (line 107)
  ```python
  df.to_csv(csv_path, index=False)
  ```

- **bound_energy_plot.py** (line 127)
  ```python
  df.to_csv(csv_path, index=False)
  ```

- **bound_energy_plot_with_frequenz_shift_fix.py** (line 148)
  ```python
  df.to_csv(csv_path, index=False)
  ```

### Dual Velocity

**Formula:** `v_esc·v_fall = c²`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (14):**

- **compute_vfall_dual_files.py** (line 9)
  ```python
  dataset, derives the dual velocity scale ``v_fall`` along with several
  ```

- **run_all_ssz_terminal.py** (line 186)
  ```python
  v_esc/c = sqrt(r_s/r) = sqrt(1/(r/rs))
  ```

- **segspace_enhanced_test_better_final.py** (line 501)
  ```python
  print("    Note: v_esc x v_fall = c^2 (invariant), not physical velocity")
  ```

- **ssz_interactive_gui.py** (line 310)
  ```python
  v_esc, v_fall = self.core.dual_velocity(r, mass_kg)
  ```

- **ssz_test_suite.py** (line 146)
  ```python
  """Test: v_esc · v_fall = c²"""
  ```

### Escape Velocity

**Formula:** `v_esc = √(2GM/r)`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (16):**

- **run_all_ssz_terminal.py** (line 186)
  ```python
  v_esc/c = sqrt(r_s/r) = sqrt(1/(r/rs))
  ```

- **segspace_enhanced_test_better_final.py** (line 501)
  ```python
  print("    Note: v_esc x v_fall = c^2 (invariant), not physical velocity")
  ```

- **segspace_final_test.py** (line 350)
  ```python
  from xml.sax.saxutils import escape as xml_escape
  ```

- **ssz_interactive_gui.py** (line 310)
  ```python
  v_esc, v_fall = self.core.dual_velocity(r, mass_kg)
  ```

- **ssz_test_suite.py** (line 146)
  ```python
  """Test: v_esc · v_fall = c²"""
  ```

### Ppn Parameters

**Formula:** `β = 1, γ = 1 (GR)`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (87):**

- **analyze_failures.py** (line 103)
  ```python
  beta = min(abs(v_tot_mps) / C, 0.999999)
  ```

- **bound_energy_english.py** (line 19)
  ```python
  def compute_bound_mass(E_gamma: float, m_e_: float = m_e, c_: float = c) -> float:
  ```

- **bound_energy_plot.py** (line 36)
  ```python
  def compute_bound_mass(E_gamma):
  ```

- **bound_energy_plot_with_frequenz_shift_fix.py** (line 35)
  ```python
  # Optional: SR-Doppler (wenn beta/beta_los vorliegt)
  ```

- **carmen_qed_incompleteness_demo.py** (line 219)
  ```python
  lines.append("1) Partial coupling: introduce alpha_em/alpha_det = 1 + beta*(N_emit−N0)")
  ```

### Metric A

**Formula:** `A(r) = 1 - r_s/r`

**Documented in:** MATHEMATICAL_FORMULAS.md

**Implementations (47):**

- **compute_vfall_dual_files.py** (line 285)
  ```python
  Compute dual velocities v_fall and diagnostic metrics for two CSV files.
  ```

- **derive_effective_stress_energy.py** (line 10)
  ```python
  ds² = -A(r) c² dt² + B(r) dr² + r²(dθ² + sin²θ dφ²),
  ```

- **expand_dataset.py** (line 100)
  ```python
  ("GW190412", "BH-merger", 30.1, 0.26, "Asymmetric mass ratio"),
  ```

- **fetch_eso_br_gamma.py** (line 36)
  ```python
  - z_geom_hint:    geometric/GR hint z (dimensionless), optional
  ```

- **fetch_robust_5000_enhanced.py** (line 183)
  ```python
  "z_geom_hint": None,  # No geometric hint available
  ```

## ⚠️  Formulas Not Found in Code

✅ All formulas found in code!

---

## 📋 Complete Mapping Table

| Formula | Status | Files | First Implementation |
|---------|--------|-------|----------------------|
| Dual Velocity | ✅ | 14 | compute_vfall_dual_files.py |
| Escape Velocity | ✅ | 16 | run_all_ssz_terminal.py |
| Golden Ratio | ✅ | 70 | calculation_test.py |
| Metric A | ✅ | 47 | compute_vfall_dual_files.py |
| Ppn Parameters | ✅ | 87 | analyze_failures.py |
| R Phi | ✅ | 26 | calculation_test.py |
| Refractive Index | ✅ | 105 | analyze_failures.py |
| Schwarzschild | ✅ | 101 | analyze_failures.py |
| Segment Density | ✅ | 27 | bound_energy_english.py |
| Time Dilation | ✅ | 19 | further-bak.py |

---

## 🎯 Recommendations

### For Developers

- Add formula references in docstrings
- Use consistent variable naming (match docs)
- Comment complex calculations with formula numbers

### For Documentation

- Add 'Implementation:' sections to formula docs
- Link to specific code files
- Include code examples

### Cross-Reference Format

**In Documentation:**
```markdown
### Formula 2.1: φ-Radius
r_φ = φ·(GM/c²)·(1 + Δ(M)/100)

**Implemented in:**
- `core/physics.py` (calculate_r_phi)
- `tests/test_ppn_exact.py` (validation)
```

**In Code:**
```python
def calculate_r_phi(M, delta_M):
    """
    Calculate φ-radius.
    
    Formula: r_φ = φ·(GM/c²)·(1 + Δ(M)/100)
    Reference: MATHEMATICAL_FORMULAS.md, Section 2.1
    """
    phi = (1 + np.sqrt(5)) / 2
    r_s = 2 * G * M / c**2
    return phi * (r_s / 2) * (1 + delta_M / 100)
```

---

**Generated by:** `scripts/create_formula_code_map.py`

© 2025 Carmen Wrede & Lino Casu
