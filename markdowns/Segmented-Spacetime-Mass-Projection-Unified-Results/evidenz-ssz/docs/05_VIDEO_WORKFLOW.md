# 🎥 Video-Workflow - Audio-First Pipeline

**Dokumentation der automatisierten Video-Generierung mit TTS-Audiobeschreibung**

---

## Übersicht

Die **SSZ Animation Master Pipeline** generiert automatisch Videos mit synchronisierten Audiobeschreibungen in drei Sprachen (DE/EN/IT):

```
TTS-Audio → Audio-Analyse → YAML-Timeline → Video-Rendering → Finalisierung
```

**Status:** 🚧 In Entwicklung

---

## 🎯 Geplante Outputs

### MP4-Videos mit Audio

| Datei | Sprache | Inhalt | Dauer |
|-------|---------|--------|-------|
| `ssz_intro_de.mp4` | Deutsch | Voiceover + Animation | ~30-40s |
| `ssz_intro_en.mp4` | English | Voiceover + Animation | ~30-40s |
| `ssz_intro_it.mp4` | Italiano | Voiceover + Animation | ~30-40s |

### Audio-Dateien

| Datei | Sprache | Format | Qualität |
|-------|---------|--------|----------|
| `ssz_intro_de.wav` | Deutsch | 48 kHz Stereo | PCM |
| `ssz_intro_en.wav` | English | 48 kHz Stereo | PCM |
| `ssz_intro_it.wav` | Italiano | 48 kHz Stereo | PCM |

---

## 🛠️ Technische Voraussetzungen

### Software-Abhängigkeiten

**1. espeak-ng (TTS-Engine)**
```bash
# Windows
choco install espeak-ng

# Linux (Ubuntu/Debian)
sudo apt install espeak-ng

# macOS
brew install espeak-ng
```

**2. FFmpeg (Audio/Video-Verarbeitung)**
```bash
# Windows
choco install ffmpeg

# Linux
sudo apt install ffmpeg

# macOS
brew install ffmpeg
```

**3. Python-Bibliotheken**
```bash
pip install numpy matplotlib scipy pyyaml
```

---

## 📝 Audioinhalte

### Deutsch (10 Sätze)

1. **Intro:** Zwei Perspektiven auf den Anfang: Singularität oder segmentierte Ordnung.
2. **ΛCDM:** Links das klassische Lambda C D M: der Beginn als unendliche Dichte; die Expansion kühlt das All.
3. **Metapher:** Die „Explosion" ist eine Metapher: Energie breitet sich aus, während Raum entsteht.
4. **Problem:** Singularitäten sind mathematisch heikel und physikalisch schwer fassbar.
5. **SSZ:** Rechts die segmentierte Raumzeit: kein Punkt, sondern eine geordnete Ursprungsschicht.
6. **Raum:** Raum entsteht durch Segmentierung; Expansion ist Entfaltung, kein Knall.
7. **Resonanz:** Resonanzen halten Dichten endlich – die Dynamik bleibt stabil.
8. **Daten:** Beide Modelle passen zur beobachteten Expansion und zu Ferndaten.
9. **Unterschied:** Doch S S Z vermeidet die unendliche Dichte und ersetzt sie durch Struktur.
10. **Fazit:** Fazit: kein Knall aus dem Nichts, sondern ein Beginn der Ordnung.

### English (10 Sentences)

1. **Intro:** Two views of the beginning: singularity or segmented order.
2. **ΛCDM:** On the left, standard Lambda C D M: an initial infinite density; expansion cools the cosmos.
3. **Metaphor:** The "explosion" is a metaphor: energy spreads as space emerges.
4. **Problem:** Singularities are mathematically tricky and physically opaque.
5. **SSZ:** On the right, segmented spacetime: not a point, but an ordered origin layer.
6. **Space:** Space forms by segmentation; expansion is unfolding, not a bang.
7. **Resonance:** Resonances keep densities finite—the dynamics remain stable.
8. **Data:** Both models agree with the observed expansion and distance data.
9. **Difference:** But S S Z avoids infinite density by replacing it with structure.
10. **Conclusion:** Conclusion: not a bang from nothing, but a beginning of order.

