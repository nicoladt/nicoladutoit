---
layout: page
permalink: /words/index.html
title: Words
description: "An archive of blog posts sorted by date."
---

<ul class="post-list">
{% for post in site.posts %} 
  <li><article><a href="{{ site.url }}{{ post.url }}"><b>{{ post.title }}</b> <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%d %B, %Y" }}</time></span></a><p> {{ post.description }}</p></article></li>
{% endfor %}
</ul>
