---
layout: post
categories: blog
title: Example of Two Panel Figures in Matplotlib
use_math: true
---

* Table of Contents
{:toc}


## Two panel figure example in Matplotlib

{% highlight python %}
    f, axarr = plt.subplots(2,sharex=True)
    lw = 2
    tfont = "Times New Roman"
    axarr[0].plot(t_ppm, d_ppm, color="0.75", linewidth=lw)
    axarr[0].plot(t_gpi, d_gpi, color="blue", linewidth=lw)
    axarr[0].set_xlim([-0.04,0.04])
    axarr[0].set_ylim([1.0e-2,500])
    axarr[0].set_yscale('log')
    axarr[0].set_ylabel(r"$\rho/\bar{\rho}$")
    axarr[0].text(-0.035,100,shock_number,fontname=tfont)
    axarr[0].text(-0.035,30,shock_time,fontname=tfont)
    axarr[1].plot(t_ppm, vx_ppm_rot, color="0.75", linewidth=lw)
    axarr[1].plot(t_ppm, vy_ppm_rot, color="0.75", linewidth=lw,linestyle="--")
    axarr[1].plot(t_ppm, vz_ppm_rot, color="0.75", linewidth=lw,linestyle=":")
    axarr[1].plot(t_gpi, vx_gpi_rot, color="blue", linewidth=lw)
    axarr[1].plot(t_gpi, vy_gpi_rot, color="red", linewidth=lw)
    axarr[1].plot(t_gpi, vz_gpi_rot, color="green", linewidth=lw)
    axarr[1].set_xlim([-0.04,0.04])
    axarr[1].set_ylim([-15,15])
    axarr[1].set_xlabel(r"$x/L$")
    axarr[1].set_ylabel(r"$v/c_{s}$")
    axarr[1].text(-0.035,12,shock_number,fontname=tfont) 
    axarr[1].text(-0.035,10,shock_time,fontname=tfont) 
    fpname = "test.png"
    plt.savefig(filename=fpname,bbox_inches="tight")
    plt.show()
{% endhighlight %}
