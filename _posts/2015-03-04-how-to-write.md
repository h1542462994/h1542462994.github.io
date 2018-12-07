---
layout: post
title: 从模板开始创建博客。
date: 2018-12-07
categories: blog
tags: [博客,小技巧]
description: 从模板开始创建博客。
---

#### 在Github上新建一个Repository

1.*创建github账户* 如果没有github账户，请[创建一个github账户](https://github.com/join)，如有则跳过这一步。假设你创建的账户名为yourname。

2.为了方便起见，你将转到一个[博客的模板](https://github.com/h1542462994/blog.io)，然后点击右上角的**Fork**。

3.依次点击**你的账户**，**Repositories**，**blog.io**，**Settings**。然后修改*Repository name*为**yourname.github.io**。

4.打开Github Desktop，克隆这个项目(Clone Repository)，然后进行配置自己的账户的操作。

#### 配置自己的账户

1.从根文件夹打开**_config.yml**，会看到下列信息，将**[]**包围的信息按照**提示**修改。

```yml
	# Site settings
	title: [Title] # 你的博客的标题
	header-img: "img/green.jpg"
	tagline: "cn"  
	description: [Description]  # 用一句话描述你的博客
	baseurl: ""
	url: [Url]  # 此处填写你的博客地址 

	# About/contact
	owner: 
	  name: [Author Name] # 填写作者信息：名字
	  email: [Email Address] # 填写作者信息：邮箱
	  bio: [Author Description] # 填写作者信息：博客描述

	# Data
	gavatar: img/favicon.png # 浏览器地址栏小图标，可自定义更改
	favicon: img/favicon.png # 浏览器地址栏小图标，可自定义更改

	# Links
	# douban_username: 
	# twitter_username: 
	github_username: 
	# facebook_username: 
	# weibo_username: 
	# zhihu_username: 

	# Build settings  
	# use Github Flavored Markdown !important  
	# document: http://jekyllrb.com/docs/configuration/#kramdown  
	markdown: kramdown
	highlighter: rouge
	permalink: pretty
	paginate: 8
	exclude: ["less","node_modules","Gruntfile.js","package.json","README.md"]

	# http://en.wikipedia.org/wiki/List_of_tz_database_time_zones
	timezone: Asia/Shanghai

	# Defaults for posts
	defaults:
	  -
		scope: 
		  path: ""
		  type: "posts"
		values:
		  layout: "post"
		  author: [Anthor Name] # 你的名字
		  header-img: "img/green.jpg" # We don't want posts without a header image, that whould mean white on white

	# Comments 
	# comments :
	  # provider : disqus # 使用 disqus 评论模块，读者翻墙才能看见
	  # duoshuo :
		# short_name :  # 填写你的 disqus id
	  # disqus :
		# short_name :  # 填写你的 disqus id

	# Analytics and webmaster tools stuff goes here
	google_analytics:  # 填写你  google_analytics id
	google_verify:
	# https://ssl.bing.com/webmaster/configure/verify/ownership Option 2 content= goes here
	bing_verify:

	# Links to include in footer navigation
```
###### 提示

```
	[Title]: 你的博客的标题，将会显示在地址栏，navbar的左端以及home页。
	[Description]: 你的博客的描述，将会显示在home页最大的字的下方。
	[Url]: 这个属性很重要，你要填你博客主页的网址，一般为yourname.github.io。
	[Author Name]: 作者的名称，一般显示在页脚（写版权声明的地方）。
	[Email Address]: 作者的邮箱，一般并没有什么用，可以忽略。
	[Author Description]: 作者的描述，将会显示在about页最大的字的下方。
```

2.