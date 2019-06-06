---
layout: post
categories: blog
title: Morpheus via Docker
use_math: true
---

* Table of Contents
{:toc}


# Morpheus via Docker

Some instructions from Ryan Hausen on how to use Morpheus with Docker:


<h1 id="working-with-the-docker-image">Working With the Docker Image</h1>
<p>Here's my process that I use when working with Docker on a remote machine. I usually run a ssh session in the remote machine and edit files locally using sshfs.</p>
<ol type="1">
<li><p>Make a working directory where the data and scripts will go in my local machine. For example, I'll make an empty dir in Documents:</p>
<blockquote>
<div class="sourceCode"><pre class="sourceCode bash"><code class="sourceCode bash"><span class="co"># local machine</span>
<span class="kw">mkdir</span> -p ~/Documents/sersic-images</code></pre></div>
</blockquote></li>
<li><p>Next, ssh into the remote machine and make a directory that will be mounted using sshfs and will mirror our local dir (leave this terminal open):</p>
<blockquote>
<div class="sourceCode"><pre class="sourceCode bash"><code class="sourceCode bash"><span class="co"># remote machine</span>
<span class="kw">mkdir</span> -p ~/Documents/sersic-imagesc
<span class="kw">cd</span> ~/Documents/sersic-images</code></pre></div>
</blockquote></li>
<li><p>Use sshfs to mount the remote dir to our local dir:</p>
<blockquote>
<div class="sourceCode"><pre class="sourceCode bash"><code class="sourceCode bash"><span class="co"># local machine</span>
<span class="co"># USUAGE: sshfs [user@]hostname:[directory] mountpoint</span>
<span class="kw">sshfs</span> brant@sparkle:/home/brant/Documents/sersic-images ~/Documents/sersic-images</code></pre></div>
</blockquote></li>
<li>Now we have a remote terminal that is in a dir that is mounted locally. Add all of the files that you want to work to the local dir and you can work from there.</li>
<li><p>Let's start using Docker in the remote terminal:</p>
<blockquote>
<div class="sourceCode"><pre class="sourceCode bash"><code class="sourceCode bash"><span class="co">#remote machine</span>

<span class="co"># run for cpu version</span>
<span class="kw">docker</span> run -it -v ~/Documents/sersic-images:/root/src morpheusastro/morpheus:latest-cpu

<span class="co">#run for gpu version</span>
<span class="kw">docker</span> run --runtime=nvidia -it -v ~/Documents/sersic-images:/root/src morpheusastro/morpheus:latest-gpu
<span class="kw">cd</span> /root/src

<span class="co"># confirm that all of the files that copied into your local dir are here too</span>
<span class="kw">ls</span></code></pre></div>
</blockquote></li>
<li>Now you're in the Docker Image! When you make changes to your local dir, they will get mirrored toyour remote dir which is mounted in Docker, so they will be reflected in the Docker image as well.</li>
<li>Now for general use see the docs: <a href="https://morpheus-astro.readthedocs.io/en/latest" class="uri">https://morpheus-astro.readthedocs.io/en/latest</a></li>
</ol>

