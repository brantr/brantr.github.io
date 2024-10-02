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


# Working With the Docker Image

>Here's my process that I use when working with Docker on a remote machine. I usually run a ssh session in the remote machine and edit files locally using sshfs.

### 1. Make a working directory where the data and scripts will go in my local machine. For example, I'll make an empty dir in Documents:
{% highlight bash%}
#local machine  
mkdir -p ~/Documents/sersic-images  
{% endhighlight %}

### 2. Next, ssh into the remote machine and make a directory that will be mounted using sshfs and will mirror our local dir (leave this terminal open):
{% highlight bash%}
#remote machine  
mkdir -p ~/Documents/sersic-images  
cd ~/Documents/sersic-images  
{% endhighlight %}

### 3. Use sshfs to mount the remote dir to our local dir:
{% highlight bash%}
#USAGE: sshfs [user@]hostname:[directory] mountpoint
#local machine
sshfs brant@sparkle:/home/brant/Documents/sersic-images ~/Documents/sersic-images  
{% endhighlight %}

Now we have a remote terminal that is in a dir that is mounted locally. Add all of the files that you want to work to the local dir and you can work from there.

### 4. Let's start using Docker in the remote terminal:
{% highlight bash%}
#remote machine
#run for cpu version
docker run -it -v ~/Documents/sersic-images:/root/src morpheusastro/morpheus:latest-cpu  
{% endhighlight %}

{% highlight bash%}
#remote machine
#run for gpu version
docker run --runtime=nvidia -it -v ~/Documents/sersic-images:/root/src morpheusastro/morpheus:latest-gpu   
{% endhighlight %}

{% highlight bash%}
#remote machine
cd  /root/src   
{% endhighlight %}

{% highlight bash%}
#remote machine
#confirm that all of the files that copied into your local dir are here too
ls  
{% endhighlight %}

### 5. Now you're in the Docker Image! When you make changes to your local dir, they will get mirrored toyour remote dir which is mounted in Docker, so they will be reflected in the Docker image as well.  

### 6. For general use see the docs: 
<a href="https://morpheus-astro.readthedocs.io/en/latest" class="uri">https://morpheus-astro.readthedocs.io/en/latest</a>

