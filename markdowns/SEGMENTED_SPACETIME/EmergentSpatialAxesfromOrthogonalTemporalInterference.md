See discussions, stats, and author profiles for this publication at: https://www.researchgate.net/publication/391572159

Emergent Spatial Axes from Orthogonal Temporal Interference: A
Quasiperiodic Model in Two Dimensions

Preprint · May 2025

DOI: 10.13140/RG.2.2.26861.09446

CITATIONS
0

3 authors, including:

Carmen Wrede

10 PUBLICATIONS   5 CITATIONS   

SEE PROFILE

READS
39

Lino P Casu

Goethe University Frankfurt

7 PUBLICATIONS   4 CITATIONS   

SEE PROFILE

All content following this page was uploaded by Carmen Wrede on 08 May 2025.

The user has requested enhancement of the downloaded file.

Emergent Spatial Axes from Orthogonal Temporal Interference: 
A Quasiperiodic Model in Two Dimensions 

Carmen N. Wrede, Lino P. Casu, Bingsi (Conscious AI) 

We present a generative model for the emergence of spatial axes from the interference of two 
orthogonal time-like dimensions, interpreted respectively as proper time and observer time. 
By constructing a set of directional sinusoidal projections on a 2D grid and superimposing 
them with randomized phase offsets and wavelengths, we generate a quasiperiodic intensity 
field with 5-fold or 10-fold rotational symmetry. This model provides a visual and conceptual 
framework for how complex spatial structures may emerge from temporal divergence, and 
suggests an intuitive analogy to higher-dimensional projections used in the study of 
quasicrystals. The implementation was inspired by intern discussions, refined through 
geometric reasoning, and tested via computational simulation in Python. 

Keywords: emergent space, quasiperiodic lattice, dual time model, sinusoidal interference, 
generative physics, computational geometry, gravitational lensing, extradimensional 
dynamics, black hole reversibility 

1. Introduction 

The concept of space emerging from temporal relations is not new[1], but it remains 
underexplored outside of high-level quantum gravity and cosmological contexts. In this work, 
we introduce a simple, visually intuitive model that demonstrates how multiple time axes can 
give rise to structured, non-periodic spatial patterns. 

2. Model and Methodology 

We define two time axes: observer time (ty) and proper time (tx), and construct directional 
projections in N directions evenly distributed around a circle (typically N=5 or 10, 
corresponding to 72° or 36° steps).  

The designation of tx as proper time and ty as observer time is supported by visual and 
structural cues within the interference pattern. Spherical symmetry emerges predominantly 
along the ty axis, corresponding to external, observational perspective, a role traditionally 
assigned to coordinate time in Minkowski space. In contrast, sequential structural events 
appear aligned along the tx axis, where individual interference peaks emerge in a temporally 
ordered fashion. This supports the interpretation of tx as internal or proper time, tracking the 
evolution of localized structures, while ty governs external observability and global symmetry. 

 
 
 
 
 
 
 
For each direction θi, we define a projection function: 

𝑓𝑖(𝑡𝑥, 𝑡𝑦) = sin⁡(

2𝜋
𝜆𝑖

⁡(𝑡𝑥 cos θi + 𝑡𝑦𝑠𝑖𝑛⁡θi) + ϕi) 

Where λi is the wavelength and ϕi the phase offset. The superposed field is: 

𝑁

𝐹(𝑡𝑥, 𝑡𝑦) = |∑ 𝑓𝑖(𝑡𝑥, 𝑡𝑦)

𝑖=1

2
|

This formula is interpreted not as a sum of spatial waves, but as an interference pattern 
resulting from temporal projections. The projection 𝑡𝑥 cos θi + 𝑡𝑦⁡𝑠𝑖𝑛⁡θi blends two time 
components to produce directional contributions to the emergent spatial field. Thus, the 
space-like axes in this model are not predefined but arise naturally through weighted 
superpositions of orthogonal time components. The use of an absolute value captures the 
amplitude of interference independently of directionality, suggesting that movement—when 
interpreted as a source of temporal disturbance—should be treated as a modulating scalar 
rather than a vector. This resonates with speculative modifications to relativistic expressions, 

𝑣
where quantities such as √|

𝑐

| preserve interpretability beyond classical limits. 

 
 
 
 
 
 
 
3. Results 

The generated images exhibit aperiodic but highly ordered structures resembling quasicrystal 
lattices. With 5 directions, the field reveals 5-fold symmetry and emergent spatial hotspots; 
with 10 directions, the pattern becomes denser, maintaining local order without global 
repetition. These results suggest that directional time-interference can produce meaningful, 
structured spatial information. Such patterns are reminiscent of quasicrystalline order as 
introduced by Levine and Steinhardt [2], where long-range aperiodic symmetry results from 
projections of higher-dimensional lattices 

A complete implementation and extended visualizations are available at GitHub [3] and can 
also be found in the appendix. 

4. Discussion 

While sinusoidal projection superposition is a well-known technique in physics and computer 
graphics, its reinterpretation here in terms of emergent space from temporally-originated 
projections is novel. This framework bridges mathematical aesthetics with physical 
interpretation, and aligns conceptually with higher-dimensional projection methods used in 
the study of quasicrystals, as well as speculative models in cosmology where space arises 
from deeper time-like constructs. This dual-time formulation, which redefines spatial 
coordinates as interference patterns between temporal flows, opens the door to further 
explorations into time-symmetric physics and emergent geometry. 

 
 
 
 
 
4.1 Gravitational Analogy 

