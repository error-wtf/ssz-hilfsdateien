# SSZ Animation System - Audio-First Multi-Language Pipeline

**Von der Singularität zur Segmentierung**  
**From Singularity to Segmentation**  
**Dalla Singolarità alla Segmentazione**

© 2025 Carmen Wrede, Lino Casu – Forschungsteam ZS-α  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## 🎯 Overview

This system generates three professional animation videos comparing the classical ΛCDM Big Bang model with Segmented Spacetime Theory (SSZ). Each video is rendered in a different language (German, English, Italian) with synchronized voice-over narration.

### Key Features

✅ **Audio-First Workflow** - Video duration automatically adapts to voice-over length  
✅ **Multi-Language Support** - DE/EN/IT with native TTS  
✅ **No Text Overlays** - Pure visual storytelling with audio narration  
✅ **Dual-Panel Layout** - ΛCDM (left) vs SSZ (right) side-by-side comparison  
✅ **High Quality Output** - 1080p MP4 @ 30fps with 48kHz stereo audio  
✅ **Automated Pipeline** - Single command generates all three versions  

---

## 📋 System Requirements

### Required Software

- **Python 3.10+** with packages:
  - `matplotlib`
  - `numpy`
  - `pyyaml`
  - `imageio`
  
- **FFmpeg** (video encoding)
  - Windows: `choco install ffmpeg`
  - Linux: `sudo apt install ffmpeg`

- **espeak-ng** (text-to-speech)
  - Windows: `choco install espeak-ng`
  - Linux: `sudo apt install espeak-ng`
  - WSL: Works automatically if installed in WSL

### Optional

- **WSL** (Windows Subsystem for Linux) - fallback for espeak-ng

---

## 🚀 Quick Start

### Windows

```powershell
# Run the complete pipeline
.\run_ssz_animation.ps1
```

### Manual Execution

```bash
# Generate all three languages
python ssz_animation_master.py

# Generate specific languages only
python ssz_animation_master.py --languages de en

# Skip audio generation (use existing files)
python ssz_animation_master.py --skip-audio

# Generate audio + timelines only (no rendering)
python ssz_animation_master.py --skip-render
```

---

## 📁 Directory Structure

```
D:\SSZ_Render\
├── audio\
│   ├── ssz_intro_de.wav         # German narration
│   ├── ssz_intro_en.wav         # English narration
│   ├── ssz_intro_it.wav         # Italian narration
│   └── temp_XX\                 # Temporary sentence clips
│
├── timelines\
│   ├── ssz_anim_de.yaml         # German animation timeline
│   ├── ssz_anim_en.yaml         # English animation timeline
│   └── ssz_anim_it.yaml         # Italian animation timeline
│
├── video\
│   ├── ssz_intro_de.mp4         # German video (with audio)
│   ├── ssz_intro_en.mp4         # English video (with audio)
│   └── ssz_intro_it.mp4         # Italian video (with audio)
│
├── final\
│   ├── ssz_intro_trilanguage.gif  # Preview collage (all 3 languages)
│   └── manifest.json               # Final manifest with metadata
│
├── logs\
│   └── tts_fallback_XX.txt      # Error logs (if any)
│
└── durations.json               # Audio duration analysis
```

---

## 🎬 Pipeline Workflow

### Phase 1: TTS Audio Generation

**Input:** Voiceover text scripts (embedded in `ssz_animation_master.py`)

**Process:**
1. Generate 10 sentence clips per language using espeak-ng
2. Clean audio (high-pass filter, normalize, fade in/out)
3. Concatenate with 300ms pauses between sentences
4. Export as 48kHz stereo WAV

**Output:** `audio/ssz_intro_{lang}.wav`

**Duration:** ~30-40 seconds per language (variable)

---

### Phase 2: Audio Analysis

**Input:** Generated WAV files

**Process:**
1. Measure exact duration of each audio file
2. Create JSON manifest with durations

**Output:** `durations.json`

