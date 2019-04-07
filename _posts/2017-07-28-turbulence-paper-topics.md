---
layout: post
categories: blog
title: Turbulence paper components
use_math: true
---

* Table of Contents
{:toc}

## Abstract and Introduction
  - very dense things are ephemeral
  - internal pressure gradient cause spreading
  - main things to worry about
  - REALISTIC
  - SIGNIFICANCE? -- matching the PDF with the dense regions, out to ~300 over density
  but it's clear that the high density things don't last long, and the regions 
  they are embedded in are overdense.
  ALSO if self gravity plays a role and you compare the things that last long enough
  for self gravity to cause them to remain permanently bound, is the fact that the
  free fall time of the region is shorter than the expansion time of the shocks of
  higher density
  - IF there is a free fall of a bigish region - it becomes jeans instable on smaller scale
  but the subsequent things that become most unstable are smaller and there is a simple
  scaling and they become smaller in proportion to inverse of density
  - ORDERLY collapse with successive smaller size, and jeans isothermal things
  = REFERENCES to people who showed that the isothermal approximation is pretty good until
  the density is high, maybe 13 orders of magnitude beyond the mean density
  = HOPE of understanding clusters and individual stars, but what implications can WE draw
  from these very stylized turbulence driving at mach noubmbers comparable to those decuded
  from molecular clouds -- CLEAR lot is not available to us.

  - LARGE SCALE gravity in the galaxies in the spiral arms and SN movements -- not because it
  has a signfiicant effect of the interior of molecular clouds, it leads to organization of
  larger scale overdensities.  IN THAT SENSE, driving like what is done in the boxes, but
  once you have discrete entities, the simplest CO/H estimates and velocity estimates suggest
  that they are partially bound, and in general a significant fraction could be bound, because
  the collapse runs away on small scales.
  - HOW MUCH driving during the collapse?  But the collapsing turbulent box and Murray et al.
  suggest that you can get more out of a collapse out of turbulent cloud out of maintaining
  turbulence, rather than collapse.

  - SUMMARIZE turbulence -- try to remove some of the mystery of what happens, and we found the
  following things -- gave us these ideas we discussed before.  Well correlated, connection 
  between sizes of regions that could be bound.


  

## Simulation description
  - ~~basic simulation design~~
  - ~~description of driving scheme~~
  - ~~tracer particle integration~~
  - simulations of exponential shock evolution

## Analysis
  - ~~reinterpolation of the particles using PPM~~
  - ~~reinterpolation of the particles using GPI~~
  - Description of the group finding method
    * fof cataloging using different density thresholds
    * merging together of groups with overlap
  - Description of the voronoi tesselation methodology
  - Description of the orientation and trajectory interpolation at the peak locations
  - Description of the tracking method for time-dependent shock evolution
  - Potential calculation
  - Bound group finding and splitting
  - time-dependent profiles of exponential shock simulations
  - time-dependent profiles of shocks from the turbulence simulations

## Simulation results
  - simulation visualization, density field colorized by velocity
  - density profile of individual shocks
  - average density profiles of all shocks, exponential profile
  - density PDF reconstructed from the tracer particle groups + voronoi tesselation
  - density PDF at different times reconstructed from tracers
  - comparisons of potential groups and density peaks
  - time evolution of the potential field, potential minima dynamical timescales vs. collapse timescales
  - time-dependent properties of shock populations, lifetimes, etc.
  - shapes of shocks, curvature
  - spatial clustering of shocks, correlation function, power spectrum?

## Analytical results
  - Exponential atmosphere calculation
  - Model for exponential shock spreading
  - Connection between shocks of different generations?


## Figures
  - log normal from shocks
  - volumes at a given density
  - densest regions -- collapse
  - ephemeral exist

## Conclusions
  - Density PDF can be described as a sum of individual shocks
  - Shocks are roughly exponential atmospheres
  - The densest shocks have strong pressure gradients that cause them to spread quickly
  - The typical lifetime of the densest shocks is short
  - The typical lifetime of potential minima is longer
  - Star formation efficiency may be a combination of the conversion of binding energy into feedback energy and the competition between collapse time and survival time of dense shocks.
  - Shocks are strongly spatially clustered, correlation function knows about the driving scale
