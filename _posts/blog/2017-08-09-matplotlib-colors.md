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
import numpy as np
import matplotlib.pyplot as plt
import math
import matplotlib as mpl
from matplotlib import gridspec 
from matplotlib import rc
from matplotlib.colors import ListedColormap
from scipy import optimize
rc('font',**{'family':'serif','serif':['Times']})
rc('text', usetex=True)

from palettable.colorbrewer.sequential import Blues_8
from palettable.colorbrewer.sequential import Blues_9
from palettable.colorbrewer.sequential import YlGnBu_8
from palettable.colorbrewer.sequential import PuBu_8


color_Bu_4 = Blues_8.mpl_colors[4]
color_outer_interval = YlGnBu_8.mpl_colors[6]
color_inner_interval = YlGnBu_8.mpl_colors[4]
color_likelihood = YlGnBu_8.mpl_colors[0]
color_scatter_points = (0.4,0.4,0.4)

print (PuBu_8.mpl_colors)
color_outer_interval = PuBu_8.mpl_colors[6]
color_inner_interval = PuBu_8.mpl_colors[4]
color_likelihood = PuBu_8.mpl_colors[0]

%{% endhighlight %}
