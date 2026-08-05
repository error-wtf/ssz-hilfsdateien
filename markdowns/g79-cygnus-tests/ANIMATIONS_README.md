# Animation System for G79 Test Suite

**Automated GIF generation for all physics tests**

---

## 📁 Files

### Core Scripts

1. **`GENERATE_TEST_ANIMATIONS.py`** - Creates base animations (10s)
   - γ_seg(r) evolution
   - Velocity excess mechanism
   - Energy release at boundary
   - Core mass scaling
   - Radio redshift mechanism

2. **`CREATE_ANIMATION_VARIANTS.py`** - Creates multiple versions
   - 5s Preview (quick overview)
   - 30s Repeat (conference loops)
   - 30s Slow Motion (detailed analysis)

3. **`RUN_TESTS_WITH_ANIMATIONS.py`** - Master script
   - Runs all physics tests
   - Generates all animations
   - Creates comprehensive report

---

## 🚀 Quick Start

### ⚠️ IMPORTANT: Pipeline Strategy

**Animationen werden NACH den Tests generiert!**

Grund: Matplotlib-Fenster würden die Test-Pipeline blockieren.

### Option 1: Optimierte Pipeline (EMPFOHLEN)
```bash
python RUN_PIPELINE_OPTIMIZED.py
```
- Führt ALLE Tests durch (nicht-blockierend)
- Generiert Animationen ERST AM ENDE
- Erstellt automatisch Varianten
- Komplette Pipeline in ~5-10 Minuten

### Option 2: Manuell (schrittweise)
```bash
# Schritt 1: Tests durchlaufen lassen
python RUN_ALL_TESTS_COMPLETE.py

# Schritt 2: Animationen generieren (NACH Tests!)
python GENERATE_TEST_ANIMATIONS.py

# Schritt 3: Varianten erstellen
python CREATE_ANIMATION_VARIANTS.py
```

### Option 3: Nur Animationen (wenn Tests bereits gelaufen)
```bash
python GENERATE_TEST_ANIMATIONS.py
python CREATE_ANIMATION_VARIANTS.py
```

---

## 📊 Generated Animations

### Base Animations (10s each, ~2-5 MB)

1. **`gamma_seg_evolution.gif`**
   - Shows γ_seg(r) profile with varying α parameter
   - Demonstrates time dilation from 5% to 50%
   - 60 frames @ 10 FPS

2. **`velocity_excess.gif`**
   - Compares classical vs SSZ velocity predictions
   - Shows expanding shell through segmented spacetime
   - Dual panel: velocity + γ_seg profile
   - 60 frames @ 10 FPS

3. **`energy_release.gif`**
   - Particle crossing g^(2) → g^(1) boundary
   - Visualizes energy release as velocity boost
   - Shows metric domains with color coding
   - 80 frames @ 10 FPS

4. **`core_mass_scaling.gif`**
   - Cumulative mass from temporal density integration
   - Shows convergence to paper value (8.7 M_☉)
   - Dual panel: γ_seg profile + integrated mass
   - 60 frames @ 10 FPS

5. **`radio_redshift.gif`**
   - Frequency shift from temporal delay
   - Shows transition from IR to radio domain
   - Dual panel: frequency + redshift parameter
   - 60 frames @ 10 FPS

### Variants (auto-generated for each base animation)

- **`*_5s.gif`** - Quick preview (first 5 seconds)
  - Use for: Social media, email attachments
  - Size: ~1-2 MB

- **`*_30s_repeat.gif`** - Extended loop (3× original)
  - Use for: Conference presentations, poster displays
  - Size: ~6-15 MB

- **`*_30s_slow.gif`** - Slow motion (⅓ speed)
  - Use for: Educational materials, detailed analysis
  - Size: ~2-5 MB

---

## 📈 Output Structure

```
animations/
├── gamma_seg_evolution.gif           # 10s original
├── gamma_seg_evolution_5s.gif        # 5s preview
├── gamma_seg_evolution_30s_repeat.gif # 30s loop
├── gamma_seg_evolution_30s_slow.gif  # 30s slow
├── velocity_excess.gif
├── velocity_excess_5s.gif
├── velocity_excess_30s_repeat.gif
├── velocity_excess_30s_slow.gif
├── energy_release.gif
├── energy_release_5s.gif
├── energy_release_30s_repeat.gif
├── energy_release_30s_slow.gif
├── core_mass_scaling.gif
├── core_mass_scaling_5s.gif
├── core_mass_scaling_30s_repeat.gif
├── core_mass_scaling_30s_slow.gif
├── radio_redshift.gif
├── radio_redshift_5s.gif
├── radio_redshift_30s_repeat.gif
└── radio_redshift_30s_slow.gif
```

