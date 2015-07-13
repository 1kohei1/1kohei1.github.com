---
layout: page
title: 1kohei1
tagline: Supporting tagline
---
{% include JB/setup %}
To share something I did not know before.

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}" class="post-list-link">{{ post.title }}</a></li>
  {% endfor %}
</ul>
