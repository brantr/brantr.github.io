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
lw = 2
ms = 7

plt.figure(figsize=[7,3.5])
f, axarr = plt.subplots(1,2)
lw = 2
tfont = "Times New Roman"

xx = [1,8192]
yy = [np.mean(t_fft_128[-3:-1]),np.mean(t_fft_128[-3:-1])]
axarr[0].plot(xx,yy,linestyle="--",color="0.75",linewidth=2)
xx = [1,8192]
yy = [np.mean(t_fft_256[-3:-1]),np.mean(t_fft_256[-3:-1])]
axarr[0].plot(xx,yy,linestyle="--",color="0.75",linewidth=2)
axarr[0].plot(n_gpu, t_fft_128,color='blue',linewidth=lw,label=r"$N_{FFT} = N_{GPU}\times 128^3$")
axarr[0].plot(n_gpu, t_fft_128,'.',color='blue',markersize=ms)
axarr[0].plot(n_gpu, t_fft_256,color='red',linewidth=lw,label=r"$N_{FFT} = N_{GPU}\times 256^3$")
axarr[0].plot(n_gpu, t_fft_256,'.',color='red',markersize=ms)
axarr[0].set_xlim([4,4096])
axarr[0].set_ylim([1.0e-1,20.0])
axarr[0].set_yscale('log')
axarr[0].set_xscale('log')
axarr[0].set_ylabel(r"$Time\,[\mathrm{seconds}]$")
axarr[0].set_xlabel(r"$N_{GPU}\,[\mathrm{Titan}]$")
axarr[0].text(60,0.5,r'$\mathrm{FFT}\,\mathrm{Only}$')
axarr[0].legend(loc=4,frameon=False,fontsize=10)
axarr[0].set_aspect(1.3)

xx = [1,8192]
yy = [np.mean(t_cholla_hydro_grav[-3:-1]),np.mean(t_cholla_hydro_grav[-3:-1])]
axarr[1].plot(xx,yy,linestyle="--",color="0.75",linewidth=2)
xx = [1,8192]
yy = [np.mean(t_cholla_hydro[-3:-1]),np.mean(t_cholla_hydro[-3:-1])]
axarr[1].plot(xx,yy,linestyle="--",color="0.75",linewidth=2)
axarr[1].plot(n_gpu, t_cholla_hydro,color='purple',linewidth=lw,label=r"$\mathrm{Hydro}\,\mathrm{Only}$")
axarr[1].plot(n_gpu, t_cholla_hydro,'.',color='purple',markersize=ms)
axarr[1].plot(n_gpu, t_cholla_hydro_grav,color='green',linewidth=lw,label=r"$\mathrm{Hydro}\,+\,\mathrm{Gravity}$")
axarr[1].plot(n_gpu, t_cholla_hydro_grav,'.',color='green',markersize=ms)
axarr[1].set_xlim([4,4096])
axarr[1].set_ylim([1.0e-1,5.0])
axarr[1].set_yscale('log')
axarr[1].set_xscale('log')
axarr[1].set_ylabel(r"$Time\,[\mathrm{seconds}]$")
axarr[1].set_xlabel(r"$N_{GPU}\,[\mathrm{Titan}]$")
axarr[1].set_aspect(1.75)
axarr[1].text(60,0.33,r'$128^3\mathrm{Cells}\,\mathrm{per}\,\mathrm{GPU}$')
axarr[1].legend(loc=4,frameon=False,fontsize=10)

for ax in axarr.flatten():
    labels = ax.get_xticklabels() + ax.get_yticklabels()
    [label.set_fontname(tfont) for label in labels]

plt.tight_layout() 

fpname = "self-gravity_weak_scaling.png"
plt.savefig(filename=fpname,bbox_inches="tight")
plt.show()
{% endhighlight %}


## Result

![self-gravity_weak_scaling.png]({{site.url}}/images.self-gravity_weak_scaling.png)