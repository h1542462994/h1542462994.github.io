---
layout: post
title: ѧϰ�Blog On Github
date: 2018-12-07
categories: blog
---

#### ��Github���½�һ��Repository

1.���û��github�˻�����[����һ��github�˻�](https://github.com/join)������������һ����
2.

#### �����Լ����˻�

1.�Ӹ��ļ��д�**_config.yml**���ῴ��������Ϣ��������ʾ�޸ġ�

```yml
# Site settings
title: �������� # ��Ĳ������֣����Զ����޶�
header-img: "img/green.jpg"
tagline: "cn"  
description: "�����ҵĲ���"  # һ�仰������Ĳ���
baseurl: ""
url: "http://cnfeat"  # �˴���д��Ĳ��͵�ַ 

# About/contact
owner: 
  name: "��������" # ��д������Ϣ������
  email: X@gmail.com # ��д������Ϣ������
  bio: "��Ĳ�������" # ��д������Ϣ����������

# Data
gavatar: img/favicon.png # �������ַ��Сͼ�꣬���Զ������
favicon: img/favicon.png # �������ַ��Сͼ�꣬���Զ������

douban_username:  # ��Ķ���id
twitter_username: 
github_username: 
facebook_username: 
weibo_username: 
zhihu_username: 

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
      author: "�������" # �������
      header-img: "img/green.jpg" # We don't want posts without a header image, that whould mean white on white

# Comments 
comments :
  provider : disqus # ʹ�� disqus ����ģ�飬���߷�ǽ���ܿ���
  duoshuo :
    short_name :  # ��д��� disqus id
  disqus :
      short_name :  # ��д��� disqus id

# Analytics and webmaster tools stuff goes here
google_analytics:  # ��д��  google_analytics id
google_verify:
# https://ssl.bing.com/webmaster/configure/verify/ownership Option 2 content= goes here
bing_verify:

# Links to include in footer navigation
```