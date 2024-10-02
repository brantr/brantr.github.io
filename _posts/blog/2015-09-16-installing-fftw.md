---
layout: post
categories: blog
title: Installing FFTW
---

---

{% highlight bash %}
cd code/fftw
curl -O http://www.fftw.org/fftw-3.3.4.tar.gz
tar -zxvf fftw-3.3.4.tar.gz
cd fftw-3.3.4
CC=mpicc CXX=mpicxx ./configure --enable-mpi
make -j 10
sudo make install
{% endhighlight %}
