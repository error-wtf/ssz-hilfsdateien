# SSZ Metric Pipeline - Unified Entry Point

Interactive pipeline to choose and run different SSZ metric implementations.

---

## 🚀 Quick Start

### Interactive Mode (Recommended)
```bash
python ssz_metric_pipeline.py
```

The pipeline will ask you:
1. **Which metric?** (φ-Spiral / Kerr-SSZ / Static)
2. **Mass?** (Solar mass or custom)
3. **Parameters?** (k, spin, etc.)

### Command-Line Mode

#### φ-Spiral Metric
```bash
# Default solar mass, k=1.0
python ssz_metric_pipeline.py --metric phi-spiral

# Custom parameters
python ssz_metric_pipeline.py --metric phi-spiral --mass 1e30 --k 1.5
```

#### Kerr-SSZ Metric
```bash
# Default solar mass, spin=0.5
python ssz_metric_pipeline.py --metric kerr

# Fast spinning black hole
python ssz_metric_pipeline.py --metric kerr --mass 2e30 --spin 0.9
```

#### Static SSZ Metric
```bash
# Default solar mass
python ssz_metric_pipeline.py --metric static

# Custom mass
python ssz_metric_pipeline.py --metric static --mass 5e30
```

---

## 📊 Available Metrics

### 1. φ-Spiral Metric (**NEW!** 🌀)
**Philosophy:** Pure rotation-based, gravitational field = rotation angle φ_G(r)

**Features:**
- ✅ NO singularities (space folds into subspace layers)
- ✅ Subspace transitions at Δφ_G = 2π
- ✅ Cross term g_tr ≠ 0 (spiral structure!)
- ✅ Time dilation: dτ/dt = sech(φ_G)
- ✅ ANITA anomalies explained

**Output:**
- Metric at different radii (φ_G, β, dτ/dt, redshift, layer)
- Subspace layer transitions
- Schwarzschild comparison

**Best for:**
- Singularity-free black hole interiors
- Phase tunneling phenomena
- Subspace layer research

---

### 2. Kerr-SSZ Metric (🔄 Rotating)
**Philosophy:** SSZ + Rotation (frame dragging)

**Features:**
- ✅ Rotating black holes
- ✅ Frame dragging (g_tφ ≠ 0)
- ✅ Ergosphere
- ✅ Inner/outer horizons
- ✅ ISCO, photon sphere

**Output:**
- Horizons (r_+, r_-)
- Ergosphere radii at different angles
- Frame-dragging frequency ω
- Redshift at equator

**Best for:**
- Spinning black holes
- Frame-dragging effects
- Astrophysical applications

---

### 3. Static SSZ Metric (⚫ Classic)
**Philosophy:** Non-rotating, pure SSZ

**Features:**
- ✅ Singularity-free (A(0) = 1)
- ✅ Natural boundary r_φ ≈ 0.809 r_s
- ✅ φ-series validated
- ✅ Smooth GR transition

**Output:**
- Metric coefficients (A, B)
- Segment density N(r)
- Schwarzschild comparison

**Best for:**
- Classic SSZ validation
- Non-rotating systems
- Educational purposes

---

## 📋 Command-Line Arguments

### Common Arguments
```
--metric {phi-spiral,kerr,static}
    Choose metric implementation
    
--mass FLOAT
    Mass in kg (default: 1.989e30 = solar mass)
```

### φ-Spiral Specific
```
--k FLOAT
    Spiral strength parameter (default: 1.0)
    Higher k → stronger spiral, more layers
```

### Kerr-SSZ Specific
```
--spin FLOAT
    Dimensionless spin parameter â ∈ [0,1] (default: 0.5)
    â=0: Schwarzschild (non-rotating)
    â=1: Extremal (maximum rotation)
```

---

## 💡 Example Sessions

### Example 1: Interactive Mode
```bash
$ python ssz_metric_pipeline.py

████████████████████████████████████████████████████████████████████████████████
█                                                                              █
█              SSZ METRIC PIPELINE - UNIFIED ENTRY POINT                       █
█                                                                              █
████████████████████████████████████████████████████████████████████████████████

Available Metric Implementations:
  1. φ-Spiral Metric     (Pure rotation-based, subspace layers)
  2. Kerr-SSZ Metric     (Rotating black holes, frame dragging)
  3. Static SSZ Metric   (Non-rotating, classic SSZ)
================================================================================

Please choose a metric implementation:

  [1] φ-Spiral Metric (φ_G-based rotation)
  [2] Kerr-SSZ Metric (Rotating black hole)
  [3] Static SSZ Metric (Non-rotating)

Enter choice [1-3]: 1

✓ Selected: phi-spiral

================================================================================
PARAMETER CONFIGURATION
================================================================================

Mass configuration:
  [1] Solar mass (1.989e30 kg)
  [2] Custom mass
Choose mass [1-2] (default=1): 1
✓ Using solar mass: 1.989e+30 kg

Spiral strength k (default=1.0): 1.5
✓ k = 1.50
================================================================================

🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀
φ-SPIRAL METRIC PIPELINE
🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀🌀

Metric: PhiSpiralSSZMetric(M=1.989e+30 kg, k=1.500, r_s=2.953e+03 m)
...
```

### Example 2: Quick Command-Line
```bash
# Compare different spiral strengths
python ssz_metric_pipeline.py --metric phi-spiral --k 0.5
python ssz_metric_pipeline.py --metric phi-spiral --k 1.0
python ssz_metric_pipeline.py --metric phi-spiral --k 2.0

# Test extremal Kerr
python ssz_metric_pipeline.py --metric kerr --spin 0.999

# Massive black hole
python ssz_metric_pipeline.py --metric static --mass 1e36
```

