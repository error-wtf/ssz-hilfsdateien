φ/2 and β in Segmented Spacetime —

Derivation, Justification, Calibration (EN)

Authors: Carmen N. Wrede, Lino P. Casu

Date: 08 Sep 2025

Version: 1.0 (Preprint)

Abstract

We close a key gap in the Segmented Spacetime (SSZ) framework by: (i) providing a geometric–physical
r =φ
  in   a   piecewise   (C²)   metric;   (ii)   defining   a  well-posed   β   constant  as   a   scale-free   coupling

justification of the  φ/2 correction  and showing how it emerges as a  natural coupling radius
(φ/2) rs
between the mass-dependent segmentation correction  

  and observables; and (iii) presenting a

Δ(M )

data-driven   procedure  for  estimating   β  with   uncertainties.   The   result   is   a   reproducible   roadmap

enabling others to calibrate scripts and analyses to empirical data in a consistent way.

1. Motivation and Problem Statement

The   SSZ   formalism   augments   GR   by   replacing   pure   curvature   with  discrete   segmentation  of

spacetime.   Two   building   blocks   have   proven   useful   in   practice:   1.   a  piecewise   metric

smooth C² transition between near and far regions; and 2. a mass-dependent correction

  with   a

A(r)
Δ(M )

 that

scales weakly and is tightly constrained by observables (orbits, shadows, frequency shifts).

Open issues were:  why  the  switch radius  is  

r =φ

(φ/2) rs

and  how  to determine  β  from data rather

than guessing. This paper supplies both the justification and a calibratable recipe.

2. Geometric Basis: φ‑Spiral and Segment Transition

The segmented geometry is characterized by scaling spiral segments. Schematic metric ansatz: 

A(r) = 1 −

2rs
r

F (r; r , p) ,
φ

B(r) =

1
A(r)

,

with 

F

 decaying steeper in the inner region (Reg. 1) than in the outer region (Reg. 2): 

F (r; r , p) =
φ

1

1
1 + (r /r)

φ

,

p

F (r; r , p) =
φ

2

1

1 + (r /r)

φ

p/2

.

Between 

rL

 and 

rR

preferred coupling radius

 , a quintic/cubic Hermite blend yields a C² transition. Claim: There exists a 
A , A1
2

 at which values, slopes, and curvatures of the two kernels 

rφ

 achieve

the best joint match inside the blend window—minimizing a “curvature-norm error”. Variation of the

functional 

J (r ) =φ

rR

∫rL

(

′′

[A (r)] +

2

2
′
λ [A (r)]

)

w(r) dr ,

λ >

0

1

yields the stationarity condition 

∂J
∂rφ

=

0 ⟹ ≈

rφ
rs

φ
2

,

for typical exponents 

p ∈ [4, 8]

 . Interpretation:

φ/2

 marks the conditioning-stable coupling point

where the inner spiral‑segmented core and the asymptotically GR‑like exterior connect with minimal

curvature compensation, preserving PPN exactness in the far-field series.

