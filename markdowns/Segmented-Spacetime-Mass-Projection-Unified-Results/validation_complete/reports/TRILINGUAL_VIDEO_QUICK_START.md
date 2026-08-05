# SSZ Trilingual Video System - Quick Start
**Erstellt:** 2025-10-27 03:30 UTC+01  
**Status:** ✅ READY TO USE

---

## 🎯 Überblick

Dieses System erstellt **hochqualitative 3-teilige Videos** in **DE/IT/EN** mit:
- ✅ **Audio-First Workflow** (Audio bestimmt GIF-Länge)
- ✅ **Hochqualitative TTS** (Azure/Google/ffmpeg)
- ✅ **3 wissenschaftliche Visualisierungen**
- ✅ **Automatische Multi-Language Produktion**

---

## 📁 Struktur

```
scripts/
├── ssz_trilingual_master.py      # 🎬 HAUPT-PIPELINE
├── ssz_azure_tts.py               # 🎤 Azure TTS Wrapper
├── ssz_video_concat.py            # 🎞️ Video-Erstellung
├── ssz_gif_renderer_part1.py     # 🎨 Intro (ΛCDM vs SSZ)
├── ssz_gif_renderer_part2.py     # 📊 Kosmologische Daten
└── ssz_gif_renderer_part3.py     # 🔬 Wissenschaftlicher Beweis

D:\SSZ_Render\trilingual\
├── audio\         # 9 WAV-Dateien (3 Parts × 3 Sprachen)
├── parts\         # 9 GIFs + 9 MP4s (Zwischenstufen)
└── final\         # 3 finale Videos (DE/IT/EN)
```

---

## 🚀 Schnellstart

### Option 1: Komplette Produktion (alle Sprachen)

```bash
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00

# Mit Azure TTS (empfohlen)
python scripts\ssz_trilingual_master.py --tts-engine azure

# Mit Google TTS
python scripts\ssz_trilingual_master.py --tts-engine google

# Mit ffmpeg Fallback
python scripts\ssz_trilingual_master.py --tts-engine ffmpeg
```

**Ergebnis:**
- `D:\SSZ_Render\trilingual\final\ssz_complete_de.mp4` (~2-4 Min)
- `D:\SSZ_Render\trilingual\final\ssz_complete_en.mp4` (~2-4 Min)
- `D:\SSZ_Render\trilingual\final\ssz_complete_it.mp4` (~2-4 Min)

---

### Option 2: Test-Mode (nur DE, nur Part 1)

```bash
python scripts\ssz_trilingual_master.py --tts-engine azure --test
```

**Ergebnis:**
- Nur Part 1 (Intro)
- Nur Deutsch
- Schneller Test (~2 Minuten)

---

## 🎤 Audio-Setup

### Azure TTS (EMPFOHLEN)

**1. Azure CLI installieren:**
```powershell
# Download von: https://aka.ms/installazurecliwindows
# Oder via Chocolatey:
choco install azure-cli
```

**2. Anmelden:**
```bash
az login
```

**3. Cognitive Services einrichten:**
```bash
# Erstelle Resource Group
az group create --name ssz-tts --location westeurope

# Erstelle Cognitive Services Account
az cognitiveservices account create \
  --name ssz-tts-service \
  --resource-group ssz-tts \
  --kind SpeechServices \
  --sku F0 \
  --location westeurope
```

**4. Testen:**
```bash
python scripts\ssz_azure_tts.py --test
```

---

### Google Cloud TTS (Alternative)

**1. Google Cloud SDK installieren**

**2. Service Account erstellen:**
```bash
gcloud auth application-default login
```

**3. API aktivieren:**
```bash
gcloud services enable texttospeech.googleapis.com
```

---

### ffmpeg TTS (Fallback)

Keine Konfiguration nötig, aber **niedrigere Qualität**.

---

## 📋 Workflow im Detail

### Phase 1: Audio-Generierung (5-10 Min)

Pipeline erstellt **9 Audio-Dateien:**

