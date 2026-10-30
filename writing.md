---
title: "Writing"
layout: default
permalink: /writing.html
---

<p><a class="site-name" href="{{ '/' | relative_url }}">Rushabh Agarwal</a></p>

## Writing

<ul class="post-list">
  {% for post in site.posts %}
    <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a> <span class="post-list-date">{{ post.date | date: "%b %Y" }}</span></li>
  {% endfor %}
</ul>
