# Changelog - SSZ Evidence Package

All notable changes to the Segmented Spacetime Mass Projection project are documented here.

**Format:** Based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)  
**Versioning:** SSZ follows custom versioning (v1-v6) based on theoretical iterations

---

## [v6] - 2025-10-26

### 🎉 Major Release - Complete Rewrite

#### Added
- **ssz_proof_sweep_v6.py** - Complete parameter space validation (27 KB)
- **ssz_proof_check_v6.py** - Quick validation toolkit (11 KB)
- **ssz_viz_v6.py** - Enhanced visualization suite (11 KB)
- **ssz_gr_bridge.py** - GR comparison framework (8 KB)
- **ssz_parameter_scan.py** - Systematic parameter exploration (11 KB)

#### Animation System - NEW!
- **ssz_bigbang_vs_ssz_anim.py** - Main dual-panel animation (35 KB)
- **ssz_animation_master.py** - Animation controller (19 KB)
- **ssz_animation_scientific.py** - Scientific presentation mode (10 KB)
- **ssz_animation_perfect.py** - High-quality rendering (10 KB)
- **ssz_animator.py** - Core animation engine (25 KB)
- **create_all_language_versions.py** - Multi-language batch generator (10 KB)

#### Cosmology Modules - NEW!
- **ssz_cosmo_animator.py** - Cosmological animations (16 KB)
- **ssz_cosmo_core.py** - Core cosmology calculations (6 KB)
- **ssz_cosmo_data.py** - Data handling (5 KB)
- **ssz_cosmo_models.py** - Model definitions (2 KB)

#### Multimedia
- **ssz_intro_de.gif** - German introduction animation (6.95 MB)
- **ssz_intro_en.gif** - English introduction animation (6.95 MB)
- **ssz_intro_it.gif** - Italian introduction animation (6.95 MB)
- **ssz_intro_de.wav** - German audio track (48.5s, 2 MB)

#### Documentation
- **SSZ_BLACKHOLE_BOMB_RESULTS.md** - Black hole bomb analysis results
- **scripts/README.md** - Complete scripts documentation
- **CHANGELOG.md** - This file

#### Data
- **ssz_v6_report.pdf** - Complete v6 scientific report (255 KB)
- **summary.json** - Aggregated results
- **process_fast.csv** - Fast processing results
- **process_risky.csv** - Risky parameter results
- **process_risky_wide.csv** - Extended risky parameters

#### Utilities
- **text_safety_check.py** - UTF-8/encoding validation (3 KB)

###changed
- All v5 scripts superseded by v6 versions
- Improved parameter accuracy
- Better GR comparison metrics
- Enhanced visualization quality
- Multi-language support in animations

#### Fixed
- UTF-8 encoding issues on Windows
- Parameter boundary conditions
- Animation frame rate consistency
- Audio sync in video exports

---

## [v5] - 2025-10-26

### Enhanced Proof System

#### Added
- **ssz_proof_sweep_v5.py** - v5 parameter sweep (32 KB)
- **ssz_proof_check_v5.py** - v5 validation (10 KB)
- **ssz_v5_report.pdf** - v5 scientific report (240 KB)

#### Visualization
- Enhanced plotting capabilities
- PDF report generation
- Better error visualization

#### Changed
- Improved mass reconstruction algorithm
- Better segment density calculations
- Enhanced photon sphere predictions

---

## [v4] - 2025-10-26

### Proof Refinement

#### Added
- **ssz_proof_sweep_v4.py** - v4 parameter exploration (23 KB)
- **ssz_proof_check_v4.py** - v4 validation suite (10 KB)

#### Changed
- Refined PPN parameter calculations
- Improved energy condition checks
- Better statistical significance testing

---

## [v3] - 2025-10-26

### Initial Structured Approach

#### Added
- **ssz_proof_sweep_v3.py** - v3 systematic sweep (21 KB)
- **ssz_proof_check.py** - Basic validation (9 KB)

#### Features
- First systematic parameter space exploration
- Basic GR comparison
- CSV output format established

---

## [Earlier Versions] - Pre-v3

### Legacy Systems

Multiple experimental scripts exploring various approaches:
- `segmented_ligo_compare*.py` series (30+ files)
- `segmented_calculation.py`
- `segmented_final_proof.py`
- Various LIGO comparison scripts

These have been superseded by the v3-v6 structured approach.

---

## Integration History

