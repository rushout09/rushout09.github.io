---
title: "Rush Agarwal"
---

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.date | date: "%b %d, %Y" }}
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