### Italiano (10 Frasi)

1. **Intro:** Due visioni dell'inizio: singolarità o ordine segmentato.
2. **ΛCDM:** A sinistra, Lambda C D M classico: densità iniziale infinita; l'espansione raffredda il cosmo.
3. **Metafora:** L'"esplosione" è una metafora: l'energia si diffonde mentre nasce lo spazio.
4. **Problema:** Le singolarità sono matematicamente delicate e fisicamente oscure.
5. **SSZ:** A destra, spazio-tempo segmentato: non un punto, ma uno strato d'origine ordinato.
6. **Spazio:** Lo spazio emerge per segmentazione; l'espansione è dispiegamento, non un botto.
7. **Risonanza:** Le risonanze mantengono finite le densità; la dinamica resta stabile.
8. **Dati:** Entrambi concordano con l'espansione osservata e le distanze cosmiche.
9. **Differenza:** Ma S S Z evita la densità infinita sostituendola con la struttura.
10. **Conclusione:** Conclusione: non un botto dal nulla, ma l'inizio dell'ordine.

---

## 🔄 Pipeline-Workflow

### Stufe 1: TTS-Audio-Generierung

**Script:** `ssz_animation_master.py`

```python
ESPEAK_VOICES = {
    'de': {'voice': 'de+f3', 'speed': 165, 'pitch': 40, 'amplitude': 175},
    'en': {'voice': 'en+f3', 'speed': 165, 'pitch': 40, 'amplitude': 175},
    'it': {'voice': 'it+f3', 'speed': 165, 'pitch': 40, 'amplitude': 175},
}
```

**Prozess:**
1. Jeden Satz einzeln mit `espeak-ng` rendern
2. 300ms Stille zwischen Sätzen einfügen
3. Alle Clips mit FFmpeg konkatenieren
4. Audio-Filter anwenden (Highpass, DynAudNorm)
5. Output: `ssz_intro_{language}.wav`

**Dauer pro Sprache:** ~30-40 Sekunden (abhängig von Sprechgeschwindigkeit)

---

### Stufe 2: Audio-Analyse

**Funktion:** `analyze_audio_duration()`

**Prozess:**
1. WAV-Datei öffnen
2. Frames zählen
3. Duration berechnen: `duration = frames / sample_rate`
4. JSON-Manifest erstellen: `durations.json`

**Beispiel-Output:**
```json
{
  "de": {"duration_s": 35.42, "audio_file": "ssz_intro_de.wav"},
  "en": {"duration_s": 34.18, "audio_file": "ssz_intro_en.wav"},
  "it": {"duration_s": 36.71, "audio_file": "ssz_intro_it.wav"}
}
```

---

### Stufe 3: YAML-Timeline-Generierung

**Funktion:** `create_yaml_timeline()`

**Zeitverteilung:**
- **Intro:** 15% (Fade-in, Title)
- **Main:** 70% (Dual-Panel Animation)
- **Outro:** 15% (Fade-out, Credits)

**Beispiel-Timeline (30s Audio):**
```yaml
metadata:
  title: "Von der Singularität zur Segmentierung"
  language: de
  total_duration: 30.00
  fps: 30
  resolution: [1920, 1080]

scenes:
  - name: intro
    duration: 4.50   # 15% von 30s
    visuals:
      - type: dual_panel
        left: {background: "#1a0a2e", effect: fade_in}
        right: {background: "#0a1f2e", effect: fade_in}
      - type: title_overlay
        text: "Von der Singularität zur Segmentierung"
  
  - name: main_comparison
    duration: 21.00  # 70% von 30s
    visuals:
      - type: dual_panel
        left: {animation: radial_explosion, particles: 150}
        right: {animation: phi_spiral, segments: 12}
  
  - name: outro
    duration: 4.50   # 15% von 30s
    visuals:
      - type: credits
        text: "© 2025 Carmen Wrede, Lino Casu"
```

---

### Stufe 4: Video-Rendering

**Script:** `ssz_video_renderer.py`

