Kinematische Schließung in segmentierter

Raumzeit: escape vs. fall

Autoren: Carmen Wrede, Lino Casu

Fokusfassung: Vertieft §4 „Kinematic closure: escape vs. fall“. ϕ‑/β‑Kalibrierungen werden erklärt, Tests

nur als Quellenhinweis (GitHub).

Abstract

v sce

−1/2

  .   Daraus   wird   ein  GR‑konjugierter   Fallwert

in   der  segmentierten   Raumzeit   (SSZ)  formal   hergestellt   wird.   Ausgangspunkt   ist   die
(1 −
  über   Gleichsetzung   der   lokalen
r /rs

Wir zeigen, wie die duale Beziehung zwischen Fluchtgeschwindigkeit  
vf all
GR‑Rotverschiebung   eines   stationären   Beobachters   im   Schwarzschild‑Außenraum,  
r /r)
s
Lorentzfaktoren   definiert.   Dieser   liefert   exakt
v
esc
v
esc
v
f all

  zu   erhalten,   führen   wir   eine  segmentierte   Normierung  des   Fallwertes   ein:
GR
f all

 . Diese Normierung ist kein physikalischer 3‑Geschwindigkeitswert, sondern

  .   Um   die   im   SSZ‑Ansatz   gewünschte  produkt‑invariante   Schließung

2
c (r /r)
(r) =
s
c2
(r) =
(r/r ) v
s

(r) v
(r) v
f all
(r) :=

GR
(r)
v
f all
c
(r) =

  und   damit   das   Produkt

  und einem  Fall‑Parameter

(r) =

GR
v
f all

GR
f all

(r)

GR

γ

ein  skalengebundener   Parameter  des   SSZ‑Formalismus,   der   die   operative   Brücke   zwischen

klassischer Energiebilanz und diskreter ϕ‑Skalierung bildet. Wir erläutern den Platz der ϕ‑Kalibrierung

(Gitter in 

ln R

 ) und die β‑Massenfeineinstellung am 

φ/2

 ‑Kopplungspunkt, ohne empirische Tests zu

duplizieren. Verweise auf Reproduktionscode und Logs erfolgen ausschließlich über GitHub.

1. Notation und Rahmen

2GM /c2

• r =s
• v
• 

esc

(r) =

2GM /r
GR‑Redshift/Lorentz:

 Schwarzschild‑Radius, 
c

U = GM /(rc )2

 . 

 . 
(1 − r /r)
 mit 
 , 

r /rs
(r) =
φN
 und Quantisierung, wenn 

 . 
N ∈ Z ln R = N ln φ

−1/2

s

 . 
ΔU ≈ N ln φ

 . 

• 

ϕ‑Gitter:

R = f

• 

Euler‑Hülle:

=
γ
GR
/f =
obs
R ≈ exp(ΔU )
r ≈φ

emit

• 

Kopplungspunkt:

φ (φ/2) rs

 mit milder Massen‑Feineinstellung über 

β

 (nicht PPN‑β).

2. Konstruktion des Fall‑Terms

2.1 GR‑konjugierter Fallwert

Setze   den  

lokalen   Lorentzfaktor   einer   hypothetischen   Fallbewegung   gleich   dem

r
GR‑Rotverschiebungsfaktor am selben 

 : 

Daraus folgt 

γ

GR

(r) =

(1 − r /r)

s

−1/2

=

(1 − (v

GR
f all

2 −1/2

/c) )

.

(v

GR
f all

2
/c) =

r /r ⇒
s

GR
v
f all

(r) =

c

r /rs

.

1

 
 
Damit gilt exakt

v
esc

(r) v

GR
f all

(r) =

(c

r /rs

2
) =

2
c (r /r).
s

Gleichung (2.1) ist eine produkt‑gewichtete Schließung mit dem dimensionslosen Faktor 

r /rs

2.2 Segmentierte Normierung zum produkt‑invarianten Dual

Der SSZ‑Formalismus benutzt eine skalierte Fall‑Variable

Dann folgt sofort

v
f all

(r) :=

r
rs

GR
v
f all

(r) =

r
rs

c

rs
r

=

c

r
rs

.

v
esc

(r) v

f all

(r) =

(c

r /rs

) (c

r/rs

) =

c .2

(2.1)

 .

(2.2)

(2.3)

Die Gleichung (2.3) ist die im Screenshot geforderte kinematische Schließung. Wichtig:

v
f all

(r)

 nach

(2.2) ist kein physikalischer 3‑Geschwindigkeitswert, sondern ein Dual‑Parameter, der die reziproke

Skalenkopplung der segmentierten Beschreibung ausdrückt.

