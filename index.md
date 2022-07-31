---
layout: default
---
{% assign sum = site.posts | size %}

<div>
📂 전체 글 수 {{sum}}개
</div>

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
