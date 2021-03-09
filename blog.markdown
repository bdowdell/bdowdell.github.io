---
layout: default
title: blog.
permalink: /blog/
---

<h1>Latest Posts</h1>

<ul class="no-bullets">
	{% for post in site.posts %}
	  <li>
	  	<h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
	  	<div class="card">{{ post.excerpt }}</div>
	  </li>
	{% endfor %}
</ul>