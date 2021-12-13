---
layout: post
title: Displacement mapping the 2019 Albanian earthquake with Sentinel 1 InSAR
description: A short trip through some amateur SAR interferometry
date: 2020-04-23
tags: remote-sensing
categories: hobbies
---

With COVID isolation continuing, I’ve returned to a topic that has interested me for a long time: synthetic aperture radar (SAR), and more specifically SAR interferometry (InSAR). InSAR is a great tool for measuring small ground displacements that can result from earthquakes, landslides, or subsidence into cavities such as those left behind by oil and gas exploration. There are a number of SAR satellites in operation currently, but I'll be using freely accessible data from the ESA's Sentinel-1 platform. 

As a first toy problem, I decided to look at the site of the [earthquake that hit Albania last year](https://en.wikipedia.org/wiki/2019_Albania_earthquake){:target="\_blank"} on November the 26th. The steps I take are largely based on [this ESA tutorial document](http://step.esa.int/docs/tutorials/S1TBX%20TOPSAR%20Interferometry%20with%20Sentinel-1%20Tutorial_v2.pdf){:target="\_blank"}.


This earthquake hit Albania near the town of Durres, so to start off I chose two SLC data products (`S1A IW SLC 1SDV 20191125T164052 20191125T164119 030070 036F2E 4A87` and `S1A IW SLC 1SDV 20191207T164051 20191207T164118 030245 03752F F624`) from Copernicus Scihub (not to be confused with Sci-hub!) that were acquired on the 25th of November and the 7th of December. Interferometry involves measuring phase differences between pairs of imagery, so we need phase-sensitive single-look complex (SLC) data products rather then the smaller and more processed products often used for SAR imaging.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/1.png class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
    Acquisition footprint for the imagery used here. We’ll be focusing on the stretch of Albanian coast just north of Durres.
</div>

After downloading the two SLC products, I imported both into into ESA’s SNAP toolbox and used the TOPS Split operator to cut down the product to the region and data of interest. We don’t need the VH scattered polarisation for interferometry and we don’t care about Italy or the Adriatic, so I sliced each data product to only include VV-polarised data from bursts 4-9 of subswath IW3, as below.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/2.png class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
    TOPS Split to reduce the size of the dataset to the regions and polarisation of interest.
</div>

I then applied orbit corrections to each each product (_Radar > Apply Orbit File_) and combined the two products into a coregistered stack with back-geocoding using the SRTM 1sec model (_Radar > Coregistration > S-1 TOPS Coregistration > S-1 Back Geocoding_). I expected this to mask out the zero-elevation sea portion of the imagery, but it didn’t seem to do so. With coregistered data in hand, I was then able to create an interferometric product in SNAP (_Radar > Interferometric > Products > Interferogram formation_), checking ‘Subtract topographic phase” to remove the influence of static ground geometry. The interferogram produced at this point is very noisy and still contains horizontal bands showing the gaps between the separate bursts collected by S-1, but the fringes of an interference pattern centred on the coast are visible if you squint a little bit.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/3.png class: "img-fluid rounded z-depth-1" zoomable: true %}
    </div>
</div>
<div class="caption">
    Interferogram. The noisy area on the left hand side is the Adriatic sea, while the land area has slightly more coherent interference phases. Horizontal bands mark the separation between the six burst images making up this large scene. The deformation resulting from the earthquake is visible as a series of concentric interference fringes, about halfway up the image and a third of the way in from the left.
</div>

The next steps are to stitch the different bursts together into a composite (“debursting”; _Radar > Sentinel-1 TOPS > S-1 TOPS Deburst_), and use a Goldstein filter (_Radar > Interferometric > Filtering > Goldstein Phase Filtering_) to clean up some of the noise. The image becomes much more clear at this point, although there are still patches of noise. We now have what looks like some decent interferometric data, but converting this into displacement measurements requires the additional step of “unwrapping”. Unwrapping is a computationally expensive process that brings my laptop to its knees for several hours at a time, so I took a subset of the most relevant parts of the image to avoid wasting CPU time processing the boring parts. In hindsight even this subset took an unreasonable amount of time to process and I should have trimmed even more aggressively.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/4.png class: "img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    Effects of debursting and Goldstein phase filterering: the bursts have been stitched into a single composite scene, and the pattern of the phase distortions is much more clearly visible. Only the subset within the rectangle is considered further.
</div>

