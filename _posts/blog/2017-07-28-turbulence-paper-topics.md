---
layout: post
categories: blog
title: Turbulence paper components
use_math: true
---

* Table of Contents
{:toc}

## Simulation description
  - basic simulation design
  - description of driving scheme
  - tracer particle integration
  - simulations of exponential shock evolution

## Analysis
  - reinterpolation of the particles using PPM
  - reinterpolation of the particles using GPI
  - Description of the group finding method
    * fof cataloging using different density thresholds
    * merging together of groups with overlap
  - Description of the voronoi tesselation methodology
  - Description of the orientation and trajectory interpolation at the peak locations
  - Description of the tracking method for time-dependent
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

## Conclusions
  - Density PDF can be described as a sum of individual shocks
  - Shocks are roughly exponential atmospheres
  - The densest shocks have strong pressure gradients that cause them to spread quickly
  - The typical lifetime of the densest shocks is short
  - The typical lifetime of potential minima is longer
  - Star formation efficiency may be a combination of the conversion of binding energy into feedback energy and the competition between collapse time and survival time of dense shocks.
  - Shocks are strongly spatially clustered, correlation function knows about the driving scale
