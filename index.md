---
title: "Rushabh Agarwal"
---
<!-- <iframe src="http://localhost:3000/"></iframe> -->

## About Me

Hi, I am Rushabh. 

I started my career as a software engineer. 

- First at Commvault Systems in 2020.
- Then at Hevo Data in 2022. 
- In 2023, I left my job to pursue entrepreneurship full-time.

It hasn’t been easy. I struggle with anxiety and staying disciplined. Maybe it’s the cost of taking risks and being ambitious

I have serious moments of genius, and when I get to working hard, no one can beat me. I am not a pompous person either. 


### What I'm Working On Currently

- **[comarketer.dev](https://comarketer.dev)**  
  Being a dev, I realised there are a lot of cool projects that goes unnoticed because of broken marketing. So I am building comarketer, a single platform for builders to market there product.

  Currently, I'm working on launching the V1 version of the product, which is an AI website builder optimized for marketing.

- **[SEOExpert AI](https://tryseoexpert.com)**  
  A productized SEO service to get actual clicks, leads, and money in the account.


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