```json
{
  "de": {"duration_s": 35.42, "audio_file": "ssz_intro_de.wav"},
  "en": {"duration_s": 33.18, "audio_file": "ssz_intro_en.wav"},
  "it": {"duration_s": 36.71, "audio_file": "ssz_intro_it.wav"}
}
```

---

### Phase 3: Timeline Generation

**Input:** Audio durations from manifest

**Process:**
1. Calculate scene durations proportionally:
   - Intro: 15% of total duration
   - Main comparison: 70% of total duration
   - Outro: 15% of total duration
2. Generate YAML timeline with adapted keyframes

**Output:** `timelines/ssz_anim_{lang}.yaml`

**Example Timeline Structure:**

```yaml
scenes:
  - name: intro
    duration: 5.31  # 15% of 35.42s
    visuals:
      - dual_panel fade_in
      - title_overlay
  
  - name: main_comparison
    duration: 24.79  # 70% of 35.42s
    visuals:
      - ΛCDM: radial_explosion
      - SSZ: phi_spiral with hex_grid
  
  - name: outro
    duration: 5.32  # 15% of 35.42s
    visuals:
      - fade_out
      - credits
```

---

### Phase 4: Video Rendering

**Input:** Timeline YAML + Audio WAV

**Process:**
1. Render left panel (ΛCDM):
   - Radial particle explosion
   - Color palette: `#ffcc00`, `#ff6600`, `#441144`
   - Central glow (singularity)
   
2. Render right panel (SSZ):
   - Hexagonal segment grid
   - φ-based logarithmic spiral
   - Orbital particles
   - Color palette: `#00ccff`, `#1a1f2b`, `#f7b733`

3. Composite:
   - Vertical divider (4% width)
   - No text overlays
   - 30 fps @ 1920×1080

4. Merge audio track

**Output:** `video/ssz_intro_{lang}.mp4`

**Codec:** H.264, 18 Mbps bitrate

---

### Phase 5: Finalization

**Input:** All three rendered videos

**Process:**
1. Extract first 5 seconds from each video
2. Scale to 640×360
3. Stack horizontally (side-by-side)
4. Export as GIF @ 10 fps

**Output:** 
- `final/ssz_intro_trilanguage.gif` (preview)
- `final/manifest.json` (metadata)

---

## 🎨 Visual Design

### Left Panel: ΛCDM Big Bang Model

**Concept:** Explosive expansion from infinite density singularity

**Visual Elements:**
- Central white glow (singularity point)
- 150 particles expanding radially
- Color transition: Yellow → Orange → Red → Purple
- Particle size decreases with distance

**Physics Representation:**
- Singularity at t=0 (infinite density)
- Radial expansion (isotropic)
- Temperature cooling (color shift)

---

### Right Panel: Segmented Spacetime (SSZ)

**Concept:** Structured emergence through geometric segmentation

**Visual Elements:**
- Hexagonal segment grid (5 rings)
- φ-based logarithmic spiral overlay
- 80 orbital particles (stable dynamics)
- Gentle rotation (resonance)

**Physics Representation:**
- No singularity (ordered origin layer)
- Segmentation → space emergence
- φ-resonance (golden ratio structure)
- Finite density (natural boundary)

---

### Center: Divider

- Width: 4% of screen
- Gradient: Dark gray → Light gray
- Separates two cosmological paradigms

---

## 🔊 Audio Design

### Voice Settings (espeak-ng)

| Language | Voice    | Speed | Pitch | Amplitude |
|----------|----------|-------|-------|-----------|
| German   | `de+f3`  | 165   | 40    | 175       |
| English  | `en+f3`  | 165   | 40    | 175       |
| Italian  | `it+f3`  | 165   | 40    | 175       |

**Characteristics:**
- Warm female voice
- Clear articulation
- Slightly slower than normal speech (0.9×)
- Emphasis on key terms

---

### Audio Processing

