# 🚀 SSZ-METRIC-PURE - 50-Phasen Master-Fahrplan

**Projekt:** Pure Segmented Spacetime Metric Library  
**Ziel:** Vereinigung von ssz-full-metric + ssz-metric-final → 100% Pure SSZ  
**Datum:** 2025-10-31  
**Status:** GESTARTET

---

## 📋 PHASEN-ÜBERSICHT

### Phase 1-10: Foundation & Safety
- [x] Phase 1: Git init & Verzeichnis-Struktur
- [ ] Phase 2: Safety checks & Provenance setup
- [ ] Phase 3: LICENSE & CITATION.cff
- [ ] Phase 4: .gitignore & pyproject.toml
- [ ] Phase 5: Basic README.md
- [ ] Phase 6: Agent output directories
- [ ] Phase 7: Manifests für beide Donor-Repos erstellen
- [ ] Phase 8: Provenance Log initialisieren
- [ ] Phase 9: Conflicts.md & Gaps.md anlegen
- [ ] Phase 10: First commit (infrastructure)

### Phase 11-20: Core Parameter System
- [ ] Phase 11: params.py - Physical constants (G, c, ℏ, φ)
- [ ] Phase 12: params.py - Mass parameters (M, r_s, r_φ)
- [ ] Phase 13: params.py - Δ(M) correction (φ-based!)
- [ ] Phase 14: params.py - Dimensionless mode
- [ ] Phase 15: params.py - Spin parameter â validation
- [ ] Phase 16: params.py - Tolerance settings
- [ ] Phase 17: params.py - Unit tests
- [ ] Phase 18: __init__.py - Package exports
- [ ] Phase 19: params.py - Documentation strings
- [ ] Phase 20: Second commit (params complete)

### Phase 21-30: Segmentation & Static Metric
- [ ] Phase 21: segmentation.py - N(r) baseline model
- [ ] Phase 22: segmentation.py - φ-structure interfaces
- [ ] Phase 23: segmentation.py - Monotonic checks
- [ ] Phase 24: metric_static.py - g_tt (non-rotating)
- [ ] Phase 25: metric_static.py - g_rr (non-rotating)
- [ ] Phase 26: metric_static.py - g_θθ, g_φφ
- [ ] Phase 27: metric_static.py - Boundary conditions
- [ ] Phase 28: tests/test_metric_symmetry.py
- [ ] Phase 29: tests/test_units_dimensions.py
- [ ] Phase 30: Third commit (static metric)

### Phase 31-40: SSZ-Kerr Rotating Metric
- [ ] Phase 31: metric_kerr_ssz.py - Coordinate system
- [ ] Phase 32: metric_kerr_ssz.py - g_tφ (frame dragging)
- [ ] Phase 33: metric_kerr_ssz.py - g_φφ corrected
- [ ] Phase 34: metric_kerr_ssz.py - Δ_SSZ(r,θ) analog
- [ ] Phase 35: metric_kerr_ssz.py - Σ_SSZ(r,θ) analog
- [ ] Phase 36: metric_kerr_ssz.py - Horizon solver
- [ ] Phase 37: metric_kerr_ssz.py - Ergosphere solver (g_tt=0)
- [ ] Phase 38: tests/test_ergosphere_horizons.py
- [ ] Phase 39: examples/compute_surfaces.py
- [ ] Phase 40: Fourth commit (Kerr metric)

### Phase 41-50: Tensors, Geodesics & Validation
- [ ] Phase 41: tensors.py - SymPy Christoffel Γ
- [ ] Phase 42: tensors.py - Riemann tensor
- [ ] Phase 43: tensors.py - Ricci tensor & scalar R
- [ ] Phase 44: tensors.py - Einstein tensor G_μν
- [ ] Phase 45: tensors.py - Numeric evaluators
- [ ] Phase 46: geodesics.py - Null geodesics
- [ ] Phase 47: geodesics.py - Timelike geodesics
- [ ] Phase 48: geodesics.py - Redshift utilities
- [ ] Phase 49: limits.py - GR-Kerr limit checks (validation only!)
- [ ] Phase 50: tests/test_limits_gr_kerr.py

---

## 🎯 ACCEPTANCE CRITERIA (Must Pass!)

1. ✅ Metric symmetry: g_μν = g_νμ
2. ✅ Signature: (-, +, +, +)
3. ✅ Ergosphere exists for â > 0
4. ✅ Horizons: Δ_SSZ = 0 has roots
5. ✅ GR-Kerr limit: a→0 recovers Schwarzschild
6. ✅ Minkowski limit: M→0 recovers flat space
7. ✅ Units consistent in geometric & dimensionless
8. ✅ No source repos modified (read-only!)
9. ✅ Provenance complete
10. ✅ All tests pass

---

## 📦 DONOR-QUELLEN (READ-ONLY)

**Donor 1:** `E:\clone\ssz-full-metric\`
- Purpose: API shapes, math utilities, test patterns
- Extract: numerical_stability.py, test infrastructure

**Donor 2:** `E:\ssz-full-metric-perfected\`
- Purpose: Pure SSZ implementations, φ-interfaces
- Extract: segmentation logic, TOV integration, ScalarActionTheory

**Donor 3:** `E:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results\`
- Purpose: Test infrastructure, validation patterns
- Extract: Test structure, UTF-8 handling, cross-platform patterns

---

## 🚀 NÄCHSTE SCHRITTE

**JETZT:** Phase 2 - Safety checks & Provenance setup

**Zeitplan:**
- Phasen 1-10: ~30 min (Infrastructure)
- Phasen 11-20: ~60 min (Parameters)
- Phasen 21-30: ~90 min (Static metric)
- Phasen 31-40: ~120 min (Kerr metric)
- Phasen 41-50: ~90 min (Tensors & validation)

**Total:** ~6 hours pure coding time

---

© 2025 Carmen N. Wrede & Lino Casu  
Licensed under the MIT License (ANTI-CAPITALIST compatible)
