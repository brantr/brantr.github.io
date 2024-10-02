---
layout: post
categories: blog
title: Fonts in Matplotlib
use_math: true
---

* Table of Contents
{:toc}


## Selecting global fonts in Matplotlib

{% highlight python %}
from matplotlib import rc
rc('font',**{'family':'sans-serif','sans-serif':['Helvetica']})
## for Palatino and other serif fonts use:
#rc('font',**{'family':'serif','serif':['Times New Roman']})
rc('text', usetex=True)
{% endhighlight %}
