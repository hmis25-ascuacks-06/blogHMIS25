---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
title: Home
nav: true
---
# Bienvenidos al blog del grupo 6 🎉
El blog, aunque realizado para una entrega en la asignatura **Herramientas y Metodologías de la Ingeniería del Software**, nos servirá para demostrar los conocimientos adquiridos a lo largo de la asignatura. Estos varían desde aprender a usar Git y sus comandos, a usar Jenkins para automatizar procesos de testeo, e incluso usar Selenium para realizar tests sobre páginas web.
# 💫Posts más recientes💫

<ul>
  {% for post in site.posts limit:2 %}
    <li>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <p class="post-meta">{{ post.date | to_date | date: "%B %d, %Y" }}</p>
      <p>{{ post.excerpt }}</p>
      <a href="{{ post.url | relative_url }}">[Sigue leyendo]</a>
    </li>
  {% endfor %}
</ul>

Si quieres ver todos los posts, [pincha aquí.](posts.md)
