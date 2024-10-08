---
title: "Rushabh Agarwal"
---
<!-- <iframe src="http://localhost:3000/"></iframe> -->

## About Me

Hi, I am Rushabh. 


I left my Software Engineering job in 2023 to explore startups.
Currently I am working on SeoExpert AI - A Productized service that uses AI agents to automate SEO.

I write infrequently about tech, business, and personal experiences. 
Some of the earlier posts are amatuer and cringe. I used to write like AI before it was (un)cool. 
Newer ones are just plain cringe.


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
