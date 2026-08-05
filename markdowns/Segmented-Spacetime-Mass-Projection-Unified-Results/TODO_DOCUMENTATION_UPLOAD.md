# 📋 TODO: Dokumentation & Repository Upload

**Stand:** 2025-10-27 06:20 UTC+01  
**Session:** Video Production & Visual Animations

---

## ✅ BEREITS ERLEDIGT (Heute)

### 1. Visual Animations Struktur
- [x] 6 detaillierte .md-Dateien in `docs/` erstellt
- [x] GIFs in `assets/ssz_animations/` kopiert
- [x] README.md erweitert mit Animation-Section
- [x] Wissenschaftliche Erklärungen komplett

### 2. Video-Produktion Scripts
- [x] Part 4 (Black Hole) Audio-Texte
- [x] Part 5 (Stellar Nucleosynthesis) GIF erstellt
- [x] Part 6 (Black Hole Bomb - Energy Finite) Audio-Texte
- [x] Audio-Texte-Sammlung: `D:\SSZ_VIDEO_AUDIOTEXTE_ALLE_TEILE.md`
- [x] Extended Video Producer: `ssz_6parts_final_producer.py`

### 3. Repository Commits (Session)
- [x] Part 4 & 5 Scripts committed
- [x] Stellar Nucleosynthesis GIF uploaded (Git LFS)
- [x] Black Hole Bomb Scripts & README

---

## ⏳ NOCH ZU TUN

### A. Video-Produktion Dateien

#### Scripts von D:\ ins Repo kopieren
```
d:\ssz_video_scripts_part6_final.py          → evidenz-ssz/scripts/video_production/
d:\ssz_6parts_final_producer.py              → evidenz-ssz/scripts/video_production/
d:\ssz_stellar_nucleosynthesis_animator.py   → evidenz-ssz/scripts/animations/
d:\SSZ_VIDEO_AUDIOTEXTE_ALLE_TEILE.md        → docs/ (oder evidenz-ssz/docs/)
```

**Status:** ⏳ Scripts noch auf D:\, nicht im Repo

**Dokumentation benötigt:**
- [ ] README.md für Video Production Workflow
- [ ] Tutorial: "Wie erstelle ich SSZ Videos?"
- [ ] Audio-Qualität Vergleich (TTS vs Manual)
- [ ] FFmpeg Integration Guide

---

### B. Finale 6-Part Videos

