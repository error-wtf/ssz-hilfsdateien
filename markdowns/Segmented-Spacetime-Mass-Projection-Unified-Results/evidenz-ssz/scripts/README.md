# SSZ Scripts Collection

**Complete toolkit for Segmented Spacetime Mass Projection analysis, visualization, and animation.**

© 2025 Carmen Wrede, Lino Casu – Forschungsteam ZS-α  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## 📂 Directory Structure

```
scripts/
├── Core Analysis (v6 - Latest)
├── Animation & Visualization
├── Cosmology Simulations
├── Testing & Validation
└── Utility Scripts
```

Total Scripts: **36 Python files**

---

## 🔬 Core Analysis Scripts (v6 - Latest Version)

### **ssz_proof_sweep_v6.py** (27 KB)
Latest proof validation sweep across parameter space.

**Usage:**
```bash
python ssz_proof_sweep_v6.py --mass 1.989e30 --radius 1e6
```

**Features:**
- Parameter space exploration
- Statistical validation
- CSV output with results
- PDF report generation

---

### **ssz_proof_check_v6.py** (11 KB)
Quick validation check for SSZ theory predictions.

**Usage:**
```bash
python ssz_proof_check_v6.py --object sun
```

**Validates:**
- Mass reconstruction accuracy
- PPN parameters (β, γ)
- Photon sphere predictions
- Energy conditions

---

### **ssz_viz_v6.py** (11 KB)
Visualization toolkit for v6 results.

**Usage:**
```bash
python ssz_viz_v6.py --input results.csv --output plots/
```

**Generates:**
- Mass-radius diagrams
- Segment density plots
- Residual analysis
- Comparison with GR

---

### **ssz_gr_bridge.py** (8 KB)
Bridge between SSZ and General Relativity predictions.

**Features:**
- GR limit validation
- Weak-field approximations
- Strong-field comparisons
- PPN framework integration

---

### **ssz_parameter_scan.py** (11 KB)
Systematic parameter space scanning.

**Parameters scanned:**
- α (segment coupling)
- φ (golden ratio variants)
- Mass ranges
- Radius ranges

---

## 🎬 Animation & Visualization Scripts

### **ssz_bigbang_vs_ssz_anim.py** (35 KB) ⭐ MAIN ANIMATION
Dual-panel animation: Classical Big Bang vs Segmented Spacetime.

**Usage:**
```bash
python ssz_bigbang_vs_ssz_anim.py --duration 60 --fps 30 --output intro.gif
```

**Features:**
- Dual-panel visualization
- Classical ΛCDM expansion (left)
- SSZ segmented structure (right)
- φ-spiral overlays
- Hexagonal segment grid
- Customizable duration/fps

**Output:**
- GIF animation (default)
- MP4 with audio (if ffmpeg available)
- Multi-language support (DE/EN/IT)

---

### **ssz_animation_master.py** (19 KB)
Master animation controller for all SSZ visualizations.

**Modes:**
- `scientific` - Technical presentation
- `perfect` - High-quality render
- `demo` - Quick preview
- `bigbang` - Cosmology comparison

**Usage:**
```bash
python ssz_animation_master.py --mode scientific --language de
```

---

### **ssz_animation_scientific.py** (10 KB)
Scientific presentation animations with detailed overlays.

**Features:**
- Equation overlays
- Physical interpretations
- Multi-language text
- High-resolution output

---

### **ssz_animation_perfect.py** (10 KB)
Highest quality rendering for publications.

**Settings:**
- 4K resolution
- 60 fps
- Anti-aliasing
- Color-corrected

---

### **ssz_animator.py** (25 KB)
Core animation engine used by all animation scripts.

**Classes:**
- `SegmentAnimator` - Main animation class
- `PhiSpiral` - Golden ratio spirals
- `HexGrid` - Hexagonal segment grid
- `TimelineController` - Frame management

---

### **create_all_language_versions.py** (10 KB)
Batch-generates animations in DE, EN, IT.

**Usage:**
```bash
python create_all_language_versions.py --base intro --output multilang/
```

**Generates:**
- `intro_de.gif` (Deutsch)
- `intro_en.gif` (English)
- `intro_it.gif` (Italiano)

---

## 🌌 Cosmology Scripts

### **ssz_cosmo_animator.py** (16 KB)
Cosmological structure formation animations.

**Simulates:**
- Large-scale structure
- Segment network evolution
- Dark matter distribution
- φ-driven clustering

---

### **ssz_cosmo_core.py** (6 KB)
Core cosmology calculations for SSZ framework.

**Functions:**
- `compute_hubble(z)` - Hubble parameter
- `segment_density(a)` - Segment evolution
- `growth_factor(z)` - Structure growth
- `phi_coupling(z)` - φ-based interactions

---

### **ssz_cosmo_data.py** (5 KB)
Cosmological data handling and preprocessing.

