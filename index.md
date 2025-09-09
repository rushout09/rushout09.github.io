---
title: "Rushabh Agarwal"
---

## About Me

Hi, I am Rushabh. 

Here's what's been up:

- **2016**: Started studying **Information Technology** at [SRM University](https://www.srmist.edu.in/), Chennai. First time living far from home.
- **2020**: Began my career as a **Software Engineer (Testing)** at [Commvault Systems](https://commvault.com).
- **2022**: Moved into **DevOps** at [Hevo Data](https://hevodata.com).
- **2023**: Left my job to pursue **entrepreneurship** full-time at [Entrepreneur First](https://joinef.com).
- **2024**: Started **VedVaani**, scaled it into one of the **Top 100 Grossing apps in India**, and [sold it to Brahmveda Ventures](https://www.entrepreneur.com/en-in/news-and-trends/brahmveda-ventures-acquires-vedvaani-to-pioneer-ai-driven/482668).
- **2024**: Started [SEOExpert AI](https://tryseoexpert.com), an **agency** to learn and help founders with **SEO and marketing**.
- **2025**: Joined [Antler](https://antler.co) and started building [Comarketer](https://www.comarketer.dev) - **AI Websites & Ads** for founders to launch & market faster.

It hasn’t been easy. I struggle with anxiety and staying disciplined. Maybe it’s the cost of taking risks and being ambitious.

I have serious moments of genius, and when I get to working hard, no one can beat me. I am not being pompous either. 

I write infrequently about tech, business, and abstract personal experiences.

Some of the earlier posts are amatuer and cringe. I used to write like AI before it was (un)cool. Newer ones are just plain cringe.


PS: I’ve skipped over a lot of failed attempts and smaller wins that shaped me just as much. Left them out here for brevity.



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
