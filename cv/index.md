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

---

## Education

* Ph.D., Astronomy, Harvard University, 2006  
* M.A., Astronomy, Harvard University, 2003  
* B.S., Physics & Astronomy, University of Washington, 2001  
  *cum laude, with Distinction in Physics*  



<ul class="post-list">
{% for post in site.categories.cv %} 
  <li><article><a href="{{ site.url }}{{ post.url }}">{{ post.title }} <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time></span>{% if post.excerpt %} <span class="excerpt">{{ post.excerpt | remove: '\[ ... \]' | remove: '\( ... \)' | markdownify | strip_html | strip_newlines | escape_once }}</span>{% endif %}</a></article></li>
{% endfor %}
</ul>
