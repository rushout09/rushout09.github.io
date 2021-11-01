---
title: "Rush Agarwal"
---
<iframe src="http://localhost:3000/"></iframe>
## Posts

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <span><b>{{ post.date | date: '%b %d, %Y' }}<b></span>
      <a class="post-item" href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
