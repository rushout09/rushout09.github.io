---
title: "Rush Agarwal"
---

## Posts

<ul id="post-list">
  {% for post in site.posts %}
    <li id="post-item">
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
