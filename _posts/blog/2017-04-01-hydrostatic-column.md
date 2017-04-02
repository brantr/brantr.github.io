---
layout: post
categories: blog
title: Hydrostatic Column
use_math: true
---

* Table of Contents
{:toc}


## Computing a density distribution in hydrostatic equilibrium with a background potential.

Evan and I are working on initial conditions generators for {\it cholla}.
Our current task is to set up an adiabatic disk in hydrostatic equilibrium
with a background potential.

I decided to initially set up the disks as vertical exponentials, and then
iterate the density profile such that the pressure gradient balances the 
vertical force from the gravitational potential.

Assuming hydrostatic equilibrium, we have  
$$$
\nabla P = \nabla\left(K \rho^\gamma\right) = \gamma K \rho^{(\gamma-1)} \frac{d\rho}{dz} = - \rho g_z
$$$

We can then set the change in density between cells to equal
$$$
\Delta \rho = - \frac{\rho^{(2-\gamma)}g_z\Delta z}{\gamma K}
$$$

We can then check whether density integrates to the surface density,
and then adjust according.

The code for a single column of gas is at:

[https://github.com/brantr/hydrostatic-column](https://github.com/brantr/hydrostatic-column)

I'm working now to integrate this into the Cholla ICs routines.