**Prozess:**
1. **Matplotlib-Animation erstellen:**
   - Left Panel: ΛCDM mit Singularität (Radial-Explosion)
   - Right Panel: SSZ mit φ-Spiralen (Hexagon-Grid)
   - Divider: Vertikaler Gradient

2. **Video ohne Audio rendern:**
   ```python
   anim.save('temp.mp4', writer=FFMpegWriter(fps=30, bitrate=18000))
   ```

3. **Audio-Spur hinzufügen:**
   ```bash
   ffmpeg -i temp.mp4 -i ssz_intro_de.wav \
          -c:v copy -c:a aac -b:a 192k \
          -shortest -y ssz_intro_de.mp4
   ```

4. **Temp-Datei löschen**

**Output:**
- `ssz_intro_de.mp4` (1920×1080, 30fps, H.264 + AAC)
- `ssz_intro_en.mp4`
- `ssz_intro_it.mp4`

---

### Stufe 5: Finalisierung

**Zusätzliche Outputs:**

1. **Preview-Collage (optional):**
   ```bash
   ffmpeg -i de.mp4 -i en.mp4 -i it.mp4 \
          -filter_complex "[0:v][1:v][2:v]hstack=inputs=3[out]" \
          -map "[out]" -r 10 trilanguage_preview.gif
   ```

2. **Manifest-Datei:**
   ```json
   {
     "created_by": "WindSurf Automation v2",
     "language_order": ["de", "en", "it"],
     "outputs": {
       "de": {"video": "ssz_intro_de.mp4", "size_mb": 15.3},
       "en": {"video": "ssz_intro_en.mp4", "size_mb": 14.8},
       "it": {"video": "ssz_intro_it.mp4", "size_mb": 15.1}
     }
   }
   ```

---

## 🚀 Verwendung

### Vollständiger Workflow

```bash
# 1. Ordner wechseln
cd /pfad/zu/evidenz-ssz/scripts/

# 2. Pipeline starten (alle 3 Sprachen)
python ssz_animation_master.py --languages de en it

# 3. Outputs prüfen
ls -lh D:\SSZ_Render/video/
```

### Nur Audio generieren

```bash
# TTS-Audio erstellen, Video überspringen
python ssz_animation_master.py --skip-render
```

### Nur eine Sprache

```bash
# Nur Deutsch
python ssz_animation_master.py --languages de
```

### WSL-Fallback (Windows)

```bash
# Falls espeak-ng nur in WSL verfügbar
python ssz_animation_master.py --use-wsl
```

---

## 📂 Output-Struktur

```
D:\SSZ_Render/
├── audio/
│   ├── ssz_intro_de.wav
│   ├── ssz_intro_en.wav
│   ├── ssz_intro_it.wav
│   └── temp_de/              # Temp-Clips (wird gelöscht)
├── video/
│   ├── ssz_intro_de.mp4      # ✅ Hauptoutput
│   ├── ssz_intro_en.mp4
│   └── ssz_intro_it.mp4
├── timelines/
│   ├── ssz_anim_de.yaml
│   ├── ssz_anim_en.yaml
│   └── ssz_anim_it.yaml
├── final/
│   ├── ssz_intro_trilanguage.gif  # Preview (optional)
│   └── manifest.json               # Metadaten
└── logs/
    └── tts_fallback_*.txt          # Error-Logs (falls vorhanden)
```

---

## ⚙️ Konfiguration

### TTS-Voice Anpassung

**Datei:** `ssz_animation_master.py` (Zeile 80-86)

```python
ESPEAK_VOICES = {
    'de': {
        'voice': 'de+f3',      # Stimme (f=weiblich, m=männlich, 1-5=Variante)
        'speed': 165,          # Wörter pro Minute
        'pitch': 40,           # Tonhöhe (0-99)
        'amplitude': 175       # Lautstärke (0-200)
    },
    # ...
}
```

**Verfügbare Stimmen testen:**
```bash
espeak-ng --voices
```

### Video-Parameter

**Datei:** `ssz_video_renderer.py` (Zeile 194)

