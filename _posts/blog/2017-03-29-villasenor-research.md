---
layout: post
categories: blog
title: Villasenor Research
use_math: true
---

* Table of Contents
{:toc}


## FFTW Solver Timings

Bruno is in the process of writing a multi-dimensional
FFT solver that enables us to utilize multi-threaded
FFTs for the 1-D FFT step of a block based FFT. This is
in contrast to PFFT, which does not allow for the use
of the threaded FFT without further alteration.

Queues take a long time to run on Titan, but he made some
progress.

Here is a plot of the timing using his code.  Note they are
essentially weak scaling tests:

![Bruno FFTW Timings]({{ site.url }}/images/bruno_fftw_sovler_timings_03292017.png)

These scalings do not look good.

Bruno was going to compare with PFFT and see how the scalings
compared, but he is having difficulty installing PFFT on Titan. I offered to try to install PFFT on the system.