**Data sources:**
- Planck CMB
- GAIA stellar catalog
- LIGO gravitational waves
- Solar System ephemeris

---

### **ssz_cosmo_models.py** (2 KB)
Cosmological model definitions.

**Models:**
- Standard ΛCDM (comparison)
- SSZ segmented cosmology
- Hybrid SSZ-CDM
- φ-driven inflation

---

## 🛠️ Utility Scripts

### **make_ssz_anim.py** (7 KB)
Quick animation generator for SSZ visualizations.

**Usage:**
```bash
python make_ssz_anim.py --object blackhole --duration 10
```

---

### **train.py** (20 KB)
Machine learning training for SSZ parameter optimization.

**Features:**
- Neural network training
- Parameter estimation
- Cross-validation
- Model export

---

### **test_pipeline_quick.py** (4 KB)
Quick pipeline test for all major functions.

**Tests:**
- Import checks
- Basic calculations
- File I/O
- Output validation

---

### **text_safety_check.py** (3 KB)
Validates text outputs for special characters and encoding.

**Checks:**
- UTF-8 encoding
- Special characters (φ, α, β, γ)
- Math symbols
- Multi-language support

---

## 📊 Testing Scripts

Located in `scripts/tests/` subdirectory (if present).

See main repository documentation for full test suite details.

---

## 🎯 Quick Start Guide

### 1. Basic Analysis
```bash
# Run v6 proof check for the Sun
python ssz_proof_check_v6.py --object sun

# Full parameter sweep
python ssz_proof_sweep_v6.py --output results/
```

### 2. Create Animation
```bash
# Quick demo (10 seconds)
python ssz_bigbang_vs_ssz_anim.py --duration 10 --fps 15

# High-quality multilingual
python create_all_language_versions.py
```

### 3. Cosmology Simulation
```bash
# Cosmological animation
python ssz_cosmo_animator.py --duration 30 --output cosmo.gif
```

---

## 📦 Dependencies

### Core Requirements
```
numpy >= 1.20
scipy >= 1.7
matplotlib >= 3.5
pandas >= 1.3
```

### Animation Requirements
```
pillow >= 9.0        # GIF export
imageio >= 2.15      # Video I/O
ffmpeg               # MP4 export (optional)
```

### Visualization Requirements
```
plotly >= 5.0        # Interactive plots
seaborn >= 0.11      # Statistical plots
```

### Machine Learning (optional)
```
torch >= 1.10        # For train.py
scikit-learn >= 1.0  # Parameter optimization
```

---

## 🔧 Installation

```bash
# Core dependencies
pip install numpy scipy matplotlib pandas

# Animation support
pip install pillow imageio

# Optional: Full visualization stack
pip install plotly seaborn torch scikit-learn
```

---

## 📚 Documentation

- **Main README:** `../README.md`
- **Animation Guide:** `../docs/SSZ_ANIMATION_README.md`
- **Visualization Guide:** `../docs/SSZ_VISUALIZATIONS_README.md`
- **Results Documentation:** `../results/README.md`

---

## 🆕 Version History

### v6 (2025-10-26) - Current
- Complete rewrite of proof validation
- Improved parameter scanning
- New cosmology modules
- Multi-language animation support

### v5 (2025-10-26)
- Enhanced visualization toolkit
- Better GR comparison
- PDF report generation

### Earlier versions
See git history for detailed changelog.

---

## 📖 Usage Examples

### Example 1: Complete Analysis Pipeline
```bash
# 1. Run proof validation
python ssz_proof_check_v6.py --object sun > results/sun_validation.txt

# 2. Parameter sweep
python ssz_proof_sweep_v6.py --mass 1.989e30 --output results/sun_sweep.csv

# 3. Generate visualizations
python ssz_viz_v6.py --input results/sun_sweep.csv --output plots/

# 4. Create animation
python ssz_bigbang_vs_ssz_anim.py --duration 30 --output animations/sun_demo.gif
```

### Example 2: Multi-Language Animation
```bash
# Generate all language versions
python create_all_language_versions.py \
    --base intro \
    --duration 60 \
    --fps 30 \
    --output multilang/
```

### Example 3: Cosmology Simulation
```bash
# Run cosmological structure formation
python ssz_cosmo_animator.py \
    --duration 60 \
    --fps 30 \
    --redshift-range 0 1000 \
    --output cosmo_evolution.gif
```

---

## 🤝 Contributing

When adding new scripts:
1. Add UTF-8 encoding declaration
2. Include docstring with usage
3. Add entry to this README
4. Update version number in header
5. Add test coverage

---

## 📬 Contact

**Forschungsteam ZS-α**  
Carmen Wrede, Lino Casu

---

## 📄 License

All scripts are licensed under the **ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

See main repository LICENSE file for details.

---

**Last Updated:** 2025-10-27  
**Total Scripts:** 36  
**Latest Version:** v6
