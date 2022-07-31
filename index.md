---
layout: default
---
{% assign sum = site.posts | size %}

<div>
  📂 전체 글 수 {{sum}}개
  <ul>
  {% for category in site.categories %}
    {% if category[0] == "python" %}
      <li>📂 Python ({{category[1].size}})</li>
        <ul>
          {% for post in site.posts %}
            <li>
              <a href="{{ post.url }}">{{ post.title }}</a>
            </li>
          {% endfor %}
        </ul>
    {% endif %}
  {% endfor %}
  </ul>  
</div>

