---
title: "Rushabh Agarwal"
---

> "All great events always hang by a hair. The skillful man takes advantage of everything and neglects nothing that can give him a few more chances; the less skillful man, sometimes by neglecting a single one, loses everything."
>
> — Napoleon Bonaparte

> "You have the right to perform your prescribed duties, but you are not entitled to the fruits of your actions. Never consider yourself the cause of the results of your activities, and never be attached to inaction."
> 
> — Bhagavad Gita 2.47

## Posts

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <span><strong>{{ post.date | date: '%b %d, %Y' }}</strong></span>
      <a class="post-item" href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
