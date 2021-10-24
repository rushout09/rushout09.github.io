---
title: "Rush Agarwal"
---

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>

## Work in progress:

- Add commenting ability. check out utterance.
- link to github profile, linkedin, twitter, edit on github. 
- Implement Tags.
- Implement Navigation.
- Blog on Why to build in public and importance of marketing.
- Detailed Blog on how I am implementing this current blog.
- Blog on how to maintain notes, docs, journal using git.