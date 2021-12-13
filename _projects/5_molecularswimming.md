---
layout: page
title: Molecular swimmers
description: Mechanical propulsion of molecules in solution
img: assets/img/molecularmotion/scalloptheorem.png
importance: 1
category: work
---

The start of my PhD focused on the possibility of 'molecular swimmers': the ability of molecules to move through solution at rates faster than diffusion. Whether or not this is possible (or at least, feasible) remains an open question: molecules are _very_ small, and molecular-scale fluid dynamics are completely different to the dynamics most of us are more familiar with from our experience larger length scales.  The classic treatment of these differences is E. M. Purcell's very readable [Life at Low Reynolds Number](http://web.mit.edu/8.592/www/lectures/lec1/Purcell.pdf) and its memorable scallop theorem, describing impossibility of swimming using reciprocal motion (like a scallop!) at low Reynolds number. Instead, non-reciprocal (=time-asymmetric) swimming motions are needed such as corkscrew flagella or semi-flexible cilia. Some non-reciprocal swimmers with rigid bodies are shown below.


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/molecularmotion/swimmers.svg class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
    Minimal geometric swimmers. Swimmers a-c use non-reciprocal motion and can operate at both low and high Reynolds number, while 'swimmer' d (a scallop!) operates by reciprocal motion and can only swim in high-Reynolds conditions: at low Reynolds number, inertia is irrelevant and the swimmers' back-stroke will undo any forward motion gained by the forward-stroke.
</div>

What might a molecular non-reciprocal swimmer look like? It would necessarily be a molecular motor: breaking time-reversal symmetry means directional cycling through (at least three) states, which is really another way of saying "uses energy to do mechanical work". I had the idea of making a simple molecular-mechanical swimmer build around two photoswitchable linkers driven indirectly by FRET from a dye appended to one end, with the distant-dependent FRET efficiency used to bias cycling towards first isomerising the near linker and only then isomerising the far linker:

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/molecularmotion/dyadswimmer.svg class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
    A four-state molecular swimmer built around two photochromic azobenzene-derived linkers. Blue irradiation is absorbed by the pendant dye (green) and preferentially transferred by FRET to the adjacent _E_-azobenzene. This brings the dye closer to the other azobenzene, setting up a second FRET transfer. These two steps would bias the system to clockwise cycling over anticlockwise cycling.
</div>

Cool idea, right? Unfortunately, I quickly realised it didn't make much sense. Let's assume that each isomerisation drives the molecule forward by distance $$d$$, and $$k$$ isomerisation events occur per unit time $$t$$. The average displacement per unit time $$\langle x \rangle$$ will then be given by

$$
\langle x \rangle = dkt
$$  

How does this compare to diffusion? Diffusive transport follows

$$
\langle x^2 \rangle = 6Dt
$$

and 'swimming' will thus be comparable to or greater than diffusion for 

$$
dk > \sqrt{6D}
$$

For a small-ish molecule in organic solution, let's say $$D = 10^{-10}~\mathrm{m^2 s^{-1}}$$. It seems reasonable that the 'step size' for an isomerising molecule must be smaller than its length, so let's charitably assume that our molecules are perfectly efficient swimmers wiht a length of 1 nm, giving us $$d = 10^{-9}~\mathrm{m}$$. The minimum isomerisation rate to drive measurable swimming motion must then be:

$$
k > \frac{\sqrt{6\times10^{-10}}}{10^{-9}}~\mathrm{s^{-1}}\\
$$


$$
k > 6\times 10^4~\mathrm{s^{-1}}
$$

That's 60 kHz of photoisomerisation _per molecule_! Perhaps not impossible in what would by that point be a lossy optical cavity, but I've got no idea how you'd be measure the diffusion of the molecules against such a bright background and in the presence of so much heating. At the very least, it's 4-5 orders of magnitude more light than we can feasibly get into a diffusion NMR setup. 

I don't think that this sort of mechanical swimming makes much sense for molecules. Since $$D \propto 1/r^2$$ and therefore $$\langle x_{diff} \rangle \propto 1/r$$, while the velocity of mechanical swimming at a given frequency follows $$\langle x_{swim} \rangle \propto r$$, the overall efficiency of swimming over diffusion is proportional to $$r^2$$ and molecules are unfortunately just too small to make much headway.

Fortunately, by the time I figured this out I'd found a new and much more interesting approach to making molecules swim faster: intriguing reports of the ["enhanced diffusion" of catalysts during chemical reactions](https://doi.org/10.1002/anie.201509237).