# 🌌 SSZ Full Pipeline - Google Colab

**One-Click Ausführung der kompletten SSZ Pipeline in Google Colab!**

---

## 🚀 Quick Start

### **Methode 1: Direkter Link (Empfohlen)**

Öffne das Notebook direkt in Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/SSZ_Full_Pipeline_Colab.ipynb)

### **Methode 2: Manuell**

1. Gehe zu: https://colab.research.google.com/
2. Klicke: `File` → `Open notebook` → `GitHub`
3. Gib ein: `error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results`
4. Wähle: `SSZ_Full_Pipeline_Colab.ipynb`

---

## 📋 Was macht das Notebook?

Das Colab-Notebook führt automatisch aus:

1. **📦 Installation** - Alle Dependencies (numpy, scipy, pandas, matplotlib, astropy)
2. **📥 Git Clone** - Repository von GitHub
3. **🔧 Konfiguration** - Umgebungsvariablen für Pipeline
4. **🚀 Pipeline-Run** - Vollständige SSZ-Analyse (~5-10 min)
5. **📊 Ergebnisse** - Reports, Plots, Statistiken
6. **💾 Download** - ZIP-Archiv mit allen Ergebnissen

---

## ⚙️ Konfiguration

Am Anfang des Notebooks kannst du folgende Optionen anpassen:

```python
# Pipeline Optionen
ENABLE_EXTENDED_METRICS = True  # Extended Metrics (Plots, Stats)
ENABLE_SEGMENT_REDSHIFT = True  # Segment-Redshift Add-on
```

### **Features:**

#### **Extended Metrics** (`SSZ_EXTENDED_METRICS=1`)
- Zusätzliche Plots (Velocity vs. Ring, Gamma vs. Ring, etc.)
- Erweiterte Statistiken (Pearson Correlation, MAE, RMSE)
- Segment Energy Plots

#### **Segment-Redshift Add-on** (`SSZ_SEGMENT_REDSHIFT=1`)
- Gravitationelle Rotverschiebung basierend auf Segment-Dichte
- 3 Proxy-Modi: N, rho-pr, gtt
- Band-Klassifikation (Radio/MW/IR/Vis/UV/X-ray/Gamma)
- Optional: Redshift-Profile Plot

---

## 🎯 One-Click Ausführung

**Alle Zellen auf einmal ausführen:**

1. Öffne Notebook in Colab
2. Klicke: `Runtime` → `Run all` (oder `Strg+F9`)
3. Warte ~5-10 Minuten
4. ✅ Fertig!

**Oder Schritt-für-Schritt:**

Führe jede Zelle einzeln aus mit dem ▶️ Button.

---

## 📊 Generierte Ergebnisse

Nach dem Lauf werden folgende Dateien generiert:

### **Reports:**
```
reports/
├── full-output.md              # Kompletter Pipeline-Output
├── summary-output.md           # Detaillierte Logs
├── RUN_SUMMARY.md              # Kompakte Zusammenfassung
├── segment_redshift.csv        # Redshift-Ergebnisse
└── segment_redshift.md         # Redshift-Report
```

### **Plots:**
```
reports/figures/
├── fig_shared_segment_redshift_profile.png
├── DemoObject/
│   ├── fig_DemoObject_ringchain_v_vs_k.png
│   ├── fig_DemoObject_gamma_log_vs_k.png
│   └── ...
└── demo/
    └── ...

out/
├── phi_step_residual_hist.png
├── phi_step_residual_abs_scatter.png
└── ...
```

### **CSV-Daten:**
```
reports/
├── g79_test.csv
├── cygx_test.csv
└── ring_chain.csv
```

---

## 💾 Download Ergebnisse

Das Notebook erstellt automatisch ein **ZIP-Archiv** mit allen Ergebnissen:

- `SSZ_Results_YYYYMMDD_HHMMSS.zip`

**Enthält:**
- Alle Reports (Markdown + CSV)
- Alle Plots (PNG + SVG)
- Output-Logs

---

## ⏱️ Laufzeit

**Geschätzte Zeiten (auf Colab Standard-Hardware):**

| Phase | Dauer |
|-------|-------|
| Dependencies Installation | ~1 min |
| Repository Clone | ~30 sec |
| Tests (67 Tests) | ~1-2 min |
| SSZ Analyse | ~2-3 min |
| Extended Metrics | ~1 min |
| Segment-Redshift | ~30 sec |
| **Gesamt** | **~5-10 min** |

**Mit GPU/TPU:** Keine signifikante Beschleunigung (CPU-bound)

---

## 🔧 Troubleshooting

### **Problem: "ModuleNotFoundError"**
**Lösung:** Stelle sicher, dass die Dependencies-Zelle ausgeführt wurde.

### **Problem: "Repository not found"**
**Lösung:** Prüfe den `REPO_URL` in der Konfigurations-Zelle.

### **Problem: "Quelle fehlt" bei Segment-Redshift**
**Lösung:** Stelle sicher, dass `ENABLE_EXTENDED_METRICS = True` gesetzt ist.

### **Problem: Plots werden nicht angezeigt**
**Lösung:** Installiere Pillow: `!pip install pillow`

---

## 📚 Pipeline-Übersicht

### **Tests:**
- **35 Physik-Tests** mit detaillierten physikalischen Interpretationen
- **23 Technische Tests** (silent mode)

### **Analysen:**
- PPN-Parameter (β, γ)
- Energie-Bedingungen (WEC, DEC, SEC)
- Dual-Velocity Invariant
- Segment-Kontinuität (C1, C2)
- Metric-Properties
- Redshift-Analyse

### **Outputs:**
- Markdown Reports
- CSV-Tabellen
- PNG/SVG Plots
- JSON Manifests

---

## 🌐 Colab-Vorteile

✅ **Keine lokale Installation nötig**  
✅ **Kostenlose GPU/TPU (optional)**  
✅ **Automatisches Dependency Management**  
✅ **Reproduzierbare Umgebung**  
✅ **Direkt teilbar (Link)**  
✅ **Integration mit Google Drive (optional)**

---

## 🔗 Weiterführende Links

- **GitHub Repository:** https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
- **Lokale Installation:** Siehe `README.md`
- **Pipeline-Dokumentation:** Siehe `OUTPUT_LOGS_README.md`
- **Add-ons:** Siehe `scripts/addons/README.md`

---

## 🤝 Beitragen

Fragen oder Verbesserungsvorschläge für das Colab-Notebook?

Erstelle ein Issue oder Pull Request auf GitHub!

---

## 📝 Lizenz

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Das Colab-Notebook ist frei verwendbar für wissenschaftliche und nicht-kommerzielle Zwecke!**

---

## 🎓 Zitierung

Wenn du die SSZ Pipeline in deiner Forschung verwendest, zitiere bitte:

```bibtex
@software{ssz_pipeline_2025,
  author = {Wrede, Carmen and Casu, Lino},
  title = {Segmented Spacetime Mass Projection - Unified Results},
  year = {2025},
  url = {https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results}
}
```

---

**Happy Computing! 🚀**