```python
fig = plt.figure(
    figsize=(19.2, 10.8),  # 1920×1080 bei dpi=100
    dpi=100,
    facecolor='black'
)
```

**Auflösung ändern:**
- 4K: `figsize=(38.4, 21.6), dpi=100`
- Full HD: `figsize=(19.2, 10.8), dpi=100`
- HD: `figsize=(12.8, 7.2), dpi=100`

---

## 🐛 Troubleshooting

### Fehler: "espeak-ng not found"

**Lösung:**
```bash
# Windows
choco install espeak-ng

# Oder WSL verwenden
python ssz_animation_master.py --use-wsl
```

### Fehler: "FFmpeg not found"

**Lösung:**
```bash
# Windows
choco install ffmpeg

# Alternative: moviepy verwenden (siehe unten)
```

### Fehler: "Audio duration mismatch"

**Problem:** Video zu kurz/lang für Audio

**Lösung:** Timeline manuell anpassen in `ssz_anim_{lang}.yaml`

### Alternative: moviepy statt FFmpeg

```bash
pip install moviepy

# Script anpassen:
# 1. Import hinzufügen: from moviepy.editor import *
# 2. FFmpeg-Calls ersetzen durch moviepy-API
```

---

## 📊 Performance

**Geschätzte Zeiten (AMD Ryzen 7 / Intel i7):**

| Schritt | Dauer | Bemerkung |
|---------|-------|-----------|
| TTS-Audio (3 Sprachen) | ~2 min | Abhängig von espeak-ng |
| Audio-Analyse | <1 s | Sehr schnell |
| YAML-Timeline | <1 s | Sehr schnell |
| Video-Rendering (1 Sprache) | ~5-10 min | 900 Frames @ 30fps |
| Video-Rendering (3 Sprachen) | ~15-30 min | Parallel möglich |
| FFmpeg Audio-Merge | <10 s | Sehr schnell |
| **Total** | **~20-35 min** | Für alle 3 Videos |

**Speicherbedarf:**
- Audio: ~3 MB (je Sprache)
- Video (temp): ~300 MB (wird gelöscht)
- Video (final): ~15 MB (je Sprache)
- **Total:** ~50 MB

---

## 🔮 Geplante Erweiterungen

### Phase 2: Erweiterte Features

- [ ] **Human Voice:** Echte Sprecher statt TTS
- [ ] **Untertitel:** SRT/VTT-Dateien generieren
- [ ] **Interaktive Timecodes:** Kapitelmarken
- [ ] **4K-Version:** Höhere Auflösung
- [ ] **YouTube-Upload:** Automatischer Upload via API

### Phase 3: Zusätzliche Videos

- [ ] **Black Hole Bomb:** Separate Video-Serie
- [ ] **Stellar Evolution:** Sternentwicklung animiert
- [ ] **Cosmic Lottery:** Leben-Wahrscheinlichkeit visualisiert

---

## 📚 Weiterführende Links

**Dokumentation:**
- [Haupt-README](../README.md)
- [Dokumentations-Index](./INDEX.md)
- [Big Bang vs. SSZ](./01_BIG_BANG_VS_SSZ.md)

**Scripts:**
- `ssz_animation_master.py` - Master-Pipeline
- `ssz_video_renderer.py` - Video-Renderer
- `ssz_animator.py` - Basis-Animator

**Tools:**
- [espeak-ng](https://github.com/espeak-ng/espeak-ng) - TTS-Engine
- [FFmpeg](https://ffmpeg.org/) - Audio/Video-Verarbeitung
- [Matplotlib](https://matplotlib.org/) - Python-Visualisierung

---

## 📝 Lizenz & Credits

**Autoren:**
- Carmen Wrede
- Lino Casu

**Lizenz:**
ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**TTS-Stimmen:**
- espeak-ng (Open Source, GNU GPL v3)

**Audio-Filter:**
- FFmpeg (GNU LGPL 2.1+)

---

> *"The cosmos is within us. We are made of star-stuff.*  
> *We are a way for the universe to know itself."*  
> — Carl Sagan

---

**© 2025 Carmen Wrede, Lino Casu**  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*
