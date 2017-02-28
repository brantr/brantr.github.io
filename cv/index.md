---
layout: page
title: curriculum vita
excerpt: "CV for Brant Robertson"
modified: 2017-02-28T01:24:00
image:
  feature: banner.jpg
  credit: Brant Robertson
  creditlink: http://brantr.github.io
---


* Table of Contents
{:toc}

## Contact Information

##### *Mailing Address*
Department of Astronomy and Astrophysics  
University of California, Santa Cruz  
1156 High Street, ISB 335  
Santa Cruz, CA 95064  

##### *Phone and Fax*

**Phone:** (831) 459-4903  
**Fax:** (831) 459-5265  

##### *Electronic Addresses*
**Email:** <a href="mailto:brant@ucsc.edu">brant@ucsc.edu</a>  
**Web:** [GitHub IO](http://brantr.github.io)   [UCSC Research Group](https://robertson.sites.ucsc.edu)  

## Education

* Ph.D., Astronomy, Harvard University, 2006  
* M.A., Astronomy, Harvard University, 2003  
* B.S., Physics & Astronomy, University of Washington, 2001  
  *cum laude, with Distinction in Physics*  

## Employment


* Associate Professor, Department of Astrophysics and Astronomy, University of California, Santa Cruz 2015-Present
* Assistant Professor, Department of Astronomy, University of Arizona 2011-2015
* Hubble Fellow, California Institute of Technology 2009-2011
* Spitzer and Institute Fellow, Kavli Institute for Cosmological Physics and Enrico Fermi Institute, University of Chicago 2006-2009


<ul class="post-list">
{% for post in site.categories.cv %} 
  <li><article><a href="{{ site.url }}{{ post.url }}">{{ post.title }} <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time></span>{% if post.excerpt %} <span class="excerpt">{{ post.excerpt | remove: '\[ ... \]' | remove: '\( ... \)' | markdownify | strip_html | strip_newlines | escape_once }}</span>{% endif %}</a></article></li>
{% endfor %}
</ul>