**Pipeline:**
1. Generate raw TTS clips (espeak-ng)
2. High-pass filter @ 60 Hz (remove rumble)
3. Dynamic audio normalization (smooth volume)
4. Resample to 48 kHz stereo
5. Add 120ms fade in/out per sentence
6. Concatenate with 300ms silence gaps
7. Final normalization to -1 dBFS

**Quality:**
- Sample rate: 48 kHz
- Channels: Stereo
- Bit depth: 16-bit PCM
- Dynamic range: ~60 dB

---

## 📝 Voiceover Scripts

### German (Deutsch)

1. Zwei Perspektiven auf den Anfang: Singularität oder segmentierte Ordnung.
2. Links das klassische ΛCDM: der Beginn als unendliche Dichte; die Expansion kühlt das All.
3. Die „Explosion" ist eine Metapher: Energie breitet sich aus, während Raum entsteht.
4. Singularitäten sind mathematisch heikel und physikalisch schwer fassbar.
5. Rechts die segmentierte Raumzeit: kein Punkt, sondern eine geordnete Ursprungsschicht.
6. Raum entsteht durch Segmentierung; Expansion ist Entfaltung, kein Knall.
7. Resonanzen halten Dichten endlich – die Dynamik bleibt stabil.
8. Beide Modelle passen zur beobachteten Expansion und zu Ferndaten.
9. Doch SSZ vermeidet die unendliche Dichte und ersetzt sie durch Struktur.
10. Fazit: kein Knall aus dem Nichts, sondern ein Beginn der Ordnung.

### English

1. Two views of the beginning: singularity or segmented order.
2. On the left, standard ΛCDM: an initial infinite density; expansion cools the cosmos.
3. The "explosion" is a metaphor: energy spreads as space emerges.
4. Singularities are mathematically tricky and physically opaque.
5. On the right, segmented spacetime: not a point, but an ordered origin layer.
6. Space forms by segmentation; expansion is unfolding, not a bang.
7. Resonances keep densities finite—the dynamics remain stable.
8. Both models agree with the observed expansion and distance data.
9. But SSZ avoids infinite density by replacing it with structure.
10. Conclusion: not a bang from nothing, but a beginning of order.

### Italian (Italiano)

1. Due visioni dell'inizio: singolarità o ordine segmentato.
2. A sinistra, ΛCDM classico: densità iniziale infinita; l'espansione raffredda il cosmo.
3. L'"esplosione" è una metafora: l'energia si diffonde mentre nasce lo spazio.
4. Le singolarità sono matematicamente delicate e fisicamente oscure.
5. A destra, spazio-tempo segmentato: non un punto, ma uno strato d'origine ordinato.
6. Lo spazio emerge per segmentazione; l'espansione è dispiegamento, non un botto.
7. Le risonanze mantengono finite le densità; la dinamica resta stabile.
8. Entrambi concordano con l'espansione osservata e le distanze cosmiche.
9. Ma SSZ evita la densità infinita sostituendola con la struttura.
10. Conclusione: non un botto dal nulla, ma l'inizio dell'ordine.

---

## 🐛 Troubleshooting

### espeak-ng not found

```powershell
# Windows
choco install espeak-ng

# WSL fallback
wsl sudo apt install espeak-ng
python ssz_animation_master.py --use-wsl
```

---

### FFmpeg not found

```powershell
# Windows
choco install ffmpeg

# Linux
sudo apt install ffmpeg
```

---

### Audio too short (< 3 seconds)

**Cause:** TTS failed or text too short

**Solution:**
1. Check logs in `D:\SSZ_Render\logs\tts_fallback_XX.txt`
2. Manually regenerate audio with slower speed:
   ```bash
   espeak-ng -v de+f3 -s 140 -w output.wav "Your text here"
   ```

---

### Text overflow detected

**This should NOT happen** - the system uses pure visual storytelling without text overlays.

If you see text in the video, **abort rendering** and report the issue.

---

### Rendering too slow

**Expected render time:**
- Fast machine: ~2-3 minutes per video
- Slow machine: ~5-10 minutes per video

