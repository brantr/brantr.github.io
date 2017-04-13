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
$$

$$
\gamma K \rho^{\gamma-1}\frac{d\rho}{dz} = -\rho(z) g(z)
$$

$$
\gamma K \rho^{\gamma-2}d\rho = - g(z) dz
$$

$$
\frac{1}{\gamma-1} \rho^{\gamma-1} + C = \frac{1}{\gamma K}\Phi(z)
$$

$$
\rho^{\gamma-1} = (\gamma-1)\rho_K^{\gamma-1}\frac{\Phi(z)}{c_s^2} + C
$$


$$
\rho = \left[(\gamma-1)\rho_K^{\gamma-1}\frac{\Phi(z)}{c_s^2} + C\right]^{\frac{1}{\gamma-1}}
$$

$$
\rho = \rho_K\left[(\gamma-1)\frac{\Phi(z)}{c_s^2} + C\right]^{\frac{1}{\gamma-1}}
$$

If we define the central midplane gas temperature at $$z=0$$
to be such that the sound speed is $$c_s$$, then $$\rho(z=0)=\rho_K$$. Given the above, we then require

$$
(\gamma-1)\frac{\Phi(z)}{c_s^2} + C = 1;\,z=0
$$

We can arrange this if we define $$\Phi(z=0)=\Phi_0$$ and write
$$
C = -(\gamma-1)\frac{\Phi_0}{c_s^2} + 1
$$

and our density profile becomes

$$
\rho = \rho_K\left[(\gamma-1)\frac{\Phi(z)-\Phi_0}{c_s^2} + 1\right]^{\frac{1}{\gamma-1}}
$$



