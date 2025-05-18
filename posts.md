---
layout: page
title:  "Posts"
permalink: /posts/
---

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p class="post-meta">{{ post.date | to_date | date: "%B %d, %Y" }}</p>
      <p>{{ post.excerpt }}</p>
      <a href="{{ post.url | relative_url }}">[Sigue leyendo]</a>
    </li>
  {% endfor %}
</ul>