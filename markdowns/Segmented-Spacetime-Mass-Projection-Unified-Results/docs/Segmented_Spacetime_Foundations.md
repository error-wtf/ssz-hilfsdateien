# Segmented Spacetime Foundations — Internal Reference

**Authors**: Lino Casu · Carmen Wrede · Bingsi  \
**Purpose**: Unified summary of the Segmented Spacetime framework plus practical testing notes for the Windsurf cosmology branch.  \
**Scope**: Concept recap, observational mapping, simulation hooks, validation, and automation commands.

---

## 1. Core Concept

- **Discrete temporal density**: gravitational curvature is modelled as nested segments with local time density `gamma_seg = dτ/dt`, where `0 < gamma_seg ≤ 1`.
- **Nested metric**:
  \[
  g_{\mu\nu}^{(2)} = \gamma_{\text{seg}}^{2}\, g_{\mu\nu}^{(1)}, \quad g^{(2)} \subset g^{(1)} \subset g^{(0)}.
  \]
- **Scaling relations**:
  - `t_local = gamma_seg * t_global`
  - `E_eff ∝ gamma_seg^{-1}`
  - `v_exp ∝ gamma_seg^{-1/2}`
  - `p_obs = (M * v_exp^2) / R`
- **Potential & gradient**:
  \[
  \Phi(r) \propto - \int \frac{1-\gamma_{\text{seg}}(r)}{r^{2}} dr, \qquad \frac{d\gamma_{\text{seg}}}{dr} < 0.
  \]
- **Reciprocity break**: outer observers measure redshift (energy deficit) while inner observers measure blueshift (energy surplus) across a segmentation interface.

---

## 2. Observational Mapping: LBV Nebula G79.29+0.46

| Region | Tracer set | T [K] | Time-flow interpretation |
| --- | --- | ---: | --- |
| H II | Br α, [Ne II], free–free | 7×10³ – 10⁴ | fast time / low curvature |
| PDR | PAHs, [C II], [O I], IR 8–100 μm | 200 – 500 | transition |
| Molecular | CO(2–1/3–2), NH₃(1,1), OH | 20 – 80 | slow time / high curvature |

**Key anomalies** (explained by segmentation):
- Expansion velocity `≈14–16 km s⁻¹`, ~5 km s⁻¹ above standard bubble models.
- Thermal inversion (cold gas inside ionised shell).
- Radio continuum overlaps dense molecular tracers.

**Diagnostics**:
\[
\begin{aligned}
 t_{\text{dyn}} &= R / v_{\text{exp}}, \\
 p_{\text{shell}} &= M_{\text{shell}} v_{\text{exp}}, \\
 E_{\text{kin}} &= \tfrac{1}{2} M_{\text{shell}} v_{\text{exp}}^{2}, \\
 \dot p_{\text{obs}} &= \frac{M_{\text{shell}} v_{\text{exp}}^{2}}{R}.
\end{aligned}
\]
Compare against driving mechanisms `dot p_wind = dot M v_inf` and `dot p_rad = L_star ⟨Q⟩ / c`. Typically `dot p_obs > dot p_wind + dot p_rad`, consistent with `gamma_seg < 1` inside the nebula.

---

## 3. Cosmological Extension

- **Effective metric**:
  \[
  g_{\mu\nu}^{\text{cosmo}} = \Gamma_{\text{seg}}^{2}(x,t)\, g_{\mu\nu}^{\text{FLRW}},
  \]
  where `Gamma_seg` is a coarse-grained mean of local `gamma_seg` fields.
- **Analogy**: nested nebular segments → cosmic web nodes; momentum excess → apparent late-time acceleration; cold inner pockets → low `gamma_seg` regions (dark sectors).

---

## 4. Implementation Hooks (Windsurf)

1. **Define `gamma_seg(r, t)`** via density or potential, e.g. `gamma_seg = 1 / (1 + alpha * rho^beta)`.
2. **Metric scaling**: modify solver metric `g <- gamma_seg^2 * g` when GR module active.
3. **Energy update**: internal energy `u <- u * gamma_seg^{-1}` per hydro step.
4. **Velocity adjustment**: `v <- v * gamma_seg^{-1/2}` for apparent expansion in reduced models.
5. **Frequency shift**: `nu_obs = nu_emit * gamma_seg` for radiative transfer outputs.

