# Extended Metrics Integration - Sichere Anleitung

**Datum:** 2025-10-18  
**Ziel:** Erweiterte Metriken + Plots am Ende von `run_all_ssz_terminal.py` ergänzen

---

## ✅ **Was bereits erstellt wurde:**

1. ✅ `core/stats.py` - Statist\-Modul mit:
   - `compute_ring_metrics()` - Berechnet γ, Δv, E_k
   - `export_ring_metrics_csv()` - Schreibt Metriken als CSV
   - `correlation_summary()` - Fit-Qualität (r(v,T), MAE, RMSE)
   - `residuals()` - Modell-Beobachtungs-Differenzen

2. ✅ `tools/figure_catalog.py` - Bereits vorhanden
3. ✅ `tools/plots.py` - Bereits vorhanden
4. ✅ `tools/io_utils.py` - Bereits vorhanden

---

## 🎯 **Was jetzt zu tun ist:**

**NUR** `run_all_ssz_terminal.py` erweitern - **NICHTS ANDERES ÄNDERN!**

---

## 📝 **Einfügeblock für run_all_ssz_terminal.py**

**Position:** Ganz am Ende der Datei (nach Zeile 730)

```python
# ==============================================================================
# EXTENDED METRICS & PLOTS (Nur wenn gewünscht)
# ==============================================================================

def _finalize_extended_outputs():
    """
    OPTIONAL: Erweiterte Metriken, Statistiken und Zusatzplots erzeugen.
    
    Wird NUR ausgeführt wenn:
    - Umgebungsvariable SSZ_EXTENDED_METRICS=1 gesetzt ist
    - Oder wenn explizit aus anderem Skript aufgerufen
    
    ÄNDERT NICHTS an der bestehenden Pipeline!
    """
    import os
    
    # Nur ausführen wenn explizit angefordert
    if not os.environ.get("SSZ_EXTENDED_METRICS", "").strip() == "1":
        return  # Nichts tun, normal beenden
    
    print("\n" + "="*80)
    print("[SSZ EXTENDED] Generating extended metrics and plots...")
    print("="*80)
    
    try:
        from pathlib import Path
        import numpy as np
        from core.stats import compute_ring_metrics, export_ring_metrics_csv, correlation_summary, residuals
        from tools.plots import line, scatter, hist
        from tools.io_utils import update_manifest, sha256_file
        
        # Beispiel-Daten (ERSETZEN durch echte Pipeline-Daten!)
        # Diese Werte müssen aus der tatsächlichen Pipeline kommen
        example_obj = "TestObject"
        example_ring_data = {
            "k": np.arange(10),
            "T": 50 + 10 * np.random.rand(10),  # Temperaturen
            "n": 1000 + 500 * np.random.rand(10),  # Dichten
            "v": 10 + 5 * np.random.rand(10),  # Geschwindigkeiten
        }
        
        # 1) Metriken berechnen
        metrics = compute_ring_metrics(
            k=example_ring_data["k"],
            T=example_ring_data["T"],
            n=example_ring_data["n"],
            v=example_ring_data["v"]
        )
        
        # 2) CSV exportieren
        csv_metrics = export_ring_metrics_csv(example_obj, metrics, outdir="reports/data")
        csv_stats = correlation_summary(example_obj, metrics, outdir="reports/stats")
        
        print(f"[SSZ EXTENDED] Metrics CSV: {csv_metrics}")
        print(f"[SSZ EXTENDED] Stats CSV: {csv_stats}")
        
        # 3) Plots erzeugen (optional)
        fig_formats = ("png", "svg")
        fig_dpi = 600
        fig_width_mm = 160
        fig_root = "reports/figures"
        
        all_paths = []
        
        # Plot 1: v vs k
        base = str(Path(fig_root) / example_obj / f"fig_{example_obj}_ringchain_v_vs_k")
        paths = line(
            metrics["k"], metrics["v"],
            "Ring index k", "Velocity v_k [km/s]",
            f"{example_obj}: Ring-chain velocity",
            base, formats=fig_formats, dpi=fig_dpi, width_mm=fig_width_mm
        )
        all_paths.extend(paths)
        
        # Plot 2: log(γ) vs k
        base = str(Path(fig_root) / example_obj / f"fig_{example_obj}_gamma_log_vs_k")
        paths = line(
            metrics["k"], metrics["log_gamma"],
            "Ring index k", "log γ",
            f"{example_obj}: Cumulative time-density",
            base, formats=fig_formats, dpi=fig_dpi, width_mm=fig_width_mm
        )
        all_paths.extend(paths)
        
        # Plot 3: Residuen-Histogramm (Beispiel)
        res = np.random.randn(len(metrics["v"])) * 0.5  # Dummy-Residuen
        base = str(Path(fig_root) / example_obj / f"fig_{example_obj}_residuals_histogram")
        paths = hist(
            res, "Residual [km/s]",
            f"{example_obj}: Residuals",
            base, formats=fig_formats, dpi=fig_dpi, width_mm=fig_width_mm
        )
        all_paths.extend(paths)
        
        print(f"[SSZ EXTENDED] Generated {len(all_paths)} figure files")
        for p in all_paths:
            print(f"  - {p}")
        
        # 4) Manifest aktualisieren
        arts = []
        for path in [csv_metrics, csv_stats]:
            arts.append({
                "role": "table",
                "path": Path(path).as_posix(),
                "sha256": sha256_file(path),
                "format": "csv"
            })
        for path in all_paths:
            arts.append({
                "role": "figure",
                "path": Path(path).as_posix(),
                "sha256": sha256_file(path),
                "format": Path(path).suffix[1:]
            })
        
        update_manifest("reports/PAPER_EXPORTS_MANIFEST.json", {"artifacts": arts})
        print("[SSZ EXTENDED] Manifest updated: reports/PAPER_EXPORTS_MANIFEST.json")
        
        print("="*80)
        print("[SSZ EXTENDED] COMPLETE!")
        print("="*80)
        
    except Exception as e:
        print(f"[SSZ EXTENDED] WARNING: Extended metrics failed: {e}")
        print("[SSZ EXTENDED] Continuing without extended outputs...")
        # Nicht abbrechen, nur warnen

# Aufruf am Ende (OPTIONAL, tut nichts wenn nicht explizit aktiviert)
if __name__ == "__main__":
    _finalize_extended_outputs()
```

