---
title: "Rush Agarwal"
---

## Posts

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <span>{{ post.date | date: '%b %d, %Y' }}</span>
      <a class="post-item" href="{{ post.url }}">{{ post.title }}</a>
      <p class="post-item">{{ post.excerpt }}</p>
    </li>
  {% endfor %}
</ul>
