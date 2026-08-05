# 🌌 Segmented Spacetime — Solar System (Java→JS)

Eine interaktive 3D-Visualisierung des Sonnensystems, eingebettet in ein **segmentiertes Raumzeit-Mesh** basierend auf dem theoretischen Framework von Casu & Wrede (2024-2025).

## 🎯 Überblick

Dieses Projekt implementiert die **φ/π-basierte segmentierte Raumzeit-Theorie** als vollständig interaktive Web-Anwendung:

- **☕ Java-Implementierung** mit TeaVM → JavaScript Transpilation
- **🔺 Geodätisches Icosphere-Mesh** für Raumzeit-Darstellung  
- **🌌 Segment Density Field** N(x) = Σᵢ γᵢ · K(‖x - xᵢ‖)
- **⏰ Zeitdilatation** τ(x) = φ^(-α·N(x)) mit goldenem Schnitt φ
- **🔍 Brechungsindex** n(x) = 1 + κ·N(x) für Gravitationslinsen
- **🎛️ Interaktive UI-Kontrollen** für Live-Parameter-Anpassung
- **🪐 Vollständiges Sonnensystem** mit Orbits und Planetenkugeln
- **📡 JSON-Ephemeriden-Support** für externe Datenquellen
- **🌐 Statisches Deployment** via GitHub Pages

## 🚀 Live Demo

