---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
---
# Posts

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


<footer>
  <h3>Dev Files</h3>
  <ul>
    {% assign devs_files = site.pages | where: "path", "devs/" %}
    {% for file in devs_files %}
      <li><a href="{{ file.url | relative_url }}">{{ file.title }}</a></li>
    {% endfor %}
  </ul>
</footer>