**Location aktuell:** `D:\SSZ_Final_Videos_6Parts\` (lokal)

**Videos:**
- [ ] `ssz_complete_6parts_de.mp4` (~35-40 MB)
- [ ] `ssz_complete_6parts_en.mp4` (~34-39 MB)
- [ ] `ssz_complete_6parts_it.mp4` (~36-41 MB)

**Problem:** Videos sind zu groß für Git (>100 MB)

**Lösungen:**
1. **Git LFS** (Large File Storage)
   ```bash
   git lfs track "*.mp4"
   git add .gitattributes
   git add evidenz-ssz/videos/*.mp4
   ```

2. **Externe Hosting**
   - YouTube Upload (öffentlich/unlisted)
   - Google Drive / OneDrive
   - Release Assets auf GitHub
   - Zenodo (wissenschaftliches Repository)

3. **Video-Kompression**
   ```bash
   ffmpeg -i input.mp4 -c:v libx264 -crf 28 -c:a aac output_compressed.mp4
   # Ziel: <50 MB pro Video
   ```

**Empfehlung:** YouTube + Git LFS für Originale

---

### C. GIF-Animationen (Fehlende)

**Bereits im Repo:** (via Git LFS)
- [x] `blackhole_segmented_spacetime.gif`
- [x] `ssz_bomb_animation.gif`
- [x] `ssz_stellar_nucleosynthesis.gif` (heute)
- [x] `ssz_proof_anim_v6.gif`
- [x] `ssz_cosmo_anim.gif`

**Noch hochladen:**
- [ ] `ssz_bigbang_vs_ssz_demo.gif` (Scientific DE/EN/IT versions)
- [ ] `ssz_scientific_de.gif` (90 MB) - als ssz_bigbang_vs_ssz_demo.gif?
- [ ] `ssz_scientific_en.gif` (90 MB)
- [ ] `ssz_scientific_it.gif` (90 MB)

**Aktion:**
```bash
# Umbenennen für Konsistenz
cd h:\WINDSURF\...\assets\ssz_animations\

# DE wird zu Demo (Standard)
Copy-Item ssz_scientific_de.gif ssz_bigbang_vs_ssz_demo.gif

# Git LFS
git lfs track "assets/ssz_animations/*.gif"
git add assets/ssz_animations/ssz_bigbang_vs_ssz_demo.gif
git commit -m "Add Big Bang vs SSZ demo animation (German version)"
```

---

### D. Dokumentation - Video System

**Fehlende Guides:**

#### 1. Video Production README
**Datei:** `evidenz-ssz/videos/README.md`

**Inhalt:**
- Overview: 6-Part Trilingual Video System
- GIF Sources & Creation
- Audio Generation (Edge-TTS)
- Video Assembly (FFmpeg/Editor)
- YouTube Upload Metadata
- Untertitel (optional)

#### 2. Animation Creation Guide
**Datei:** `evidenz-ssz/animations/CREATION_GUIDE.md`

**Inhalt:**
- Matplotlib Setup
- Colormaps & SSZ Theme
- GIF Export Settings
- Frame Rate Optimization
- File Size Management
- Scientific Visualization Best Practices

#### 3. Audio Scripts Archive
**Datei:** `evidenz-ssz/docs/AUDIO_SCRIPTS_ARCHIVE.md`

**Inhalt:**
- Alle Audio-Texte (DE/EN/IT)
- Timing Guidelines
- Voice-Over Recommendations
- TTS vs Human Voice Comparison
- Professional Recording Tips

---

### E. Wissenschaftliche Dokumentation

#### Papers aktualisieren

**1. SSZ Cosmology Paper**
**Datei:** `papers/SSZ_Cosmology_Full.md`

**Fehlende Abschnitte:**
- [ ] Part 5: Stellar Nucleosynthesis in SSZ
  - CNO Cycle modifications
  - Segment density in stellar cores
  - Enhanced fusion stability
  - Element production rates

**2. Black Hole Physics Paper**
**Datei:** `papers/SSZ_Black_Holes.md`

**Fehlende Abschnitte:**
- [ ] Part 6: Energy Finiteness Proof
  - Black Hole Bomb experiment results
  - Segment damping mechanism
  - Thermodynamic consistency
  - Information preservation

**3. Mathematical Proof Paper**
**Datei:** `papers/SSZ_Mathematical_Proof.md`

**Status:** Vollständig (v6 bereits dokumentiert)

---

### F. Code-Dokumentation

#### Scripts ohne Docstrings

**Finden:**
```bash
# Alle Python-Dateien ohne Docstrings
grep -L '"""' evidenz-ssz/scripts/**/*.py
```

**Hinzufügen:**
- [ ] Alle Video Production Scripts
- [ ] Animation Generator Scripts
- [ ] Utility Tools

**Standard-Docstring:**
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Script Name - Brief Description

Detailed description of what this script does,
its inputs, outputs, and scientific purpose.

Usage:
    python script_name.py --arg value

Dependencies:
    - numpy
    - matplotlib
    - etc.

Author: Carmen Wrede, Lino Casu
Date: 2025-10-XX
License: ANTI-CAPITALIST SOFTWARE LICENSE v1.4
"""
```

---

### G. Tests & Verification

**Neue Scripts brauchen Tests:**

#### Video Production Tests
**Datei:** `tests/test_video_production.py`

```python
def test_audio_generation():
    """Test Edge-TTS audio generation"""
    pass

def test_gif_loading():
    """Test GIF frame loading and looping"""
    pass

def test_video_concatenation():
    """Test FFmpeg video merging"""
    pass
```

#### Animation Tests
**Datei:** `tests/test_animations.py`

```python
def test_stellar_nucleosynthesis_animation():
    """Test SSZ stellar animation generation"""
    pass

def test_gif_file_sizes():
    """Ensure GIFs are under size limits"""
    pass
```

---

### H. GitHub Release

**Nächstes Release:** v1.5.0

**Changelog:**
```markdown
## v1.5.0 - Trilingual Video Production System (2025-10-27)

### Added
- 6-Part Trilingual Video System (DE/EN/IT)
- Part 4: Black Hole in SSZ (no singularity)
- Part 5: Stellar Nucleosynthesis (life prerequisites)
- Part 6: Black Hole Bomb (energy is finite)
- Visual Animations Section in README
- 6 Detailed Animation Explanations (docs/)
- Stellar Nucleosynthesis GIF (20s, 4 panels)

### Documentation
- Audio Scripts Archive (all 6 parts, 3 languages)
- Video Production Workflow
- Animation Creation Guide
- YouTube Upload Metadata

### Scripts
- ssz_6parts_final_producer.py (automated video generation)
- ssz_stellar_nucleosynthesis_animator.py
- ssz_video_scripts_part6_final.py

### Data
- 18 Audio Files (6 parts × 3 languages)
- 3 Final Videos (~100 MB total)
```

**Assets:**
- Videos als Release Assets (wenn >100 MB)
- Komprimierte Archive

---

### I. Externe Platforms

#### YouTube

**Kanal:** SSZ Cosmology (anlegen?)

**Videos hochladen:**
1. `ssz_complete_6parts_de.mp4`
2. `ssz_complete_6parts_en.mp4`
3. `ssz_complete_6parts_it.mp4`

