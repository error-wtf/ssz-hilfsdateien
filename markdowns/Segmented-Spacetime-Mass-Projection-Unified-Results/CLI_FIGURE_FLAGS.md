# CLI Figure Flags - Integration Guide

**Status:** Ready for copy-paste into CLI scripts  
**Target Files:** `cli/ssz_rings.py`, `run_all_ssz_terminal.py`

---

## 1. Add Argparse Flags

**In your argparse setup (e.g., `cli/ssz_rings.py`):**

```python
# --- Figure Generation Flags ---
parser.add_argument("--fig", action="store_true",
                    help="Erzeuge Abbildungen (PNG+SVG)")

parser.add_argument("--fig-formats", default="png,svg",
                    help="Kommagetrennte Formate: png,svg (Standard: png,svg)")

parser.add_argument("--fig-dpi", type=int, default=600,
                    help="PNG-Auflösung in DPI (Standard: 600)")

parser.add_argument("--fig-width-mm", type=float, default=160.0,
                    help="Figur-Breite in Millimetern (160mm = 2-Spalten, 84mm = 1-Spalte)")

parser.add_argument("--fig-out", default="reports/figures",
                    help="Wurzelordner für Abbildungen (Standard: reports/figures)")
```

---

## 2. Usage in Pipeline

**At the end of your analysis pipeline:**

```python
# --- Example: In run_all_ssz_terminal.py or cli/ssz_rings.py ---

if args.fig:
    from tools.figure_orchestrator import finalize_figures
    import numpy as np
    
    # Prepare datasets
    datasets = {
        "k": ring_indices,                    # Ring numbers [1, 2, 3, ...]
        "v": velocities,                      # Velocities [km/s]
        "log_gamma": np.log(gamma),           # Log of cumulative gamma
        "gamma": gamma,                       # Cumulative gamma
        "nu_out": nu_out                      # Output frequencies [Hz]
    }
    
    # Infer object name from input
    obj_name = infer_object_name(args)  # e.g., "G79" from CSV filename
    
    # Generate figures + index + manifest
    finalize_figures(args, obj_name, datasets)
```

---

## 3. Example Command Line

```bash
# Basic usage (default settings)
python -m cli.ssz_rings --csv data/observations/G79.csv --v0 12.5 --fig

# Custom settings
python -m cli.ssz_rings \
  --csv data/observations/G79.csv \
  --v0 12.5 \
  --fig \
  --fig-formats png,svg \
  --fig-dpi 600 \
  --fig-width-mm 160 \
  --fig-out reports/figures

# High-resolution for print
python -m cli.ssz_rings \
  --csv data/observations/CygnusX.csv \
  --v0 1.3 \
  --fig \
  --fig-dpi 1200 \
  --fig-width-mm 160
```

---

## 4. Output Structure

After running with `--fig`, you get:

```
reports/figures/
├── G79/
│   ├── fig_G79_ringchain_v_vs_k.png       (600 DPI)
│   ├── fig_G79_ringchain_v_vs_k.svg       (vector)
│   ├── fig_G79_gamma_log_vs_k.png
│   ├── fig_G79_gamma_log_vs_k.svg
│   ├── fig_G79_freqshift_vs_gamma.png
│   └── fig_G79_freqshift_vs_gamma.svg
├── CygnusX/
│   └── (same structure)
├── shared/
│   └── (comparison plots)
└── FIGURE_INDEX.md                         (all figures + captions)

reports/PAPER_EXPORTS_MANIFEST.json         (all artifacts + SHA256)
```

---

## 5. Console Output

```
[SSZ] Generating figures for G79...

[SSZ] Figures written:
  - reports/figures/G79/fig_G79_ringchain_v_vs_k.png
  - reports/figures/G79/fig_G79_ringchain_v_vs_k.svg
  - reports/figures/G79/fig_G79_gamma_log_vs_k.png
  - reports/figures/G79/fig_G79_gamma_log_vs_k.svg
  - reports/figures/G79/fig_G79_freqshift_vs_gamma.png
  - reports/figures/G79/fig_G79_freqshift_vs_gamma.svg

Index: reports/figures/FIGURE_INDEX.md
Manifest: reports/PAPER_EXPORTS_MANIFEST.json
```

---

## 6. For Carmen (Paper Workflow)

**Step 1:** Run analysis with `--fig` flag  
**Step 2:** Open `reports/figures/FIGURE_INDEX.md`  
**Step 3:** Copy figure paths and captions into LaTeX/Markdown  
**Step 4:** Verify checksums in `PAPER_EXPORTS_MANIFEST.json`  

**LaTeX Example:**
```latex
\begin{figure}[h]
  \centering
  \includegraphics[width=0.8\textwidth]{figures/G79/fig_G79_ringchain_v_vs_k.pdf}
  \caption{Ring-Ketten-Propagation im SSZ-Feld. Die Umlaufgeschwindigkeit 
           v_k steigt trotz fallender Temperatur über k und reproduziert 
           die 14–16 km s⁻¹.}
  \label{fig:g79_velocity}
\end{figure}
```

---

## 7. Adding More Figures

**To add a new figure type:**

1. Add caption to `tools/figure_catalog.py`:
   ```python
   CAPTIONS["my_new_figure"] = "Description of my new figure..."
   ```

2. Add generation logic to `tools/figure_orchestrator.py`:
   ```python
   # In generate_figures()
   if "x_data" in datasets and "y_data" in datasets:
       p = _fig_base(fig_root, obj, "my_new_figure")
       paths += line(datasets["x_data"], datasets["y_data"], 
                     "X Label", "Y Label", f"{obj}: Title", p, ...)
   ```

3. Update your pipeline to include the new data in `datasets` dict

---

## 8. Troubleshooting

**Problem:** Figures not generated  
**Solution:** Check `args.fig` is `True` and datasets dict has required keys

**Problem:** Missing captions in index  
**Solution:** Add caption to `tools/figure_catalog.py`

**Problem:** Low resolution PNG  
**Solution:** Increase `--fig-dpi` (600 = draft, 1200 = print)

**Problem:** Wrong figure size  
**Solution:** Adjust `--fig-width-mm` (160 = 2-col, 84 = 1-col)

---

## 9. Integration Checklist

- [ ] Add argparse flags to CLI script
- [ ] Import `finalize_figures` in pipeline
- [ ] Prepare `datasets` dict with required arrays
- [ ] Call `finalize_figures(args, obj_name, datasets)`
- [ ] Test with `--fig` flag
- [ ] Verify output in `reports/figures/`
- [ ] Check `FIGURE_INDEX.md` and `MANIFEST.json`

---

**Ready to integrate!** Copy-paste snippets above into your CLI scripts. 🚀

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
