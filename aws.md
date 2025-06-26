---
layout: default
title: AWS Topics
permalink: /aws/
---

# AWS Cloud Technical Essentials

<ul>
  {% assign sorted_posts = site.aws-cloud-technical-essentials | sort: "order" %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
