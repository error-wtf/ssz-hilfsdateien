# SSZ Glossar (Deutsch)

**Status:** KANONISCH

---

## Kernkonzepte

| Begriff | Symbol | Definition |
|---------|--------|------------|
| **Segmentdichte** | Ξ (Xi) | Dimensionsloses Skalarfeld zur Messung der Raumzeitsegmentierung am Radius r. Bereich: 0 ≤ Ξ ≤ 0.802 |
| **Zeitdilatation** | D | SSZ-Zeitdilatationsfaktor: D = 1/(1+Ξ). Verhältnis von Eigenzeit zu Koordinatenzeit |
| **Skalierungsfaktor** | s | Radiale Skalierung: s = 1+Ξ = 1/D. Effektiver Brechungsindex |
| **Schwarzschild-Radius** | r_s | r_s = 2GM/c². Charakteristischer Gravitationsradius |
| **Goldener Schnitt** | φ | φ = (1+√5)/2 = 1.618... Strukturkonstante in SSZ |
| **Schnittpunkt** | r* | Radius, an dem D_SSZ = D_GR für eine angegebene Xi-Form gilt: r*/r_s = 1.594811 (Abkling/global) oder 1.386562 (Sättigung/lokal) |

---

## Regime

| Begriff | Definition |
|---------|------------|
| **g1 (Schwaches Feld)** | Bereich r/r_s > 2.2. SSZ ≡ ART. Formel: Ξ = r_s/(2r) |
| **g2 (Starkes Feld)** | Bereich r_s/r < 1.8. SSZ ≠ ART. Formel: Ξ = min(1-exp(-φr_s / r), Ξ_max) |
| **Mischzone** | Übergangsbereich 1.8 ≤ r/r_s ≤ 2.2. Hermite-C²-Interpolation |
| **Photonensphäre** | Bereich 2.2 ≤ r/r_s ≤ 3.0. SSZ-optimale Zone |
| **Kohärenz-Kollaps** | Irreversibler Übergang g1→g2. Nicht umkehrbar |

---

## Methoden

| Begriff | Definition |
|---------|------------|
| **Ξ-Proxy** | Direkte Verwendung von Ξ für zeitartige Observablen (Uhren, Rotverschiebung) |
| **PPN** | Parametrisierter Post-Newtonscher Formalismus. Für Null- (Licht) und Orbitobservablen |
| **PPN-Vervollständigung** | Multiplikation des Ξ-Ergebnisses mit (1+γ) für Null-Observablen |
| **Faktor-2-Regel** | Null-Observablen brauchen PPN (1+γ)=2, nicht nur Ξ |
| **Anti-Zirkularität** | Prinzip: Formeln nie gegen Daten kalibrieren, die sie vorhersagen |

---

## Schlüsselwerte

| Begriff | Wert | Bedeutung |
|---------|------|-----------|
| **Ξ_max** | 0.802 | Maximale Segmentdichte (am Horizont) |
| **D_min** | 0.555 | Minimale Zeitdilatation (am Horizont) |
| **z_max** | 0.802 | Maximale Rotverschiebung (am Horizont) |
| **r*/r_s** | 1.594811 | Abkling/globaler `D_SSZ = D_GR`-Schnittpunkt |
| **r*/r_s** | 1.386562 | Sättigung/lokaler `D_SSZ = D_GR`-Schnittpunkt |
| **φ/2** | 0.809 | Kopplungsfaktor |

---

## Objekte & Experimente

| Begriff | Definition |
|---------|------------|
| **Dunkler Stern** | SSZ-Alternative zum Schwarzen Loch — keine Singularität, kein Ereignishorizont, endliches D |
| **Natürliche Grenze** | SSZ-Ersatz für Ereignishorizont: r_φ = (φ/2)·r_s·[1+β·Δ(M)] |
| **Pound-Rebka** | 1960er Experiment zur Bestätigung der gravitativen Rotverschiebung über 22.6 m |
| **Cassini** | 2003 Shapiro-Verzögerungsmessung: γ = 1.000021 ± 0.000023 |
| **S2-Stern** | Stern in Sgr-A*-Orbit — Schwachfeld-Test (SSZ ≡ ART) |
| **G79.29+0.46** | LBV-Nebel — exploratorische Molekülzonen-Diagnostik; aktueller All-Tests-Lauf enthält eine Parsec-Konversionswarnung |

---

## Mathematische Begriffe

| Begriff | Definition |
|---------|------------|
| **Hermite-C²-Interpolation** | Quintisches Polynom mit Stetigkeit von Funktion, erster und zweiter Ableitung |
| **Δ(M)** | Massenabhängige Korrektur: Δ = A·exp(-α/M^B). Aus φ-Geometrie, nicht Fitting |
| **v_esc** | Fluchtgeschwindigkeit: c·√(r_s/r) |
| **v_fall** | Fallgeschwindigkeit: c·√(r/r_s) |
| **Kinematische Schließung** | v_esc × v_fall = c² (universelle Invariante) |

---

## Veraltet (VERBOTEN)

| Begriff | Status |
|---------|--------|
| **Ξ = (r_s/r)² × exp(-r/r_φ)** | ❌ VERBOTEN — veraltete Formel, nie verwenden |
| **90/110 Regimegrenzen** | ❌ Das sind Testpunkte, KEINE Regimegrenzen |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
