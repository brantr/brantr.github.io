---
layout: post
categories: blog
title: Connecting UV Luminosity to Stellar Mass
use_math: true
---

* Table of Contents
{:toc}


## UV Luminosity Function

If we have a UV luminosity function, a connection
between UV luminosity and star formation rate,
and a relation between star formation rate and
stellar mass, we can estimate a stellar mass function.

Consider a UV luminosity function
$$
\Phi(M_{UV}) \equiv \frac{dn}{d M_{UV}}
$$
with units Mpc$$^{-3}$$ mag$$^{-1}$$,
such that the galaxy number density is  
$$
n(<M_{UV}) = \int_{-\infty}^{M_{UV}} \Phi(M_{UV})dM_{UV}.
$$

## Star formation rate function

To convert the UV luminosity function into a star formation rate function, we need to have some connection between $M_{UV}$ and SFR.
Here, we will take $$L_{UV}$$ to be the monochromatic UV luminosity
with units ergs s$$^{-1}$$ Hz$$^{-1}$$. The connection between 
star formation rate and $$L_{UV}$$ is often written in the form  
$$
\log_{10}\left[\frac{SFR}{M_{\odot}~\mathrm{yr}^{-1}}\right] = \log_{10}
\left(\nu L_{UV}\right) + A_{SFR,UV} \equiv \log_{10} L_{UV} + B_{SFR,UV}
$$  
assuming that $$\nu$$ corresponds to the monochromatic frequency
that defines what we mean by "UV". $$A_{SFR,UV}$$ and $$B_{SFR,UV}$$
are constants.

We can work in magnitudes rather than luminosity by noting
that  
$$
L_{UV} = D_{UV} 10^{-0.4 M_{UV}}
$$  
where $$D_{UV}$$ is some constant. If $$SFR\propto L_{UV}$$ as above,
then we just have  
$$
\log_{10} SFR = -0.4 M_{UV} + C_{SFR}
$$  
or  
$$
d\log_{10} SFR = -0.4 dM_{UV}
$$  
or  
$$
\frac{dM_{UV}}{d\log_{10} SFR} = -2.5 [\frac{\mathrm{mag}}{\mathrm{dex}}].
$$  

We can then write the SFR function as   
$$
\frac{dn}{d\log_{10} SFR} = \frac{dn}{dM_{UV}} \frac{dM_{UV}}{d\log_{10}SFR}.
$$  

## Stellar mass function

If we assume a one-to-one correlation between
star formation rate and stellar mass, then it's straightforward
to convert between the SFR rate to the stellar mass function.

Let's assume a connection between star formation rate and
stellar mass of  
$$
\log_{10} SFR = \gamma \log_{10} M_{\star} + K_{SFR,\star}
$$  
or  
$$
\frac{d\log_{10} SFR}{d\log_{10} M_{\star}} = \gamma.
$$  
The units are $$[\mathrm{dex}/\mathrm{dex}]$$, or no units!

We then have the stellar mass function as  
$$  
\frac{dn}{d\log_{10} M_{\star}} = \frac{dn}{dM_{UV}} \frac{dM_{UV}}{d\log_{10}SFR} \frac{d\log_{10}SFR}{d\log_{10} M_{\star}}.
$$  
This function has units of Mpc$$^{-3}$$ dex$$^{-1}$$.

## Scatter in stellar mass vs. SFR