**Total:** 20 GIF files (~50-100 MB)

---

## 🎨 Customization

### Modify Animation Parameters

Edit `GENERATE_TEST_ANIMATIONS.py`:

```python
# Change frame count
alpha_values = np.linspace(0.05, 0.5, 120)  # 120 frames instead of 60

# Change FPS
writer = PillowWriter(fps=20)  # 20 FPS instead of 10

# Change resolution
fig, ax = plt.subplots(figsize=(16, 10))  # Larger figure
```

### Add New Animations

1. Define animation function:
```python
def generate_my_animation():
    fig, ax = plt.subplots(figsize=(12, 8))
    
    def animate(frame):
        ax.clear()
        # Your plotting code here
    
    anim = animation.FuncAnimation(fig, animate, frames=60)
    anim.save(OUTPUT_DIR/"my_animation.gif", writer=PillowWriter(fps=10))
    plt.close()
```

2. Call function in main script:
```python
generate_my_animation()
```

---

## 🔧 Dependencies

```bash
pip install numpy matplotlib scipy pillow pandas
```

**Required:**
- `numpy` - Numerical calculations
- `matplotlib` - Plotting and animation
- `pillow` - GIF file handling

**Optional:**
- `scipy` - Advanced fitting
- `pandas` - Data handling

---

## ⚡ Performance

### Generation Times
- Base animations (5): ~2-3 minutes
- Variants (15): ~1-2 minutes
- **Total:** ~3-5 minutes for complete set

### File Sizes
- Original (10s): 2-5 MB each
- 5s preview: 1-2 MB each
- 30s repeat: 6-15 MB each
- 30s slow: 2-5 MB each

### Optimization Tips

1. **Reduce frame count** for faster generation:
   ```python
   frames=30  # Instead of 60
   ```

2. **Lower FPS** for smaller files:
   ```python
   writer = PillowWriter(fps=5)  # Instead of 10
   ```

3. **Smaller figure size** for faster rendering:
   ```python
   figsize=(10, 6)  # Instead of (12, 8)
   ```

---

## 📝 Integration with Tests

### Automatic Generation After Tests

The `RUN_TESTS_WITH_ANIMATIONS.py` script:

1. Runs all physics tests with detailed output
2. Generates base animations from test results
3. Creates all variants automatically
4. Generates summary report with file list

### Manual Integration

```python
# In your test script
import subprocess
import sys

# After test completes
print("\nGenerating animation...")
subprocess.run([sys.executable, "GENERATE_TEST_ANIMATIONS.py"])
```

---

## 🎯 Use Cases

### Research Paper
- Use **original (10s)** in supplementary materials
- Reference animations in figure captions
- Host on journal website or arXiv

### Conference Presentation
- Use **30s repeat** for poster displays
- Use **5s preview** in slide transitions
- Use **30s slow** for detailed explanation

### Social Media / Outreach
- Use **5s preview** for Twitter/X
- Use **original** for YouTube shorts
- Add captions with key findings

### Education
- Use **30s slow** for lectures
- Pause at specific frames for discussion
- Compare animations side-by-side

---

## 🐛 Troubleshooting

### Problem: "No module named 'PIL'"
**Solution:**
```bash
pip install pillow
```

### Problem: Animations too large
**Solution:** Reduce frame count or FPS
```python
frames=30, interval=200  # Half the frames, double interval
```

### Problem: Generation too slow
**Solution:** Use smaller figure size or fewer data points
```python
figsize=(10, 6)  # Smaller
r_range = np.linspace(0.1, 5.0, 100)  # Fewer points
```

### Problem: GIFs not looping
**Solution:** Ensure `loop=0` in save command
```python
frames[0].save(output, save_all=True, append_images=frames[1:], loop=0)
```

---

## 📚 References

### Physics Background
- Paper: "Segmented Spacetime and the Origin of Molecular Zones"
- Authors: Carmen N. Wrede, Lino P. Casu, Bingsi
- Object: G79.29+0.46 (LBV nebula)

### Technical Documentation
- Matplotlib Animation: https://matplotlib.org/stable/api/animation_api.html
- Pillow GIF: https://pillow.readthedocs.io/en/stable/handbook/image-file-formats.html#gif

---

## ✅ Verification

After generation, check:

```bash
# List all animations
ls -lh animations/*.gif

# View total size
du -sh animations/

# Count files (should be 20)
ls animations/*.gif | wc -l
```

Expected output:
```
20 files
Total size: 50-100 MB
5 base + 15 variants
```

---

© 2025 Carmen N. Wrede, Lino P. Casu, Bingsi  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
