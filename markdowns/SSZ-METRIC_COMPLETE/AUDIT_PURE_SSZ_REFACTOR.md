# Audit: Pure SSZ Refactoring & Scaffolding Separation

This audit evaluates each source file in the repository to isolate the canonical, pure SSZ-Core metric from General Relativity (GR), Schwarzschild, and Kerr Boyer-Lindquist scaffolds.

## File Audit & Separation Matrix

| File | Role | Contains Pure SSZ-Core Logic? | Contains Kerr/Schwarzschild/GR Dependency? | Target Action | Justification |
| :--- | :--- | :---: | :---: | :---: | :--- |
| `src/ssz_core/phi_spiral.py` | 2PN φ-spiral calibration and pure $\phi$-spiral metric. | **Yes** | **No** (Only uses $r_s$ as a physical scale scale) | **Refactor & Integrate** | This is the true mathematical foundation of SSZ: rotation-based gravity with $g_{tr} = c \tanh(\phi_G)$. Move to `src/ssz_metric_pure/core.py`. |
| `src/ssz_core/metric.py` | Static blended SSZ metric construction. | **Partial** | **Yes** (Contains standard GR Schwarzschild $A_{GR} = 1 - \frac{r_s}{r}$ and blending structures) | **Refactor / Move Comparison** | Keep only pure SSZ in core. Move GR/Schwarzschild equations used for validation to `comparison/gr_reference.py`. |
| `src/ssz_core/metric_kerr.py` | Rotating metric with frame-dragging, $\Sigma$, $\Delta$, $r_\pm$. | **No** (It is a standard Kerr metric dressed with SSZ factor) | **Yes** (Direct Boyer-Lindquist architecture, Kerr horizons, etc.) | **Move to Legacy/Comparison** | This is a "Kerr metric with SSZ-dressing" rather than a native SSZ derivation. Move to `legacy/metric_kerr_legacy.py`. |
| `src/ssz_core/segment_density.py` | Segment density $\Xi(r)$ definitions. | **Yes** | **No** | **Refactor & Unify** | Ensure exactly one canonical, consistent definition of $\Xi(r)$ is used (with $\Xi = \gamma - 1$). Move to `src/ssz_metric_pure/core.py`. |
| `src/ssz_core/blend_zone.py` | Hermite $C^2$ continuity blend zones. | **Yes** | **No** | **Refactor & Move** | Move to `src/ssz_metric_pure/core.py` or keep as auxiliary inside package. |
| `src/ssz_core/observables.py` | Physical observables mapper (Redshift, Lensing, Shapiro). | **Yes** | **No** (Uses standard PPN framework) | **Refactor & Move** | Move to `src/ssz_metric_pure/observables.py`. Enforce strict separation (no hidden Kerr/GR imports). |
| `src/ssz_core/curvature.py` | Numerical and symbolic curvature and connection calculator. | **Yes** | **No** (It is a general mathematical geometry engine) | **Refactor & Move** | Move to `src/ssz_metric_pure/tensor.py` and ensure the numerical differentiator truly evaluates at $x$ instead of a frozen state. |
| `src/ssz_core/__init__.py` | Package initialization and module exports. | **Yes** | **Yes** (Exports Kerr-like components) | **Refactor** | Rebuild under the canonical package `src/ssz_metric_pure/__init__.py` with no Kerr/GR core exports. |

## Actions and Refactoring Protocol

1. **Repackage to `ssz_metric_pure`**: Unify all package namespaces under `ssz_metric_pure`.
2. **Strict Kerr & GR Isolation**:
   - `metric_kerr.py` goes to `legacy/metric_kerr_legacy.py` and is **never** imported by the core package.
   - All $A_{GR}$ / Schwarzschild reference formulas are extracted from `metric.py` and moved to `comparison/gr_reference.py`.
3. **Core API Unification**:
   - Deliver clear, consistent mathematical symbols: $\Xi(r) = \gamma(r) - 1$, $\gamma(r) = \cosh(\phi_G(r))$, $D(r)s(r) = 1$.
   - All tests must run against the unified `ssz_metric_pure` package.
