---
layout: post
title: Don't be scared of diffusion NMR!
description: Some basic tips for good NMR diffusion measurements
date: 2021-12-19
comments: true
tags: NMR, diffusion, chemistry
categories: work
---


A friend messaged me the other day for some advice on how to run diffusion NMR measurements - or perhaps more accurately, on how _not_ to run them. Without meaning to be in any way comprehensive and assuming basic familiarity with NMR and diffusion, here are some of thoughts on the matter. Here the key things to be aware of at all times when performing diffusion NMR measurements, as I see it:

1. Changes in (static) sample temperature or viscosity during the measurement or between measurements
2. Convection
3. Peak overlap between different chemical species
4. Changing signal intensity during the measurement correlated with the gradient list


# Diffusion: basic physics 

What governs diffusion rates? The Stokes-Einstein-[Sutherland](https://doi.org/10.1080/14786440509463331) equation for the diffusion of a hard spherical particle at low Reynolds number tells us:

$$
D = \frac{k_B T}{6\pi\eta r}
$$

where $$k_B$$ is Boltzmann's constant, $$T$$ is the (absolute) temperature, $$\eta$$ is the dynamic viscosity, and $$r$$ is the radius of the diffusing particle. It would be tempting to say that diffusion is only really sensitive to changes of $$r$$, since $$\eta$$ is fixed for a given solvent and temperature changes will be relatively small for a system at 298 K +/- a degree or so. <em>This is not the case</em>, as for most solvents the viscosity $$\eta$$ _also_ varies strongly as a function of temperature. Empirical measurements have found that the dependence of diffusion on temperature is often closer to an exponential Arrhenian relationship:

$$
D(T) = A\exp{(-\frac{E_a}{k_B T})}
$$

It's not at all clear to me if $$A$$ and $$E_a$$ are physically meaningful quantities. This Arrhenian relationship also tends to break down for more "structured" solvents with stronger intermolecular interactions, such as water and small alcohols. Here are some [reported values]( https://doi.org/10.1039/B005319H) of the "activation energy" for diffusion of common molecular solvents:

| Solvent | $$E_a~\mathrm{/~kJ~mol^{-1}}$$  |
| ---- | ---- |
| Cyclohexane | 13.7 |
| Dioxane | 13.9 |
| Dodecane | 13.7 |
| DMSO | 14.9 |
| Tetradecane | 15.6 |
| Pentanol | 24.1 |

The take-home here is that diffusion measurements are specific to a solution temperature, and that good temperature control and/or monitoring ([try a methanol capillary!](https://dx.doi.org/doi/10.1002/cphc.201900150)) are essential for quantitative diffusion measurements. 

# Diffusion NMR

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/diffusionnmr/pgste.png class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Basic pulsed gradient stimulated echo (PGSTE) diffusion NMR sequence.
</div>

Stejskal-Tanner:

$$
I = I_0 e^{-D(g^2\delta^2\gamma^2(\Delta-\delta/3))}
$$

## Convection

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/diffusionnmr/convection.png class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Convection ruins diffusion NMR measurements and can occur at any time. Left: convection is often visible as an unusual phase twist in some of the 1D gradient slice spectra. Right: convection occurs when a more dense section of fluid is higher than a less dense section of fluid. Assuming positive thermal expansion (warmer fluid is less dense than cooler fluid), this can happen either when a vertical temperature gradient results in cool fluid sitting above warm fluid (Rayleigh-Benard convection) or when a horizontal temperature gradient exists (Hadley convection). A layer of warm fluid above a layer of cool fluid does not result in a density inversion, and cannot drive convection.
</div>

## Overlapping peaks give averaged diffusion coefficients

Pulsed-gradient diffusion NMR measurements involve:
1. Acquiring a sequence of 1D spectra with a range of gradient pulse strengths
2. Extracting the intensities (integrals or peak heights) of peaks of interest
3. Fitting the Stejsal-Tanner equation to these intensities as a function of gradient strength, and obtaining diffusion coefficients


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/diffusionnmr/peakoverlap.png class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Diffusion NMR measurements generally cannot resolve the diffusion coefficients of two overlapping peaks. Here, compounds A (red peaks) and B (blue peaks) respectively have diffusion coefficients of 1 and 3. These diffusion coefficients can be measured accurately by integrating non-overlapping peaks (red and blue lines) and fitting peak intensities to the Stejskal-Tanner equation. If the overlapping peak (green) is used  for monoexponential fitting, an intermediate _average_ diffusion value will be obtained.
</div>




