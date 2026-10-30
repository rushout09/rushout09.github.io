---
title: "Rushabh Agarwal"
---

<p class="site-name">Rushabh Agarwal</p>

## About

I live in India and have recently started exploring Brain-AI interfaces.

On the side, I run [Sareeviz](https://sareeviz.com), which makes AI photos and videos for Indian fashion brands. It started as a problem I saw in the textile industry.

I also help my father run our family's textile weaving factory.

## Writing

<ul class="post-list">
  {% for post in site.posts %}
    <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a> <span class="post-list-date">{{ post.date | date: "%b %Y" }}</span></li>
  {% endfor %}
</ul>
