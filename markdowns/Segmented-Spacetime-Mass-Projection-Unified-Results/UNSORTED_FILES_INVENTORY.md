# 📦 UNSORTED Files - Vollständiges Inventar

**Datum:** 2025-10-27  
**Status:** 🔍 INVENTORY - Needs Review & Integration

---

## 🎯 Überblick

Systematische Erfassung ALLER noch nicht integrierten Dateien in:
- `G:\UNSORTED\` und Subfolders
- `D:\mnt\data\`
- `D:\` (Root - neue Scripts)

---

## 📊 G:\UNSORTED\ - Struktur

### Bereits integriert ✅
```
G:\UNSORTED\
├── *.gif (10 files)          → evidenz-ssz/animations/ ✅
├── *.md (3 files)            → evidenz-ssz/results/ ✅
├── ssz_blackhole_bomb*.py    → evidenz-ssz/results/scripts/ ✅
├── ssz_bomb_animation.py     → evidenz-ssz/results/scripts/ ✅
├── data/*_v6.* (15 files)    → evidenz-ssz/results/data/ ✅
└── extended_results/plots/ (4 PNG) → evidenz-ssz/results/plots/ ✅
```

### Noch NICHT integriert ⚠️

#### 1. G:\UNSORTED\data\
**Inhalt:** Viele v4/v5 Plots + non-v6 files

```
data/
├── boundary_lambdaA_vs_Omega0_uniform.png       (34 KB)
├── boundary_lambdaA_vs_Omega0_uniform_v5.png    (34 KB)
├── boundary_lambdaA_vs_Omega0_weighted.png      (35 KB)
├── boundary_lambdaA_vs_Omega0_weighted_v5.png   (35 KB)
├── disagreement_map_uniform.png                 (51 KB)
├── disagreement_map_uniform_v5.png              (45 KB)
├── disagreement_map_weighted.png                (52 KB)
├── disagreement_map_weighted_v5.png             (46 KB)
├── heatmap_stability_uniform.png                (50 KB)
├── heatmap_stability_uniform_v5.png             (45 KB)
├── heatmap_stability_weighted.png               (50 KB)
├── heatmap_stability_weighted_v5.png            (45 KB)
├── lambdaA_diff_map_uniform_v5.png              (29 KB)
├── lambdaA_diff_map_weighted_v5.png             (30 KB)
├── proof_check_log_v6.csv                       (445 B) ✅ KEEP
├── proof_check_result_v6.json                   (808 B) ✅ KEEP
├── proof_sweep_results_v6.csv                   (77 KB) ✅ KEEP
├── proof_sweep_summary_v6.json                  (683 B) ✅ KEEP
└── stability_boundaries_v6.csv                  (4.7 KB) ✅ KEEP
```

**Empfehlung:** 
- ❌ v4/v5 Plots NICHT integrieren (veraltet, nur v6 relevant)
- ✅ Nur v6 CSV/JSON behalten (bereits integriert)

---

#### 2. G:\UNSORTED\extended_results\proof_reports\
**Inhalt:** Alte v4 Proof Reports

```
proof_reports/
├── boundary_lambdaA_vs_K.png                    (?)
├── boundary_lambdaA_vs_Omega0_uniform_v4.png    (?)
├── boundary_lambdaA_vs_Omega0_weighted_v4.png   (?)
├── disagreement_map_uniform_v4.png              (?)
├── disagreement_map_weighted_v4.png             (?)
├── heatmap_stability.png                        (?)
├── heatmap_stability_uniform_v4.png             (?)
└── heatmap_stability_weighted_v4.png            (?)
```

**Empfehlung:** 
- ❌ v4 Plots NICHT integrieren (veraltet)

---

#### 3. G:\UNSORTED\offline_assets\
**Inhalt:** Unbekannt (needs inspection)

**TODO:** Check contents

---

#### 4. G:\UNSORTED\mnt\data\
**Inhalt:** Duplikate von G:\UNSORTED\data\ + D:\mnt\data\

**Empfehlung:** 
- ❌ IGNORE (Duplikate)

---

## 📊 D:\mnt\data\ - Vollständiges Inventar

### Bereits integriert ✅
```
D:\mnt\data\
├── *_v6.png (10 files)                          → evidenz-ssz/results/data/ ✅
├── *_v6.csv (3 files)                           → evidenz-ssz/results/data/ ✅
├── *_v6.json (2 files)                          → evidenz-ssz/results/data/ ✅
└── SSZ_PROOF_SUMMARY_v6.md                      → evidenz-ssz/results/ ✅
```

### NICHT integriert - ABER WICHTIG! ⭐

#### 1. PDFs (Scientific Reports)
```
├── ssz_v5_report.pdf                            (252 KB) ⚠️
└── ssz_v6_report.pdf                            (255 KB) ⭐ CRITICAL!
```

**Empfehlung:** 
- ✅ **ssz_v6_report.pdf MUST INTEGRATE!**
- ❌ v5_report.pdf (veraltet, nur v6 relevant)

**Ziel:** `evidenz-ssz/results/ssz_v6_report.pdf`

---

#### 2. Videos & Audio ⭐ NEW CONTENT!
```
├── ssz_cosmo_anim.gif                           (2.2 MB) ⚠️
├── ssz_cosmo_anim.mp4                           (0.13 MB) ⭐
├── ssz_proof_anim_v6.gif                        (6.3 MB) ⚠️
├── ssz_proof_anim_v6.mp4                        (0.33 MB) ⭐
└── ssz_proof_anim_v6.wav                        (1.1 MB) 🔊
```

**Empfehlung:** 
- ✅ **MP4s integrieren** (kleine Größe, besser als GIF)
- ✅ **WAV behalten** (Audio für TTS)
- ⚠️ GIFs optional (schon viele GIFs in animations/)

**Ziel:** 
- `evidenz-ssz/animations/ssz_cosmo_anim.mp4` (Cosmology animation)
- `evidenz-ssz/animations/ssz_proof_anim_v6.mp4` (v6 Proof animation)
- `evidenz-ssz/animations/audio/ssz_proof_anim_v6.wav`

---

#### 3. Alte Versionen (v3/v4/v5)
```
├── proof_sweep_results_v3.csv                   (153 B)
├── proof_sweep_results_v5.csv                   (7.8 MB!) ❌ HUGE
├── proof_sweep_summary_v3.json                  (582 B)
├── proof_sweep_summary_v4.json                  (582 B)
├── proof_sweep_summary_v5.json                  (1.4 KB)
├── stability_boundaries_v3.csv                  (581 B)
└── stability_boundaries_v5.csv                  (1 KB)
```

**Empfehlung:** 
- ❌ ALLE alten Versionen IGNORIEREN (nur v6 relevant)
- ❌ v5 CSV ist 7.8 MB! Zu groß, veraltet

---

#### 4. Debug Folders (leer)
```
├── text_debug_de/ (0 items)
├── text_debug_en/ (0 items)
└── text_debug_it/ (0 items)
```

**Empfehlung:** 
- ❌ IGNORE (leer)

---

## 💻 D:\ Root - Neue Scripts (105+ files!)

### Kategorien

#### 1. SSZ Core Scripts ⭐ WICHTIG
```
D:\
├── ssz_animation_master.py                      (19 KB) ⭐⭐⭐
├── ssz_video_renderer.py                        (10 KB) ⭐⭐
├── ssz_proof_sweep_v6.py                        (29 KB) ⭐ (bereits in results/)
├── ssz_proof_sweep_v5.py                        (33 KB) ❌ veraltet
├── ssz_proof_sweep_v4.py                        (24 KB) ❌ veraltet
├── ssz_proof_sweep_v3.py                        (22 KB) ❌ veraltet
├── ssz_proof_check_v6.py                        (11 KB) ⭐ (bereits in results/)
├── ssz_proof_check_v5.py                        (10 KB) ❌ veraltet
├── ssz_proof_check_v4.py                        (10 KB) ❌ veraltet
├── ssz_proof_check.py                           (10 KB) ❌ veraltet
├── ssz_viz_v6.py                                (?) ⭐ (bereits in results/)
├── ssz_plot_packager.py                         (8 KB) ⚠️
├── ssz_parameter_scan.py                        (12 KB) ⚠️
├── ssz_resonance_explorer.py                    (17 KB) ⚠️
├── ssz_live_visualizer.py                       (14 KB) ⚠️
├── ssz_simple_render.py                         (5 KB) ⚠️
├── ssz_cosmo_models.py                          (2 KB) ⚠️
├── ssz_cosmo_data.py                            (5 KB) ⚠️
├── ssz_cosmo_core.py                            (7 KB) ⚠️
└── ssz_covariant_smoketest_verbose_lino_casu.py (8 KB) ⚠️
```

**Empfehlung:**
- ✅ **ssz_animation_master.py** - Video-Pipeline Master ⭐⭐⭐
- ✅ **ssz_video_renderer.py** - Video-Renderer ⭐⭐
- ⚠️ **ssz_plot_packager.py** - Möglicherweise nützlich
- ⚠️ **ssz_parameter_scan.py** - Research tool
- ⚠️ **ssz_resonance_explorer.py** - Interactive exploration
- ⚠️ **ssz_live_visualizer.py** - Real-time visualization
- ⚠️ **ssz_cosmo_*.py** (3 files) - Cosmology modules
- ❌ Alle v3/v4/v5 Scripts IGNORIEREN

**Ziel:** 
- `evidenz-ssz/scripts/ssz_animation_master.py`
- `evidenz-ssz/scripts/ssz_video_renderer.py`
- Optionally: `evidenz-ssz/scripts/tools/` (für die anderen)

---

#### 2. Animation Scripts
```
D:\
├── make_ssz_anim.py                             (?)
├── create_all_language_versions.py              (?) ⚠️ CRITICAL!
├── ssz_bigbang_vs_ssz_anim.py                   (aktiv geöffnet!)
└── blackhole_animation.py                       (?) ⚠️
```

**Empfehlung:**
- ✅ **create_all_language_versions.py** - Multi-Language Generator! ⭐⭐⭐
- ✅ **ssz_bigbang_vs_ssz_anim.py** - Demo animation
- ✅ **blackhole_animation.py** - BH visualization
- ⚠️ **make_ssz_anim.py** - Check if different from above

**Ziel:** `evidenz-ssz/scripts/`

---

#### 3. Segmented Spacetime Tests (Legacy)
```
D:\
├── segmented_ligo_compare_*.py                  (4 versions) ❌
├── segmented_full_proof.py                      ❌
├── segmented_final_proof*.py                    (3 versions) ❌
├── segmented_calculation.py                     ❌
├── segmented_and_ligo_compare*.py               (4 versions) ❌
├── segmented_ultimate_test.py                   ❌
├── segmented_space_time_full_proof.py           ❌
├── segmented_ligo_test_h5.py                    ❌
└── segmented mass.py                            ❌
```

**Empfehlung:** 
- ❌ ALLE IGNORIEREN (legacy, superseded by current scripts)

---

#### 4. LIGO/Data Fetching Scripts
```
D:\
├── fetch_missing_ligo.py                        ❌
├── fetch_missing_f_obs*.py                      (4 versions) ❌
├── fetch_ligo*.py                               (2 versions) ❌
├── fetch_eso_br_gamma.py                        ❌
└── ligo_compare.py                              ❌
```

**Empfehlung:** 
- ❌ ALLE IGNORIEREN (nicht Teil von evidenz-ssz)

---

#### 5. Unrelated Projects ❌
```
D:\
├── afd-verbot*.py                               (3 files) ❌ Unrelated
├── bild_scraper.py                              ❌ Unrelated
├── carmens_paper_test.py                        ❌ Test file
├── diag-csv.py                                  ❌ Utility
├── icd-csv.py                                   ❌ Utility
├── data-csv.py                                  ❌ Utility
├── galilean redshift.py                         ❌ Unrelated
├── google_search.py                             ❌ Utility
├── projektil-geometrie.py                       ❌ Unrelated
├── python-script.py                             ❌ Generic
├── playlist.py                                  ❌ Unrelated
├── quasikristall.py                             ❌ Unrelated
├── researchgate_weinberg_response.py            ❌ Unrelated
├── pdf.py                                       ❌ Utility
├── run.py                                       ❌ Generic
├── riemann*.py                                  (4 files) ❌ Unrelated
└── scrape-split.py                              ❌ Utility
```

**Empfehlung:** 
- ❌ ALLE IGNORIEREN (nicht SSZ-related)

---

## 🎯 EMPFOHLENE INTEGRATION - Prioritäten

### 🔴 KRITISCH - MUST HAVE

#### 1. PDF Report
```
✅ D:\mnt\data\ssz_v6_report.pdf → evidenz-ssz/results/
```

#### 2. Video Animations
```
✅ D:\mnt\data\ssz_proof_anim_v6.mp4 → evidenz-ssz/animations/
✅ D:\mnt\data\ssz_cosmo_anim.mp4 → evidenz-ssz/animations/
✅ D:\mnt\data\ssz_proof_anim_v6.wav → evidenz-ssz/animations/audio/
```

#### 3. Key Scripts
```
✅ D:\ssz_animation_master.py → evidenz-ssz/scripts/
✅ D:\ssz_video_renderer.py → evidenz-ssz/scripts/
✅ D:\create_all_language_versions.py → evidenz-ssz/scripts/
```

---

### 🟡 OPTIONAL - Nice to Have

#### 1. Additional Animation Scripts
```
⚠️ D:\ssz_bigbang_vs_ssz_anim.py → evidenz-ssz/scripts/
⚠️ D:\blackhole_animation.py → evidenz-ssz/scripts/
⚠️ D:\make_ssz_anim.py → evidenz-ssz/scripts/ (if unique)
```

#### 2. Research Tools
```
⚠️ D:\ssz_plot_packager.py → evidenz-ssz/scripts/tools/
⚠️ D:\ssz_parameter_scan.py → evidenz-ssz/scripts/tools/
⚠️ D:\ssz_resonance_explorer.py → evidenz-ssz/scripts/tools/
⚠️ D:\ssz_live_visualizer.py → evidenz-ssz/scripts/tools/
```

#### 3. Cosmology Modules
```
⚠️ D:\ssz_cosmo_*.py (3 files) → evidenz-ssz/scripts/cosmo/
```

---

### 🟢 IGNORE - Don't Need

```
❌ All v3/v4/v5 versions (outdated)
❌ All LIGO/fetch scripts (not part of evidenz-ssz)
❌ All unrelated projects (AFD, scraper, etc.)
❌ All legacy segmented_*.py scripts
❌ All utility scripts (csv, pdf, etc.)
```

---

## 📊 Zusammenfassung

### Dateien-Status

| Kategorie | Total | Integriert | Empfohlen | Optional | Ignore |
|-----------|-------|------------|-----------|----------|--------|
| **G:\UNSORTED\** | ~50 | 29 | 0 | 0 | 21 |
| **D:\mnt\data\** | ~45 | 15 | 3 | 2 | 25 |
| **D:\ Scripts** | 105+ | 7 | 3 | 10 | 85+ |
| **TOTAL** | ~200 | 51 | 6 | 12 | 131+ |

### Integration Priorities

**Phase 1 - KRITISCH (6 files):**
1. ✅ ssz_v6_report.pdf
2. ✅ ssz_proof_anim_v6.mp4
3. ✅ ssz_cosmo_anim.mp4
4. ✅ ssz_proof_anim_v6.wav
5. ✅ ssz_animation_master.py
6. ✅ ssz_video_renderer.py
7. ✅ create_all_language_versions.py

**Phase 2 - OPTIONAL (12 files):**
- Animation scripts (3)
- Research tools (4)
- Cosmology modules (3)
- Additional GIFs (2)

**Phase 3 - IGNORE (131+ files):**
- All legacy/outdated versions
- All unrelated projects
- All utility scripts

---

## 🚀 Nächste Schritte

### Sofort (Phase 1):
1. Copy `ssz_v6_report.pdf` to `evidenz-ssz/results/`
2. Copy MP4s + WAV to `evidenz-ssz/animations/`
3. Copy 3 key scripts to `evidenz-ssz/scripts/`
4. Update `evidenz-ssz/results/README.md` (add PDF reference)
5. Update `evidenz-ssz/animations/README.md` (add MP4s)
6. Git commit + push

### Optional (Phase 2):
1. Review animation scripts (uniqueness)
2. Create `evidenz-ssz/scripts/tools/` if useful
3. Create `evidenz-ssz/scripts/cosmo/` if relevant

### Later:
1. Clean up `G:\UNSORTED\` (delete v3/v4/v5)
2. Archive `D:\` scripts not needed
3. Document which scripts are obsolete

---

**© 2025 Carmen Wrede, Lino Casu**  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*

**Erstellt:** 2025-10-27 00:15 UTC+01:00