| Part | Sprache | Dauer | Inhalt |
|------|---------|-------|--------|
| 1 | DE | ~35s | Intro: ΛCDM vs SSZ |
| 1 | EN | ~32s | Intro: ΛCDM vs SSZ |
| 1 | IT | ~37s | Intro: ΛCDM vs SSZ |
| 2 | DE | ~55s | Cosmo: Hubble, BAO, Growth |
| 2 | EN | ~52s | Cosmo: Hubble, BAO, Growth |
| 2 | IT | ~58s | Cosmo: Hubble, BAO, Growth |
| 3 | DE | ~75s | Proof: Parameter Space |
| 3 | EN | ~70s | Proof: Parameter Space |
| 3 | IT | ~78s | Proof: Parameter Space |

**Total:** ~500s Audio (~8 Min)

---

### Phase 2: GIF-Rendering (30-60 Min)

Für **jedes Audio** wird ein GIF mit **exakt passender Länge** erstellt:

**Beispiel DE Part 1:**
```
Audio: 35.2s
FPS: 30
Frames: 1056
→ GIF: 35.2s (perfekt synchron)
```

**Total:** 9 GIFs (~50-200 MB gesamt)

---

### Phase 3: MP4-Erstellung (5-10 Min)

Jedes GIF wird mit seinem Audio zu einem MP4 kombiniert:

```bash
ffmpeg -i part1_de.gif -i part1_de.wav \
  -c:v libx264 -crf 18 -preset slow \
  -c:a aac -b:a 320k \
  part1_de.mp4
```

**Total:** 9 MP4s (Zwischenstufen)

---

### Phase 4: Concatenation (2-5 Min)

Pro Sprache werden die 3 Parts zusammengefügt:

**Deutsch:**
```
part1_de.mp4 (35s) +
part2_de.mp4 (55s) +
part3_de.mp4 (75s)
= ssz_complete_de.mp4 (165s = 2:45 Min)
```

**Total:** 3 finale Videos

---

## ⏱️ Zeitplanung

| Phase | Dauer | Details |
|-------|-------|---------|
| Audio-Generierung | 5-10 Min | Abhängig von TTS-Engine |
| GIF-Rendering Part 1 | 10-15 Min | 9 GIFs à 30-40s |
| GIF-Rendering Part 2 | 15-20 Min | 9 GIFs à 50-60s |
| GIF-Rendering Part 3 | 15-25 Min | 9 GIFs à 70-80s |
| MP4-Erstellung | 5-10 Min | ffmpeg Encoding |
| Concatenation | 2-5 Min | ffmpeg concat |
| **GESAMT** | **52-85 Min** | **~1-1.5 Stunden** |

**Bei Test-Mode:** ~5 Minuten (nur 1 Sprache, 1 Part)

---

## 📊 Output-Qualität

### Audio
- **Sample Rate:** 48 kHz
- **Bit Depth:** 24-bit
- **Format:** WAV (unkomprimiert)
- **Loudness:** -14 LUFS (normalisiert)
- **Qualität:** ⭐⭐⭐⭐⭐ (Azure/Google) | ⭐⭐⭐ (ffmpeg)

### Video
- **Resolution:** 1920×1080 (1080p)
- **FPS:** 30
- **Codec:** H.264 (libx264)
- **CRF:** 18 (hohe Qualität)
- **Audio:** AAC 320 kbps
- **Größe:** ~50-150 MB pro finales Video

### GIFs (Intermediate)
- **Resolution:** 1920×1080
- **FPS:** 30 (Audio-abhängig)
- **Größe:** ~5-30 MB pro GIF

---

## 🔧 Troubleshooting

### Problem: "Azure CLI nicht gefunden"

**Lösung:**
```powershell
# Installiere Azure CLI
choco install azure-cli
# Oder Download von: https://aka.ms/installazurecliwindows
```

---

### Problem: "ffmpeg nicht gefunden"

**Lösung:**
```powershell
# Installiere ffmpeg
choco install ffmpeg
# Oder Download von: https://ffmpeg.org/download.html
```

---

### Problem: "Audio-Dauer 0.0s"

**Ursache:** ffprobe kann Audio nicht lesen

**Lösung:**
```bash
# Teste ffprobe
ffprobe -v error -show_entries format=duration D:\SSZ_Render\trilingual\audio\part1_de.wav

# Wenn Fehler: Installiere ffmpeg neu
choco uninstall ffmpeg
choco install ffmpeg
```

---

### Problem: "GIF-Rendering zu langsam"

