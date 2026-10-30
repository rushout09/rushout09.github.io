---
title: "Photos"
layout: default
permalink: /photos.html
---

<p><a class="site-name" href="{{ '/' | relative_url }}">Rushabh Agarwal</a></p>

## Photos

<style>
  body { max-width: 1000px; }
  .photo-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); gap: 28px 20px; }
  .photo-grid figure { margin: 0; }
  .photo-grid img { display: block; width: 100%; aspect-ratio: 4 / 5; object-fit: cover; border-radius: 4px; }
  .photo-grid figcaption { margin-top: 8px; font-size: 0.9rem; line-height: 1.5; color: var(--muted); }
</style>

<!-- Posts from instagram.com/rushin_out, listed in _data/instagram.json (newest first). -->
<div class="photo-grid">
{% for p in site.data.instagram %}
  <figure>
    <a href="{{ p.permalink }}"><img src="{{ p.image | relative_url }}" alt="" loading="lazy"></a>
    {% if p.caption != "" %}<figcaption>{{ p.caption }}</figcaption>{% endif %}
  </figure>
{% endfor %}
</div>
