# Metric Comparison: Kerr-SSZ vs. φ-Spiral

Direct side-by-side comparison of the two main SSZ metric implementations.

---

## 🚀 Quick Start

```bash
python compare_metrics.py
```

**Output:** Complete comparison across 9 categories with numerical results.

---

## 📊 What Gets Compared

### 1. **Conceptual Framework**
- Philosophy and approach
- Coordinate systems
- Rotation mechanisms

### 2. **Line Elements**
- Mathematical forms
- Key differences in structure

### 3. **Tensor Structure**
- 4×4 metric tensor layout
- Off-diagonal terms (g_tφ vs. g_tr)

### 4. **Numerical Comparison**
- Metric components at same mass
- Direct numerical differences

### 5. **Singularity Behavior**
- Behavior at r=0
- Behavior at r_s
- Horizon structure

### 6. **Feature Comparison**
- Side-by-side feature list
- Strengths/weaknesses

### 7. **Use Cases**
- When to use Kerr-SSZ
- When to use φ-Spiral

### 8. **Mathematical Complexity**
- Code complexity
- θ-dependence
- Auxiliary functions

### 9. **Summary Table**
- Complete overview
- Key differences/similarities

---

## 🎯 Key Findings

### **Main Differences:**

| Aspect | Kerr-SSZ | φ-Spiral |
|--------|----------|----------|
| **Off-Diagonal** | g_tφ (frame drag) | g_tr (spiral) |
| **Horizons** | Yes (r_±) | No (layers) |
| **Rotation** | Physical spin â | Geometric φ_G |
| **Use Case** | Astrophysical | Theoretical |

### **Main Similarities:**

- ✅ Both singularity-free (SSZ)
- ✅ Both have off-diagonal terms
- ✅ Both asymptotically flat
- ✅ Both satisfy energy conditions

---

## 📈 Sample Output

```
================================================================================
4. NUMERICAL COMPARISON (Solar Mass)
================================================================================

Mass: 1.989e+30 kg (solar)
Schwarzschild radius: 2.953e+03 m
φ-Spiral k: 1.0
Kerr spin â: 0.5

────────────────────────────────────────────────────────────────────────────────
METRIC COMPONENTS AT EQUATOR (θ = π/2)
────────────────────────────────────────────────────────────────────────────────
r/r_s      Kerr g_tt/c²         Spiral g_tt/c²       Δ%             
────────────────────────────────────────────────────────────────────────────────
1.5        -0.186957            -0.444444            137.781
2.0        -0.333333            -0.600000            80.000
3.0        -0.526316            -0.758314            44.065
5.0        -0.720000            -0.880797            22.333
10.0       -0.857143            -0.949254            10.745

────────────────────────────────────────────────────────────────────────────────
OFF-DIAGONAL TERMS
────────────────────────────────────────────────────────────────────────────────
r/r_s      Kerr g_tφ/c          Spiral g_tr/c        Type                
────────────────────────────────────────────────────────────────────────────────
1.5        -0.029849            0.538516             Different!
2.0        -0.033333            0.600000             Different!
3.0        -0.037305            0.680827             Different!
5.0        -0.039984            0.759836             Different!
10.0       -0.041649            0.840528             Different!

Note: g_tφ (Kerr) vs. g_tr (Spiral) are DIFFERENT physical effects!
  Kerr:   Frame dragging (rotation of spacetime)
  Spiral: Spiral structure (time-radius coupling)
```

---

## 🔬 Scientific Interpretation

### **Kerr-SSZ Metric:**
- **Physics:** Frame dragging from physical rotation
- **Observable:** Can match spinning black hole observations
- **Structure:** Boyer-Lindquist coordinates, familiar to GR
- **Applications:** M87*, Sgr A*, astrophysical jets

### **φ-Spiral Metric:**
- **Physics:** Geometric rotation angle φ_G(r)
- **Observable:** Predicts subspace layer effects
- **Structure:** Novel spiral embedding
- **Applications:** ANITA anomalies, phase tunneling

---

## 💡 When to Use Each

### Use **Kerr-SSZ** for:
✅ Rotating black holes with observational data  
✅ Frame-dragging calculations  
✅ ISCO, photon orbits for spinning BHs  
✅ Comparison with standard Kerr solutions  
✅ Ergosphere physics  

### Use **φ-Spiral** for:
✅ Singularity-free interior studies  
✅ Subspace layer investigations  
✅ ANITA-type anomaly explanations  
✅ Pure geometric rotation effects  
✅ Alternative to event horizons  

### Use **BOTH** for:
✅ Maximum theoretical completeness  
✅ Cross-validation of SSZ framework  
✅ Understanding different rotation mechanisms  

---

## 🎓 Educational Value

This comparison demonstrates:

1. **Multiple Valid Approaches:** SSZ allows different formulations
2. **Different Physics:** Off-diagonal terms encode different effects
3. **Complementary Strengths:** Each metric excels in different areas
4. **Unified Framework:** Both share core SSZ principles

---

## 🔗 Related Files

- **Pipeline:** `ssz_metric_pipeline.py` (choose metric interactively)
- **Kerr-SSZ:** `src/ssz_metric_pure/metric_kerr_ssz_kerr_by_ki.py`
- **φ-Spiral:** `src/ssz_metric_pure/metric_phi_spiral_ssz_by_human.py`
- **φ-Spiral Demo:** `examples/demo_phi_spiral.py`

---

## 📚 Further Reading

- **φ-Spiral Guide:** `examples/README_PHI_SPIRAL.md`
- **Implementation:** `PHI_SPIRAL_IMPLEMENTATION_COMPLETE.md`
- **Pipeline Guide:** `PIPELINE_README.md`

---

## 🎯 Conclusion

> **Both metrics are valid SSZ implementations with different strengths.**
> 
> **Kerr-SSZ** → Astrophysical applications, familiar structure  
> **φ-Spiral** → Theoretical exploration, novel concepts
> 
> **Choose based on your research question!**

---

© 2025 Carmen N. Wrede & Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Compare. Understand. Choose.** 🔄🌀
