# 🚀 Segmented Spacetime Theory - Quick Start Guide

Schnelleinstieg in die vollständige **Segmented Spacetime (SSZ) Computation & Visualization Suite**.

## ⚡ 5-Minuten-Start

### **Option 1: Python (Empfohlen)**

```bash
# 1. Dependencies installieren
pip install numpy matplotlib plotly scipy pandas

# 2. Basis-Demo starten
python ssz_unified_suite.py

# 3. Interaktive GUI öffnen
python ssz_interactive_gui.py
```

**Was passiert:**
- Berechnet σ(r), τ(r), n(r) für Sonnenmasse
- Zeigt 4 Plots: Segmentdichte, Zeitdehnung, Optischer Index, Dual-Velocity
- Exportiert Kalibrierungsdaten als JSON
- Erstellt 3D-Visualisierung als HTML

### **Option 2: WebGL (Browser)**

```bash
# Lokaler Server
cd segmented-solar-webgl/docs
python -m http.server 8000

# Browser öffnen
# http://localhost:8000
```

**Features:**
- GPU-beschleunigte Shader-Berechnungen
- Interaktive 3D-Rotation mit Maus
- Live-Parameter-Slider (α, κ, p)
- 60 FPS bei 20.000+ Vertices

### **Option 3: Java/TeaVM**

```bash
cd segmented-solar-java
mvn clean package
open docs/index.html
```

**Besonderheiten:**
- Java → JavaScript Transpilation
- LUT-basierte Farbpaletten
- Multi-Field-Modi (N, τ, n)
- Screenshot-Export

## 📊 Erste Schritte - Python

### **1. Grundlegende Berechnung**

```python
from ssz_unified_suite import SSZCore

# SSZ-Kern initialisieren
core = SSZCore()

# Sonnenmasse verwenden
M = core.const.M_SUN

# Grundgrößen berechnen
rs = core.schwarzschild_radius(M)
rphi = core.r_phi(M)

print(f"Schwarzschild-Radius: {rs:.2e} m")
print(f"Natural Boundary: {rphi:.2e} m")
print(f"Verhältnis r_φ/r_s: {rphi/rs:.6f}")
print(f"φ/2: {core.const.PHI/2:.6f}")
```

**Erwartete Ausgabe:**
```
Schwarzschild-Radius: 2.95e+03 m
Natural Boundary: 2.39e+03 m
Verhältnis r_φ/r_s: 0.809017
φ/2: 0.809017
```

### **2. Felder berechnen**

```python
# Test-Radius: 2 × Schwarzschild-Radius
r = 2 * rs

# Segmentdichte
sigma = core.sigma(r, M)
print(f"σ(2r_s) = {sigma:.4f}")  # ≈ 0.5

# Zeitdehnung (α = 1.0)
tau = core.tau(r, M, alpha=1.0)
print(f"τ(2r_s) = {tau:.4f}")  # ≈ 0.7

# Optischer Index (κ = 0.015)
n = core.n_index(r, M, kappa=0.015)
print(f"n(2r_s) = {n:.4f}")  # ≈ 1.0075
```

### **3. Visualisierung erstellen**

```python
from ssz_unified_suite import SSZVisualizer

viz = SSZVisualizer(core)

# Radiale Profile plotten
fig, data = viz.plot_radial_fields(M, alpha=1.0, kappa=0.015)
plt.savefig('ssz_fields.png', dpi=300)

# 3D-Visualisierung
fig_3d = viz.plot_3d_field(M, field_type='sigma')
fig_3d.write_html('ssz_3d.html')

# φ-Euler-Spirale
fig_spiral = viz.plot_euler_spiral()
plt.show()
```

## 🎛️ Interaktive GUI

### **Starten**

```python
python ssz_interactive_gui.py
```

### **Bedienung**

**Parameter-Slider:**
- **Mass [M☉]**: 0.1 - 1000 Sonnenmassen
- **α**: 0.1 - 3.0 (Zeitdilatations-Kopplung)
- **κ**: 0.0 - 0.05 (Optische Kopplung)

**Preset-Buttons:**
- **Sun**: 1 M☉
- **Sgr A***: 4.15×10⁶ M☉
- **Cygnus X-1**: 24 M☉
- **Earth**: 3×10⁻⁶ M☉

**Actions:**
- **🔬 Verify Theory**: Führt Konsistenz-Tests aus
- **📊 Export Data**: Speichert Parameter als JSON
- **🌐 3D Visualization**: Öffnet interaktive Plotly-Ansicht
- **🌀 φ-Euler Spiral**: Zeigt φ-Wachstum

### **Tabs**