2.3 Gültigkeitsbereich und Interpretation

• 

(2.1) gilt allgemein im Schwarzschild‑Außenraum. 

• 

(2.3) ist eine definitorische Dualität des SSZ‑Parameters (2.2). Sie macht die operative Brücke

sichtbar: Wenn 

vesc
dass das Produkt konstant bleibt. 

 in schwachen Feldern klein wird, wächst der skalen‑duale Fallparameter so,

• 

Physikalische Messungen koppeln über Ratios und ϕ‑Gitter; die Dualität steuert die 

Skalenseite, nicht die lokale 3‑Kinematik von Testteilchen.

3. Verbindung zur ϕ‑Skalierung und zur Euler‑Hülle

 . Die Euler‑Hülle

Die messbare Größe ist das Frequenz‑/Uhren‑Ratio  
  . SSZ postuliert  diskrete Skalenübergänge  mit
R = φN
ΔU ≈ N ln φ
Die kinematische Schließung (2.3) liefert dazu die mechanische Seite: Sie bindet die potentielle Energie
∝ 1/r
Inneren.

  an   einen   reziproken   Skalenparameter   und   verhindert   divergierende   Beschleunigerbilder   im

 reproduziert GR; sie fällt auf das ϕ‑Gitter, wenn 

R ≈ eΔU

 .

R

4. ϕ‑Kalibrierung (Erklärung ohne Tests)

• 

Gittervariable:

∗

n (R) =

ln R/ ln φ
 . 

N = round(n )∗

 . 

• 

Segmentanzahl:

• 

Residual:

ε = n −∗ N

 misst die Abweichung vom idealen Gitter. 

Geometrische Rückführung: Eine einzige Euler‑Exponentialbewegung 
• 
i)θ)
Rotation (Phase) und Skalierung (Betrag) gekoppelt.

 liefert pro Vierteldrehung 

k = 2 ln φ/π

Δθ = π/2

 den Faktor 

 mit 

z(θ) = z exp((k +
0
φ

 im Betrag. Damit sind 

2

5. β‑Feineinstellung am 

φ/2

 ‑Kopplungspunkt (Erklärung)

• 

Kopplungspunkt:

φ (φ/2) rs
die GR‑Außenserie und PPN‑Werte. 

r ≈φ

 minimiert Blend‑Artefakte einer C²‑Stückmetrik und erhält

• 

β‑Term:

r (M ; β) =
φ
β

r [1 +φ

β Δ(M )]

 , 

∣β∣ ≪ 1

 . 

• 

Bedeutung:

ist nicht die PPN‑β. Er verschiebt nur sanft die innere Skalenlage in Abhängigkeit

eines langsamen Massen‑Proxys 

Δ(M )

 . 

• 

Konsequenz: Außen bleibt PPN‑kompatibel; innen reguliert die Segmentierung die Krümmung

ohne Singularitäten.

6. Physikalisches Bild in Kürze

1) Außen: GR‑Hülle, kontinuierlich, PPN‑Werte identisch zu GR in gemessener Ordnung.

2) Grenzen: Diskrete ϕ‑Schritte in Ratios 

R

 .

3)  Innen:  Stückweise   konstante   Skalen,   C²‑Blend   um  

rφ

  ;   kinematische   Schließung   (2.3)   verknüpft

Skalen‑Dualität mit Energiebilanz.

4) Messstrategie: Nur noch Ratios und Gitterstruktur; numerische Tests werden nicht hier, sondern im

Code belegt.

7. Quellenhinweis: Reproduktion und Tests (nur Verweis)

Alle Skripte, Logs und reproduzierbaren Läufe liegen in den GitHub‑Repos der Autor:innen, u. a.:

- Segmented‑Spacetime‑Mass‑Projection‑Unified‑Results — Kernskripte (ϕ‑Gitter, Euler‑Rückführung,
rφ β
 , 
- Zusatz‑Repos für Datenvorbereitung und Archiv‑Quellen.

 ).

Die Paper‑Fassung verweist auf die Repos; keine Testtabellen im Haupttext.

8. Schluss

v
Die produkt‑invariante Schließung 
esc
Fall‑Parameters (2.2). Zusammen mit der ϕ‑Kalibrierung und der sanften 

v =
f all

β

c2

 entsteht aus der skalengebundenen Definition des

 ‑Feineinstellung liefert SSZ

ein  reduziertes,  aber  belastbares  Gerüst:  außen  GR‑gleich,  innen  regulär,  und  operativ  durch  Ratios

testbar. Die empirischen Nachweise stehen ausschließlich im Code und den GitHub‑Protokollen.

3