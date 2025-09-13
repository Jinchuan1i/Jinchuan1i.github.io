---
layout: default
title: Jefferson Li — Portfolio
last_updated: Sep 12, 2025
---

<section class="hero">
  <h1>Hi, I'm Jefferson.</h1>
  <p class="muted">
    This site collects coursework, projects, and notes.
  </p>
</section>

<section class="grid">
  {% assign items = site.projects | sort: "updated" | reverse %}
  {% for p in items %}
  <article class="card">
    <h3><a href="{{ p.url | relative_url }}">{{ p.title }}</a></h3>
    {% if p.subtitle %}<div class="muted">{{ p.subtitle }}</div>{% endif %}
    {% if p.blurb %}<div class="desc">{{ p.blurb }}</div>{% endif %}
    {% if p.updated %}<div class="meta">Updated: {{ p.updated }}</div>{% endif %}
  </article>
  {% endfor %}
</section>