---

## 🔧 **Wie aktivieren:**

### **Standardmodus (KEINE Änderung):**
```bash
python run_all_ssz_terminal.py
```
→ Läuft wie bisher, **KEINE** erweiterten Metriken

### **Erweiterte Metriken aktivieren:**
```bash
# Windows PowerShell:
$env:SSZ_EXTENDED_METRICS="1"
python run_all_ssz_terminal.py

# Linux/Mac:
export SSZ_EXTENDED_METRICS=1
python run_all_ssz_terminal.py
```
→ Erzeugt **zusätzlich**: Metriken-CSVs + Plots

---

## ⚠️ **Wichtige Hinweise:**

### **Sicherheit:**
1. ✅ **Bestehende Pipeline unberührt** - Nur Ergänzung am Ende
2. ✅ **Standard-Verhalten gleich** - Keine Änderung ohne Flag
3. ✅ **Fehler isoliert** - Exception Handler verhindert Absturz
4. ✅ **Keine globalen Änderungen** - Alles in eigener Funktion

### **Datenintegration:**
Der obige Code verwendet **Beispieldaten**. Für echte Integration:

```python
# ERSETZEN:
example_ring_data = {
    "k": np.arange(10),
    "T": 50 + 10 * np.random.rand(10),
    # ...
}

# DURCH echte Pipeline-Daten:
# (Falls verfügbar in run_all_ssz_terminal.py)
ring_data = {
    "k": ... # aus Pipeline
    "T": ... # aus Pipeline
    "n": ... # aus Pipeline
    "v": ... # aus Pipeline
}
```

---

## 📊 **Erzeugte Outputs:**

```
reports/
├─ data/
│  └─ TestObject_ring_metrics.csv       ← Metriken (k, T, n, v, γ, log γ, Δv, E)
├─ stats/
│  └─ TestObject_fit_summary.csv        ← Statistiken (r(v,T), MAE, RMSE)
└─ figures/
   └─ TestObject/
      ├─ fig_TestObject_ringchain_v_vs_k.png|svg
      ├─ fig_TestObject_gamma_log_vs_k.png|svg
      └─ fig_TestObject_residuals_histogram.png|svg
```

---

## 🎯 **Zusammenfassung:**

| Aktion | Geändert? | Risiko |
|--------|-----------|--------|
| `core/stats.py` erstellen | ✅ Neu | ✅ Sicher (neues Modul) |
| `run_all_ssz_terminal.py` erweitern | ✅ Nur am Ende | ✅ Sicher (isoliert) |
| Bestehende Pipeline | ❌ NEIN | ✅ Keine Änderung |
| Standard-Verhalten | ❌ NEIN | ✅ Nur mit Flag aktiv |

---

## ✅ **Ready to integrate!**

**Nächster Schritt:** Code-Block am Ende von `run_all_ssz_terminal.py` einfügen.

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
