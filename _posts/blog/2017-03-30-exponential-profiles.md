---
layout: post
categories: blog
title: Exponential Profiles
use_math: true
---

* Table of Contents
{:toc}


## Exponential Profile Behind Shocks

In previous work, we had computed both exponential
atmosphere models based on the convergence of the
velocity field and by fitting simple exponentials behind
the shocks.

A natural follow on is to show how close to exponential
the shock profiles are behind the peak. To do this I follow
the procedure outlined here:

[Procedure for Exponential Profile Fitting]({{ site.url }}/html/exponential_fits_03302017.html)

The juypter notebook can be found [here]({{ site.url }}/notebooks/exponential_fits_03302017.ipynb).

Essentially, I use the profiles interpolated along a 
skewer through the simulation volume, oriented along the
principal axes defined by diagonalizing the moment of
inertia tensor.  As before, I fit a simple exponential profile.  I then use this fitted exponential profile to define a new range overwhich I perform a re-fit.  I repeat this for the 100 most dense shocks.

The following figures shows the results. The solid black line is an exponential. The light gray lines are the individual shock profiles, rescaled by the fitted exponential scale length and maximum. The blue solid line is the median of the gray curves at each radius, and the dashed blue lines show the 16% and 84% percentiles of the distribution in the shock profiles at each radius. Here I plot the 100 most dense shocks.

![Exponential Profiles]({{ site.url }}/images/exponential_profiles_03302017.png)

## Exponential Profiles for All Shocks

The above figure only shows the 100 most dense shocks.  I have recomputed this for all shocks with peak densities $$ \rho > 25 \bar{\rho} $$.

![Exponential Profiles All Shocks]({{ site.url }}/images/exponential_profiles_all_03302017.png)