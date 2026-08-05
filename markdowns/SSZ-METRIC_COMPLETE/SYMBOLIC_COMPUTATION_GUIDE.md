# SSZ Symbolic Computation Guide

Complete guide for symbolic tensor computation using SymPy.

© 2025 Carmen N. Wrede & Lino Casu

---

## 📦 Available Scripts

### 1. **`ssz_symbolic_pack.py`** - Complete Tensor Pack

**Computes:**
- Metric tensor $g_{\mu\nu}$ (4x4)
- Inverse metric $g^{\mu\nu}$ (4x4)
- Christoffel symbols $\Gamma^\rho_{\mu\nu}$ (all non-zero)
- **Full Riemann tensor** $R^\rho_{\phantom{\rho}\sigma\mu\nu}$ (256 components)
- Ricci tensor $R_{\mu\nu}$ (4x4)
- Ricci scalar $R$
- Einstein tensor $G^\mu_{\phantom{\mu}\nu}$ (4x4, mixed indices)
- **Kretschmann scalar** $K = R_{\mu\nu\rho\sigma} R^{\mu\nu\rho\sigma}$

**Use for:**
- Complete tensor derivation
- Paper appendix material
- Full validation of all curvature invariants

**Runtime:** ⚠️ **10-30 minutes** (Riemann + Kretschmann are compute-intensive)

**Usage:**
```bash
python src/ssz_metric_pure/ssz_symbolic_pack.py > output_full.txt
```

---

### 2. **`ssz_symbolic_fast.py`** - Fast Computation Mode ⚡

**Computes:**
- Metric tensor $g_{\mu\nu}$ (4x4)
- Inverse metric $g^{\mu\nu}$ (4x4)
- Christoffel symbols $\Gamma^\rho_{\mu\nu}$ (all non-zero)
- Ricci tensor $R_{\mu\nu}$ (4x4) - **direct method, no full Riemann**
- Ricci scalar $R$
- Einstein tensor $G^\mu_{\phantom{\mu}\nu}$ (4x4, mixed indices)

**Additional Tests:**
- ✅ Metric compatibility: $\nabla_\alpha g_{\mu\nu} = 0$
- ✅ Killing vector test: $\partial_T g_{\mu\nu} = 0$ (stationarity)

**Skips:**
- ❌ Full Riemann tensor (not needed for Einstein equations)
- ❌ Kretschmann scalar (too slow, use weak-field approximation)

**Use for:**
- Quick validation
- Paper calculations (Einstein tensor, Ricci)
- Daily workflow

**Runtime:** ✅ **1-3 minutes**

**Usage:**
```bash
python src/ssz_metric_pure/ssz_symbolic_fast.py > output_fast.txt
```

---

### 3. **`symbolic_tensor_derivation.py`** - Object-Oriented Interface

**Features:**
- User-friendly class-based API
- Calibrated $\phi_G = \sqrt{2GM/(rc^2)}$ or symbolic $\phi(r)$
- LaTeX export to file
- Display methods with pretty-printing

**Use for:**
- Interactive Jupyter notebooks
- Custom computations
- Educational purposes

**Usage:**
```python
from ssz_metric_pure.symbolic_tensor_derivation import SSZSymbolicTensors

ssz = SSZSymbolicTensors(use_calibrated=True)
results = ssz.compute_all()
ssz.display_results(results)
ssz.export_all_latex(results, "output.tex")
```

---

## 🎯 Which Script to Use?

| Task | Recommended Script | Runtime |
|------|-------------------|---------|
| Quick Einstein tensor check | `ssz_symbolic_fast.py` | 1-3 min |
| Paper calculations (G, R) | `ssz_symbolic_fast.py` | 1-3 min |
| Complete tensor derivation | `ssz_symbolic_pack.py` | 10-30 min |
| Kretschmann scalar | `ssz_symbolic_pack.py` | 10-30 min |
| Interactive work | `symbolic_tensor_derivation.py` | Variable |
| Metric compatibility tests | `ssz_symbolic_fast.py` | 1-3 min |

---

## 📐 Notation

### Coordinates
$(x^\mu) = (T, r, \theta, \varphi)$

Indices: $\mu, \nu, \rho, \sigma \in \{0, 1, 2, 3\}$

### SSZ Functions
- $\phi(r) = \phi_G(r)$: Spiral angle
- $\gamma(r) = \cosh(\phi)$: Hyperbolic factor
- $\beta(r) = \tanh(\phi)$: Velocity-like factor

### Calibration
**Weak-field matched:**
$$\phi_G(r) = \sqrt{\frac{2GM}{rc^2}} = \sqrt{\frac{r_g}{r}}$$

where $r_g = 2GM/c^2$ is the Schwarzschild radius.

---

## 📊 Output Format

All scripts output LaTeX-ready strings that can be directly copied into papers.

### Example Output (Ricci Scalar)