---

## 📁 File Structure

```
E:\clone\ssz-metric-pure\
├── ssz_metric_pipeline.py              # Main pipeline script ⭐
├── src/ssz_metric_pure/
│   ├── __init__.py                     # Updated with all exports
│   ├── metric_phi_spiral_ssz_by_human.py   # φ-Spiral (NEW!)
│   ├── metric_kerr_ssz_kerr_by_ki.py       # Kerr (Backup)
│   └── metric_static.py                    # Static SSZ
└── examples/
    ├── demo_phi_spiral.py              # φ-Spiral demo
    └── basic_usage.py                  # Static demo
```

---

## 🔧 Installation

```bash
cd E:\clone\ssz-metric-pure
pip install -e .
```

---

## 📊 Output Format

### Console Output
- **Banner:** Metric choice and parameters
- **Tables:** Formatted data (radii, metric components, etc.)
- **Comparisons:** SSZ vs. Schwarzschild/GR
- **Summary:** Key results and next steps

### Data Shown

#### φ-Spiral
- φ_G, β, γ (rotation fields)
- Time dilation, redshift
- Subspace layer number
- Layer transitions (2π boundaries)

#### Kerr-SSZ
- Horizons (r_+, r_-)
- Ergosphere radii
- Frame-dragging frequency ω
- Metric components (g_tt, g_tφ)

#### Static SSZ
- Metric coefficients (A, B)
- Segment density N(r)
- Natural boundary r_φ
- GR comparison

---

## 🎯 Tips & Tricks

### Best Practices

1. **Start Interactive:** Get familiar with options
2. **Save Output:** Redirect to file for analysis
   ```bash
   python ssz_metric_pipeline.py --metric phi-spiral > results.txt
   ```

3. **Parameter Sweep:** Test different values systematically
   ```bash
   for k in 0.5 1.0 1.5 2.0; do
       python ssz_metric_pipeline.py --metric phi-spiral --k $k
   done
   ```

4. **Compare Metrics:** Run all three for same mass
   ```bash
   python ssz_metric_pipeline.py --metric phi-spiral --mass 1e30
   python ssz_metric_pipeline.py --metric kerr --mass 1e30
   python ssz_metric_pipeline.py --metric static --mass 1e30
   ```

### Common Workflows

#### Research Workflow
1. Choose metric type based on physics
2. Run with default parameters (solar mass)
3. Adjust parameters to match observations
4. Generate detailed visualizations (use demo scripts)
5. Export data for further analysis

#### Educational Workflow
1. Start with Static SSZ (simplest)
2. Understand singularity-free property
3. Move to φ-Spiral (subspace layers)
4. Finally Kerr-SSZ (rotating)
5. Compare all three side-by-side

---

## 🐛 Troubleshooting

### Import Errors
**Problem:** `ModuleNotFoundError: No module named 'ssz_metric_pure'`

**Solution:**
```bash
cd E:\clone\ssz-metric-pure
pip install -e .
```

### Wrong Metric Module
**Problem:** `ImportError: cannot import name 'PhiSpiralSSZMetric'`

**Solution:** Ensure `__init__.py` has been updated (should already be done)

### Invalid Parameters
**Problem:** Spin > 1 or negative mass

**Solution:** Check parameter ranges:
- Mass: > 0 kg
- Spin (Kerr): 0 ≤ â ≤ 1
- k (φ-Spiral): > 0 (typically 0.1 - 10)

---

## 📚 Further Resources

### Documentation
- **φ-Spiral:** `examples/README_PHI_SPIRAL.md`
- **Complete Impl:** `PHI_SPIRAL_IMPLEMENTATION_COMPLETE.md`
- **Static SSZ:** `QUICKSTART.md`
- **Kerr-SSZ:** Docstrings in `metric_kerr_ssz_kerr_by_ki.py`

### Demo Scripts
- **φ-Spiral:** `examples/demo_phi_spiral.py` (full demo with plots)
- **Static SSZ:** `examples/basic_usage.py`

### Advanced Usage
```python
# Import directly in Python
from ssz_metric_pure import PhiSpiralSSZMetric, KerrSSZMetric, StaticSSZMetric

# Create metrics
phi_metric = PhiSpiralSSZMetric(mass=1e30, k=1.5)
kerr_metric = KerrSSZMetric(KerrSSZParams(mass=1e30, spin=0.9))
static_metric = StaticSSZMetric(SSZParams(mass=1e30))

# Use them...
```

---

## 🎉 Next Steps

After running the pipeline:

1. **Visualizations:** Run demo scripts for plots
   ```bash
   cd examples
   python demo_phi_spiral.py
   ```

2. **Analysis:** Export data and analyze in Jupyter/Pandas

3. **Research:** Use metrics in your own calculations

4. **Contribute:** Suggest improvements or extensions

---

## 📧 Contact

**Questions? Issues? Feature Requests?**

- GitHub Issues: Report bugs
- Email: Contact authors for scientific inquiries
- Collaboration: Research partnerships welcome

---

## ⚖️ License

**ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

Free for:
- ✅ Scientific research
- ✅ Educational purposes
- ✅ Non-commercial use

Prohibited:
- ❌ Capitalist exploitation

---

© 2025 Carmen N. Wrede & Lino Casu

**Choose Your Metric. Explore Spacetime. No Singularities.** 🌀⚫🔄
