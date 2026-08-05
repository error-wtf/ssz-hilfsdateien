# SSZ Segmented Space-Time Proof Summary

SSZ SEGMENTED SPACE-TIME PROOF SUMMARY

Datenverzeichnis: d:\mnt\data

Angefragter Prefix: v6 → Verwendet: v6

Artefakt results: d:\mnt\data\proof_sweep_results_v6.csv

Artefakt boundaries: d:\mnt\data\stability_boundaries_v6.csv

Artefakt summary: d:\mnt\data\proof_sweep_summary_v6.json

Vorhandene Abbildungen:

  - heatmap_stability_uniform_v6.png

  - heatmap_stability_weighted_v6.png

  - disagreement_map_uniform_v6.png

  - disagreement_map_weighted_v6.png

  - boundary_lambdaA_vs_Omega0_v6.png

  - lambdaA_diff_map_v6.png



FORMALER BEWEISRAHMEN

Definitions:

  D1 (Segmentierung): Diskrete Segmente mit lokaler Dämpfung λ_A und Dichte σ(θ).

  D2 (Roundtrip-Gain): G = exp(∫ γ_loc ds) · (1−κ) − Dämpfungsterme (λ_A·σ, Spiegelterm log_mirror).

  D3 (Stabilität): log G < 0 (direkt) bzw. analytisches Kriterium Ξ < λ_A K σ₀ (modellabhängig).

Assumptions:

  A1: Glatte, beschränkte γ_loc(θ) entlang des Rundlaufs.

  A2: Nichtnegative Dämpfungsanteile (λ_A σ(θ), κ, Spiegelverluste).

  A3: Segmentkopplung wirkt linear stabil (keine Verstärkung zwischen Segmenten ohne Gain).

Lemmas:

  L1 (Monotonie): Erhöht man die effektive Segmentdichte σ, verschiebt sich log G nach unten.

    Skizze: Skizze: γ_loc bleibt unverändert, λ_A·σ skaliert auf jedem Segment → größere Dichte erhöht die Dämpfungssumme und senkt log G.

  L2 (Subadditivität): Segmentweise Dämpfung addiert sich zu einer globalen Schranke für log G.

    Skizze: Skizze: log G = ∫ γ_loc ds − Σ λ_A σ_k + log_mirror; jedes Segment trägt höchstens λ_A σ_k bei → Summe bildet globale Grenze.

  L3 (Weighted-Shift): Weighted-Segmentierung verschiebt die Stabilitätsgrenze nach unten relativ zu uniform.

    Skizze: Skizze: Höhere σ in resonanten Bereichen erhöht lokale Dämpfung; folgt aus Vergleich der gewichteten Riemann-Summen (vgl. Lemma L1).

Theorem:

  T1 (Hinreichende Stabilität): Wenn Ξ ≤ λ_A K σ₀ − ε mit ε > 0, dann ist G < 1 und die Rundlauf-Amplitude fällt exponentiell (kein Runaway).

    Beweisskizze: Beweisskizze: (i) Ξ erfasst maximalen Gain-Beitrag unter A1–A3. (ii) Lemma L2 liefert log G ≤ Ξ − λ_A K σ₀. (iii) Der Abstand ε>0 erzwingt log G < 0. Lemma L3 zeigt, dass weighted-Segmentierung konservativer Stabilität liefert.



Beide Modi (aggregiert)

  Einträge: 348

  Agreement (direct vs criterion): 0.966 (n=348)

  logG-Statistiken: min=-152.6973, median=189.1294, max=370.7849

  Beispielhafte λ_A-Stabilitätsraten:

    - K=8, λ_A=0.00000 → 0.000

    - K=8, λ_A=0.80000 → 0.027

    - K=16, λ_A=0.00000 → 0.000

    - K=16, λ_A=0.80000 → 0.056

    - K=32, λ_A=0.00000 → 0.000

    - K=32, λ_A=0.80000 → 0.056

    - K=64, λ_A=0.00000 → 0.000

    - K=64, λ_A=0.80000 → 0.118

  Disagreement-Hotspots:

    - K=8, λ_A=0.00000 → 0.000

    - K=8, λ_A=0.80000 → 0.027

    - K=16, λ_A=0.00000 → 0.000

    - K=16, λ_A=0.80000 → 0.056

    - K=32, λ_A=0.00000 → 0.000

    - K=32, λ_A=0.80000 → 0.056

    - K=64, λ_A=0.00000 → 0.000

    - K=64, λ_A=0.80000 → 0.059

  WARN: Bei λ_A → 0 wurden positive logG-Werte gefunden (prüfe Gain-Setup).



