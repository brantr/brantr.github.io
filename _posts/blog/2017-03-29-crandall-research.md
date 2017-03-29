---
layout: post
categories: blog
title: Crandall Research
use_math: true
---

* Table of Contents
{:toc}


## Source -- Image Registration

Sara has been conducting some tests to see how
well SEP (pythonified Sextractor) recovers the
input mock catalog properties.  She has created
a python notebook for this study at:

[Source Recovery Jupyter Notebook](https://nbviewer.jupyter.org/gist/sararosecran/9c0edda1bd579440c00d77cd9c95088b)

When overlaying the sources as a function of
RA and dec on top of the image, there appears to
be an unusual shift or distortion in the image.

![RA-Dec Registration]({{ site.url }}/images/ra_dec_registration_03292017.png)

However, the pixel location of the sources appears to
be correct:
 
![Pixel Registration]({{ site.url }}/images/pixel_registration_03292017.png)

I reviewed what Sara did and noticed that she assumed
RA and Dec are aligned with the pixel values:

{% highlight python %}
x_test = (0,0,nx-1,nx-1)
y_test = (0,ny-1,0,ny-1)
ra_test, dec_test = world(fname_img, x_test, y_test)
print ra_test, dec_test
{% endhighlight %}

Which gives

{% highlight python %}
[ 53.10148765  53.10187856  53.1288215   53.12920629] [-27.8135469  -27.7892198  -27.81388789 -27.78956071]
{% endhighlight %}

This means the x and y pixels are not aligned with RA and Dec. Using world min and max determined from the pixel extent will lead to a distortion.

The corresponding notebook is here:

[JWST Source Registration Test Jupyter Notebook]({{ site.url }}/notebooks/jwst_mock_image_source_registration_03292017.ipynb)


## JWST PSF Aperture Corrections

We would also like to measure the JWST PSF aperture 
corrections for point sources. We suspect that some of
the offset between the source magnitudes found by SEP
and those in the original mock catalog originate solely
from the SEP aperture photometry.  This effect should be
easy to measure.

Here are the JWST PSFs:

[JWST PSFs (tarball)](http://mips.as.arizona.edu/~cnaw/psf.tgz)

Using the F090W PSF, I computed the following aperture
corrections:


![F090W aperture correction]({{ site.url }}/images/F090W_aperture_correction.png)

The notebook I used to compute the aperture correction is [here]({{ site.url }}/notebooks/jwst_psf_aperture_correction.ipynb).
