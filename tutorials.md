---
layout: page
title: 笔记
permalink: /tutorials/
---

{% assign categories = site.tutorials | map: "category" | uniq %}

{% for cat in categories %}
  <h2>{{ cat | capitalize }}</h2>
  <ul>
    {% assign sorted = site.tutorials | where: "category", cat | sort: "lesson" %}
    {% for item in sorted %}
      <li>
        <a href="{{ item.url }}">{{ item.title }}</a>
      </li>
    {% endfor %}
  </ul>
{% endfor %}