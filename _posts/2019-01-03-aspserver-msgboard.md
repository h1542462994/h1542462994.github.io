---
layout: post
title: "[Project]tty全平台后端(正在开发)-留言板"
create: 2018-01-03
update: 2019-01-03
categories: blog
tags: [Project]
description: ""
---

[主页](https://h1542462994.github.io/blog/2018/12/23/aspserver-index/)

`API系列` [API文档-用户部分](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/)  [API文档-留言板](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/)   [API文档-微精弘](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-wejh/)

`工程与部署` [MySql文档](https://h1542462994.github.io/blog/2018/12/23/aspserver-mysql/)  [部署](https://h1542462994.github.io/blog/2018/12/23/aspserver-deploy/)

`杂项` [*数据(调试用)](https://h1542462994.github.io/blog/2018/12/23/aspserver-data/)    [第三方提供的API](https://h1542462994.github.io/blog/2018/12/23/aspserver-providedapi/)

`日志` [更新日志](https://h1542462994.github.io/blog/2019/01/09/aspserver-updatelog/)

`想法&开发者提示` [留言板](https://h1542462994.github.io/blog/2019/01/03/aspserver-msgboard/)

-------

#### 想法

原先的版本没有账号系统，而且没有自定义头像的功能。

#### 架构

没有分类系统，每个用户都可以新建一个话题，其他人可以在底下评论。

```csharp
{
    "id":"$id:int",
    "user":{
        "username":"$username:string",
        "nickname":"$nickname:string",
        "type":"$type:int"//0普通用户，1VIP用户。
    },
    "meta":{
        "portrait":"$portrait:string",
        "istop":"$istop:boolean",//是否置顶。
        "islocked":"$islocked:boolean",//是否已经锁定。
        "time":"$time:string"//这里指更新的日期和时间。
    },
    "content":"$content:string",
    "comments":[{
        "id":"$id:int",
        "user":{
            "username":"$username:string",
            "nickname":"$nickname:string",
            "type":"$type:int"
        },
        "time":"$time:string",
        "content":"$content:string",
    }]
}
```

数据库

```csharp
username:string
time:datetime
istop:int
islocked:int
comments:string ::jsonof array[id,username,time,content]
```

聊天系统

```json
{
    "name":"chat",
    "table":{
        "id":"int not null AUTO_INCREMENT",
        "from":"text",
        "to":"text",
        "time":"datetime",
        "content":"text"
    }
}
```

```
create table chat(
    int not null AUTO_INCREMENT,
    from text not null,
    to text not null,
    time text not null,
    content text not null,
    PRIMARY KEY(id)
);

```