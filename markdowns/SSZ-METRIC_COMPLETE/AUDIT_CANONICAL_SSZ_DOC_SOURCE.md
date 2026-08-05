# Audit: Canonical SSZ Documentation Alignment & Refactoring Matrix

This audit evaluates each source file in the repository to align the implementation strictly with the canonical specifications in `ssz-complete-documentation`.

The central objective is to enforce the **Axiomatic Segmentation Chain** where the Segment Density $\Xi(r)$ is the absolute physical primary field, and all scaling factors, rapidity factors, and metric components emerge directly from it.

## 🔗 File Audit & Action Matrix

| Path | Current Role | Pure SSZ Core? | Uses Canonical $\Xi(r)$? | Contains Kerr/Schwarzschild/GR Scaffold? | Target Action | Justification |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- |
| `src/ssz_metric_pure/__init__.py` | Package initialization and module exports. | **Yes** | **Yes** (As derived) | **No** (Fully clean) | **Refactor** | Register and export new axiomatic segmentation-based functions and APIs. |
| `src/ssz_metric_pure/constants.py` | Physical constants and parameters. | **Yes** | **No** (Holds constants only) | **No** | **Keep** | Standard SI constants and Golden Ratio $\varphi$. |
| `src/ssz_metric_pure/core.py` | Mathematical potentials and splines. | **Yes** | **No** (Used $\gamma$-first approach previously) | **No** | **Refactor** | Make $\Xi(r)$ the primary field. Implement `compactness_x`, `xi_weak`, `xi_strong`, `xi_blend`, `xi_canonical`, and derive $D, s, \gamma, \beta$ directly from $\Xi$. |
| `src/ssz_metric_pure/metric.py` | Metric components and diagonal forms. | **Yes** | **No** (Used $\gamma$-first approach previously) | **No** | **Refactor** | Construct the metric tensor directly from $D(\Xi) = 1/(1+\Xi)$ and $s(\Xi) = 1+\Xi$. |
| `src/ssz_metric_pure/tensor.py` | Numeric and symbolic curvature engines. | **Yes** | **No** (General geometry engine) | **No** | **Refactor** | Unify under `ssz_metric_pure` namespace with no-freeze comments. |
| `src/ssz_metric_pure/observables.py` | Observables mapper (Redshift, Lensing, Shapiro). | **Yes** | **No** | **No** | **Refactor** | Implement strict Postulate 5 routing: `classify_observable` and `method_for_observable` for `NULL_LIGHT`, `TIMELIKE_STATIC`, and `TIMELIKE_ORBIT`. |
| `src/ssz_metric_pure/validation.py` | Algebraic coupling validation. | **Yes** | **No** | **No** | **Refactor** | Verify axiomatic $D(\Xi) \cdot s(\Xi) = 1$ identity. |

## 🛡️ Forbidden Scaffold Detection

A rigorous regex search was performed on the `src/ssz_metric_pure/` core files to guarantee that no GR, Schwarzschild, or Kerr Boyer-Lindquist strings, variables, or functions exist in the core implementation code. All references are fully isolated in `legacy/` or `comparison/`.
