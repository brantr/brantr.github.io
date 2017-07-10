---
layout: post
categories: blog
title: Matplotlib Imshow Orientation
use_math: true
---

* Table of Contents
{:toc}


## Matplotlib imshow() orientation

In imshow(), the second index is aligned with the "x" axis.  And [0,0] is in the upper left.  So both `origin="lower"' and a transpose are needed in most cases to align [i,j] with [x,y].

{% highlight python %}
nx = 512
ny = 512
image = np.zeros((nx,ny))
for i in range(nx):
  for j in range(ny):
    image[i,j] = np.sin(2*np.pi*float(i)/float(nx)) + np.sin(6*np.pi*float(y)/float(ny))
plt.imshow(image.T,origin="lower")
{% endhighlight %}

<img src="{{ site.url }}/images/imshow_orientation.png" width=500>
