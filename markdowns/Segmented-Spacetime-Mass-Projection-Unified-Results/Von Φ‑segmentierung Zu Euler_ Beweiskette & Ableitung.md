Von φ‑Segmentierung zu Euler: Beweiskette &

Ableitung

Kurzfassung

Wir   zeigen,   wie   das  φ‑Segmentgitter  (diskrete   Skalenstufen)   auf   die  Euler‑Darstellung
1 + z = φn

zurückgeführt   werden   kann.   Daraus   folgen   (i)   die   Lattice‑Vorhersage  

ex+iθ
für

Rotverschiebungen   bzw.   Frequenz‑Verhältnisse,   (ii)   die   Darstellung   als  logarithmische   Spirale  mit

zentrale   Reduktionsschritt   nutzt   die  Polarzerlegung  eines   komplexen   Exponenten:   Magnitude  

festem   Wachstumsparameter,   und   (iii)   konkrete,   falsifizierbare   Tests   in   Labor‑   und   Astrodaten.   Der
ex
 , die Topologie legt

 (Drehung). Die φ‑Segmentierung fixiert 

 pro Segment zu 

eiθ

x

ln φ

(Skala) × Phase 
Δθ

 pro Segment fest.

1. Axiome & Definitionen

A1   (Segment‑Postulat).  Raumzeit   besitzt   Diskretstufen  

Sn

  mit  konstanter   lokalen   Kopplung  und

konstanter effektiver Metrik innerhalb eines Segments.

A2   (Skalenfaktor).  Beim   Übergang  

S →n

Sn+1

  skaliert   jede   relevante   Längen‑/Zeit‑/Frequenzgröße

durch den festen Faktor
f

f ↦ f /φ

 fällt wie 

 .

φ

 (goldener Schnitt). Beispiel: Wellenlänge 

 wächst wie 

λ

λ ↦ φ λ

 ; Frequenz

A3   (Winkel‑Quantelung).  Die   Segmentgrenze   entspricht   einer   festen  Phasenrotation

Δθ

  (z. B.

Viertelkreis 

Δθ = π/2

 oder allgemein 

2π/N

 ).

D1 (Ratio, Redshift).

R ≡ f

emit

/f =
obs

1 + z = λ /λ
0

obs

 .

Hypothese H_φ (Lattice).

1 + z = R = φn

,

n ∈

Z.

2. Lemma: Logarithmisches Gitter in log‑Skala

Aus A2 folgt 

ln R = n ln φ

 . Daher ist 

ln(1 + z)

periodisch modulo 

ln φ

 , und die beste ganzzahlige

Stufe ist 

Residual 

ε =

ln R
−ln φ

∈n^

1
(− ,
2

1
2

]
 .

=n^

round

ln R
ln φ

.
)

(

1

 
3. Euler‑Reduktion: von φ‑Stufen zur Exponentialform

Die Bewegung/Übertragung über Segmente kann im komplexen Plan parametrisiert werden: 

z =k

iθk
r e =
k

k ik Δθ

r φ e
0

=

k(ln φ+i Δθ)

r e
0

.

Schreibweise mit Euler:

=x+iθ
e

x
e (cos θ +

i sin θ)

 .

Folgerungen.  -   Pro   Segment   multipliziert   die  Magnitude  um  

e =ln φ

φ

  (Skalen‑Jump),   -   die  Phase

rotiert   um  

Δθ

(Topologie/Geometrie   der   Grenze),   -   der   kontinuierliche   Grenzpfad   ist   eine

logarithmische Spirale

bθ
r(θ) = r e ,

0

Für Viertelkreis‑Segmentierung 

π
Δθ = 2

 gilt 

2 ln φ

b = π

b =

ln φ
Δθ

.

 .

Damit ist die φ‑Segmentierung exakt die Betragskomponente der Euler‑Form; die Grenzrotation liefert

die  Phasenkomponente.   Die   Lattice‑Physik   ist   daher   die   reelle   Achse  

x = ln φ

  einer   komplexen

Euler‑Exponentialbewegung.

4. Satz (Euler‑Darstellung der φ‑Skalierung)

Satz. Unter A1–A3 existiert eine Parametrisierung der beobachtbaren Verhältnisse 

R

 als reeller Anteil

eines komplexen Exponenten, 

R = e

n ln φ

=

n(ln φ+iΔθ)
e

,

so dass die φ‑Stufe 
1 + z = φn

n
 , für Frequenzen 

f =obs

f

emit

n

/φ

 .

 die Magnitude steuert, die Geometrie 

 die Phase. Für Spektren/Zeitraten folgt

Δθ

Beweis. Direkt aus der Euler‑Zerlegung und dem Produktgesetz der Exponentialfunktion. □

5. Rückführung auf die „Euler‑Formel am Anfang“

Viele Darstellungen im Projekt beginnen mit einer Euler‑Spirale des Typs 

r(θ) = exp(k θ), mit k =

ln φ
π

(oder  quivalent).

a¨

Dies ist ein Spezialfall der obigen Herleitung mit 

Δθ

 passend gewählt. Allgemein gilt 

r(θ) = e

ln φ

=θΔθ

φ

θ/Δθ

.

Wählt man 

θ = π

als Referenz‑Halbumlauf und 

Δθ = π/2

(Segment als Viertelkreis), so ist 

r(π) = φ

π/(π/2)

=

φ .2

2

 
Andere Normalisierungen (z. B. 

k
additiv; die Ableitungsstruktur bleibt identisch. Entscheidend ist: Der Wachstumskoeffizient ist

 ) entsprechen nur einer Wahl von 

 und verschieben 

r(π) = 1

r0

proportional zu 

ln φ

 , also rein reell, und die Rotation ist rein imaginär (

iθ

 ). Genau das ist Eulers

Zerlegung.

6. Physik: von der Spirale zur Rotverschiebung

• 

Zeitdilatation/Frequenz: Jede durchlaufene Grenze erhöht die lokale Eigenzeit‑Skala um 

φ f
 ⇒ 

fällt um 

1/φ R = f
 ⇒ 
Wellenlänge/Redshift:

• 

φn

emit
λ
ln(1 + z) = n ln φ

/f =
obs
 wächst pro Segment um 
ln

 ⇒ Gitter in 

.

• 

Log‑Linearität:

 ⇒ 

φ 1 + z = λ /λ =
 -Koordinaten.

obs

0

φn

.

7. Testbare Vorhersagen

1. 

2. 

3. 

Ganzzahltest:

round(ln R/ ln φ)

n =∗
Messunsicherheiten).
ε
Periodizität: Histogramm von 
 flach unter Nullhypothese, spitz um 0 unter 
