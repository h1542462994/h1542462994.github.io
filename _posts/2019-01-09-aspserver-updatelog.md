---
layout: post
title: "[Project]tty全平台后端(正在开发)-更新日志"
create: 2019-01-09
update: 2019-01-10
categories: blog
tags: [Project]
description: ""
---

-------

[主页](https://h1542462994.github.io/blog/2018/12/23/aspserver-index/)    [项目地址](https://github.com/TropicalTeamYard/tty.platform.aspserver)<br/>
`API系列` [API-映射表](https://h1542462994.github.io/blog/2019/01/12/aspserver-apimap) [API文档-用户部分](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/)  [API文档-留言板](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/)   [API文档-微精弘](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-wejh/)<br/>
`工程与部署` [MySql文档](https://h1542462994.github.io/blog/2018/12/23/aspserver-mysql/)  [部署](https://h1542462994.github.io/blog/2018/12/23/aspserver-deploy/)<br/>
`杂项` [&数据(调试用)](https://h1542462994.github.io/blog/2018/12/23/aspserver-data/)    [第三方提供的API](https://h1542462994.github.io/blog/2018/12/23/aspserver-providedapi/)<br/>
`日志` [更新日志](https://h1542462994.github.io/blog/2019/01/09/aspserver-updatelog/)<br/>
`想法&开发者提示` [留言板](https://h1542462994.github.io/blog/2019/01/03/aspserver-msgboard/)    [开发规范](https://h1542462994.github.io/blog/2019/01/11/aspserver-regular/)  

-------

## API文档-更新日志

*2019/1/2* `sql` 数据库添加AES加密

*2019/1/3* `user` 将用户系统和微精弘独立

*2019/1/3* `user` *精弘快速登录 

> 该方法准备弃用，合并到登录方法

*2019/1/3* `user` [`link_1`]获取学校时间

*2019/1/3* `user` 绑定精弘账号

*2019/1/3* `user` 绑定正方教务系统账号

*2019/1/3* `user` 获取正方课表

*2019/1/3* `user` 获取绑定信息

*2019/1/7* `user` 添加用户头像

*2019/1/8* `user` 修改登录，注册密码为需要MD5加密

*2019/1/9* `msgboard` 添加留言板模块

*2019/1/10* `msgboard` 留言评论添加id字段

*2019/1/12* `msgboard` 实现留言增加的功能

*2019/1/12* `msgboard` 添加修改留言和删除留言的接口

### TODO

[`link_1`] `user` 能够在寒暑假也能获取时间

~~`global` 添加网页端登录接口~~

`user` 绑定校园卡账号

`user` 绑定图书馆账号

~~`user` 绑定原创教务系统账号~~

### 问题

> 欢迎各位发现问题的`Pull`一下，以及时发现并更正问题。

### 收藏的标签
