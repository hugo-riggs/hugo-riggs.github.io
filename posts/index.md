---
layout: default 
title:  "Posts"
---

### Contents:

<ul>
{% for post in site.posts %}
	<li>
		<a href="{{ post.url }}">{{ post.title }}</a>
	</li>
{% endfor %}
</ul>

