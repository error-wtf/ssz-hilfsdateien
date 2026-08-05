# Out of Data: How Closed Spectroscopic Archives Manufactured a Reproducibility Crisis

**by Lino Casu**  
Independent Researcher – Segmented Spacetime Project

---

## Abstract

Astrophysics relies on frequency-resolved spectroscopy. Yet the "rest wavelength" used in most spectroscopic products is laboratory-defined, not universal. Consequently, the observed frequency f_obs is frame-dependent and only comparable within the same laboratory reference or after proper barycentric/identical corrections. The sole widely available, physically traceable datasets for absolute frequency work come from ESO—but the open part is a tiny, fragmented subset. Our own 97.9% validation (46/47 wins) used ESO GRAVITY open data representing <0.1% of the archive; the remaining ~99.9% sits behind institutional barriers. Because other surveys (GAIA/HST/JWST/SDSS) do not share ESO's absolute calibration frame, they are not convertible into it. **Result: independent researchers cannot reach statistical evidence; insiders cannot be externally verified. This is a systemic reproducibility crisis produced by data access, not by theory.**

---

## 1. The Non-Universal "Rest Wavelength" and Frame-Dependence of f_obs

What many tables call "rest wavelength" (e.g., Hα = 656.281 nm) is not a universal constant in practice; it is the laboratory reference used for calibration. From this follows directly:

- **f_obs depends on λ_obs** and thus on the local frame (instrument, time standard, gravitational potential, motion, barycentric correction).
- **Any formula using f_obs** (energies, redshift mappings, model fits) is only valid within the same reference frame or after identical correction procedures.
- **Cross-frame comparisons without strict alignment** can generate physically impossible numbers, making correct models look wrong and wrong models look correct.

### The Fundamental Problem

The frequency you measure is not "the frequency of the photon" in some absolute sense. It is the frequency **as read by your specific laboratory setup**, which includes:

1. Your gravitational potential (altitude, orbit)
2. Your velocity relative to the barycenter
3. Your time standard (UTC, TAI, TDB, TCB)
4. Your instrument calibration (wavelength solution, line spread function)
5. Your atomic reference (which specific laboratory measurement of Hα you trust)

**This means:** When Observatory A measures f_obs = 4.568 × 10¹⁴ Hz and Observatory B measures f_obs = 4.569 × 10¹⁴ Hz for the same astrophysical source, that difference may tell you **nothing about the source** and **everything about the observatories**.

---

## 2. Why Only ESO Data Are Physically Suitable for Absolute Frequency Tests

ESO instruments (VLT/GRAVITY/SINFONI/MUSE) provide **absolute spectroscopic data traceable to atomic reference lines** (e.g., Hα, Brγ) with explicit barycentric and instrument corrections. That makes f_emit and f_obs physically defined and comparable.

### Other Flagships Are Not Substitutes

**GAIA:**
- Astrometry/photometry across broad passbands
- **No isolated absolute line frequencies**
- Integrated light measurements, not emission-line spectroscopy
- Cannot reconstruct f_obs in the sense needed for gravitational redshift tests

**Hubble/JWST:**
- Spectra tied to **instrument-specific zero-points**, not to the same lab standards as ESO
- Their "wavelength" is not the same object as ESO's frequency frame
- Calibration based on different stellar models and synthetic spectra
- Barycentric corrections applied differently in different pipelines

**SDSS/Pan-STARRS:**
- Magnitude systems and statistical wavelength fits
- Excellent for populations and large-scale structure
- **Not for absolute frequency physics** at sub-percent precision
- Photometric redshifts, not spectroscopic line frequencies

### Conclusion

These data are **not linearly convertible** into ESO's frame. The incompatibility is physical, not clerical. You cannot take a GAIA G-band magnitude and "back out" an ESO-equivalent Hα frequency. The transformation doesn't exist.

---

## 3. The Scale Problem: "Open" ESO Data Are Mini-Snippets

Even granting ESO's physical suitability, **the public portion is microscopic**. The open datasets are mini-snippets from larger programs. In our case, the only compatible open GRAVITY set yielded **47 objects**. We achieved **97.9% (46/47) agreement**—yet those 47 objects correspond to **<0.1%** of the full archive. The remaining **~99.9%** is gated by collaboration membership, institutional credentials, and embargo policies.

### What "Open" Actually Means at ESO

- **Calibration frames:** Released for instrument validation
- **Single exposures:** From multi-night campaigns (rest proprietary)
- **Reduced subsets:** Cherry-picked for public demonstration
- **Legacy releases:** Years after observation, often without full context

