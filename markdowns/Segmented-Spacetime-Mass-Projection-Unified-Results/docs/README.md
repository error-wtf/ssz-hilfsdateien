# SSZ Documentation – Theory & Code Foundations

**Complete guide to understanding and implementing Segmented Spacetime**

© Carmen Wrede & Lino Casu, 2025

---

## 🎓 Theory & Code Documentation ⭐ NEW

**Complete understanding from physics to implementation:**

### 📖 Main Index
**[THEORY_AND_CODE_INDEX.md](THEORY_AND_CODE_INDEX.md)** - Start here for complete overview

### 📚 Documentation Parts

1. **[PHYSICS_FOUNDATIONS.md](PHYSICS_FOUNDATIONS.md)** (12 KB)
   - Physical concepts explained intuitively
   - No heavy mathematics
   - Perfect for students and physicists
   - Topics: Segmented Spacetime, φ, dual velocities, black holes

2. **[MATHEMATICAL_FORMULAS.md](MATHEMATICAL_FORMULAS.md)** (2.5 KB+)
   - All formulas with derivations
   - Complete mathematical formulation
   - For theorists and mathematicians
   - Topics: r_φ, Δ(M), PPN, metrics, redshifts

3. **[CODE_IMPLEMENTATION_GUIDE.md](CODE_IMPLEMENTATION_GUIDE.md)** (WIP)
   - Core algorithms explained
   - Code snippets with documentation
   - For developers
   - Topics: Newton solver, Decimal precision, tests

4. **[EXAMPLES_AND_APPLICATIONS.md](EXAMPLES_AND_APPLICATIONS.md)** (WIP)
   - Practical use cases
   - Step-by-step examples
   - For researchers
   - Topics: Sun, Sgr A*, GAIA data, multi-ring analysis

---

## 🧭 Quick Navigation

**For Students:**
```
1. PHYSICS_FOUNDATIONS.md (concepts)
2. MATHEMATICAL_FORMULAS.md (math)
3. theory/ papers (advanced)
```

**For Developers:**
```
1. CODE_IMPLEMENTATION_GUIDE.md (algorithms)
2. EXAMPLES_AND_APPLICATIONS.md (examples)
3. ../tests/ (test framework)
```

**For Researchers:**
```
1. THEORY_AND_CODE_INDEX.md (overview)
2. theory/ (21 papers)
3. ../papers/validation/ (11 papers)
```

---

## 📁 Directory Structure

```
docs/
├── THEORY_AND_CODE_INDEX.md      # Main index ⭐
├── PHYSICS_FOUNDATIONS.md         # Physical concepts ⭐
├── MATHEMATICAL_FORMULAS.md       # All formulas ⭐
├── CODE_IMPLEMENTATION_GUIDE.md   # Code guide (WIP)
├── EXAMPLES_AND_APPLICATIONS.md   # Examples (WIP)
├── theory/                        # 21 theory papers
│   └── README.md
├── segwave_guide.md               # SegWave guide
├── SSZ_COSMOS_PLAN.md             # Cosmos pipeline
└── README.md                      # This file
```

---

## 🔬 Cosmology Pipeline (Legacy)

This directory also contains the Segmented Spacetime (SSZ) cosmology pipeline that ingests Gaia data, constructs SSZ fields, embeds solar system segments, and generates interactive visualizations.

### Pipeline Summary

1. Fetch Gaia data using `scripts/gaia/fetch_gaia_adql.py` or cone search helper `scripts/gaia/fetch_gaia_conesearch.py`.
2. Preprocess outputs with `scripts/preprocess/gaia_clean_map.py` and `scripts/preprocess/gaia_frame_transform.py`.
3. Build cosmology field via `scripts/SSZ/build_ssz_model.py` and solar embedding via `scripts/SSZ/build_solar_system_model.py`.
4. Visualize with `scripts/viz/plot_ssz_maps.py` (cosmology) and `scripts/viz/plot_solar_ssz.py` (solar segments).
5. Run everything end-to-end with `run_gaia_ssz_pipeline.py`.

Outputs and manifests are stored under `experiments/<RUN_ID>/`, `models/cosmology/<RUN_ID>/`, and `models/solar_system/<RUN_ID>/`.

---

## 📖 Related Documentation

- **[../DOCUMENTATION_INDEX.md](../DOCUMENTATION_INDEX.md)** - Complete repository documentation index
- **[../README.md](../README.md)** - Main repository README
- **[../INSTALL_README.md](../INSTALL_README.md)** - Installation guide

---

**Last Updated:** 2025-10-19  
**Status:** ✅ Complete theory & code foundations available