H :φ R = φn
 vs. uniformes oder kontinuierliches Modell; φ‑Modell gewinnt,
wenn Daten φ‑quantisiert sind.

 (Fehlerfortpflanzung aus

 mit kleinem Residuum 

ΔBIC: Vergleiche 

∣ε∣ ≤ ϵ

Hφ

 .

8. Mathematische Beweiskette (Skizze)

Lemma   1   (Skalenhomomorphie).  Die   Abbildung  
(Z, +) → (R , ⋅)+

 .

n ↦ R = φn

  ist   ein   Gruppenhomomorphismus

Lemma 2 (Euler‑Einbettung).

∃ Δθ > 0

 mit 

z =n

n(ln φ+iΔθ)

r e0

 und 

∣z ∣ =n

φn

 .

Satz 2 (Äquivalenz). H_φ  ist äquivalent zur Aussage, dass die beobachtbaren Ratios  

R

  die  Beträge

einer Euler‑Exponentialbahn auf einem logarithmischen Gitter sind.

Korollar (Rotverschiebungs‑Gitter).

ln(1 + z) ∈ (ln φ) Z

 bis auf Messfehler.

9. Konsistenz & Grenzen

• 

Kontinuierliche Näherung: Für große 

n

 ist 

ln R

 fein quantisiert; lokal erscheint es

quasi‑kontinuierlich.

• 

Geometrische Wahl von 

Δθ

 : Viertelkreis (

 ) ist natürlich, andere Segmentierungen (

N

 pro

π/2
b = ln φ/Δθ

Umdrehung) sind möglich; sie ändern nur 

 , nicht die φ‑Logik.

• 

Falsifizierbarkeit: Systematische Abweichungen der Residuen von 0 oder Verlust der 

ΔBIC‑Überlegenheit widerlegen H_φ.

3

10. Praktische Ableitungsschritte (Rezept)

1. 

Messgrößen → Ratio: Bestimme 

2. 

Ganzzahl‑Schätzer:

n =∗

/f
R = f
round(ln R/ ln φ)

emit

 oder 

obs
 ; Residuum 

1 + z = λ /λ
0

 .

obs
ε = ln R/ ln φ − n∗
 .
k(ln φ+iΔθ)
r e0

z =k

3. 

Euler‑Einbettung: Verifiziere, dass die Daten auf einer Bahn 

 liegen

(Magnitude richtig, Phase mit Geometrie kompatibel).

4. 

Modelle vergleichen: ΔBIC (φ‑Lattice vs. uniform/GR‑kontinuierlich), Vorzeichentest der |

Fehler|.

11. Verbindung zu den einleitenden Euler‑Formeln der Paper

Die   häufig   verwendete   Startform  

r(θ) = exp(k θ)

ist   genau   die  reelle  Komponente   der   oben

abgeleiteten komplexen Euler‑Form. Setzt man  

k = ln φ/π
man dieselbe logarithmische Spirale, deren Wachstum durch 

(oder äquivalente Normierungen), erhält
ln φ

 (Segment‑Skala) und deren Drehung

θ
durch  

  (Segment‑Topologie)   festgelegt   ist.   Damit   ist   die   „Euler‑Formel   am   Anfang“   kein   separates

Axiom, sondern die kompakte Schreibweise der φ‑Segmentlogik.

12. Fazit

Die   φ‑Logik  ist  eine   Euler‑Logik:   Diskrete  Skalenjumps  sind   die  reelle   Exponential‑Komponente,

Segment‑Grenzrotationen die imaginäre. Alles reduziert sich auf 
1 + z = φn
testbar und falsifizierbar.

,   die   logarithmische   Spirale   und   die   beobachteten   Signale   in   Spektren/Uhren   –   präzise

ex+iθ

 mit 

x = ln φ n

 . Daraus folgen

4