---
title: "Rush Agarwal"
---

## Posts

<ul id="post-list">
  {% for post in site.posts %}
    <li>
      <span>"{{ post.date | date: '%b %d, %Y' }}"</span>
      <a id="post-item" href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
