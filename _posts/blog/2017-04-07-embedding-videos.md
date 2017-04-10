---
layout: post
categories: blog
title: Embedding QuickTime Videos
use_math: true
---

* Table of Contents
{:toc}


## Example embedding of a quicktime movie

{% highlight html%}
<div>
<video controls preload width=500>
<source src="{{ site.url }}/movies/disk.mov" type="video/quicktime">
</video>
</div>
{% endhighlight %}

## Movie

<html>
<video controls preload width=500 markdown="0">
<source src="{{ site.url }}/movies/disk.mov" type="video/quicktime">
</video>
</html>

## Try iframe

<iframe width=500 src="{{ site.url }}/movies/disk.mov"></iframe>

## Try include.

{% include "{{ site.url }}/html/disk_04092017.html" %}