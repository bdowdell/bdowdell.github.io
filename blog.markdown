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
	  	{%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
	  	<div class="post-excerpt">
	  		<span class="post-meta">{{ post.date | date: date_format }}</span>
	  		<div class="content">
	  			{{ post.excerpt }}
	  			:point_right: <a href="{{ post.url }}">read more ...</a>
	  		</div>
	  	</div>
	  </li>
	{% endfor %}
</ul>