1. **📈 Radial Profiles**: σ(r), τ(r), n(r), Dual-Velocity
2. **📊 Parameter Study**: Sensitivitätsanalyse für α und κ

## 🌐 WebGL-Version

### **Browser öffnen**

```
http://localhost:8000
```

### **Kontrollen**

**Kamera:**
- **Rotation**: Linke Maustaste + Ziehen
- **Zoom**: Mausrad
- **Pan**: Rechte Maustaste + Ziehen

**GUI-Panel (rechts):**
- **⚙️ Field Parameters**: α, κ, p, N_max, N_bg
- **🎨 Visualization**: Field Mode, Palette, Wireframe
- **ℹ️ Info**: Mesh-Statistiken

**Field Modes:**
- **N(x)**: Segment Density (Blau)
- **τ(x)**: Time Dilation (Rot)
- **n(x)**: Refractive Index (Grün)

**Paletten:**
- **Turbo**: Google Turbo (Standard)
- **Viridis**: Perceptually uniform
- **Plasma**: Hoher Kontrast
- **Greys**: Monochrom

## 🧪 Tests ausführen

### **Vollständige Test-Suite**

```bash
python ssz_test_suite.py
```

**Test-Kategorien:**
- ✅ Mathematische Konsistenz (φ-Präzision, Grenzwerte)
- ✅ Physikalische Limits (Keine Singularitäten)
- ✅ Numerische Stabilität (Große Massenbereiche)
- ✅ Performance (Geschwindigkeits-Benchmarks)
- ✅ Bekannte Werte (Sonnenmasse, Sgr A*)

**Erwartete Ausgabe:**
```
🧪 SSZ Comprehensive Test Suite
==================================================
📋 Running TestSSZMathematicalConsistency...
  ✅ test_phi_precision
  ✅ test_schwarzschild_radius_scaling
  ✅ test_natural_boundary_ratio
  ...
📊 Test Summary:
Total Tests: 23
Passed: 23
Failed: 0
Success Rate: 100.0%
🎉 All tests passed!
```

## 📁 Projekt-Übersicht

```
SSZ-Complete-Suite/
├── ssz_unified_suite.py          # ⭐ Kern-Implementation
├── ssz_interactive_gui.py        # 🎛️ Desktop-GUI
├── ssz_test_suite.py             # 🧪 Test-Suite
├── segmented-solar-webgl/        # 🌐 WebGL-Version
├── segmented-solar-java/         # ☕ Java-Version
└── README_SSZ_COMPLETE.md        # 📚 Vollständige Doku
```

## 🔬 Wissenschaftliche Anwendungen

### **Beispiel 1: Schwarzes Loch analysieren**

```python
# Sgr A* (supermassives schwarzes Loch)
M_sgr = core.const.M_SGR_A

# Natural Boundary berechnen
rs_sgr = core.schwarzschild_radius(M_sgr)
rphi_sgr = core.r_phi(M_sgr)

print(f"Sgr A* Event Horizon: {rs_sgr/1e9:.2f} Millionen km")
print(f"Sgr A* Natural Boundary: {rphi_sgr/1e9:.2f} Millionen km")

# Zeitdehnung am Event Horizon
tau_horizon = core.tau(rs_sgr * 1.01, M_sgr, alpha=1.0)
print(f"Zeitdehnung bei r_s: τ = {tau_horizon:.4f}")
```

### **Beispiel 2: Lensing-Vorhersage**

```python
# Lichtablenkung durch optischen Index
r_test = 10 * core.schwarzschild_radius(M)
n_value = core.n_index(r_test, M, kappa=0.015)

# Ablenkungswinkel (vereinfacht)
deflection_angle = (n_value - 1) * 2  # Radiant
print(f"Brechungsindex bei 10r_s: n = {n_value:.6f}")
print(f"Geschätzte Ablenkung: {deflection_angle*206265:.2f} arcsec")
```

### **Beispiel 3: Parameter-Studie**

```python
import numpy as np
import matplotlib.pyplot as plt

# α-Variation
alphas = np.linspace(0.1, 3.0, 50)
r_test = 2 * core.schwarzschild_radius(M)

tau_values = [core.tau(r_test, M, alpha) for alpha in alphas]

plt.figure(figsize=(10, 6))
plt.plot(alphas, tau_values, 'r-', linewidth=2)
plt.xlabel('α (Time Dilation Coupling)')
plt.ylabel('τ(2r_s)')
plt.title('Time Dilation Sensitivity to α')
plt.grid(True, alpha=0.3)
plt.show()
```

## 🎯 Häufige Aufgaben

### **Daten exportieren**

