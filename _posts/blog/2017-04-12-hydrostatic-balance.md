---
layout: post
categories: blog
title: Hydrostatic Balance
use_math: true
---

* Table of Contents
{:toc}


## Hydrostatic Balance of an Adiabatic Fluid in a Background Potential

Consider an adiabatic fluid with an adiabatic index
$$ \gamma $$. We want to compute the density structure 
$$ \rho(z) $$ in a potential $$ \Phi(z) $$. The gas
pressure is $$ P = K \rho^{\gamma} $$.

First, note that
$$
c_s^2 = \gamma P /\rho_K = \gamma K \rho_K^{\gamma-1}
$$
or
$$
\gamma K = c_s^2 \rho_K^{1-\gamma}
$$

The equation of vertical hydrostatic equilibrium is

$$
\frac{dP}{dz} = -\rho(z) g(z)  
\gamma K \rho^{\gamma-1}\frac{d\rho}{dz} = -\rho(z) g(z)
\gamma K \rho^{\gamma-2}d\rho = - g(z) dz
\frac{1}{\gamma-1} \rho^{\gamma-1} + C = \frac{1}{\gamma K}\Phi(z)
\rho^{\gamma-1} = (\gamma-1)\rho_K^{\gamma-1}\frac{\Phi(z)}{c_s^2} + C
$$