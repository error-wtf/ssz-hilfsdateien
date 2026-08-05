# Ring-Temperatur → Geschwindigkeit Integration

## 📊 Übersicht

Die Ring-Temperatur-Analyse wurde vollständig in die Summary-Pipeline integriert. Sie berechnet Geschwindigkeitsprofile aus Temperaturverhältnissen zwischen Ringen basierend auf dem Modell:

```
v_k = v_{k-1} · q_k^{-1/2}
```

wo `q_k = T_k / T_{k-1}` das Temperaturverhältnis ist.

## 🔧 Integration

### In `ci/summary-all-tests.py`

**Neue Funktionen** (Zeile ~226-296):
- `compute_ring_velocity_from_temperature()` - Berechnet v_pred aus T_proxy
- `render_ring_section_markdown()` - Generiert Markdown-Tabelle

**Neue Parameter**:
- `--rings-csv` - Pfad zum Ring-CSV (Spalten: `ring`, `T_proxy_K`, optional `v_obs_kms`)
- `--rings-v0` - Baseline-Geschwindigkeit bei Ring 0 (Default: 10.0 km/s)

**Workflow** (Zeile ~330-369):
1. Ring-CSV einlesen
2. Temperaturverhältnisse berechnen (`q_k`)
3. Geschwindigkeiten vorwärts propagieren (`v_pred_kms`)
4. Optional: Residuen zu beobachteten Werten (`v_obs_kms`)
5. Artefakte speichern in `<output_dir>/ring_temp2v/`

## 📁 CSV-Format

### Minimales Format
```csv
ring,T_proxy_K
0,500.0
1,480.0
2,460.0
```

### Mit beobachteten Geschwindigkeiten
```csv
ring,T_proxy_K,v_obs_kms
0,500.0,10.0
1,480.0,10.5
2,460.0,11.0
```

## 🚀 Verwendung

### Manueller Aufruf
```powershell
cd H:\WINDSURF\Segmented-Spacetime-Mass-Projection-Unified-Results_bak_2025-10-17_17-03-00

# Mit Ring-CSV
python ci/summary-all-tests.py `
  --run-dir . `
  --run-id <run_id> `
  --out reports/<run_id>/output-summary.md `
  --rings-csv data/example_rings.csv `
  --rings-v0 10.0
```

### Automatische Integration

Die Ring-Analyse wird automatisch ausgeführt, wenn `--rings-csv` übergeben wird. Die Suite-Integration ist in `ci/autorun_suite.py` möglich:

```python
# In ci/autorun_suite.py, bei summary-all-tests.py Aufruf:
cmd = [
    sys.executable, "-X", "utf8", str(summary_script),
    "--run-dir", str(ROOT),
    "--run-id", run_id,
    "--out", str(md_out),
    "--rings-csv", "data/example_rings.csv",  # ← hinzufügen
    "--rings-v0", "10.0"                       # ← hinzufügen
]
```

## 📤 Output

### Markdown-Report

Die Ring-Sektion erscheint **ganz oben** in `output-summary.md`:

```markdown
## Ring-Temperatur → Geschwindigkeitsprofil (Section 4.6)

_Eingang_: pro Ring Temperatur-Proxy `T_proxy_K`, Vorwärtsmodell `v_k = v_{k-1} · q_k^{-1/2}` mit `q_k = T_k/T_{k-1}`.

| ring | T_proxy_K | q_k | v_pred_kms | v_obs_kms | residual_kms |
| --- | --- | --- | --- | --- | --- |
| 0 | 500 | nan | 10 | 10 | 0 |
| 1 | 480 | 0.96 | 10.206 | 10.5 | 0.294 |
| 2 | 460 | 0.958 | 10.423 | 11 | 0.577 |

**Δv_gesamt** = 0.423 km/s &nbsp;&nbsp;•&nbsp;&nbsp; **Faktor** = 1.042×
**MAE** (wo beobachtet) = 0.435 km/s
```

### Artefakte

```
reports/<run_id>/ring_temp2v/
├── ring_results.csv    → Vollständige Tabelle mit allen Spalten
└── ring_summary.json   → Zusammenfassung (delta_v, ratio, mae, etc.)
```

**ring_summary.json** Format:
```json
{
  "delta_v_kms": 0.423,
  "velocity_ratio": 1.042,
  "mae_kms": 0.435,
  "v0_kms": 10.0,
  "num_rings": 3
}
```

## 🛡️ Fehlerbehandlung

| Situation | Verhalten |
|-----------|-----------|
| pandas/numpy fehlt | Warnung, Ring-Sektion mit Hinweis |
| CSV nicht gefunden | Warnung, Ring-Sektion mit Pfad-Info |
| Falsche Spalten | Exception, Ring-Sektion mit Fehler |
| `--rings-csv` nicht übergeben | Ring-Analyse übersprungen |

## 📊 Visualisierung (Optional)

Falls `ci/summary_visualize.py` erweitert wird, können Plots hinzugefügt werden:

```python
# In summary_visualize.py
def plot_ring_velocity(ring_csv: Path, assets_dir: Path):
    df = pd.read_csv(ring_csv)
    
    # Plot 1: v_pred vs Ring
    plt.figure()
    plt.plot(df["ring"], df["v_pred_kms"], marker="o")
    plt.xlabel("Ring Index")
    plt.ylabel("v_pred [km/s]")
    plt.title("Ring: Predicted Velocity Profile")
    plt.savefig(assets_dir / "ring_vpred.png", dpi=150)
    
    # Plot 2: v_pred vs v_obs (falls vorhanden)
    if "v_obs_kms" in df.columns:
        plt.figure()
        plt.plot(df["ring"], df["v_pred_kms"], "o-", label="v_pred")
        plt.plot(df["ring"], df["v_obs_kms"], "x-", label="v_obs")
        plt.xlabel("Ring Index")
        plt.ylabel("Velocity [km/s]")
        plt.title("Ring: Predicted vs Observed")
        plt.legend()
        plt.savefig(assets_dir / "ring_pred_obs.png", dpi=150)
```

## 🔬 Physikalischer Hintergrund

Das Modell basiert auf der Annahme, dass:
1. Temperatur und Geschwindigkeit über einen Power-Law gekoppelt sind
2. `v ∝ T^{-1/2}` (aus v_therm ~ √T für thermische Bewegung)
3. Das Verhältnis zwischen benachbarten Ringen propagiert sich vorwärts

**Anwendungen**:
- Akkretionsscheiben (radiale Geschwindigkeitsprofile)
- Galaxien-Rotationskurven (falls T als Proxy für Potentialtiefe)
- Protoplanetare Scheiben (Temperatur-Gradienten → Geschwindigkeit)

## 🆘 Troubleshooting

### "pandas required for ring temperature analysis"
→ Installieren: `pip install pandas numpy`

### Leere Tabelle in Markdown
→ CSV-Format prüfen (Header: `ring,T_proxy_K`)

### MAE = None
→ Keine `v_obs_kms` Spalte im CSV oder alle NaN

### Plots fehlen
→ Optional, nur mit `summary_visualize.py` + matplotlib

---

**Erstellt**: 2025-10-17  
**Version**: 1.0  
**Status**: ✅ Integriert in ci/summary-all-tests.py
