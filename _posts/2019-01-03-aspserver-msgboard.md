---
layout: post
title: "[Project]微精弘全平台后端(正在开发)-留言板"
create: 2018-01-03
update: 2019-01-03
categories: children
tags: [Project]
description: ""
---

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