**Metadata (aus METADATA dict):**
```
Titel: SSZ Kosmologie – Vom Big Bang bis zur Endlichkeit der Energie
Beschreibung: [Teil 1-6 Timestamps + GitHub Link]
Tags: SSZ, Segmented Spacetime, Black Hole, etc.
Sprache: DE/EN/IT
Kategorie: Wissenschaft & Technik
```

**Thumbnails:**
- Frame aus jedem Teil extrahieren
- Composite-Bild erstellen

#### ResearchGate / arXiv

**Pre-Print:**
- [ ] SSZ Cosmology Full Paper
- [ ] Black Hole Bomb Experimental Validation
- [ ] Stellar Nucleosynthesis in SSZ

---

### J. README Updates

#### Main README.md

**Fehlende Sections:**

1. **Video Gallery**
   ```markdown
   ## 📺 Educational Videos
   
   **6-Part Trilingual Series** (DE/EN/IT)
   
   1. Big Bang vs Segmentation
   2. Cosmological Observations
   3. Mathematical Stability
   4. Black Holes (No Singularity)
   5. Stellar Nucleosynthesis
   6. Energy is Finite
   
   [▶️ Watch on YouTube]() | [📥 Download (Git LFS)]()
   ```

2. **Quick Start Guide Update**
   - Video Production Workflow
   - Animation Generation
   - Documentation Navigation

#### evidenz-ssz/README.md

**Update:**
- [ ] Part 4, 5, 6 hinzufügen
- [ ] Video Production Section
- [ ] Animation Catalog erweitern

---

## 📊 Prioritäten

### HOCH (Diese Woche)
1. ✅ Visual Animations Struktur (DONE)
2. ⏳ Video Scripts ins Repo kopieren
3. ⏳ Git LFS für große GIFs konfigurieren
4. ⏳ Video Production README erstellen
5. ⏳ YouTube Upload (3 Videos)

### MITTEL (Nächste Woche)
6. Audio Scripts Archive dokumentieren
7. Papers aktualisieren (Part 5 & 6)
8. Tests für neue Scripts schreiben
9. Animation Creation Guide
10. GitHub Release v1.5.0

### NIEDRIG (Optional)
11. Docstrings vervollständigen
12. ResearchGate Upload
13. Untertitel generieren
14. Thumbnail-Design

---

## 🎯 Nächste Schritte (Heute)

### 1. Scripts ins Repo kopieren
```powershell
# Video Production
Copy-Item D:\ssz_video_scripts_part6_final.py `
          h:\WINDSURF\...\evidenz-ssz\scripts\video_production\

Copy-Item D:\ssz_6parts_final_producer.py `
          h:\WINDSURF\...\evidenz-ssz\scripts\video_production\

# Animations
Copy-Item D:\ssz_stellar_nucleosynthesis_animator.py `
          h:\WINDSURF\...\evidenz-ssz\scripts\animations\

# Docs
Copy-Item D:\SSZ_VIDEO_AUDIOTEXTE_ALLE_TEILE.md `
          h:\WINDSURF\...\docs\
```

### 2. Git LFS Setup
```bash
# Install Git LFS (if not installed)
git lfs install

# Track large files
git lfs track "assets/ssz_animations/*.gif"
git lfs track "evidenz-ssz/videos/*.mp4"

# Add .gitattributes
git add .gitattributes

# Check status
git lfs ls-files
```

### 3. Commit & Push
```bash
git add evidenz-ssz/scripts/video_production/
git add evidenz-ssz/scripts/animations/
git add docs/
git add assets/ssz_animations/
git add README.md

git commit -m "Complete video production system and visual animations

- Added 6-part trilingual video production scripts
- Created stellar nucleosynthesis animator
- Extended README with visual animations section
- Documented all audio scripts for manual recording
- Added 6 detailed animation explanations"

git push
```

---

## 📝 Checkliste Zusammenfassung

**Dateien:**
- [ ] 4 Python Scripts (D:\ → Repo)
- [ ] 3 Finale Videos (YouTube + Git LFS?)
- [ ] 3 Scientific GIFs umbenennen/hochladen
- [ ] 1 Audio-Texte Dokumentation

**Dokumentation:**
- [ ] Video Production README
- [ ] Animation Creation Guide
- [ ] Papers Update (Part 5 & 6)
- [ ] YouTube Metadata

**Infrastructure:**
- [ ] Git LFS konfigurieren
- [ ] GitHub Release v1.5.0 vorbereiten
- [ ] YouTube Kanal Setup
- [ ] Tests schreiben

**Total:** ~20 Tasks | Geschätzt: 4-6 Stunden Arbeit

---

**Erstellt:** 2025-10-27 06:20 UTC+01:00  
**Nächstes Review:** Nach Video-Upload

© 2025 Carmen Wrede, Lino Casu
