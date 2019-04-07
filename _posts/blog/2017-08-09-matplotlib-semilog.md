---
layout: post
categories: blog
title: Matplotlib colors
use_math: true
---

* Table of Contents
{:toc}

% syntax highlighting
%{% highlight python %}

plt.xlim([0,1])
plt.ylim([0,1.1])
plt.ylabel(r'$P_V({<}\rho|\bar{\mathcal{M}})$',usetex=True)
plt.xlabel(r'$\bar{\mathcal{M}}$',usetex=True)
#plt.text(3,3.e-4,r"$\rho = \bar{\rho}/\bar{\mathcal{M}}$",usetex=True,color=color_cf)
plt.axes().set_aspect(0.90909,'box-forced')

xo = np.log10(4)
xt = np.log10(1.42)
xe = np.log10(1.2)
plt.xticks([0,1],['1','10'])
minor_ticks = []
for i in range(0,1):
    for j in range(2,10):
         minor_ticks.append(i+np.log10(j))
plt.gca().set_xticks(minor_ticks, minor=True)

%{% endhighlight %}
