---
layout: page
title: "Tags"
comments: false
sharing: true
footer: true
---

{% capture tags %}
  {% for tag in site.categories %}
    {{ tag[0] }}
  {% endfor %}s
{% endcapture %}
{% assign sortedtags = tags | split:' ' | sort %}

{% for tag in sortedtags %}
  <h3 id="{{ tag }}">{{ tag }}</h3>
  <ul>
  {% for post in site.categories[tag] %}
    <li>
      {% include postlistitem.html %}
    </li>
  {% endfor %}
  </ul>
{% endfor %}