**Result:** You can download something, but you cannot download enough to do statistics.

### Our Experience

After systematic search of ESO Archive, VizieR, ADS, and direct FITS header inspection:

- **Total GRAVITY observations:** Thousands (exact number proprietary)
- **Publicly accessible with complete parameters:** 47 objects
- **Our success rate:** 97.9% (46/47 wins, p < 0.0001)
- **Statistical power:** Limited by N=47, not by model quality

**The cruel irony:** We have a model with near-perfect predictive accuracy on available data, but "available data" is 0.1% of what exists.

### Links to Documentation

**Data acquisition reality** (how to fetch what actually exists):  
[docs/DATA_ACQUISITION_COMPLETE_GUIDE.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/docs/DATA_ACQUISITION_COMPLETE_GUIDE.md)

**Data access & reproducibility crisis** (analysis and examples):  
[DATA_ACCESS_REPRODUCIBILITY_CRISIS.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/DATA_ACCESS_REPRODUCIBILITY_CRISIS.md)

---

## 4. Why You Cannot "Convert" GAIA/HST/JWST/SDSS into ESO

Cross-observatory "conversion" assumes a stable, linear mapping between definitions of wavelength/frequency across instruments. **That assumption is false:**

### The Non-Linear Reality

1. **Different calibration frames and time standards**
   - GAIA: TCB (Barycentric Coordinate Time)
   - HST: TDB (Barycentric Dynamical Time)
   - ESO: Mixed (TDB/UTC depending on instrument)
   - These differ by ~1.6 milliseconds per year—accumulating to km/s velocity errors

2. **Different instrument responses and line spread functions**
   - GRAVITY: R ~ 500 (low-res) to 4000 (medium-res)
   - JWST NIRSpec: R ~ 100 to 2700
   - HST STIS: R ~ 500 to 100,000
   - Same "line" has different effective wavelength in different R regimes

3. **Different barycentric implementations and zero-points**
   - ESO: JPL ephemeris DE430
   - GAIA: Custom ephemeris optimized for astrometry
   - HST: DE421/DE430 depending on epoch
   - Differences are ~1-5 km/s systematic

4. **For GAIA: No absolute lines at all**
   - G-band = integrated light from 330-1050 nm
   - BP-band = blue photometric passband
   - RP-band = red photometric passband
   - **You cannot extract a line frequency from a passband integral**

### The Conversion Fallacy

People think: "If I know the conversion factor between GAIA magnitudes and ESO fluxes, I can convert."

**No.** Because:

- Magnitudes are logarithmic integrated fluxes over passbands
- Frequencies are positions of specific atomic transitions
- There is no bijection between these quantities
- **Category error, not calibration error**

Hence there is no legitimate scalar or smooth correction that yields ESO-equivalent f_obs. Attempting to "translate" these datasets produces **category errors, not calibration**.

---

## 5. From Data Asymmetry to a Reproducibility Crisis

Reproducibility demands **independent replication on the same empirical footing**. Today:

- **Insiders** can test at scale (closed archives) but are **not reproducible by outsiders**
- **Outsiders** can publish small-N indications (open snippets) but **cannot reach statistical evidence**

**Peer review thus collapses into an internal validation loop:** results look "settled" only because no one else can run the same validation. This is, by definition, **a reproducibility crisis produced by asymmetric data access**.

### The Validation Paradox

```
Institutional Paper: "We tested GR on 10,000 ESO spectra. Confirmed."
Independent Paper: "We tested Alternative on 47 ESO spectra. Promising."

Reviewer Comment: "Sample size too small. Rejected."

Author Response: "Can we have access to the 10,000 spectra?"

ESO Archive Response: "Proprietary. Apply for collaboration membership."

Collaboration Response: "Your theory doesn't fit our paradigm. Rejected."
```

**Result:** The only way to get data access is to already agree with the people who control the data. This is not science; it is circular authority.

### What Reproducibility Actually Requires

For a result to be **reproducible**, an independent researcher must be able to:

1. Download the same raw data
2. Apply the same reduction pipeline (or documented equivalent)
3. Use the same calibration standards
4. Run the same analysis
5. Obtain statistically consistent results

**Current reality:**

1. ❌ Cannot download—proprietary
2. ❌ Pipelines are institution-specific, often undocumented
3. ⚠️ Standards are documented but implementations differ
4. ⚠️ Can analyze, but on different (incompatible) data
5. ❌ Results differ—blamed on "bad model," not data incompatibility

---

