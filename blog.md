---
layout: default
title: Blog
permalink: /blog
---

## Blog

{% if site.posts.size > 0 %}
<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <em>{{ post.date | date: "%b %-d, %Y" }}</em> &mdash;
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
{% else %}
_No posts yet — check back soon._
{% endif %}
