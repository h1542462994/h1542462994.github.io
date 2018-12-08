---
layout: page
title: "Tags"
description: "哈哈，你找到了我的文章基因库"  
header-img: "img/semantic.jpg"  
---

##本页使用方法

1. 在下面选一个你喜欢的词
2. 点击它
3. 相关的文章会「唰」地一声跳到页面顶端
4. 马上试试？

##基因列表

<!--标签云-->
<div id='tag_cloud' class='tags'>
{% for tag in site.tags %}
<a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
{% endfor %}
</div>

<!--标签列表-->
<div class="one-tag-list">
{% for tag in site.tags %}
  <span class="fa fa-tag listing-seperator" id="{{ tag[0] }}">
	<span class="tag-text">{{ tag[0] }}</span>
  </span>
{% for post in tag[1] %}
  <li class="listing-item">
  <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
  <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
  <div class="post-preview">
	<a href="{{ post.url }}" title="{{ post.title }}">
		<h2 class="post-title">{{ post.title }}</h2>
		{% if(post.subtitle && post.subtitle.length) { %}
			<h3 class="post-subtitle">{{ post.subtitle }}</h3>
		{% } %}
	</a>
  </div>
{% endfor %}
{% endfor %}
 </div>

<script src="/media/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 
<script language="javascript">
$.fn.tagcloud.defaults = {
    size: {start: 1, end: 1, unit: 'em'},
      color: {start: '#f8e0e6', end: '#ff3333'}
};

$(function () {
    $('#tag_cloud a').tagcloud();
});
</script>

