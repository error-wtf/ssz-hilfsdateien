# 💫 Segmented Spacetime — Solar System Visualization

A 3D dynamic visualization of our Solar System embedded in a **Segmented Spacetime Mesh** based on the theoretical framework from Casu & Wrede 2024–25 papers.

## 🎯 Overview

This project creates an interactive 3D visualization where celestial bodies (Sun, planets, asteroids, comets, nearby stars) are embedded in a Segmented Spacetime mesh representing φ– and π–driven segment structures with gravitational curvature appearing as local mesh deformation.

## 📦 Data Sources

- **GAIA DR3/DR4**: Star positions, proper motions, parallaxes
- **VizieR**: Planetary data (orbital elements, masses)  
- **JPL Horizons**: Optional high-precision ephemerides

## 🧠 Physics Model

- Segment density field: `N(x) = Σ_i γ_i · φ^(-α·r_i)`
- Local time dilation: `τ(x) = φ^(-β·N(x))`
- Refractive index: `n(x) = 1 + κ·N(x)`
- Natural Boundary saturation: `N(x) ≤ N_max`

## 🚀 Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Run basic demo
python -m src.app --epoch 2025-01-01 --mesh-subdiv 6 --range-au 120

# Generate interactive visualization
python -m src.app --show-orbits --show-spiral-clocks
```

## 📁 Structure

```
segmented-solar/
├─ data/               # Raw and processed astronomical data
├─ src/                # Core modules
├─ notebooks/          # Jupyter analysis notebooks  
├─ assets/             # Colormaps and resources
└─ solar_system_segmented.html  # Output visualization
```

## 🎨 Features

- Interactive 3D mesh with segment density visualization
- Real astronomical data integration
- φ-spiral "Normaluhr" clocks around planets
- Adjustable physics parameters via UI sliders
- WebGL export for web deployment

## 📚 References

- Casu & Wrede (2024–2025): *Segmented Spacetime Series*
- GAIA DR3 Technical Documentation
- VizieR Catalogue Service
