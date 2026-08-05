# Publication Highlights - DEPRECATED

**⚠️ This directory is deprecated. Old German plots have been removed.**

## Current Location

**Scientific English highlights are now in:**
```
../final_highlights/
```

### Available Files:
- `Highlight1_Temporal_Density_Framework.png` (335 KB) + PDF
- `Highlight2_Observational_Evidence.png` (339 KB) + PDF  
- `Highlight3_Model_Validation.png` (334 KB) + PDF

### Generation Script:
```bash
python GENERATE_ENGLISH_HIGHLIGHTS.py
```

## What Changed

**Removed (incorrect):**
- ❌ `Highlight2_Daten.png` - Had "center colder" error
- ❌ German informal language
- ❌ Missing Section 5.6 recoupling energy framework

**Added (correct):**
- ✅ Recoupling energy (Eq. 18): ΔT_rec ≈ T_loc(1-γ_seg)
- ✅ Velocity excess (Eq. 17): √(v₀² + 2c²(1-γ_seg⁻¹))
- ✅ Scientific English, publication-ready
- ✅ Proper references to paper equations

## LaTeX Usage

```latex
\begin{figure*}[ht]
  \centering
  \includegraphics[width=0.95\textwidth]{final_highlights/Highlight3_Model_Validation.png}
  \caption{Segmented Spacetime framework validation showing recoupling energy 
           release at the g² → g¹ boundary (Section 5.6, Equations 17-18).}
  \label{fig:validation}
\end{figure*}
```

---

© 2025 Carmen N. Wrede, Lino P. Casu, Bingsi  
Paper: "Segmented Spacetime and the Origin of Molecular Zones in Expanding Nebulae"  
Object: G79.29+0.46 (LBV nebula, Cygnus X)

**Status: READY FOR PUBLICATION** ✅