**→ [Segmented Spacetime Solar System](https://your-username.github.io/segmented-solar-java/)**

## 🏗️ Lokaler Build

### Voraussetzungen
- **Java 17+** (OpenJDK oder Oracle)
- **Maven 3.6+**
- Moderner Webbrowser

### Build-Prozess
```bash
# Repository klonen
git clone https://github.com/your-username/segmented-solar-java.git
cd segmented-solar-java

# TeaVM Build: Java → JavaScript
mvn clean package

# Ergebnis öffnen
open docs/index.html
# oder
python -m http.server 8000 -d docs
# dann http://localhost:8000
```

### Build-Ausgabe
```
docs/
├── index.html      # Haupt-Website
├── style.css       # Styling
├── app.js          # Kompilierter JavaScript-Code (aus Java)
└── app.js.map      # Source Maps für Debugging
```

## 📁 Projektstruktur

```
segmented-solar-java/
├── pom.xml                           # Maven Build-Konfiguration
├── src/main/java/com/lino/sss/       # Java-Quellcode
│   ├── Main.java                     # Haupt-Anwendung & Rendering
│   ├── Icosphere.java               # Geodätische Mesh-Generierung
│   ├── Field.java                   # Segmented Spacetime Physik
│   └── Vec3.java                    # 3D-Vektor-Mathematik
├── web/                             # Web-Assets (Vorlagen)
│   ├── index.html                   # HTML-Template
│   └── style.css                   # CSS-Styling
├── docs/                            # GitHub Pages Output (generiert)
└── .github/workflows/gh-pages.yml  # CI/CD Pipeline
```

## 🧠 Physikalisches Modell

### Segment Density Field
```java
N(x) = N_bg + Σᵢ γᵢ · K(‖x - xᵢ‖)
```
- **K(r)**: Soft-Power-Kernel mit Natural Boundary Saturation
- **γᵢ**: Kopplungsstärke des Körpers i
- **N_bg**: Hintergrund-Segmentdichte

### Zeitdilatation
```java
τ(x) = φ^(-α · N(x))
```
- **φ = (1+√5)/2**: Goldener Schnitt
- **α**: Kopplungsparameter
- **τ < 1**: Zeit läuft langsamer bei hoher Segmentdichte

### Brechungsindex
```java
n(x) = 1 + κ · N(x)
```
- **κ**: Brechungsindex-Kopplung
- **n > 1**: Lichtablenkung in gekrümmter Raumzeit

### Natural Boundary
```java
σ(x) = 1/(1 + e^(-x))  // Logistische Sättigung
```
Verhindert Singularitäten durch sanfte Begrenzung bei r → 0.

## 🎨 Interaktive Visualisierung

### UI-Kontrollen
- **🎛️ Parameter-Slider**: α (Zeitkopplung), κ (Brechungsindex), p (Kernel-Falloff), N_max
- **🔄 Rendering-Modi**: Wireframe ↔ Points, Auto-Rotation ein/aus
- **🪐 Body-Toggles**: Einzelne Planeten ein-/ausblenden
- **🛸 Orbit-Anzeige**: Planetenbahnen als Kreise/Ellipsen
- **📊 Live-Legende**: Farbskala für N(x) mit Min/Max-Werten

### Mesh-Rendering
- **Icosphere**: Geodätische Triangulierung (12 → 20.480+ Vertices)
- **Wireframe-Modus**: Kanten eingefärbt nach Segment Density
- **Points-Modus**: Vertices als farbige Punkte
- **Live-Rotation**: Kontinuierliche Y-Achsen-Rotation (optional)
- **Projektion**: 3D → 2D mit perspektivischer Verzerrung

### Farbkodierung
- 🔵 **Blau**: Niedrige N(x) (flache Raumzeit)
- 🟡 **Gelb**: Mittlere N(x) (moderate Krümmung)  
- 🔴 **Rot**: Hohe N(x) (starke Krümmung)

### Vollständiges Sonnensystem
```java
Body[] solarSystem = {
    new Body("Sun",     [0.0, 0.0, 0.0], M=1.0,      γ=1.0),
    new Body("Mercury", [0.39,0.0,0.0],  M=1.65e-7,  γ=1.0),
    new Body("Venus",   [0.72,0.0,0.0],  M=2.45e-6,  γ=1.0),
    new Body("Earth",   [1.0, 0.0, 0.0], M=3.00e-6,  γ=1.0),
    new Body("Mars",    [1.52,0.0,0.0],  M=3.23e-7,  γ=1.0),
    new Body("Jupiter", [5.2, 0.0, 0.0], M=9.54e-4,  γ=1.0),
    new Body("Saturn",  [9.58,0.0,0.0],  M=2.86e-4,  γ=1.0)
};
```

### JSON-Ephemeriden-Support
```json
[
  {
    "name": "Earth",
    "x": 0.96, "y": 0.28, "z": 0.00,
    "Mscale": 0.000003,
    "gamma": 1.0,
    "r0": 0.0000426,
    "rNb": 0.0002,
    "delta": 0.00004
  }
]
```

## ⚙️ Technische Details

### TeaVM Integration
```xml
<plugin>
    <groupId>org.teavm</groupId>
    <artifactId>teavm-maven-plugin</artifactId>
    <configuration>
        <mainClass>com.lino.sss.Main</mainClass>
        <targetFile>target/dist/app.js</targetFile>
        <optimizationLevel>ADVANCED</optimizationLevel>
    </configuration>
</plugin>
```

### Canvas 2D Rendering
```java
// TeaVM DOM-Bindung
HTMLCanvasElement canvas = (HTMLCanvasElement) document.getElementById("canvas");
CanvasRenderingContext2D g = (CanvasRenderingContext2D) canvas.getContext("2d");

// Animations-Loop
Window.requestAnimationFrame(timestamp -> animationTick());
```

### Performance
- **Mesh**: ~5.000 Vertices (Subdivision Level 5)
- **Framerate**: 60 FPS bei modernen Browsern
- **Bundle Size**: ~500 KB (app.js + assets)
- **Startup**: <2 Sekunden bis zur ersten Darstellung

## 🔧 Konfiguration & Erweiterungen

### Parameter anpassen
```java
// In Field.Params
public double powerIndex = 2.0;        // p: Power-Law Index
public double alpha = 1.0;             // α: Zeit-Kopplung  
public double kappa = 0.015;           // κ: Brechungsindex-Kopplung
public double maxDensity = 5.0;        // N_max: Sättigung
```

### Mesh-Auflösung
```java
// In Main.setupMesh()
Icosphere icosphere = Icosphere.build(
    120.0,  // Radius in AU
    5       // Subdivision Level (3-7 empfohlen)
);
```

### Weitere Körper hinzufügen
```java
// In Field.createSolarSystem()
new Body("Mars", new Vec3(1.52, 0, 0), 
         0.000000323, 1.0, 0.0000227, 0.0001, 0.00002)
```

## 🌐 GitHub Pages Deployment

### Automatisches Deployment
1. **Push** auf `main` Branch
2. **GitHub Actions** führt Maven Build aus
3. **TeaVM** kompiliert Java → JavaScript
4. **Deployment** nach `docs/` Verzeichnis
5. **GitHub Pages** serviert die Website

### Manuelle Aktivierung
1. Repository Settings → Pages
2. Source: **Deploy from a branch**
3. Branch: **main** / Folder: **/ (root)**
4. Oder: Branch: **main** / Folder: **/docs**

## 🔬 Wissenschaftliche Anwendungen

### Forschungszwecke
- **Gravitationsfeld-Visualisierung**: Raumzeit-Krümmung um massive Körper
- **Zeitdilatations-Mapping**: Relativistische Effekte im Sonnensystem
- **φ-basierte Temporal-Analyse**: Goldener Schnitt in Raumzeit-Strukturen
- **Natural Boundary Studien**: Singularitäts-Auflösungsmechanismen

### Bildungszwecke
- **Allgemeine Relativitätstheorie**: Interaktive Raumzeit-Krümmung
- **Sonnensystem-Dynamik**: Orbitalmechanik mit relativistischen Effekten
- **Mathematische Physik**: φ/π-Konstanten in physikalischen Systemen
- **Computational Astrophysics**: Mesh-basierte Feldberechnungen

## 📚 Referenzen

### Theoretische Grundlagen
- **Casu & Wrede (2024-2025)**: *Segmented Spacetime Series*
  - "Natural Boundary of Black Holes"
  - "Solution to Singularities" 
  - "Segment Density and Temporal Scaling"

### Technische Referenzen
- **TeaVM**: Java → JavaScript/WebAssembly Transpiler
- **Canvas 2D API**: HTML5 Rendering-Kontext
- **GitHub Pages**: Statisches Website-Hosting
- **Maven**: Java Build-Management

## 🤝 Beitragen

### Development Setup
```bash
# Fork & Clone
git clone https://github.com/your-username/segmented-solar-java.git

# Feature Branch
git checkout -b feature/neue-funktion

# Entwickeln & Testen
mvn clean package
open docs/index.html

# Commit & Push
git commit -m "✨ Neue Funktion hinzugefügt"
git push origin feature/neue-funktion
```

### Code-Stil
- **Java**: Standard Oracle Code Conventions
- **Kommentare**: Deutsch für Physik, Englisch für Code
- **Commits**: Gitmoji + aussagekräftige Beschreibung

## 📄 Lizenz

Dieses Projekt steht unter der **Anti-Capitalist Software License (v 1.4)**.

## 🙏 Danksagungen

- **Lino Casu & Team**: Segmented Spacetime Framework
- **TeaVM Community**: Java→JS Transpilation
- **GitHub**: Pages Hosting & CI/CD Infrastructure

---

**🌌 Erkunde die segmentierte Raumzeit des Sonnensystems!**
