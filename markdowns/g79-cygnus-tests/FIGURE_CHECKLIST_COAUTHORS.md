# Figure Review Checklist for Co-Authors
## Segmented Spacetime Paper - Quick Reference

**Last Updated:** 2025-11-07  
**Status:** Ready for arXiv submission  
**Review Deadline:** [Add date]

---

## 📋 Quick Action Items

### ⏰ **21-Minute Quick Fixes (Do Before Submission)**

- [ ] **Figure 1:** Add dashed/dotted line styles (colorblind accessibility)
- [ ] **Figure 3:** Fix check mark font warning (use "PASS" or unicode-safe font)
- [ ] **All Figures:** Verify color palette consistency
- [ ] **All Figures:** Add minor tick marks to axes
- [ ] **Figure 3:** Add χ² or p-values to validation table

**Assignee:** __________  
**Deadline:** __________

---

### 🎯 **Medium Priority (3.5 Hours, Before Journal Submission)**

- [ ] **Figure 1B:** Separate T_kinetic and T_rotational curves
- [ ] **Figure 1:** Add residual sub-panels (Observed - Model)
- [ ] **Create:** Conceptual diagram (nebula cross-section with γ_seg overlay)
- [ ] **All Figures:** Generate colorblind-safe versions
- [ ] **Figure 3:** Export as LaTeX table for direct inclusion

**Assignee:** __________  
**Deadline:** __________

---

### 🔬 **Optional Enhancements (For High-Impact Journals)**

- [ ] Interactive dashboard (Dash/Streamlit)
- [ ] Animation suite (5 GIFs)
- [ ] Multi-object comparison (η Car, AG Car, etc.)
- [ ] Monte Carlo uncertainty visualization

**Assignee:** __________  
**Deadline:** __________

---

## 📊 Figure-Specific Notes

### **Figure 1: Framework**

**What's Good:**
- Clear visual hierarchy
- Uncertainty bands included
- Formula box with parameters

**Needs Attention:**
- Temperature panel shows scatter (explain thermal inversion mechanism in caption)
- Formula box overlaps high-γ region (consider moving)
- Add line styles for accessibility

**Caption Status:** ✅ Journal-ready (see PUBLICATION_REVIEW_ANALYSIS.md)

---

### **Figure 2: Observations**

**What's Good:**
- Multi-wavelength coverage clearly shown
- Comparative panel (classical vs. SSZ vs. observed)
- Spectral overlap visualization effective

**Needs Attention:**
- Large error bars in Panel A (consider box plots instead)
- Panel D legend overlaps data (move to outside margin)
- Add significance markers to velocity comparison

**Caption Status:** ✅ Journal-ready

---

### **Figure 3: Validation**

**What's Good:**
- Comprehensive validation summary
- Clean table formatting
- All matches highlighted

**Needs Attention:**
- ⚠️ Font warning: check mark glyph missing
- Add statistical significance column (p-values)
- Standardize reference format (use bibcodes)

**Caption Status:** ✅ Journal-ready (move below table for ApJ)

---

## 🎨 Style Consistency Check

| Element | Status | Notes |
|---------|--------|-------|
| Color Palette | ✅ | Blue/Red/Green consistent |
| Font Family | ⚠️ | Times New Roman (unicode issue in Fig 3) |
| Font Sizes | ✅ | 10-12pt (readable) |
| Line Widths | ✅ | 2.0-2.5pt for data |
| Grid Style | ✅ | Dotted, alpha=0.25 |
| Error Bars | ✅ | Included where applicable |
| Legend Position | ✅ | Doesn't obscure data |
| Axis Labels | ✅ | Bold, proper units |

---

## 📁 File Organization

### **Current Structure:**
```
publication_figures_english/
├── Figure1_Framework.pdf (70.4 KB) ✅
├── Figure1_Framework.png (backup)
├── Figure2_Observations.pdf (51.8 KB) ✅
├── Figure2_Observations.png (backup)
├── Figure3_Validation.pdf (76.1 KB) ⚠️
├── Figure3_Validation.png (backup)
└── model_predictions.csv ✅
```

