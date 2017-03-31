---
layout: post
categories: blog
title: Cholla Scaling Tests with PFFT-based Gravity Solver
use_math: true
---

* Table of Contents
{:toc}


## Cholla is integrating a FFT-based gravity solver

We want to include self-gravity into Cholla, so Bruno Villasenor is implementing a FFT-based gravity solver into Cholla. The idea is to use the block-based FFT-solver PFFT to allow for Cholla to retain its current domain decomposition while solving for the gravitational potential on a grid.

The key is to produce a FFT-based solver that scales as well as the Cholla hydro does (which is nearly perfect in weak scaling).

## Scaling tests with PFFT-based FFT alone

One important initial test is to see what the scaling of PFFT as a stand-alone FFT solver is. This will let us discover whether the integration of PFFT with Cholla causes any additional scaling degradation. Here we show Bruno's scaling of PFFT with node count on Titan (single core per node).  The weak scaling of PFFT as an FFT solver is quite good.

![PFFT as an FFT-solver]({{ site.url }}/images/pfft_fft_timing_03312017.png)

## Scaling tests with Cholla + a PFFT-based gravity solver

Here is a similar scaling plot, now showing the performance of Cholla using PFFT as an FFT-solver for computing the gravitational potential. Two things to note.  First, the weak scaling including PFFT as a solver is terrific. Second, the FFT solve is dominating the computational cost by a factor of $$ \sim 3.5\times $$.

![Cholla + PFFT]({{ site.url }}/images/cholla_pfft_gravity_timing_03312017.png)

