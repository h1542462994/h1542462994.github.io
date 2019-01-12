---
layout: post
title: "[Project]tty全平台后端(正在开发)-留言板"
create: 2018-01-03
update: 2019-01-03
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

## 留言板

> 这篇文档存粹是为了随便写点东西，技术文档请看API。

### 想法

原先的版本没有账号系统，而且没有自定义头像的功能。所以在账号系统的架构上想添加留言的功能，并做到能够添加评论。

> *mark*:原先的版本并不是我做的。

### 架构

没有分类系统，每个用户都可以新建一个话题，其他人可以在底下评论。

> `jschema`

```csharp
{
    "id":"int",
# delete description:简化信息
    "user":{
        "username":"string",
        "nickname":"string",
        "type":"enumint"//0普通用户，1VIP用户。
    },
# enddelete
# add
    "username":"string"
# endadd
# delete
    "meta":{
        "portrait":"$portrait:string",
        "istop":"$istop:boolean",//是否置顶。
        "islocked":"$islocked:boolean",//是否已经锁定。
        "time":"$time:string"//这里指更新的日期和时间。
    },
# enddelete
# add
    "time":"string",
    "istop":"int",//是否置顶
    "islocked":"int",//是否锁定评论
# endadd
    "content":"string",
# delete
    "comments":[{
        "id":"int",
        "user":{
            "username":"string",
            "nickname":"string",
            "type":"int"
        },
        "time":"string",
        "content":"string",
    }]
# enddelete
# add
    "commentidlast":"int",
    [SqlSerizable:jsonstring]
    "comments":[{
        "id":"int",//添加这个字段是为了后续删除评论。
        "username":"string",
        "time":"string",
        "content":"string"
    }]
# endadd
}
```

> *mark:* ①其实做了分类系统就更像一个论坛了。②这样的架构评论没有形成树状架构，但限于开发者本人知识，暂不开发。③上述架构还有待完善，因为需要考虑到将用户信息和留言内容分离。

### 数据库

> 更新后的架构请转到[MySql文档](https://h1542462994.github.io/blog/2018/12/23/aspserver-mysql/#留言系统模块)，下文部分并不会经常更新。

```csharp
{
    "name":"msgboard",
    "table":
    {
        "id":"int not null AUTO_INCREMENT",
        "username":"text not null",
        "time":"text not null",
        "istop":"int not null",
        "islocked":"int not null",
        "content":"text",
        "commentlastid":"int not null",
        "comments":"text",
        "pic":"MediumBlob"
    },
    "primarykey":"id"    
}
```

### 帮助文档

> 这一部分会告诉你如何优雅实现留言板的功能。

1. 获取留言信息后，用户信息不完整，这个可以在本地写一个缓存，并通过[获取用户公共信息API](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/#用户公共信息)来获取。

2. 接着1，还提供了[获取用户公共信息MD5码的API](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/#用户公共信息md5))。

3. 想要设置用户头像，请转到[设置用户信息的API](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/#24设置用户信息)。

> 设置用户头像还没有测试过。

## 聊天系统

> 这部分估计很久才开工，这里只是冲个数。

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