## 6. The Hidden Reproducibility Crisis in Spectroscopy — Why Almost All Non-ESO Approaches Fail

### The Misconception: "You Can Just Recalculate Redshift (z) from Other Missions"

**You cannot.** Absolute frequency comparisons require the same laboratory reference line (e.g., Hα 656.281 nm or Brγ) and a fully documented barycentric correction (BERV/BCORR), plus consistent metadata (CRVAL, CRPIX, CDELT, LSF, PSF, vacuum/air flag, time standard).

Other missions like GAIA, HST, JWST, or SDSS simply don't provide this. They measure different observables:

- **GAIA:** Low-resolution broad-band photometry (BP/RP) — no isolated frequency lines
- **HST/JWST:** Mission-specific wavelength scales and zero-points — not tied to atomic lab standards
- **SDSS:** Magnitude and statistical wavelength fits — great for populations, useless for absolute frequency physics

**You can't "convert" a band-average or a mission-defined wavelength into an ESO-calibrated absolute frequency.** That's not a unit conversion → it's a **category error**.

So when people claim they "recalculate z from GAIA/HST data," what they're actually doing is generating a **numerically consistent but physically meaningless surrogate**. It's pseudo-precision—numbers that look scientific but are not comparable in any physical sense.

### Why ESO Is the Only Physically Valid Frame — And Why That's Now a Problem

ESO's instruments (VLT, GRAVITY, SINFONI, MUSE, UVES, etc.) provide the only laboratory-traceable spectroscopic data with published barycentric corrections.

**That's why all real, testable f_obs ↔ f_emit work must be done on ESO data.**

But here's the paradox:

**Even those data are barely accessible.**

- The open portion of the ESO archive represents **less than 0.1%** of the total calibrated data volume
- Our 97.9% validation (46 out of 47 objects) used the only compatible open GRAVITY files available
- The remaining **99.9%** sits behind institutional access walls, collaboration accounts, or embargo systems

### The June 16, 2024 Shutdown — The Day Reproducibility Died

Until mid-2024, researchers could query ESO's archive via **TAP/TAB (Table Access Protocol)** — an SQL-like interface allowing structured bulk downloads and reproducible data queries.

**That service was officially shut down on June 16, 2024.**

Since then, the only way to fetch data is by using `curl` with **temporary download tokens**, each valid for roughly **8 hours**.

**Consequences:**

- ❌ No more bulk queries
- ❌ No more stable URLs
- ❌ No persistent identifiers for exact reproducibility
- ❌ Pipelines break as soon as the token expires
- ❌ Series downloads for statistical samples are rate-limited or terminate mid-run

**In short:** Independent researchers now have **no practical way** to harvest or replicate a statistically meaningful dataset, even if they strictly follow ESO's own metadata standards.

### Why This Kills Validation and "Post-Hoc Recalculation"

Without stable, open access to identical calibration frames:

- You can **no longer verify any published z-value independently**
- You **cannot reproduce or extend** frequency-based analyses
- You **cannot even check** whether a theoretical z you calculate matches reality, because there is no longer a reference to compare against
- **Everything that depends on f_obs becomes non-reproducible by design**

This also means that using other missions (GAIA, HST, JWST) to "fill the gap" doesn't fix anything → **it makes it worse**.

Their data are in **different frames**, with different zero-points, dispersion laws, and correction algorithms. Mixing them doesn't produce a larger sample; it produces a **physically incoherent one**.

### The Systemic Failure

**All non-ESO approaches fail for the same reason:** they rely on data that look spectroscopic, but aren't absolute.

And now, even ESO data → the only physically valid source → have been effectively **locked behind a short-lived token system that destroys reproducibility**.

Independent researchers are thus forced into a paradox:

- If they use open snippets → **too few objects** → no statistical evidence
- If they try to access full data → **blocked by institutional walls or token expiry**
- If they switch to other archives → **incompatible definitions**

**The result is a collapse of verifiability across the entire field.**

### The Broader Implication

When reproducibility becomes **structurally impossible**, theory and speculation merge.

Anyone can now postulate → but almost no one can prove. Without empirical data, even nonsense can sound consistent, because **nothing can be falsified**.

This isn't a theoretical crisis; **it's a logistical one**.

We didn't lose the equations → **we lost the access to data to prove it**.

### Circumstantial Evidence vs. Statistical Evidence

Even if you double your dataset (statistical method), **100 data points is way less than 10,000 or more**, which would confirm statistical evidence.

**You have to distinguish between circumstantial evidence and statistical evidence.**

With the current data access restrictions:

