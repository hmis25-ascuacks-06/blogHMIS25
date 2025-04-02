---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: custom-home
---
# Posts

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        {% if post.date %}
            <p>Existe</p>
        {% else %}
            <p>No existe</p>
        {% endif %}
      <p class="post-meta">{{ post.date | to_date | date: "%B %d, %Y" }}</p>
      <p>{{ post.excerpt }}</p>
      <a href="{{ post.url | relative_url }}">[Sigue leyendo]</a>
    </li>
  {% endfor %}
</ul>
