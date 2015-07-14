---
layout: page
title: 1kohei1
tagline: Supporting tagline
---
{% include JB/setup %}
To share something I did not know before.

#### Posts
<ul class="post-list">
  {% for post in site.posts %}
    <li class="post-list-item">
    	<a href="{{ BASE_PATH }}{{ post.url }}" class="post-list-link">
    		{{ post.title }}
    	</a>
	    	<section class="post-meta">
		    	<time class="post-date" date-time="{{ post.date }}">{{ post.date | date_to_long_string }}</time>
	    	</section>
    </li>
  {% endfor %}
</ul>