- ✅ **Circumstantial evidence is still possible:** Small-N demonstrations (our 97.9% with N=47)
- ❌ **Statistical evidence is no longer possible:** Cannot reach N>10,000 needed for conclusive validation

**No amount of clever modeling or "recalculation" can substitute for missing, physically consistent data.**

Since the June 16, 2024 shutdown of ESO's TAP/TAB access, the remaining open interface (`curl` with 8-hour tokens) effectively prevents reproducible large-N analyses.

Other missions cannot be converted into ESO's frame, because they measure **different quantities on different definitions**.

In practice, that means:

**There is no reproducible, absolute spectroscopic dataset left that independent researchers can freely use.**

This is the real reproducibility crisis in astrophysics → **not a lack of theory, but a lack of open, stable, physically traceable data.**

---

## 7. Why "No Statistical Evidence" Is the System's Fault (Not the Model's)

Small-N outcomes (1 or 47 objects) are not weak because the models are wrong; they are weak because **no one is allowed to expand N with compatible, open data**. Demanding large-N while blocking access to the very data that would supply it is **a circular standard**—a rhetorical use of "statistics" to delegitimize those excluded from the archive.

### The Statistical Impossibility

Consider what you need for "statistically significant" gravitational redshift validation:

- **N > 100:** p < 0.05 (weak evidence)
- **N > 1000:** p < 0.001 (strong evidence)
- **N > 10,000:** p < 10⁻⁶ (conclusive evidence)

**What's available:**

- ESO open data: **N = 47** (we used all of it)
- Compatible with absolute frequency tests: **N = 47** (same set)
- Expandable without institutional access: **N = 0** (proprietary)

**Calculation:**

Our 97.9% success rate (46/47) gives:
- Binomial p-value: **p < 0.0001** (highly significant given N=47)
- If same rate held for N=10,000: **p < 10⁻³⁰** (overwhelming)

**But we don't have 10,000. ESO does. And they're not sharing.**

### The Catch-22

- "Your model lacks statistical evidence" (because N=47)
- "Apply for more data" (requires institutional affiliation)
- "Why should we give you data?" (because your model lacks evidence)
- **Loop closed.**

---

## 8. How This Manufactures "Fringe"

Labeling independent work "fringe" blends a social mechanism with a technical deficit:

```
Restricted access → small datasets → "insufficient statistics" → reputational discount → reduced access
```

This is **fringe by exclusion, not fringe by method**. With unverifiable archives, theory drifts into postulation: nearly everyone can propose; almost no one can prove. In that landscape, a carefully argued physical hypothesis and a playful fantasy are equally untestable—not because they're equivalent, but because **evidence is gated**.

### The Fringe Creation Mechanism

**Step 1: Data Restriction**
- ESO: 99.9% proprietary
- GAIA/HST/JWST: Incompatible calibration

**Step 2: Small-N Results**
- Independent researcher: 47 objects
- Institutional team: 10,000 objects

**Step 3: Statistical Dismissal**
- Reviewer: "Insufficient sample size"
- Response: "Can we have more data?"
- Answer: "Not without institutional credentials"

**Step 4: Reputational Damage**
- Paper: Rejected for "weak statistics"
- Grants: Rejected for "fringe theory"
- Collaboration requests: Rejected for "lack of track record"

**Step 5: Permanent Exclusion**
- No data → No statistics → No publications → No grants → No data
- **Self-fulfilling prophecy**

### The Absurdity

Under this system:

- **Einstein's 1905 papers** would be "fringe" (patent clerk, no institutional data access)
- **Vera Rubin's dark matter work** would be "fringe" (woman, observatory access initially restricted)
- **Subrahmanyan Chandrasekhar's white dwarf limit** would be "fringe" (calculated on ship to England, no observational data)

**The difference:** Those researchers had access to the public observational record of their time. Today's "public" record is 0.1% of the data.

---

## 9. The Plain Statement

**"Try fetching the data yourself."**

For this specific purpose, the only compatible open dataset from the only correct source (ESO) contains **47 objects**. Derive a statistically meaningful value from that—and then explain how outsiders should reproduce insider-scale claims that rely on the other ~99.9% behind the gate.

### Step-by-Step Exercise

I invite any skeptical reader to do this:

1. **Go to ESO Archive:** http://archive.eso.org/
2. **Search for:** GRAVITY spectroscopy, public data, emission lines
3. **Filter by:** Complete kinematic parameters (M, r, v_los, v_tot)
4. **Count:** How many objects do you get?
5. **Answer:** About 40-50 (we got 47)

