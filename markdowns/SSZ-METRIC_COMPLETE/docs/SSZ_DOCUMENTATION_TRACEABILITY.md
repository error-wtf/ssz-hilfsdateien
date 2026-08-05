# SSZ Documentation Traceability Matrix

**Version:** `v1.1.0-canonical-pure`  
**Single Source of Truth:** `ssz-complete-documentation`  

---

This document traces the implementation files of the **Canonical Pure SSZ Metric** repository back to their authoritative mathematical and physical postulates.

## 🗺️ Postulate Traceability Map

| Postulate | Theoretical Definition | Implementation File | Verification Test Suite |
| :--- | :--- | :--- | :--- |
| **Postulate 1: Primitive Field** | Spacetime geometry is generated causally by a primary physical segment density scalar field $\Xi(r)$. | `@/home/error/Downloads/ssz-metric-complete/src/ssz_metric_pure/core.py` | `tests/test_canonical_xi_primary.py` |
| **Postulate 2: Reciprocal Coupling** | Dilation $D(\Xi) = 1/(1+\Xi)$ and radial stretching $s(\Xi) = 1+\Xi$ satisfy $D \cdot s = 1$. | `@/home/error/Downloads/ssz-metric-complete/src/ssz_metric_pure/core.py` | `tests/test_segmentation_concept.py` |
| **Postulate 3: Metric Generation** | Spherically symmetric static spacetime metric is given by $g_{\mu\nu} = \operatorname{diag}(-D^2 c^2, s^2, r^2, r^2\sin^2\theta)$. | `@/home/error/Downloads/ssz-metric-complete/src/ssz_metric_pure/metric.py` | `tests/test_metric_from_xi.py` |
| **Postulate 4: Local $c$ Invariance** | Local light travel speed in orthonormal frames is invariant and equal to $c$. | `@/home/error/Downloads/ssz-metric-complete/src/ssz_metric_pure/segmentation.py` | `tests/test_segmentation_concept.py` |
| **Postulate 5: Prime Directive** | Null/light observables must be PPN-completed, while clocks map directly. | `@/home/error/Downloads/ssz-metric-complete/src/ssz_metric_pure/observables.py` | `tests/test_observable_prime_directive.py` |

---

## 🏗️ Architectural Component Directory

### 1. Core Potentials & Splines (`core.py`)
- **Regime Transition Boundaries:** $1.8 r_s$ and $2.2 r_s$.
- **Transition Spline:** C² quintic Hermite spline solver matching exactly the first and second derivatives of the strong and weak branches.

### 2. Operational Segmentation (`segmentation.py`)
- **Segment Distance:** $\rho(r_1, r_2) = \int_{r_1}^{r_2} (1 + \Xi(r)) dr$ implemented via trapezoidal integration.
- **Local speed check:** Orthonormal velocity field solver verifying $d\hat{r}/d\hat{t} = c$.

### 3. Curvature Tensor Pipeline (`tensor.py`)
- **Numerical Derivative Engine:** Avoids variable freezing by dynamically evaluating perturbed metrics on $x \pm h$.
- **Geometric Connections:** Automatically computes Riemann, Ricci, and Einstein curvature tensors directly from the metric function.

### 4. Prime Directive Mapper (`observables.py`)
- **Observables Classifier:** Enforces the PPN routing of light-like trajectories to safeguard against the absence of the spatial metric component, while routing static clock measurements directly.