Result 1 (φ/2 correction).  The  physical  coupling point of the piecewise metric sits at
r =φ
energy-condition issues) and stabilizes shadow and orbital signatures.

 . This choice minimizes transition artefacts (spurious stresses, unphysical

(φ/2) rs

3. Mathematical Sketch of the φ/2 Result

For 

A (r) =

i

1 − 2r F (r)/r
s

i

 one has 

A (r) =

′
i

2r

Fi
s r2
(

−

′
Fi
r

,
)

A (r) =

′′
i

2r
s

′
2Fi
r2

(

−

2Fi
r3

−

′′
Fi
r

.
)

Imposing C² matching at 

r , rL R

 and comparing the exponent-dependent derivatives 

′′
′
F , F1
1

 vs. 

′′
′
F , F2
2

leads to a moment-balance of the form 

μ (p)
1

[

p

rφ
r
( ) ]

r≈rL

≃

μ (p)
2

[

rφ
r

( ) ]

p/2

,

r≈rR

which—under a narrow blend window 

r ≈L

r ≈R κ rφ

 —implies 

κ ≈ φ

 and 

r /r ≈
s
φ

φ/2

. Full

constants 

μ (p)
1,2
below (Sec. 5).

 can be supplied in a supplementary note; the key point is the observational criterion

4. Dynamic View: φ/2 as Effective “Segment Boundary”

The φ‑spiral scaling interprets time dilation as segment counting. At 

rφ

 the segment density is such

that the inner, more finely segmented core becomes  compatible  with the outer GR‑like scale. Hence,
φ/2
coefficients remain stable.

  explains   why   transition   artefacts   are   minimal:  photon   sphere,   shadow   radius,   and   PPN

5. Observational Criterion (Validation of the φ/2 Point)

We enforce, simultaneously: - (i) PPN exactness outside (

β = γ = 1

 ); - (ii) Energy conditions satisfied

through the transition; - (iii)  Shadow consistency  (Sgr A, M87); - (iv)  C² continuity  of the piecewise

metric.

The φ/2 point is the switching radius where these four constraints can be met simultaneously without
r =φ

fine-tuning   the   blend   window.   In   practice:   set  

  →   Hermite   blend   →   run   tests   (PPN,

(φ/2) rs

energy, shadow).

2

6. The β Constant: Definition and Role

We   define  β  as   a  dimensionless  coupling   between   the  mass-dependent   segmentation   correction
Δ(M )

 and observables, via an effective coupling radius

r (M ; β) =
φ

φ
2

r
s

[

1 + β Δ(M )

]

with 

r =s

2GM /c2

 . The function 

Δ(M )

 varies slowly and can be taken (as in code) as a normalized

raw-delta form. β is not the PPN β (which remains 1); it parameterizes only the additional 

segmentation fineness beyond the GR limit.

Implications: - 

β = 0

 ⇒ pure φ/2 transition without extra mass scaling (SSZ reduces to the GR limit of

the piecewise metric outside). -  

β

= 0

 ⇒ small, controlled, mass-dependent shifts of  

 and thus fine

rφ

modifications to shadows, orbits, and time-dilation observables.

7. Estimating β from Data (Algorithm)

Target:  A dataset  

D = {(Obs , Σ , M , … )}

i

i

i

  (e.g., orbits, shadow diameters, frequency shifts) yields

residuals

ε (β) =
i

Model(M ; r (M ; β)) −
φ

i

i

Obs ,i

which we minimize with a robust objective 

Φ(β) = median ∣ε (β)∣ .

i

i

Uncertainties via bootstrap CIs and an exact binomial sign test (is SSZ systematically closer to data

than GR×SR?).

Procedure:  1.  Preparation:  choose  

  (e.g.,   the   normalized   raw_delta(M)   used   in   code).   2.

Initial estimate: linearize 

rφ

 in 

β

Δ(M )
 and solve 

β =0

arg

min
β

w (r

φ,pred

∑ i
i

(M ; β) −

i

r
φ,inv

2
(Obs )) ,
i

where 

rφ,inv

 is obtained by inverting the corresponding observable (shadow/orbit/shift). 3. Refinement:

1‑D Brent/Golden‑section search on 

Φ(β)

 around 

β0

 . 4. Uncertainty:

Nboot

 resamples → distribution

of 

β

 → median and (16,84)‑percentiles. 5. Validation: (a) PPN test (β=γ=1 outside), (b) energy

conditions, (c) sign test vs. GR×SR baseline.

Output:

±β^

σβ

 with quality metrics (median deviation, sign‑test p‑value).

8. Units and Practical Implementation

• 

Core formulas use only 

G, c, φ, rs Δ(M )
Inversion from observables (e.g., shadow): 
• 
r (M ; β)
φ

 is dimensionless.
κ rs
b =ph
 only at higher order, hence PPN coefficients remain unchanged.

κ = 3

 (GR: 

/23

 on 

κ

 ; 

 ); SSZ corrections act via 

3

• 

r (M ; β)
Code hook: Replace fixed 
 and run the above calibration on your
φ
datasets (e.g.,  real_data_full.csv ). Existing bootstrap/sign‑test utilities can be reused.

(φ/2) rs

r =φ

 by 

9. Consistency with GR/SR

• 

PPN limit: Outer series 

A(U ) = 1 − 2U + 2U +2 O(U ) ⇒3

β

=PPN

γ
=PPN

1

 . SSZ‑β is a 

different coupling (segmentation), leaving PPN coefficients intact.

• 

Energy conditions: The φ/2 choice minimizes unphysical stresses in the blend; small

β‑corrections keep conditions within tolerance.
≪ 1

Shadows & QNMs: β‑driven changes are 

• 

 % and become precision tests.

10. Reporting Template (for Reproduction)

Table A (Calibration):

β^

 , CI

68%

 , median deviation (SSZ vs. data), sign‑test p.

Table B (Robustness): sensitivity to 

p

 , blend width, alternative 

Δ(M )

 .

Fig. 1:

Φ(β)

 and bootstrap distribution.

Fig. 2: Residuals vs. mass.

11. Discussion

The  φ/2 correction  is not a numerical artefact but the  variationally preferred  coupling point of a

piecewise, segment‑driven metric.  β  is the natural,  low‑scaling  complement that introduces mild mass

dependence   without   disturbing   the   GR   limit.   Together   they   yield   a  simple,   reproducible  recipe

calibrated to observations.

12. Conclusion

With 

r =φ

(φ/2) rs

 and a data‑determined  , SSZ is sufficiently closed to (i) reproduce GR/SR in the

β^

exterior exactly, (ii) introduce structurally faithful interior modifications, and (iii) deliver precise, testable

predictions. The community gets a clear replication roadmap.

Appendix A — Practical Pseudocodes

A1. φ/2 Blend (Cubic/Quintic Hermite) 1. Set 

r =φ

(φ/2) rs

 ; choose 

p ∈ [4, 8]
 .

2. Define 

F , F1
2

3. Choose narrow 

 ; compute 
[r , r ]
L R

A , A1
2
 around 

 and derivatives.
κ rφ κ ≈ φ

 ).

 (

4. Blend with Hermite polynomials; verify C² and energy conditions.

A2. β Calibration (1‑D)

input: data D, function Delta(M), model pipeline

beta0 = LSQ_initial_estimate(D)  # linearized

4

beta_hat = argmin_beta median(|residuals(beta)|)

CI = bootstrap(beta_hat; Nboot)

signtest = exact_binomial_test(signs_vs_GR)

References

1. 

Segmented Spacetime – A New Perspective on Light, Gravity and Black Holes. Wrede & Casu

(preprint).
File:  SegmentedSpacetime-ANewPerspectiveonLightGravityandBlackHoles.pdf .

2. 

Segmented Spacetime – Solution to the Paradox of Singularities. Wrede & Casu (preprint).
File:  SegmentedSpacetime-Solutiontotheparadoxofsingularities.pdf .

3. 

Segmented Spacetime and the Natural Boundary of Black Holes: Implications for the

Cosmic Censorship Conjecture. Wrede & Casu (preprint).
File:  SegmentedSpacetimeandtheNaturalBoundaryofBlackHoles-
ImplicationsfortheCosmicCensorshipConjecture.pdf .

4. 

Segmented Spacetime and φ as a Temporal Growth Function. Wrede & Casu (preprint).
File:  Segmented Spacetime and ϕ as a Temporal Growth Function.pdf .

5. 

Segmented Spacetime and π. Wrede & Casu (preprint).
File:  SegmentedSpacetimeandPi.pdf .

6. 

Bound Energy and the Structural Origin of the Fine‑Structure Constant. Wrede & Casu

(preprint).
File:  SegmentedSpacetimeBoundEnergyandtheStructuralOriginofthefine-
structureconstant.pdf .

7. 

Segment‑Based Group Velocity. Wrede & Casu (preprint).
File:  Segment-BasedGroupVelocity.pdf .

8. 

Emergent Spatial Axes from Orthogonal Temporal Interference. Wrede & Casu (preprint).
File:  EmergentSpatialAxesfromOrthogonalTemporalInterference.pdf .

9. 

Segmented Spacetime – A Geometric‑Topological Model (DE). Wrede & Casu (preprint).
File:  Segmentierte Raumzeit – Ein geometrisch-topologisches Modell.pdf .

10. 

Segmented‑Spacetime‑Mass‑Projection‑Unified‑Results (GitHub repository).

URL: https://github.com/LinoCasu/Segmented-Spacetime-Mass-Projection-Unified-Results

11. 

LOST_EINSTEIN_PAPERS (GitHub repository).

URL: https://github.com/LinoCasu/LOST_EINSTEIN_PAPERS

12. 

Gravitational Redshift (reference formulas and weak‑field limit).

URL: https://en.wikipedia.org/wiki/Gravitational_redshift

5