```python
from ssz_unified_suite import SSZDataExport

export = SSZDataExport(core)

# Kalibrierungsdaten
calib_data = export.export_calibration_data()
# Speichert: ssz_calibration.json

# Verifikation
export.verify_ssz_predictions()
```

### **Eigene Masse verwenden**

```python
# Beispiel: Neutronenstern (1.4 M☉)
M_neutron = 1.4 * core.const.M_SUN

rs = core.schwarzschild_radius(M_neutron)
rphi = core.r_phi(M_neutron)

# Felder berechnen
r_array = np.logspace(np.log10(rs*1.01), np.log10(rphi*0.99), 1000)
sigma_array = [core.sigma(r, M_neutron) for r in r_array]
```

### **3D-Plot anpassen**

```python
# Höhere Auflösung
fig_3d = viz.plot_3d_field(
    M=core.const.M_SUN,
    field_type='tau',      # 'sigma', 'tau', oder 'n'
    alpha=1.5,             # Zeitdilatations-Parameter
    kappa=0.025,           # Optische Kopplung
    resolution=100         # Mesh-Auflösung (Standard: 50)
)

fig_3d.show()
```

## 🐛 Troubleshooting

### **Problem: Import-Fehler**

```bash
# Lösung: Dependencies installieren
pip install numpy matplotlib plotly scipy pandas
```

### **Problem: GUI startet nicht**

```bash
# Lösung: tkinter installieren (Linux)
sudo apt-get install python3-tk

# macOS (via Homebrew)
brew install python-tk
```

### **Problem: WebGL zeigt nichts**

```
# Lösung: Browser-Konsole prüfen (F12)
# Sicherstellen, dass app.js geladen wurde
# Ggf. CORS-Fehler → Lokalen Server verwenden
```

### **Problem: Maven nicht gefunden**

```bash
# Lösung: Maven installieren
# Ubuntu/Debian
sudo apt-get install maven

# macOS
brew install maven

# Windows
# Download von https://maven.apache.org/
```

## 📚 Weiterführende Ressourcen

### **Dokumentation**
- `README_SSZ_COMPLETE.md`: Vollständige Dokumentation
- `ssz_unified_suite.py`: Docstrings für alle Funktionen
- `ssz_test_suite.py`: Beispiele für Verwendung

### **Theoretische Papers**
1. "Segmented Spacetime and π"
2. "Natural Boundary of Black Holes"
3. "Von Φ-Segmentierung zu Euler"
4. "Solution to the Paradox of Singularities"

### **Online-Ressourcen**
- GitHub Repository: `github.com/your-username/SSZ-complete-suite`
- WebGL Demo: `your-username.github.io/segmented-solar-webgl`
- Java Demo: `your-username.github.io/segmented-solar-java`

## 🎓 Lernpfad

### **Anfänger**
1. ✅ `ssz_unified_suite.py` ausführen
2. ✅ Grundlegende Berechnungen verstehen
3. ✅ Interaktive GUI erkunden
4. ✅ WebGL-Version im Browser testen

### **Fortgeschritten**
1. ✅ Eigene Massen und Parameter testen
2. ✅ Parameter-Studien durchführen
3. ✅ 3D-Visualisierungen anpassen
4. ✅ Test-Suite erweitern

### **Experte**
1. ✅ Neue Felder implementieren
2. ✅ GPU-Shader optimieren
3. ✅ Astronomische Daten integrieren
4. ✅ Wissenschaftliche Papers schreiben

## 🚀 Nächste Schritte

Nach dem Schnellstart:

1. **Experimentieren**: Parameter variieren und Effekte beobachten
2. **Visualisieren**: Eigene Plots und 3D-Ansichten erstellen
3. **Verifizieren**: Test-Suite ausführen und verstehen
4. **Erweitern**: Neue Features implementieren
5. **Publizieren**: Ergebnisse teilen und diskutieren

---

## 🌟 Zusammenfassung

**3 Wege zur SSZ-Exploration:**

1. **Python**: `python ssz_interactive_gui.py` → Desktop-App
2. **WebGL**: `http://localhost:8000` → Browser-3D
3. **Java**: `mvn package` → TeaVM-Version

**Alle implementieren:**
- ✅ Vollständige SSZ-Mathematik (σ, τ, n)
- ✅ Interaktive Parameter-Kontrollen
- ✅ Wissenschaftliche Visualisierungen
- ✅ Verifikations-Tests

**🌌 Viel Erfolg beim Erkunden der segmentierten Raumzeit!**

*Implementiert das vollständige Casu & Wrede Framework • Wissenschaftlich validiert • Open Source*
