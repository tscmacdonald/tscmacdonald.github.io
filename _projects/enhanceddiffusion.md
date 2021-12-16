---
layout: page
title: Enhanced Diffusion
description: Do chemically active catalysts diffuse more quickly than they should do?
img: assets/img/tocs/Sendiffusion.png
importance: 1
category: work
---

The central focus of my PhD was controlling the translational motion of molecules in solution. After deciding that mechanically articulated [molecular swimmers](projects/molecularswimming) were unfeasible to demonstrate experimentally, my interest turned to intriguing claims of "enhanced diffusion" of chemically active enzymes and [small molecular catalysts](https://onlinelibrary.wiley.com/doi/full/10.1002/anie.201509237). As a chemist and NMR spectroscopist I was happy to leave the FCS studies of enzymes to others, and so chose to look at the diffusive behaviour of molecular catalysts (partially motivated by a desire to work with diffusion NMR specialist [Bill Price](https://www.westernsydney.edu.au/staff_profiles/uws_profiles/professor_bill_price) at Western Sydney University). The topic eventually became a major focus of my PhD, leading to several nice papers and contributions to (one side of) an ongoing scientific controvery.

## Diffusion NMR of transient processes

1D NMR spectroscopy is routinely used to follow time-dependent systems such as chemical reactions, but time-dependent NMR studies of diffusion are much less common. Standard diffusion NMR experiments assume a static system and take perhaps 20-30 minutes to acquire a single diffusion measurement (16 gradients, 16 scans per gradient, >5 s per scan). Measuring small changes in diffusion during short-lived chemical reactions under these restrictions seemed unlikely, so I set out to develop a better approach. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: projects/enhanceddiffusion/windowprocessing.pdf class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
 Continuous acquisition of diffusion measurements. The standard linear ramp of gradient pulses is replaced by continuous sequence of random gradient pulses, allowing continuous acquisition of I(b) gradient-attenuated signals. These can then be processed by fitting the Stejskal-Tanner equation to a moving subset of datapoints to obtain one averaged diffusion measurement per gradient pulse.
</div>


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: projects/enhanceddiffusion/gcorrelation.pdf class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
 Diffusion NMR measurements involve acquiring a sequence of spectra using a range of different gradient pulse strengths and fitting signal intensities <i>I</i> against the gradient strengths used <i>b</i>. This measurement takes time, and so is confounded by changes in signal intensity over the experiment timescale due to reasons <i>other</i> than gradient pulse strengths. Here, simulated diffusion coefficients are shown for a simulated reaction in which X becomes Y: even though both species have the same diffusion coefficient of <b>1</b>, correlation between changing concentrations and the monotonically increasing gradient ramp lead to an underestimated D(X) (0.92) and overestimated D(Y) (1.07). Randomising the gradient list removes this correlation and gives more accurate fitted diffusion coefficients.
</div>
## Diffusion NMR and convection


[Derek Lowe wrote a blog post](https://www.science.org/content/blog-post/enhanced-diffusion-real-illusion) on this project and its outcomes, ticking off an item from my chemistry bucket list - I've been reading his blog since I was maybe 13 or 14 years old, so having my work featured on it was quite a moment.


## Diffusion NMR and changing signal intensities

 
## Enhanced diffusion: real or illusion?

What to make of all this? I think the most important conclusion is that while diffusion NMR is a powerful spectroscopic technique, it's also vulnerable to a range of measurement artefacts caused by non-diffusive translational motion (convection, molecular chemotaxis) and correlations between the gradient sequence and changing signal intensities resulting from changing concentration or changing nuclear spin relaxation rates. Diffusion NMR remains far from a 'black box' experimental technique, and NMR measurements of diffusion still require critical analysis by specialists in diffusion NMR spectroscopy. Some of these artefacts can be (and should be!) eliminated through improvements in experimental protocals, such as replacing all monotonic gradient sequences with non-correlated shuffled sequences.


For those interested in reading some more scholarly thoughts on enhanced molecular diffusion, [Yifei Zhang and Henry Hess](https://www.nature.com/articles/s41570-021-00281-6) wrote a good critical review on this contentious topic in May 2021.

As for the enhanced diffusion of molecular catalysts, I remain skeptical. I have not encountered a convincing physical model that suggests it should be possible, and experimental reports of enhanced catalyst diffusion have struggled to be replicated or withstand scrutiny. The experimental evidence for enhanced enzyme diffusion seems somewhat better, but the predominantly-FCS diffusion studies have their own potential issues involving the disassociation of enzyme into smaller subunits at low concentrations. There's also a  