### 2025-10-27 - GitHub Integration Wave 4-5
**Commits:** d075a3a, e3582d6

#### Added to Repository
- All v6 scripts
- Complete animation system
- Cosmology modules
- Multi-language GIFs (3 files, ~21 MB total)
- German audio track
- Documentation updates
- Git LFS configuration

#### Repository Stats
- Total Scripts: 36
- Total Animations: 12 GIFs + 2 MP4s
- Total Size: ~500 MB (via Git LFS)
- Commits Today: 5

---

### 2025-10-26 - GitHub Integration Wave 1-3
**Commits:** cdcd6ad, 7242404, e5f74ac

#### Added to Repository
- Initial multimedia assets
- 2 MP4 animations
- 4 PNG diagrams
- 2 WAV audio files
- Core scripts (make_ssz_anim.py, train.py)
- Documentation READMEs
- Inventory reports

---

## File Statistics

### Current Repository Contents (v6)

**Scripts:** 36 Python files  
**Animations:** 12 GIFs (~470 MB) + 2 MP4s (~0.5 MB)  
**Audio:** 3 WAV files (~4.5 MB)  
**Images:** 5 PNGs (~1.5 MB)  
**Reports:** 2 PDFs (~500 KB)  
**Data:** 8 CSVs + 3 JSONs  
**Documentation:** 14 Markdown files  

**Total Size:** ~500 MB (Git LFS enabled for large files)

---

## Breaking Changes

### v6 → v5
- API changes in proof validation functions
- New parameter names (alpha → α consistency)
- Output format changes (added physical interpretations)
- Report structure changed

### v5 → v4
- CSV column names standardized
- Removed deprecated `old_format` output option

---

## Deprecations

### Deprecated in v6
- All v1-v5 scripts (superseded by v6)
- Legacy `segmented_*.py` comparison scripts
- Old LIGO comparison tools (pre-structured approach)

### To Be Removed
- `ssz_plot_packager.py` (functionality merged into ssz_viz_v6.py)
- Legacy riemann test scripts (redundant)

---

## Migration Guide

### From v5 to v6

#### Scripts
```bash
# OLD (v5)
python ssz_proof_sweep_v5.py --mass 1e30

# NEW (v6)
python ssz_proof_sweep_v6.py --mass 1e30 --output results/
```

#### API Changes
```python
# OLD (v5)
from ssz_core import validate_mass
result = validate_mass(mass, radius)

# NEW (v6)
from ssz_proof_check_v6 import SSZValidator
validator = SSZValidator()
result = validator.validate_mass(mass, radius)
```

#### Output Format
v6 adds physical interpretations to all outputs:
- CSV files now include `physical_interpretation` column
- PDF reports have extended discussion sections
- Plots include theory comparison overlays

---

## Roadmap

### Planned for v7 (Future)
- [ ] Real-time interactive visualizations
- [ ] Web-based animation configurator
- [ ] Automated parameter optimization
- [ ] LIGO data pipeline integration
- [ ] Planck CMB analysis tools

### Planned for v6.1 (Next Minor Release)
- [ ] Audio generation for EN/IT animations
- [ ] MP4 video export with audio
- [ ] Extended cosmology simulations
- [ ] API documentation (Sphinx)
- [ ] Unit test coverage >90%

---

## Known Issues

### Current (v6)
- Large GIF files may exceed GitHub non-LFS limits (workaround: use LFS)
- Audio not yet available for EN/IT versions (only DE)
- ffmpeg required for MP4 export (optional dependency)
- Windows UTF-8 encoding requires manual setup in some cases

### In Progress
- Investigating animation rendering performance on low-end hardware
- Improving parameter scan speed (~30% optimization possible)

---

## Contributors

**Forschungsteam ZS-α**
- Carmen Wrede - Theory, Analysis, Documentation
- Lino Casu - Implementation, Validation, Visualization

---

## License

All versions are licensed under the **ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

---

## References

### Scientific Papers
- Casu & Wrede (2025) - Segmented Spacetime Mass Projection Framework
- See `papers/` directory for full bibliography

### External Dependencies
- NumPy, SciPy, Matplotlib (BSD licenses)
- Pandas (BSD license)
- Pillow, ImageIO (PIL/MIT licenses)
- FFmpeg (LGPL/GPL, optional)

---

**Last Updated:** 2025-10-27  
**Current Version:** v6  
**Repository:** https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
