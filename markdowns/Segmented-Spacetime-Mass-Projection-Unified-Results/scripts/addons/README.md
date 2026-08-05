# SSZ Pipeline Add-ons

**Non-invasive Erweiterungen** - KEINE Änderungen an der Haupt-Pipeline!

Diese Add-ons können **nach** der normalen Pipeline ausgeführt werden und erweitern die Analysen um zusätzliche Features.

---

## 🎯 Verfügbare Add-ons

### 1. **Segment-Redshift** (`segment_redshift_addon.py`)

Berechnet gravitationelle Rotverschiebung basierend auf Segment-Dichte-Integration.

**Features:**
- 3 Proxy-Modi: `N` (Segment-Dichte), `rho-pr` (Stress-Energy), `gtt` (Metrik)
- Flexible Radien: r_em, r_out
- Beliebige Emissionsfrequenzen (Radio bis Gamma)
- Automatische Band-Klassifikation
- Optional: Plot-Generierung

---

## 🚀 Verwendung

### **Windows (PowerShell):**
```powershell
# Nach Pipeline-Run:
pwsh -File scripts\addons\run_segment_redshift.ps1
```

### **Linux/WSL (Make):**
```bash
# Nach Pipeline-Run:
make -C scripts/addons segment-redshift
```

### **Direkt (Python):**
```bash
python scripts/addons/segment_redshift_addon.py \
  --segment-redshift \
  --proxy N \
  --nu-em 1.0e18 \
  --r-em 2.0 \
  --r-out 50.0 \
  --seg-plot
```

---

## 📊 Outputs

Alle Add-ons schreiben ausschließlich nach:

```
reports/
├── segment_redshift.csv       # CSV-Tabelle mit Ergebnissen
├── segment_redshift.md        # Markdown-Report
└── figures/
    └── fig_shared_segment_redshift_profile.png  # Plot (wenn --seg-plot)
```

**KEINE Änderungen an:**
- Pipeline-Skripten
- Bestehenden Reports
- Core-Modulen
- Test-Suite

---

## ⚙️ Parameter

### **Segment-Redshift:**

| Parameter | Default | Beschreibung |
|-----------|---------|--------------|
| `--segment-redshift` | - | **Pflicht:** Aktiviert Add-on |
| `--proxy` | `N` | Proxy-Modus: `N`, `rho-pr`, `gtt` |
| `--nu-em` | `1.0e18` | Emissionsfrequenz in Hz |
| `--r-em` | `2.0` | Emissionsradius in r_s |
| `--r-out` | `50.0` | Äußerer Radius in r_s |
| `--seg-plot` | - | Erstelle Plot |

**Proxy-Modi:**

- **`N`:** Segment-Dichte (erfordert `reports/ring_chain.csv`)
- **`rho-pr`:** Stress-Energy (erfordert `reports/energy_conditions.csv`)
- **`gtt`:** Metrik-Komponente (erfordert `reports/metric_profile.csv`)

---

## 📖 Beispiele

### **Standard (X-ray):**
```bash
python scripts/addons/segment_redshift_addon.py --segment-redshift
```

### **Radio-Band:**
```bash
python scripts/addons/segment_redshift_addon.py \
  --segment-redshift \
  --nu-em 1.4e9 \
  --r-em 5.0 \
  --r-out 100.0
```

### **Mit Stress-Energy Proxy:**
```bash
python scripts/addons/segment_redshift_addon.py \
  --segment-redshift \
  --proxy rho-pr \
  --nu-em 5.0e14 \
  --seg-plot
```

---

## 🔍 Ergebnis-Interpretation

### **CSV-Output:**
```csv
r_em(rs),r_out(rs),proxy,Phi_seg,chi_em,nu_em_Hz,nu_inf_Hz,band,source
2.0,50.0,N,0.123456,8.839e-01,1.000e+18,8.839e+17,X-ray,reports/ring_chain.csv
```

**Spalten:**
- `Phi_seg`: Integrierte Segment-Dichte (dimensionslos)
- `chi_em`: Redshift-Faktor χ = e^(-Φ)
- `nu_inf_Hz`: Beobachtete Frequenz bei r → ∞
- `band`: Auto-klassifiziert (VLF/Radio/Microwave/IR/Optical/UV/X-ray/Gamma)

### **Markdown-Report:**
```markdown
# Segment Redshift (Add-on)
- Source: `reports/ring_chain.csv` (proxy=N)
- Integration: r_em=2 r_s → r_out=50 r_s
- Φ_seg = **0.123456** → χ_em = e^-Φ = **8.839e-01**
- ν_em = **1.000e+18 Hz** → ν_∞ = **8.839e+17 Hz**  (**X-ray**)
```

---

## 🛡️ Sicherheit

**Garantien:**
- ✅ Keine Änderungen an bestehenden Dateien
- ✅ Kein Überschreiben von Pipeline-Outputs
- ✅ Nur Lese-Zugriff auf Pipeline-Daten
- ✅ Eigener Namespace (`segment_redshift.*`)
- ✅ Opt-in: Nur mit `--segment-redshift` aktiv

**Falls Quell-Daten fehlen:**
- Add-on schreibt Info in `reports/segment_redshift.md`
- Exit 0 (kein Pipeline-Fehler)
- Log-Meldung: `[SSZ][addon] Quelle fehlt → report.`

---

## 🧪 Tests

```bash
# Schnelltest (ohne Plot):
python scripts/addons/segment_redshift_addon.py --segment-redshift

# Mit Plot:
python scripts/addons/segment_redshift_addon.py --segment-redshift --seg-plot

# Check Output:
cat reports/segment_redshift.md
```

---

## 📚 Integration in CI/CD

```yaml
# .github/workflows/pipeline.yml
- name: Run Pipeline
  run: python run_all_ssz_terminal.py

- name: Run Add-ons
  run: |
    python scripts/addons/segment_redshift_addon.py \
      --segment-redshift --seg-plot
```

---

## ❓ FAQ

**Q: Muss ich die Pipeline anpassen?**
A: Nein! Add-ons sind komplett unabhängig.

**Q: Was wenn die Quell-Datei fehlt?**
A: Add-on schreibt Info-Report und beendet sich sauber (Exit 0).

**Q: Kann ich eigene Proxies hinzufügen?**
A: Ja! Einfach in `segment_redshift_addon.py` erweitern.

**Q: Werden Pipeline-Ergebnisse überschrieben?**
A: Nein! Add-ons haben eigenen Namespace (`segment_redshift.*`).

---

## 📝 Lizenz

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Add-ons sind optional und ändern NICHTS an der Kern-Pipeline!**
