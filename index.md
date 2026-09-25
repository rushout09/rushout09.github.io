---
title: "Rushabh Agarwal"
---

## Dharma

*The duty and work that shape destiny.*

- [Sareeviz](https://sareeviz.com): AI photos and videos for saree and fashion sellers.
- [Rungs](https://rungslabs.com): five apps, coming soon, that teach calisthenics, running, cycling, swimming and meditation one rung at a time.
- Publications: a network of niche ones, planned, for the writing and media side of things.
- SEO consulting for clients.
- Software for textile manufacturing: an ERP and a platform for designs.
- A weekly research session with Claude on investments, and probably on which apps and games are worth building. It may grow into a public tracker of what comes out of it.

## Samskara

*The impressions and habits that shape a person, and the rites that mark a passage.*

### Books

- [Shoe Dog](https://en.wikipedia.org/wiki/Shoe_Dog), Phil Knight. Read once, reading again.
- [Made in Japan](https://en.wikipedia.org/wiki/Made_in_Japan:_Akio_Morita_and_Sony), Akio Morita. Reading now. Craft, taste, quality obsession and East-West philosophy.
- [Steve Jobs](https://en.wikipedia.org/wiki/Steve_Jobs_%28book%29), Walter Isaacson. Reading now. Zen, design, quality obsession.

### Quotes

> "All great events always hang by a hair. The skillful man takes advantage of everything and neglects nothing that can give him a few more chances; the less skillful man, sometimes by neglecting a single one, loses everything."
>
> Napoleon Bonaparte

> "You have the right to perform your prescribed duties, but you are not entitled to the fruits of your actions. Never consider yourself the cause of the results of your activities, and never be attached to inaction."
>
> Bhagavad Gita 2.47

> "All that is gold does not glitter,
> Not all those who wander are lost;
> The old that is strong does not wither,
> Deep roots are not reached by the frost.
>
> From the ashes a fire shall be woken,
> A light from the shadows shall spring;
> Renewed shall be blade that was broken,
> The crownless again shall be king."
>
> J. R. R. Tolkien, The Fellowship of the Ring

### Videos

- [Train Who You Become](https://www.youtube.com/shorts/SHLEAp1CPQ4), Ascendra.
- [A Reminder To Let Go](https://www.youtube.com/shorts/8tdojVyyNKo), whyDEKHO by Hemant.
- [4-Year Marketing Degree in 2 Minutes](https://www.youtube.com/shorts/wcXIL6INX4w), GROWTH.

### Habits

- Cycling
- Calisthenics
- Eating right
- Sleeping on time

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
