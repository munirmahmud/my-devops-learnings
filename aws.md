---
layout: default
title: AWS Topics
permalink: /aws/
---

# AWS Learning Posts

<ul>
  {% assign sorted_posts = site.aws | sort: "order" %}
  {% for post in sorted_posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
