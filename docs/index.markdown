---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: "Blog HMIS"
theme: Simplex
---
# Latest Posts

{% for post in site.posts %}
  - [{{ post.title }}]({{ post.url }})  
{% endfor %}