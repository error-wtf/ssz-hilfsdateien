# Large GIF Animations - Regeneration Guide

## Why are some GIFs missing?

Large GIF files (>10 MB) are excluded from the Git repository to reduce clone size and avoid LFS bandwidth limits.

**Missing GIFs:**
- `ssz_scientific.gif` (90.12 MB)
- `ssz_scientific_de.gif` (90.07 MB)
- `ssz_scientific_en.gif` (90.23 MB)
- `ssz_scientific_it.gif` (90.23 MB)
- `ssz_perfect_demo.gif` (67.80 MB)
- `blackhole_segmented_spacetime.gif` (12.60 MB)

**Total saved:** ~450 MB

## How to regenerate missing GIFs

All missing animations can be regenerated using the provided scripts:

### 1. Scientific Overview Animations

```bash
# Generate all language versions
python ssz_scientific_overview_anim.py --lang en
python ssz_scientific_overview_anim.py --lang de
python ssz_scientific_overview_anim.py --lang it
python ssz_scientific_overview_anim.py --lang all  # All languages
```

### 2. Perfect Demo Animation

```bash
python ssz_perfect_demo_anim.py
```

### 3. Black Hole Segmented Spacetime

```bash
python ssz_blackhole_bomb_template.py
# or
python blackhole_animation.py
```

### 4. Batch Regeneration

Regenerate all missing GIFs at once:

```bash
# Windows
.\scripts\regenerate_large_gifs.ps1

# Linux/Mac
./scripts/regenerate_large_gifs.sh
```

## Alternative: Download from Release

If you don't want to regenerate, download pre-rendered GIFs from the latest release:

```bash
# Download from GitHub Releases
wget https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/releases/latest/download/ssz_animations.zip

# Extract
unzip ssz_animations.zip -d assets/ssz_animations/
```

## File Locations

After regeneration, GIFs will be in:
- `assets/ssz_animations/` (main location)
- `evidenz-ssz/animations/` (backup/legacy)
- `media/` (selected highlights)

## Notes

- Generation time: ~5-30 minutes per GIF (depending on complexity)
- Requires: matplotlib, pillow, numpy
- Output quality: High resolution (1920x1080 or higher)
- Frame rate: 30 FPS
- These files are **automatically excluded** from Git commits via `.gitignore`

## Why exclude from Git?

✅ **Pros:**
- Faster clone times (450 MB saved)
- No LFS bandwidth issues
- Smaller repository size
- Easy to regenerate

❌ **Cons:**
- Need to regenerate after clone (one-time, ~30 min)
- Or download from releases

**Recommendation:** Use the batch regeneration script after first clone.
