---
layout: page
title: arXiv
excerpt: "An archive of arXiv notes sorted by date."
search_omit: true
---

Short notes about arXiv postings relevant to astrophysics.

<ul class="post-list">
{% for post in site.categories.arxiv %} 
  <li><article><a href="{{ site.url }}{{ post.url }}">{{ post.title }} <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time></span>{% if post.excerpt %} <span class="excerpt">{{ post.excerpt | remove: '\[ ... \]' | remove: '\( ... \)' | markdownify | strip_html | strip_newlines | escape_once }}</span>{% endif %}</a></article></li>
{% endfor %}
</ul>
