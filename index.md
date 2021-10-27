---
title: "Rush Agarwal"
---

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <i>post.date</i>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