### 4.1 Hydro Loop Sketch

```python
for cell in grid:
    rho = state.rho[cell]
    pot = state.phi[cell]
    gamma_seg = gamma_from_density(rho)  # 0 < gamma <= 1

    if config.metric_scaling:
        metric[cell] *= gamma_seg ** 2
    if config.energy_scaling:
        state.energy[cell] *= gamma_seg ** -1
    if config.velocity_scaling:
        state.velocity[cell] *= gamma_seg ** -0.5

    if config.radiation.shift_frequency:
        state.nu_obs[cell] = state.nu_emit[cell] * gamma_seg
```

### 4.2 Example YAML (`configs/autofetch.yaml` template)

```yaml
simulation:
  name: G79_segmented
  dt: 1.0e3 yr
  steps: 5000
  grid:
    nx: 512
    ny: 512
    nz: 1
    box_pc: 8.0

physics:
  eos: ideal
  cooling: tabulated_ISM
  gravity: poisson

segmented_spacetime:
  enabled: true
  mode: density
  gamma:
    alpha: 0.8
    beta: 0.6
    floor: 0.05
  scaling:
    metric: true
    velocity: true
    energy: true
  radiation:
    shift_frequency: true
    synth_maps:
      bands: ["24um", "70um", "CO32_mom0", "NH3_11_mom0", "radio_21cm"]

outputs:
  cadence: 50
  fields: [rho, v, u, Phi, gamma_seg]
  products:
    - type: profile
      var: [gamma_seg, T, v]
      center: [0, 0]
    - type: map
      var: ["radio_21cm", "CO32_mom0"]
      projection: faceon
```

---

## 5. Validation Checklist

- **WCS alignment**: all FITS products registered on a common beam/footprint.
- **Kinematics**: moment-1 gradient ≲ few km s⁻¹ pc⁻¹; line widths dominated by non-thermal component.
- **Emission overlap**: radio free–free contours intersect molecular moment-0 maps inside the IR shell.
- **Energetics**: `dot p_obs / dot p_wind ≳ 1` and stable under error budget.
- **Single gamma profile** reproduces temperature, velocity, and radio morphologies simultaneously.

---

## 6. Testing & Automation

- **Install requirements**:
  ```powershell
  pip install -r requirements.txt
  ```

- **End-to-end smoke fetch & tests**:
  ```powershell
  python scripts/autofetch.py 2025-10-17_gaia_ssz_real
  ```
  Logs under `data/logs/autofetch_*.log`, manifest at `experiments/2025-10-17_gaia_ssz_real/autofetch_manifest.json`.

- **Standalone pytest run**:
  ```powershell
  python -m pytest scripts/tests -q --disable-warnings
  ```

  Includes cosmology kernel tests (`test_ssz_kernel.py`), segmenter checks (`test_segmenter.py`), cosmological field assembly (`test_cosmo_fields.py`), multibody field validation (`test_cosmo_multibody.py`), and Gaia/SDSS smoke fetchers.

- **Optional pipeline**: provide `run_gaia_ssz_pipeline.py` with `run_ssz_cosmo()` or set `run_pipeline = False` in `AutoFetchConfig` to silence warnings.

---

## 7. Quick Reference

- **Slow time ⇒ cold/dense ⇒ radio/mm emission.**
- **Fast time ⇒ hot/diffuse ⇒ optical/IR emission.**
- **Momentum & energy scale as `gamma_seg^{-1}`, velocity as `gamma_seg^{-1/2}`.**
- **Mass emerges from curvature**: `Phi(seg) → g → T`, not `T → g`.

---

## 8. References

- Jiménez-Esteban et al. (2010), *ApJ*, 713, 429.  
- Rizzo et al. (2014), *A&A*, 563, A7.  
- AKARI diffuse maps (2015, JAXA release).  
- Casu & Wrede (2025), *Segmented Spacetime and the Origin of Molecular Zones in Expanding Nebulae*.  
- Internal SSZ Notes v1.0–v4.1.
