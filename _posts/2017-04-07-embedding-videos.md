---
layout: post
categories: blog
title: Embedding QuickTime Videos
use_math: true
---

* Table of Contents
{:toc}

# Attempts at including video in a github post.

I'd like to include the video tag in a github post.  I know that I can upload an HTML file and connect directly.
But I would like to include a link directly in a website.

Unfortunately, none of the following seem to work...


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

Doesn't seem to work.

## Give up.

[Click here to see the movie]({{ site.url }}/movies/disk.mov)
