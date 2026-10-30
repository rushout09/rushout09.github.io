<!-- Sections taken off the home page on 30 Oct 2026, kept here unpublished. -->

## Main quest

A brain-computer interface: reading brain waves well enough to turn thought straight into text and actions, with no keyboard or voice in between. It is the idea that blows my mind and the one I would happily spend years on. It is a moonshot, which is rather the point.

## Side quests

- [Sareeviz](https://sareeviz.com): AI photos and videos for Indian fashion photo studios and ecommerce brands. It began as a problem, and an opportunity, inside my family's textile business, and I happened to be standing in the right spot at the right time, with the right people around me. It is built with AI and sells useful AI to Indian MSMEs, which means it could not have existed at any other point in time. So far it is the thing I have made that earns the most.
- [doomreader](https://doomreaderapp.com): books, read the way you doomscroll, one short card at a time. I built it because I wanted it. I like reading and have tried hard with Google Books and Kindle, but neither ever turned reading into a habit, so I made the app that could. Then it seemed a waste not to sell it: if it brings in some quiet revenue next to Sareeviz, that is a win. I also have a theory that AI has reached an inflection point, where a habit app like Duolingo takes months to build rather than years.
- [Rungs Labs](https://rungslabs.com): five apps, coming soon, that teach calisthenics, running, cycling, swimming and meditation one rung at a time.

## Also on the plate

- A network of niche publications, planned.
- Software for textile manufacturing: an ERP and a platform for designs.
- A weekly research session with Claude on investments, and on which apps and games are worth building.

## Books

- [Shoe Dog](https://en.wikipedia.org/wiki/Shoe_Dog), Phil Knight. Read once, reading again.
- [Made in Japan](https://en.wikipedia.org/wiki/Made_in_Japan:_Akio_Morita_and_Sony), Akio Morita. Reading now. Craft, taste, quality obsession and East-West philosophy.
- [Steve Jobs](https://en.wikipedia.org/wiki/Steve_Jobs_%28book%29), Walter Isaacson. Reading now. Zen, design, quality obsession.

## Quotes

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

## Videos

- [Train Who You Become](https://www.youtube.com/shorts/SHLEAp1CPQ4), Ascendra.
- [A Reminder To Let Go](https://www.youtube.com/shorts/8tdojVyyNKo), whyDEKHO by Hemant.
- [4-Year Marketing Degree in 2 Minutes](https://www.youtube.com/shorts/wcXIL6INX4w), GROWTH.

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