Unwrapping attempts to convert periodic phase measurements into absolute displacement measurements, effectively by working out the boundaries between integer numbers of wavelengths. I’ve tried to illustrate this below with a crude MS Paint slice-up of a line measured from the centre of the concentric phase rings to the top right corner of the subset shown above.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/5.png class: "img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    Phase unwrapping to access displacement information. Phase is periodic over -π/+π, but successful unwrapping can tell us how many wavelengths two points are removed from each other, as well as the relative phase. Here, there seems to be a 3 or 4-wavelength difference in displacement between the centre of the disturbance (left) and the top right corner of the image (right), depending on whether the extremely noisy band is a full phase cycle or not. This corresponds to a ~15–20 cm displacement at a C-band SAR wavelength of 5.5 cm.
</div>

SNAP can’t do phase unwrapping, but it can interface with a utility—snaphu—which does. I can’t seem to get the actual processing to work within SNAP, but was able to export the phase data for unwrapping (_Radar > Interferometric > Unwrapping > Snaphu Export_) and then run snaphu from the command line on the exported data. This took about five hours wall time to complete on my laptop (Ryzen 3500U), running as 6 CPU threads.

Once the unwrapping has finished, the unwrapped data can be imported into SNAP (_Radar > Interferometric > Unwrapping > Snaphu Import_) and converted from unwrapped phase information to displacement data (_Radar > Interferometric > Products > Phase to Displacement_). We now have a displacement map (below), but it’s hard to relate this to on-the ground differences. The major changes in displacement (to the left and bottom) are over the water, probably caused by changing tides, and the imagery is still a satellite-eye view that can’t be directly projected onto terrain.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/6.png class: "img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    Displacement map before range-doppler correction. The deformation resulting from the earthquake can be seen as a pale yellow patch in the centre of the image, but is overshadowed by the uninteresting but major changes in displacement over the Adriatic sea.
</div>

Finally, we can run a range-doppler correction on the displacement map (_Radar > Geometric > Terrain Correction > Range-Doppler Terrain Correction_) to produce a displacement map of the land area only, scaled to a correct geographic projection. This product can be viewed in SNAP, but for convenience we can export it as a KMZ file and view it in Google Earth superimposed over optical imagery. At this point it’s clear that the unwrapping process has somehow missed the baseline (I suspect that the large area of water might have interfered): the relative changes in displacement look good, but somehow we have the earthquake epicentre set as the location which hasn’t moved, and the rest of the country having dropped by ~10 cm around it. This is clearly incorrect, but I don’t actually know how to re-set the baseline for the displacement band correctly. For a rough estimate I’d add about 9–9.5 cm to the numbers displayed on the legend, suggesting that Hamallaj was lifted by about 11–12 cm following the November earthquake. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/7.png class: "img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    Displacement mapping exported to Google Earth. The upthrust from the earthquake is clearly visible, centred on Hamallaj, but the baseline has somehow ended up miss-set such that the rest of the country appears to have dropped while Hamallaj maintained its previous location.
</div>

I don’t have much other information regarding this earthquake to compare this data to, but Wikipedia has a nice map showing the shaking intensity resulting from the earthquake. It compares well to the displacement data obtained here, but the epicentre seems to sit to the northeast of the region of maximum displacement (white-yellow). A little further north there’s an area that the interferometry data says _dropped_ as a result of the earthquake, shown in blue. Knowing very little about seismology, my interpretation of this would be that the earthquake involved a movement from the northeast to the southwest: following the fault, rock moved southwest leading to a bulge in the southwest and a depression in the northeast.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/8.png class: "img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    The displacement map compares well to the map of shaking intensity, and from first principles I think it’s suggestive of a movement towards the southwest, leaving a dip (blue) to the northeast.
</div>

It seems that this guess is actually pretty close to the truth. An article published on studying this earthquake with Sentinel-1 data ([_Remote Sensing_ __2020__, _12_, 846](https://doi.org/10.3390/rs12050846)) includes this figure showing a modelled downwards displacement to the northeast, but it looks like the patchy blue stuff in the displacement data above is an artefact rather than a real deformation. Ah well, you don’t get everything but I’m still pretty happy with how this turned out.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/albanianinsar/9.png class: "img-fluid rounded z-depth-1"%}
    </div>
</div>
<div class="caption">
    This work from some people with actual expertise in the area ([_Remote Sensing_ __2020__, _12_, 846](https://doi.org/10.3390/rs12050846)) seems close to my uninformed speculation of a northeast to southwest fault.
</div>

For anyone interested, here’s the [.kmz](https://drive.google.com/file/d/1_TBzUFNNS-o2Nrai4obZTgf2uTMb-rzf/view?usp=sharing) of the displacement data.