Modus: uniform

  Einträge: 176

  Agreement (direct vs criterion): 0.972 (n=176)

  logG-Statistiken: min=-116.4394, median=191.3864, max=370.7849

  Beispielhafte λ_A-Stabilitätsraten:

    - K=8, λ_A=0.00000 → 0.000

    - K=8, λ_A=0.80000 → 0.000

    - K=16, λ_A=0.00000 → 0.000

    - K=16, λ_A=0.80000 → 0.056

    - K=32, λ_A=0.00000 → 0.000

    - K=32, λ_A=0.80000 → 0.056

    - K=64, λ_A=0.00000 → 0.000

    - K=64, λ_A=0.80000 → 0.118

  Disagreement-Hotspots:

    - K=8, λ_A=0.00000 → 0.000

    - K=8, λ_A=0.80000 → 0.000

    - K=16, λ_A=0.00000 → 0.000

    - K=16, λ_A=0.80000 → 0.056

    - K=32, λ_A=0.00000 → 0.000

    - K=32, λ_A=0.80000 → 0.056

    - K=64, λ_A=0.00000 → 0.000

    - K=64, λ_A=0.80000 → 0.059

  WARN: Bei λ_A → 0 wurden positive logG-Werte gefunden (prüfe Gain-Setup).



Modus: weighted

  Einträge: 172

  Agreement (direct vs criterion): 0.959 (n=172)

  logG-Statistiken: min=-152.6973, median=180.2568, max=370.7849

  Beispielhafte λ_A-Stabilitätsraten:

    - K=8, λ_A=0.00000 → 0.000

    - K=8, λ_A=0.80000 → 0.056

    - K=16, λ_A=0.00000 → 0.000

    - K=16, λ_A=0.80000 → 0.056

    - K=32, λ_A=0.00000 → 0.000

    - K=32, λ_A=0.80000 → 0.056

    - K=64, λ_A=0.00000 → 0.000

    - K=64, λ_A=0.80000 → 0.118

  Disagreement-Hotspots:

    - K=8, λ_A=0.00000 → 0.000

    - K=8, λ_A=0.80000 → 0.056

    - K=16, λ_A=0.00000 → 0.000

    - K=16, λ_A=0.80000 → 0.056

    - K=32, λ_A=0.00000 → 0.000

    - K=32, λ_A=0.80000 → 0.056

    - K=64, λ_A=0.00000 → 0.000

    - K=64, λ_A=0.80000 → 0.059

  WARN: Bei λ_A → 0 wurden positive logG-Werte gefunden (prüfe Gain-Setup).



Boundary-Analyse

  uniform: direct=7 kritische Punkte, criterion=7

    Δλ_A max=0.6086, median=0.3348

  weighted: direct=9 kritische Punkte, criterion=9

    Δλ_A max=0.6527, median=0.3566

  Weighted ≤ Uniform: 1.000 der 7 Paare erfüllen λ_A,crit(weighted) ≤ λ_A,crit(uniform)



Numerische Zusammenfassung (aus JSON):

  points: 348

  agreement_ratio: 0.9655172413793104

  max_abs_diff_lambdaAcrit: 0.652734375

  any_crossings: True

  notes: Adaptive sweep complete; inspect CSV for detailed transitions.

  crossings_direct: 16

  crossings_criterion: 16



Scope des Beweises

  Modellbeweis: Stabilität im SSZ-Rahmen gesichert (siehe T1).

  Kein Natur-/GR-Endbeweis: Offene Schritte →

    - Ableitung der SSZ-Dämpfung aus den GR-Grundgleichungen (Stress-Energie statt Phänomenologie).

    - Spektral-/Operatorbeweis (Selbstadjungiertheit, Energiemorawetz, Lyapunov).

    - Kontinuumslimit K → ∞ inkl. Gitter-Unabhängigkeit.

    - Kerr-Grenzfälle & Kopplung zu Teukolsky-Moden ohne "Cavity"-Artefakte.

    - Beobachtbare Vorhersagen (QNM-Shifts, Echo-Signaturen, Spin-Cutoff) als empirischer Test.



Hinweis: Agreement-Warnschwelle = 0.95.