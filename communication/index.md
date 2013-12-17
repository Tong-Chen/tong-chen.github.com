---
title: Carved stones
layout: page
---

<ul class="listing">
{% for cat in site.categories %}
{% if cat[0] == 'communication' %}
{% if cat[1].size > 0 %}
{% for post in cat[1] %}
  <li class="listing-item">
  <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
  <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
{% endfor %}
{% else %}
  <li class="listing-item">
  <a href="{{ site.baseurl }}" title="Too lazy to have a post">Return home</a>
  </li>
{% endif %}
{% endif %}
{% endfor %}
</ul>