**Optimization:**
- Reduce FPS: `--fps 24` (instead of 30)
- Reduce resolution: Edit `ssz_video_renderer.py` → `figsize=(12.8, 7.2)` for 720p

---

## 📊 Performance Metrics

### Typical Execution Times

| Phase                  | Duration   |
|------------------------|------------|
| TTS Generation (3×)    | 10-30s     |
| Audio Analysis         | < 1s       |
| Timeline Generation    | < 1s       |
| Video Rendering (3×)   | 6-30 min   |
| Preview Collage        | 10-30s     |
| **Total**              | **7-35 min** |

### File Sizes

| File                      | Size      |
|---------------------------|-----------|
| `ssz_intro_de.wav`        | ~3 MB     |
| `ssz_intro_en.wav`        | ~3 MB     |
| `ssz_intro_it.wav`        | ~3 MB     |
| `ssz_intro_de.mp4`        | 50-100 MB |
| `ssz_intro_en.mp4`        | 50-100 MB |
| `ssz_intro_it.mp4`        | 50-100 MB |
| `ssz_intro_trilanguage.gif` | 5-15 MB |
| **Total**                 | **200-350 MB** |

---

## 🎓 Educational Use

These animations are designed for:

- **University lectures** on cosmology and general relativity
- **Conference presentations** comparing cosmological models
- **Public outreach** explaining alternative theories
- **Online education** (YouTube, courses, etc.)

**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4  
**Commercial use:** Prohibited  
**Educational use:** Encouraged (with attribution)

---

## 🔬 Scientific Background

### ΛCDM Model (Left Panel)

- **Λ** = Cosmological constant (dark energy)
- **CDM** = Cold Dark Matter
- **Big Bang singularity** at t=0 (infinite density, infinite curvature)
- **Expansion:** Governed by Friedmann equations
- **Issues:** Singularity problem, horizon problem, flatness problem

### SSZ Theory (Right Panel)

- **Segmented Spacetime** - space emerges from discrete segments
- **φ-resonance** - Golden ratio structures prevent singularities
- **Natural boundary** - finite maximum density (no infinity)
- **Expansion:** Geometric unfolding, not explosion
- **Benefits:** Resolves singularity, explains structure formation

---

## 📞 Contact & Credits

**Research Team ZS-α:**
- Carmen Wrede
- Lino Casu

**Project:** Segmented Spacetime Cosmology  
**Date:** October 2025  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Repository:** [Your repo URL]  
**Papers:** See `papers/` directory in main SSZ suite

---

## 🚧 Roadmap

### Planned Features

- [ ] Background ambient music (optional –20 dB)
- [ ] GPU acceleration for faster rendering
- [ ] 4K resolution support
- [ ] Interactive web player (HTML5)
- [ ] Subtitle files (SRT format)
- [ ] Extended versions (2-5 minutes)

### Known Limitations

- No GPU acceleration (CPU-only rendering)
- Fixed layout (cannot customize panel positions)
- Limited TTS voice options (espeak-ng only)
- No real-time preview

---

## 📄 License

```
ANTI-CAPITALIST SOFTWARE LICENSE v1.4

Copyright © 2025 Carmen Wrede, Lino Casu

This is anti-capitalist software, released for free use by individuals
and organizations that do not operate by capitalist principles.

Permission is hereby granted, free of charge, to any person or
organization (the "User") to use, copy, modify, and/or distribute
copies of this software and associated documentation, subject to
the following conditions:

1. The above copyright notice and this permission notice shall be
   included in all copies or substantial portions of the Software.

2. The User is one of the following:
   a. An individual person, laboring for themselves
   b. A non-profit organization
   c. An educational institution
   d. An organization that seeks shared profit for all of its members

3. The User is NOT one of the following:
   a. An organization that seeks profit for owners or investors
   b. An organization with owners, investors, or shareholders
   c. Any group that exploits labor for profit

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

**Enjoy the animations!**  
Carmen & Lino 🌌