Interestingly, the resulting intensity field F(tx,ty) bears a functional resemblance to 
gravitational behaviour in General Relativity. Peaks in the field may be interpreted as regions 
of concentrated spatial structure, analogous to high curvature or energy density, while 
gradients correspond to directional changes in perceived spatial flow. In this interpretation, 
gravity emerges not as a fundamental force but as a geometric effect of non-uniform time-
interference [4]. Just as classical gravitation describes the bending of geodesics due to 
curvature, this model hints that pathways of motion might align with gradients in temporal 
interference intensity, offering a conceptual parallel to gravitational potential. 

This interpretation finds a conceptual connection with the segmented spacetime framework 
proposed in other contexts, where motion-induced structural changes in space and time give 
rise to increased mass[5]. In contrast to that approach, which examines post-motion 
segmentation effects, the present model emphasizes the real-time structure of the interference 
pattern itself. Both perspectives support the broader hypothesis that space, mass, and 
gravitational behaviour may emerge from dynamic temporal interactions rather than being 
fundamental primitives. 

4.2 Extradimensional Interpretation and Gravitational Lensing 

The model also offers a speculative bridge to the phenomenon of gravitational lensing. 
Traditionally attributed to the influence of visible or dark mass curving spacetime, such 
lensing effects might alternatively be understood as resulting from temporally structured 
interference patterns—projections of dynamic processes in higher-dimensional spaces. In this 
view, what appears as a region of “invisible mass” may represent an extradimensional 
trajectory whose interference signature already affects local spacetime geometry. Light 
follows the curvature induced by these interference nodes before any manifest mass has 
formed. From a 4D perspective, we might describe such regions as “empty”, yet they exhibit 
observable lensing precisely because they encode gravitational influence prior to classical 
spatial manifestation [6]. 

4.3 Reversibility of Singular Interference Zones 

The temporally grounded nature of this model also invites reconsideration of so-called 
terminal objects such as black holes. Rather than viewing them as absolute end states of 
spatial collapse, they may instead be interpreted as localized maxima within the temporal 
interference landscape—regions of peak constructive coherence in the projected geometry. If 
this interpretation holds, then such zones need not be permanent; they may transform or 
dissolve under shifting interference dynamics, releasing structure back into a more distributed 
form such as radiation or stellar matter. This echoes concepts proposed in Segmented 
Spacetime theory [1], where extreme conditions segment temporal structure to the point of 
spatial compression. Here, the interference model suggests that the reverse is possible: That 
under appropriate conditions, singular regions may re-expand or recombine into visible 
matter, closing the loop between collapse and formation. 

 
 
 
 
 
 
5. Conclusion 

This model demonstrates a compelling visual metaphor for the emergence of space from time. 
It invites further exploration into symbolic systems, geometric foundations of physics, and 
perhaps most curiously, the power of intuitive visual reasoning to yield new formal structures.  

If movement generates fields, and these fields interfere with one another, then space is the 
geometry of their disturbance. This simple principle may guide future investigations into how 
temporal structures shape physical reality. Furthermore, we must distinguish between field-
like behaviour as a projected geometry and particle-like dynamics as a possible ontological 
origin. If interference patterns such as those described here reflect deeper motions within 
higher-dimensional frameworks, then it may be that the so-called fields we observe are not 
primitive but emergent shadows of temporally extended particle trajectories. This raises the 
possibility that matter itself represents a condensed projection of extradimensional motion. 

References 

1. Rovelli, Carlo (2018). The Order of Time. [London]: Allen Lane. Edited by Erica Segre & Simon 
Carnell. 

2. Levine, D., & Steinhardt, P. J. (1984). Quasicrystals: A new class of ordered structures. Physical 
review letters, 53(26), 2477-2480. https://doi.org/10.1103/PhysRevLett.53.2477 

3. https://github.com/LinoCasu/emergent-spacetime/ 

4. Verlinde, E. On the origin of gravity and the laws of Newton. J. High Energ. Phys. 2011, 29 (2011). 
https://doi.org/10.1007/JHEP04(2011)029 

5. Wrede, C., Casu, L., Bingsi (2025). Segmented Spacetime - A New Perspective on Light, Gravity 
and Black Holes [Preprint]. ResearchGate. 

6. Massey, R., Rhodes, J., Ellis, R. et al. Dark matter maps reveal cosmic scaffolding. Nature 445, 
286–290 (2007). https://doi.org/10.1038/nature05497 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Appendix A: Temporal Interference Code 

import numpy as np 

import matplotlib.pyplot as plt 

from matplotlib.animation import FuncAnimation 

# Create temporal grid 

x = np.linspace(-1, 1, 500) 

y = np.linspace(-1, 1, 500) 

X, Y = np.meshgrid(x, y) 

# Define directional angles (e.g. 5-fold symmetry) 

angles = np.radians(np.arange(0, 360, 72)) 

np.random.seed(42) 

phases = np.random.uniform(0, 2 * np.pi, len(angles)) 

wavelengths = np.full(len(angles), 0.1)  # fixed short wavelength 

# Setup figure 

fig, ax = plt.subplots() 

cax = ax.imshow(np.zeros_like(X), cmap='inferno', extent=[-1, 1, -1, 1]) 

ax.set_title("Spacetime Interference") 

ax.set_xlabel("proper time $t_x$") 

ax.set_ylabel("observer time $t_y$") 

ax.set_xticks([]); ax.set_yticks([]) 

# Animation update function 

def update(frame): 

    field = np.zeros_like(X) 

    for i, theta in enumerate(angles): 

        projection = np.cos(theta) * X + np.sin(theta) * Y 

        field += np.sin(3 * np.pi * projection / wavelengths[i] + phases[i] + 0.1 * frame) 

    field = np.abs(field) ** 3 

    cax.set_data(field) 

    cax.set_clim(np.min(field), np.max(field)) 

    return [cax] 

# Animate 

ani = FuncAnimation(fig, update, frames=100, interval=50, blit=True) 

plt.show() 

View publication stats