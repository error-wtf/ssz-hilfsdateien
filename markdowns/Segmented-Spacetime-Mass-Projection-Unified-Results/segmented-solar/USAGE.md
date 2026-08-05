# 🌌 Segmented Spacetime Solar System - Usage Guide

## Quick Start

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Run Simple Demo
```bash
python demo_simple.py
```
This creates `segmented_spacetime_demo.html` - open it in your browser!

### 3. Run Full Application
```bash
python -m src.app --epoch 2025-01-01 --mesh-subdiv 5 --range-au 100
```

## Command Line Options

### Basic Usage
```bash
python -m src.app [OPTIONS]
```

### Key Parameters

**Data & Epoch:**
- `--epoch 2025-01-01` - Target epoch for planetary positions
- `--include-asteroids` - Include major asteroids (Ceres, Vesta, etc.)
- `--include-moons` - Include major moons (Moon, Io, Europa, etc.)
- `--include-gaia` - Include GAIA stars for external field

**Mesh Configuration:**
- `--mesh-subdiv 6` - Icosphere subdivision level (3-8)
- `--range-au 120` - Mesh radius in AU

**Physics Parameters:**
- `--alpha 1.0` - Time dilation coupling: τ(x) = φ^(-α·N(x))
- `--kappa 0.015` - Refractive index coupling: n(x) = 1 + κ·N(x)
- `--p 2.0` - Power-law index for segment density kernel
- `--N-max 5.0` - Maximum segment density (Natural Boundary)

**Visualization:**
- `--show-orbits` - Display orbital trajectories
- `--show-spiral-clocks` - Show φ-spiral temporal clocks
- `--save-images` - Export PNG images of field visualizations
- `--interactive` - Launch interactive Dash dashboard

### Example Commands

**Basic Solar System:**
```bash
python -m src.app --epoch 2025-01-01 --mesh-subdiv 5
```

**Full System with Orbits:**
```bash
python -m src.app --include-asteroids --include-moons --show-orbits --save-images
```

**Interactive Dashboard:**
```bash
python -m src.app --interactive --mesh-subdiv 4
```

**High-Resolution Mesh:**
```bash
python -m src.app --mesh-subdiv 7 --range-au 200 --include-gaia
```

## Output Files

### Generated Files:
- `solar_system_segmented.html` - Interactive 3D visualization
- `data/processed/mesh_vertices.csv` - Mesh vertex coordinates
- `data/processed/mesh_faces.csv` - Mesh triangular faces
- `data/processed/field_data.csv` - N(x), τ(x), n(x) values at vertices
- `data/processed/body_catalog.csv` - Celestial body properties
- `segmented_spacetime_*.png` - Field visualization images (if --save-images)

### Data Cache:
- `data/raw/gaia_stars_*.csv` - Cached GAIA stellar data
- `data/raw/planetary_data.csv` - Cached planetary orbital elements
- `data/raw/asteroid_data_*.csv` - Cached asteroid data

## Physics Model

### Segmented Spacetime Framework

**Segment Density Field:**
```
N(x) = N_bg + Σ_i γ_i · K_i(||x - x_i||)
```

**Kernel Function:**
```
K_i(r) = (M_i / (r + r0)^p) · σ((r_nb - r)/δ)
```
where σ is the logistic function for Natural Boundary saturation.

**Time Dilation:**
```
τ(x) = φ^(-α · N(x))
```
where φ = (1+√5)/2 is the Golden Ratio.

**Refractive Index:**
```
n(x) = 1 + κ · N(x)
```

### Parameter Guidelines

**α (Time Coupling):**
- 0.5-1.0: Weak time dilation effects
- 1.0-2.0: Moderate effects (recommended)
- 2.0+: Strong effects near massive bodies

**κ (Refractive Coupling):**
- 0.001-0.01: Subtle lensing effects
- 0.01-0.05: Moderate lensing (recommended)
- 0.05+: Strong gravitational lensing

**Mesh Subdivision:**
- 3-4: Fast preview (~1K-5K vertices)
- 5-6: Standard quality (~5K-20K vertices)
- 7-8: High resolution (~20K-80K vertices)

## Interactive Features

### 3D Visualization Controls:
- **Rotate:** Click and drag
- **Zoom:** Mouse wheel or pinch
- **Pan:** Shift + click and drag
- **Field Selection:** Dropdown to switch between N(x), τ(x), n(x)

### Dashboard Sliders:
- **α slider:** Adjust time dilation coupling in real-time
- **κ slider:** Modify refractive index coupling
- **Field selector:** Switch between segment density, time dilation, and refractive index

## Jupyter Notebook

Run the interactive demo notebook:
```bash
jupyter notebook notebooks/demo.ipynb
```

The notebook includes:
- Step-by-step field calculation
- Field distribution analysis
- Radial profile plots
- φ-spiral demonstration around Jupiter

## Troubleshooting

### Common Issues:

**Import Errors:**
```bash
pip install --upgrade numpy scipy pandas astropy astroquery plotly numba
```

**GAIA Query Timeout:**
- Use `--gaia-maxdist-pc 20` for smaller queries
- Skip GAIA with basic Solar System only

**Memory Issues:**
- Reduce `--mesh-subdiv` to 4 or 5
- Decrease `--range-au` to 50-100

**Visualization Not Loading:**
- Check that `segmented_spacetime_demo.html` was created
- Try opening in different browser (Chrome/Firefox recommended)
- Ensure JavaScript is enabled

### Performance Tips:

**Fast Preview:**
```bash
python demo_simple.py  # ~5 seconds
```

**Production Quality:**
```bash
python -m src.app --mesh-subdiv 6 --show-orbits  # ~30 seconds
```

**High Resolution:**
```bash
python -m src.app --mesh-subdiv 7 --include-gaia --save-images  # ~2-5 minutes
```

## Scientific Applications

### Research Use Cases:
1. **Gravitational Field Visualization** - Study curvature around massive bodies
2. **Time Dilation Mapping** - Visualize relativistic effects in Solar System
3. **Light Propagation** - Analyze refractive index variations
4. **φ-Spiral Analysis** - Investigate Golden Ratio temporal structures
5. **Natural Boundary Studies** - Examine singularity resolution mechanisms

### Educational Applications:
1. **General Relativity (GR) (GR) Visualization** - Interactive spacetime curvature
2. **Solar System Dynamics** - Orbital mechanics with relativistic effects
3. **Mathematical Physics** - Golden Ratio φ in physical systems
4. **Computational Astrophysics** - Mesh-based field calculations

## Citation

If you use this software in research, please cite:
```
Segmented Spacetime Solar System Visualization
Based on Casu & Wrede (2024-2025) Segmented Spacetime Framework
https://github.com/segmented-spacetime/solar-visualization
```

## Support

For issues and questions:
- Check the troubleshooting section above
- Review the Jupyter notebook examples
- Examine the demo scripts for usage patterns