**Lösung:**
```bash
# Nutze niedrigere DPI (schneller, aber niedriger Qualität)
python scripts\ssz_gif_renderer_part1.py --duration 35 --lang de --output test.gif --dpi 75
```

---

### Problem: "Video-Sync nicht perfekt"

**Ursache:** FPS-Mismatch zwischen GIF und Audio

**Lösung:**
Pipeline berechnet automatisch korrekte Frame-Anzahl. Wenn Problem besteht:
```python
# In ssz_gif_renderer_part1.py:
total_frames = int(duration * fps)  # Exakt!
```

---

## 🎬 Erweiterte Nutzung

### Nur Audio generieren

```python
from ssz_azure_tts import generate_tts_azure

duration = generate_tts_azure(
    text="Mein Text",
    lang='de',
    output_path=Path('test_de.wav')
)
print(f"Dauer: {duration}s")
```

---

### Nur GIF rendern (mit vorhandenem Audio)

```bash
python scripts\ssz_gif_renderer_part1.py \
  --duration 35.2 \
  --lang de \
  --output D:\test_intro_de.gif \
  --fps 30 \
  --dpi 100
```

---

### Videos manuell concatenieren

```python
from ssz_video_concat import concat_videos

videos = [
    Path('part1_de.mp4'),
    Path('part2_de.mp4'),
    Path('part3_de.mp4')
]

concat_videos(videos, Path('final_de.mp4'))
```

---

## 📝 Logs & Debugging

**Alle Logs werden gespeichert:**
```
D:\SSZ_Render\trilingual\logs\
└── production_20251027_033000.log
```

**Log-Inhalt:**
```
======================================================================
PHASE 1: Audio-Generierung
======================================================================

→ Generiere Audio: part1 (DE)
  ✓ part1_de.wav (35.23s)

→ Generiere Audio: part1 (EN)
  ✓ part1_en.wav (32.45s)

...
```

---

## 🚀 Production Checklist

**Vor dem Start:**
- [ ] Azure CLI installiert und konfiguriert
- [ ] ffmpeg installiert und im PATH
- [ ] Verzeichnis `D:\SSZ_Render\` erstellt
- [ ] Genug Speicherplatz (~2 GB für alle Dateien)

**Nach der Produktion:**
- [ ] Alle 3 finale Videos existieren
- [ ] Audio-Sync geprüft (erste 10s ansehen)
- [ ] Dateigröße OK (~50-150 MB pro Video)
- [ ] Thumbnails erstellen (optional)
- [ ] Upload zu GitHub LFS oder YouTube

---

## 📦 GitHub Upload (Optional)

**Mit Git LFS (für große Dateien):**

```bash
# Git LFS installieren
git lfs install

# Video-Dateien tracken
git lfs track "*.mp4"
git add .gitattributes

# Finale Videos committen
git add D:\SSZ_Render\trilingual\final\*.mp4
git commit -m "Add trilingual SSZ videos (DE/IT/EN)"
git push
```

**Oder:** Upload zu YouTube/Vimeo für Embedding

---

## ✅ Status

**Implementiert:**
- ✅ Haupt-Pipeline (`ssz_trilingual_master.py`)
- ✅ Azure TTS Wrapper
- ✅ GIF-Renderer Part 1 (Intro)
- ✅ GIF-Renderer Part 2 (Cosmo)
- ✅ GIF-Renderer Part 3 (Proof)
- ✅ Video-Concatenation
- ✅ Audio-First Workflow
- ✅ Multi-Language Support

**Getestet:**
- ⏳ Wartet auf User-Ausführung

**Nächste Schritte:**
1. User testet Test-Mode (`--test`)
2. User entscheidet: Azure vs. Google vs. ffmpeg
3. User startet Full-Production
4. User prüft Output-Qualität

---

## 📞 Support

**Bei Problemen:**
1. Prüfe Log-Datei in `D:\SSZ_Render\trilingual\logs\`
2. Teste einzelne Komponenten (nur Audio, nur GIF)
3. Prüfe ffmpeg/ffprobe Installation
4. Öffne Issue auf GitHub

---

**Status:** ✅ SYSTEM READY | BEREIT FÜR PRODUKTION  
**Next:** User startet Test-Mode

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
