---
layout: page
title: Enhanced Diffusion
description: Do chemically active catalysts diffuse more quickly than they should do?
img: assets/img/tocs/Sendiffusion.png
importance: 1
category: work
---

## Introduction

The central focus of my PhD was controlling the translational motion of molecules in solution. After deciding that [mechanically articulated molecular swimming](https://tscmacdonald.github.io/projects/molecularswimming) was unlikely to be  experimentally measurable, my interest turned to intriguing reports of "enhanced diffusion" of chemically active [enzymes](https://pubs.acs.org/doi/abs/10.1021/acs.accounts.8b00286) and [small molecular catalysts](https://onlinelibrary.wiley.com/doi/full/10.1002/anie.201509237) as measured by FCS, DLS, microfluidics experiments, and pulsed-gradient diffusion NMR. As a chemist and NMR spectroscopist I was happy to leave the optical studies of enzymes to others, and so chose to look at the diffusive behaviour of molecular catalysts as-measured by NMR spectroscopy. We also wanted an excuse to work with diffusion NMR specialist [Bill Price](https://www.westernsydney.edu.au/staff_profiles/uws_profiles/professor_bill_price) at Western Sydney University!

The question of enhanced diffusion eventually became a major focus of my PhD, leading to several nice papers and contributions to (one side of) an ongoing scientific controvery.

## Diffusion NMR of transient processes

1D NMR spectroscopy is routinely used to follow time-dependent systems such as chemical reactions, but time-dependent NMR studies of diffusion are much less common. Standard diffusion NMR experiments assume a static system and take perhaps 20-30 minutes to acquire a single diffusion measurement (16 gradients, 16 scans per gradient, >5 s per scan), which is quite slow compared to many reaction timescales. Measuring small, transient changes in diffusion under these standard conditions seemed unsatisfying, so I set out to develop [a better approach to time-resolved diffusion NMR measurements](https://dx.doi.org/10.1002/cphc.201900150). We ended up settling on a simple but effective approach of continuously acquiring spectra while drawing from a long sequence of pseudo-random gradient pulses, shown below. This approach let us acquire diffusion measurements as fast as we could could acquire single-point spectra, typically 0.5-3 minutes for 4-16 point phase cycles.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/enhanceddiffusion/windowprocessing.png class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
 <a href=https://dx.doi.org/10.1002/cphc.201900150>Continuous acquisition of diffusion measurements.</a> The standard linear ramp of gradient pulses is replaced by continuous sequence of random gradient pulses, allowing continuous acquisition of I(b) gradient-attenuated signals. These can then be processed by curve-fitting a moving subset of datapoints to obtain one averaged diffusion measurement per gradient pulse.
</div>

I realised fairly quickly during this project that random gradient sequences (as above) aren't only useful for seamless continuous data acquistion. Because diffusion NMR experiments measure signal intensities resulting from a sequence of gradients applied over time, experiments using correlated gradient sequences (e.g. monotonically increasing or decreasing) are vulnerable to artefacts when the measured signal intensity increases or decreases for <i>other</i> reasons during the experiment. A monotonically increasing gradient sequence, for example, will overestimate the measured diffusion coefficient of a chemical species with decreasing concentration during the experiment. Randomising the sequence of gradients used in a diffusion experiment to eliminate any monotonic correlation is a simple, low-effort measure to remove these artefacts. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/enhanceddiffusion/gcorrelation.png class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
 Diffusion NMR measurements involve acquiring a sequence of spectra using a range of different gradient pulse strengths and fitting signal intensities <i>I</i> against the gradient strengths used <i>b</i>. This measurement takes time, and so is confounded by changes in signal intensity over the experiment timescale due to reasons <i>other</i> than gradient pulse strengths. Here, simulated diffusion coefficients are shown for a simulated reaction in which X becomes Y: even though both species have the same diffusion coefficient of 1, correlation between changing concentrations and the monotonically increasing gradient ramp lead to an underestimated D(X) (0.92) and overestimated D(Y) (1.07). Randomising the gradient list removes this correlation and gives more accurate fitted diffusion coefficients.
</div>

At the time, I thought this problem of cross-correlated gradient sequences and signal intensities was interesting but unlikely to be significant in practice. In the example above, concentrations doubling or halving during a complete gradient sequence only caused a ~10\% error in diffusion measurements: a relatively small error from what seemed an unrealistically fast reaction process. What I didn't recognise at the time but would [help identify later](https://pubs.acs.org/doi/abs/10.1021/jacs.1c09455) was that _signal intensities_ can sometimes change much more rapidly than reaction kinetics in an NMR experiment, such as when relatively small changes in the concentration of paramagnetic species result in large changes of system-wide relaxation rates.

Having developed a way to rapidly acquire NMR diffusion measurements of evolving systems, it was finally time to take a closer look at the mysteries of enhanced diffusion.

## Diffusion NMR and convection

[A re-examination of reported enhanced diffusion of molecular catalysts](https://onlinelibrary.wiley.com/doi/full/10.1002/anie.201910968).	

[Derek Lowe wrote a blog post](https://www.science.org/content/blog-post/enhanced-diffusion-real-illusion) on this project and its outcomes, ticking off an item from my chemistry bucket list - I've been reading his blog since I was maybe 13 or 14 years old, so having my work featured on it was quite a moment.


## Diffusion NMR and changing signal intensities

This topic really kicked off in 2020 following the publication of [a paper in Science](https://www.science.org/doi/full/10.1126/science.aba8425) claiming observations of enhanced diffusion for a copper-catalysed "click" reaction, as measured by diffusion NMR and microfluidics. With limited evidence of experimental protocols given and no raw data provided, it was hard to evaluate this critically. The NMR measurements at least seemed to show a number of flaws: gradient lists were monotonic (as above, vulnerable to artefacts when correlated against changes in signal intensity), diffusion enhancements were presented only in relative $$\Delta D/D_0$$ terms against an unknown $$D_0$$ with no absolute measurements given, and some of the language used seemed to suggest only a passing familiarity with diffusion NMR. I was able to contribute to [a joint critique of these claims](https://www.science.org/doi/10.1126/science.abe8322) as a postscript to my then-submitted PhD, which prompted [a response to the critique](https://www.science.org/doi/full/10.1126/science.abe8678), and then an avalanche of comments and full papers over the next six months. First [the original authors repeated their claims (JPCL)](https://pubs.acs.org/doi/abs/10.1021/acs.jpclett.1c00066), prompting another [comment critiquing those claims](https://pubs.acs.org/doi/abs/10.1021/acs.jpclett.1c00995) and [a reply to the comment](https://pubs.acs.org/doi/abs/10.1021/acs.jpclett.1c01312), then [the claims repeated (ACS nano)](https://pubs.acs.org/doi/full/10.1021/acsnano.1c05168) while a third rebuttal of the original claims appeared in [a joint paper (JACS) from three research groups collectively showing no evidence of enhanced diffusion](https://pubs.acs.org/doi/abs/10.1021/jacs.1c09455) and examining the potential of changing concentrations of paramagnetic relaxants (like Cu(II)) to interfere with NMR diffusion measurements. 

The conclusion seems to be that the original observation of "enhanced diffusion" resulted from a combination of factors:
* Steady-state changes in real $$D$$ during the reaction led to an apparently 'enhanced' relative $$\Delta D/D_0$$ when divided by the unusually small end-of-reaction $$D_0$$.  
* The confusion of diffusion coefficients from multiple species with overlapping chemical shifts, leading to time-dependent changes in 'average' $$D$$ as the composition of the overlapping signals changed during the reaction 
* Artefacts from a semi-monotonic gradient sequence correlated with rapidly changing signal intensities from paramagnetic-induced relaxation  from the Cu(I)-Cu(II) redox couple. 

The saga will probably continue from here.

## Enhanced diffusion: real or illusion?

What to make of all this? I think the most important conclusion is that while diffusion NMR is a powerful spectroscopic technique, it's also vulnerable to a range of measurement artefacts. These can be caused by non-diffusive translational motion (convection, molecular chemotaxis), correlations between the gradient sequence and changing signal intensities, and errors in processing and data presentation (such as relative changes in diffusion 'normalised' against arbitrary parameters). Diffusion NMR remains far from a 'black box' experimental technique, and NMR measurements of diffusion still require critical analysis grounded in an understanding of NMR fundamentals. Some of these artefacts can be (and should be!) eliminated through improvements in experimental protocals, such as replacing all monotonic gradient sequences with non-correlated shuffled sequences, while others still require specialist knowledge to identify, diagnose, and remove.


As for the enhanced diffusion of molecular catalysts, I remain skeptical. I have not encountered a convincing physical model that suggests it should be possible, and experimental reports of enhanced catalyst diffusion have struggled to be replicated or withstand scrutiny. The experimental evidence for enhanced enzyme diffusion seems somewhat better, but the predominantly-FCS diffusion studies have their own potential issues involving the disassociation of enzyme into smaller subunits at low concentrations. This field also suffers from an ongoing confusion of controversial and mysterious "enhanced diffusion" with entirely non-controversial chemical chemotaxis up or down a concentration gradient. Several reports have used microfluidics experiments to demonstrate the motion of active catalysts up or down a concentration gradient of substrate: while this is interesting in its own right and potentially a useful way to drive transport at the nano-scale, it is explicitly _not_ "enhanced diffusion" above what would be expected normally.

For those interested in reading some more scholarly thoughts on enhanced molecular diffusion by a team that haven't been in the trenches themselves (so to speak), [Yifei Zhang and Henry Hess](https://www.nature.com/articles/s41570-021-00281-6) wrote a good critical review on this contentious topic in May 2021.