### **Additional Files Needed:**
- [ ] `figure_captions.txt` (extracted from review doc)
- [ ] `supplementary_animations/` (if creating GIFs)
- [ ] `figure_source_code/` (reproducibility)
- [ ] `colorblind_versions/` (accessibility)

---

## 🔍 Pre-Submission Checklist

### **arXiv**

- [ ] All figures referenced in text
- [ ] Figure numbers sequential
- [ ] Captions self-contained
- [ ] PDF files <500 KB each
- [ ] Fonts embedded
- [ ] 300 DPI minimum
- [ ] Filenames match manuscript references

### **ApJ Submission**

- [ ] Convert to AASTeX format
- [ ] Figures at first citation point
- [ ] Use `\begin{figure*}` for 2-column
- [ ] Include alt-text descriptions
- [ ] CMYK color space for print
- [ ] Permission statements (all original)
- [ ] Data availability statement

### **Supplementary Materials**

- [ ] `model_predictions.csv` included
- [ ] Figure generation scripts provided
- [ ] README with reproduction instructions
- [ ] Zenodo DOI for code/data
- [ ] License file (ANTI-CAPITALIST v1.4)

---

## 🚨 Known Issues

### **Critical (Fix Before Submission):**
1. **Figure 3:** Check mark glyph warning
   - **Fix:** Change `'✓'` to `'PASS'` or use DejaVu font
   - **Location:** Line 362 in GENERATE_PUBLICATION_FIGURES_ENGLISH.py
   - **Time:** 1 minute

### **Important (Fix Before Journal):**
2. **Figure 1B:** T_kinetic vs. T_rotational confusion
   - **Fix:** Add separate curves with labels
   - **Explain:** NH₃ rotational temp ≠ dust kinetic temp in g² regime
   - **Time:** 30 minutes

### **Minor (Consider for Revision):**
3. **All Figures:** Colorblind accessibility
   - **Fix:** Add line style variations
   - **Test:** Using Coblis simulator
   - **Time:** 20 minutes

---

## 📧 Communication

### **Internal Review:**
- Circulate to co-authors by: __________
- Collect feedback by: __________
- Implement changes by: __________

### **External Review:**
- Share with collaborators: __________
- Request feedback from: __________
- Finalize by: __________

---

## 🎯 Success Metrics

| Metric | Target | Current | Status |
|--------|--------|---------|--------|
| Publication-Ready Score | A | A- | 🟡 |
| All Critical Issues Fixed | 100% | 0% | 🔴 |
| Captions Complete | 100% | 100% | 🟢 |
| Accessibility (Colorblind) | 90% | 70% | 🟡 |
| File Size <500 KB | 100% | 100% | 🟢 |
| Reproducible Code | Yes | Yes | 🟢 |

---

## 📚 Resources

### **Documentation:**
- Full Review: `PUBLICATION_REVIEW_ANALYSIS.md`
- Figure Generation: `GENERATE_PUBLICATION_FIGURES_ENGLISH.py`
- Model Data: `publication_figures_english/model_predictions.csv`

### **Tools:**
- **Colorblind Simulator:** https://www.color-blindness.com/coblis-color-blindness-simulator/
- **Color Palette:** https://colorbrewer2.org/
- **LaTeX Tables:** https://www.tablesgenerator.com/latex_tables
- **Font Checker:** `fc-list | grep "Times"`

### **Journal Guidelines:**
- **ApJ:** https://journals.aas.org/graphics-guide/
- **A&A:** https://www.aanda.org/for-authors/latex-issues
- **arXiv:** https://arxiv.org/help/submit

---

## ✍️ Sign-Off

Once all critical and important items are complete:

**Lead Author Approval:**  
Name: __________  
Date: __________  
Signature: __________

**Co-Author Review:**  
Name: __________  
Date: __________  
Comments: __________

**Final Approval for Submission:**  
Name: __________  
Date: __________  
Journal: __________

---

## 💬 Notes & Discussion

*Use this space for team comments:*

---

---

**Version:** 1.0  
**Prepared by:** Scientific Visualization Analysis  
**Contact:** [Add email]  
**License:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4

