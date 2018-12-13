---
layout: page
title: "Archive"
description: "文章归档"
header-img: "img/Red-Brown.jpg"
---

<div class="one-tag-list">
{% for post in site.posts %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
	<span class="fa fa-tag listing-seperator" id="year:{{y}}">
		<span class="tag-text">{{ y }}</span>
	</span>
  {% endif %}
  <div class="post-preview">
	<a href="{{ post.url }}" title="{{ post.title }}">
		<h2 class="post-title">{{post.title}}</h2>
		<h3 class="post-subtitle">create: {{ post.create | date:"%Y-%m-%d" }} | update: {{ post.update | date:"%Y-%m-%d" }}</h3>
	</a>
  </div>
{% endfor %}
</div>