```latex
--- Scalar R ---
\frac{2}{\cosh^{2}{\left(\phi{\left(r \right)} \right)}} 
\left(
  \frac{d^{2}}{d r^{2}} \phi{\left(r \right)} \tanh{\left(\phi{\left(r \right)} \right)} 
  + \frac{\left(\frac{d}{d r} \phi{\left(r \right)}\right)^{2}}{\cosh^{2}{\left(\phi{\left(r \right)} \right)}}
  - 2 \left(\frac{d}{d r} \phi{\left(r \right)}\right)^{2} \tanh^{2}{\left(\phi{\left(r \right)} \right)} 
  + \frac{2 \frac{d}{d r} \phi{\left(r \right)} \tanh{\left(\phi{\left(r \right)} \right)}}{r}
\right)
```

Copy-paste this directly into your LaTeX document.

---

## ⚙️ Performance Tips

### For Faster Computation:

1. **Use `ssz_symbolic_fast.py` whenever possible**
   - Skips expensive Riemann tensor computation
   - Direct Ricci calculation is much faster

2. **Limit simplification:**
   ```python
   # In scripts, comment out excessive simplify() calls
   # expr = sp.simplify(expr)  # <- can be slow
   ```

3. **Cache results:**
   ```bash
   # Save output to file for reuse
   python ssz_symbolic_fast.py > cached_results.txt
   ```

4. **Use calibrated mode:**
   - Calibrated $\phi_G$ simplifies faster than general $\phi(r)$

---

## 🧪 Validation Tests

### Metric Compatibility: $\nabla_\alpha g_{\mu\nu} = 0$

Verifies that the Christoffel symbols correctly satisfy the metric compatibility condition:

$$\nabla_\alpha g_{\mu\nu} = \partial_\alpha g_{\mu\nu} - \Gamma^\beta_{\alpha\mu} g_{\beta\nu} - \Gamma^\beta_{\alpha\nu} g_{\mu\beta} = 0$$

**Run with:** `ssz_symbolic_fast.py`

### Killing Vector: $\partial_T g_{\mu\nu} = 0$

Verifies stationarity (time-translation invariance):

$$\partial_T g_{\mu\nu} = 0 \quad \forall \mu, \nu$$

This implies conserved energy:
$$E = -g_{TT} \frac{dT}{d\lambda} = \text{const}$$

**Run with:** `ssz_symbolic_fast.py`

---

## 📁 File Organization

```
src/ssz_metric_pure/
├── ssz_symbolic_pack.py           # Complete (slow)
├── ssz_symbolic_fast.py           # Fast mode
└── symbolic_tensor_derivation.py  # OOP interface
```

---

## 🔧 Troubleshooting

### "Computation takes too long"
- ✅ Use `ssz_symbolic_fast.py` instead
- ✅ Reduce `simplify()` calls
- ✅ Use calibrated mode

### "Out of memory"
- ✅ Close other applications
- ✅ Use fast mode (skips 256-component Riemann)
- ✅ Run on a machine with more RAM

### "Need Kretschmann scalar"
- ⚠️ Must use `ssz_symbolic_pack.py` (slow)
- ✅ Or use weak-field approximation: $K = 48G^2M^2/(c^4r^6)$

---

## 📚 References

1. Wrede, C. & Casu, L. (2025). *SSZ φ-Spiral Metric: Complete Tensor Formulation*.
2. SymPy Documentation: https://docs.sympy.org/
3. Related files:
   - `APPENDIX_A_PROOF_PACK.tex` - Complete analytical proofs
   - `SSZ_EINSTEIN_RICCI_CURVATURE.tex` - LaTeX documentation

---

## 🎓 For Students & Reviewers

**Understanding the output:**

1. **General $\phi(r)$ formulas:**
   - Show structure of SSZ modifications
   - Ready for any spiral profile $\phi(r)$

2. **Calibrated $\phi_G = \sqrt{r_g/r}$:**
   - Matches GR in weak field
   - Numerical evaluation possible

3. **LaTeX strings:**
   - Copy directly into papers
   - No manual typesetting needed

**Verification:**
- Compare symbolic output with numerical code
- Check weak-field limit against GR
- Verify all tensor identities

---

## ✅ Quick Start

**For paper calculations (recommended):**
```bash
python src/ssz_metric_pure/ssz_symbolic_fast.py > ricci_einstein.txt
```

**For complete derivation:**
```bash
python src/ssz_metric_pure/ssz_symbolic_pack.py > full_tensors.txt
# (go get coffee, this takes 10-30 min)
```

**For interactive work:**
```python
from ssz_metric_pure.symbolic_tensor_derivation import SSZSymbolicTensors
ssz = SSZSymbolicTensors(use_calibrated=True)
results = ssz.compute_all()
```

---

**© 2025 Carmen N. Wrede & Lino Casu**  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*

**"Symbolic Tensors. LaTeX-Ready. φ-Driven."** 📐✨