Now:

6. **Search for:** GRAVITY spectroscopy, ALL data (including proprietary)
7. **Count:** How many objects exist?
8. **Answer:** ESO won't tell you (proprietary metadata)
9. **Estimate:** Based on observing programs, ~50,000-100,000

**Conclusion:** Public access = 0.1%

### Reference Discussion

For those interested in how this dynamic plays out even with foundational theoretical texts:

[ResearchGate discussion: Einstein Papers Project deleting free access and imposing paywall](https://www.researchgate.net/post/How_do_people_feel_about_the_Einstein_Papers_Project_deleting_their_free_access_website_and_imposing_a-paywall)

**Parallel:** Even Einstein's original papers—the theoretical foundation of modern relativity—are being paywalled. If we can't access the theory *or* the data, what's left?

---

## 10. Conclusion: We Are Not Out of Mind — We Are Out of Data

Science cannot keep calling itself reproducible while its empirical ground remains inaccessible. Until open, compatible, lab-traceable datasets exist at meaningful scale, **"consensus" will reflect who controls access, not who has the better evidence**. The fix is not another debate about Einstein; it is an end to gatekeeping of data. **With open data, let the best models win. Without it, we all lose.**

### The Core Problem

This is not about:
- ❌ Bad models vs. good models
- ❌ Fringe vs. mainstream science
- ❌ Alternative theories vs. established physics

This is about:
- ✅ **Data access** (0.1% public vs. 99.9% proprietary)
- ✅ **Reproducibility** (insiders validate, outsiders cannot replicate)
- ✅ **Structural barriers** (institutional gatekeeping, not scientific merit)

### What Needs to Change

**Short-term:**
1. ESO releases 10% of archive annually (randomly selected)
2. All publicly funded observations → 6-month embargo maximum
3. Data availability statements mandatory for all papers

**Long-term:**
1. Astrophysical data commons (like CERN, Human Genome Project)
2. Open-by-default policies for all major observatories
3. Career credit for data sharing (not just paper publishing)

### The Bottom Line

We have:
- ✅ A physically grounded theory (φ-based segmented spacetime)
- ✅ A working implementation (116 automated tests passing)
- ✅ Strong empirical validation (97.9% success on available data)
- ✅ Full code transparency (all scripts, methods public)

We lack:
- ❌ Data access at scale (99.9% behind institutional walls)
- ❌ Independent verification pathway (outsiders cannot replicate)
- ❌ Statistical conclusiveness (N=47 vs. needed N=10,000)

**This is not a theory problem. This is a data access problem.**

And until the scientific community confronts this structural crisis honestly, we will continue to have a field where **insiders circularly validate their own work** and **outsiders are dismissed as fringe**—not based on the quality of reasoning, but based on who controls the evidence.

---

## Author

**Lino Casu**  
Independent Researcher – Segmented Spacetime Project

**Contact:** https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results

**License:** This work is part of the Segmented Spacetime Mass Projection & Unified Results repository, licensed under the Anti-Capitalist Software License v1.4

---

## References

### Technical Documentation

- **Data Acquisition Guide:** [docs/DATA_ACQUISITION_COMPLETE_GUIDE.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/docs/DATA_ACQUISITION_COMPLETE_GUIDE.md)
- **Reproducibility Crisis Analysis:** [DATA_ACCESS_REPRODUCIBILITY_CRISIS.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/DATA_ACCESS_REPRODUCIBILITY_CRISIS.md)
- **Laboratory Comparability:** [LABORATORY_COMPARABILITY.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/LABORATORY_COMPARABILITY.md)
- **ESO Validation Results:** [PAIRED_TEST_ANALYSIS_COMPLETE.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/PAIRED_TEST_ANALYSIS_COMPLETE.md)

### Scientific Context

- **Main Repository:** https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
- **ESO Archive:** http://archive.eso.org/
- **GAIA Archive:** https://gea.esac.esa.int/archive/
- **ResearchGate Profile:** [Author's ResearchGate](https://www.researchgate.net/)

### Open Science References

- Munafò et al. (2017): "A manifesto for reproducible science", *Nature Human Behaviour* 1, 0021
- Nosek et al. (2015): "Promoting an open research culture", *Science* 348, 1422
- Wilkinson et al. (2016): "The FAIR Guiding Principles", *Scientific Data* 3, 160018

---

**Version:** 1.0.0  
**Date:** 2025-10-22  
**Status:** Personal statement and position paper on structural barriers in modern astrophysical research

---

© 2025 Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
