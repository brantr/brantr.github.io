---
layout: post
categories: blog
title: Restarting the research blog.
use_math: true
---

* Table of Contents
{:toc}

I've decided to (re)start the research blog to keep a better
record of everything I've been up to. Most of these entries
will be in bulleted form for convenience.

## Continued recovery

I'm still recovering from surgery on March 24. Progress
has been correspondingly slow.

## JWST NIRCam/NIRSpec GTO proposal

The JWST NIRCam and NIRSpec GTO teams are submitting a 
joint proposal to execute a ~800h program in the 
CANDELS regions of GOODS-N and GOODS-S. The team met at
8AM Pacific in their regular telecon to discuss the
last few components to the proposal, including the
justification of parallel NIRCam/NIRSpec observations.

## JEWELS HST Proposal (PI Capak)

I agreed to help with Peter Capak's HST proposal for
WFC3 imaging in the COSMOS field. I offered to create a
figure comparing the sizes of the HUDF, CANDELS, and the
proposed HST-JEWELS fields.

![JEWELS AREA]({{ site.url }}/images/jewels_area.png)

The figure was created by smoothing a dark matter density
field at $$ z\sim7 $$ and then colorizing the density
field based on the smoothed overdensity.  The scripts for
producing this figure sit on gray:~/Desktop/hst_cycle_25/capak/.

## WFIRST

The WFIRST Annual Report for the EXPO team was submitted to 
Jeff Kruk and Dominic Benford. The annual report is available
at

[WFIRST EXPO Annual Report](https://drive.google.com/open?id=0B3IF6fs3vx_6SEtIZWplVGJqM1E)

The year 2 work plan and monthly report are due in three days.

We are additionally trying to schedule a telecon to frame the
big picture for SSR. The WFIRST DRM telecon was delayed until
next Tuesday. The WFIRST Simulation WG telecon may be scheduled
for the week of April 17, when I am at Evan's thesis defense.

## Disk initial conditions

Evan and I had some correspondence about the disk initial conditions
in Cholla. The cold isothermal initial conditions likely were
not resolving the pressure scale length, leading to a vertical
collapse. With a hotter disk temperature, the disk expands radially.
This issue identified a problem with the radial acceleration balance
in the ICs generator, which Evan will work to address.  More information
on the disk ICs can be found here:

[3D Disk ICs](http://evaneschneider.github.io/site/2017/Milky-Way-3D/)
[Hydrostatic Balance Issues](http://evaneschneider.github.io/site/2017/Hydrostatic-Blues/)

## Computing

* Registered for the DGX cloud computing updates.

* Also, discovered that on a node without an xserver, one
can use matplotlib by

{% highlight python %}
import matplotlib as mpl
mpl.use('Agg')
{% endhighlight %}

* GTC Talk is on May 9th.


## Administrativa

Wrote announcement for the prelim exam revision, which drops the
elective component.  Enrico forwarded it to the department. Revised
grades for Astro 5.

