---
layout: post
title: "[wejh]微精弘全平台后端(正在开发)-数据库模型与交互"
create: 2018-12-23
update: 2018-12-23
categories: children
tags: [wejh]
description: ""
---

## mysql语句

------

### 数据库

#### 配置

##### mssql

将文档中所有`MySqlUtil`换成`SqlUtil`。

> 注意，因为`MySqlUtil`和`SqlUtil`依赖的类并不相同，所以创建了两个类，以适配数据库，但是两种数据库的语法是相同的。

修改`appsettings.json`中的`ConnectionStrings`为
```
{
    "wejhplatform":"Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=wejhplatform;Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False"
}
```

##### mysql

导入`NuGet`包`MySQL.Data`。

将文档中所有`SqlUtil`换成`MySqlUtil`。

修改`appsettings.json`中的`ConnectionStrings`为
```
{
    "wejhplatform":"server=localhost;userid=root;password=123456;database=wejhplatform;"
}
```

#### contents

```
{
    "name":"wejhplatform",
    "tables":[
        "usercredit",

    ]
}
```

#### create database

```
create database wejhplatform;
use wejhplatform;
```

### 登录模块

#### models

```
{
    "name": "usercredit",
    "table":{
        "id": "int not null AUTO_INCREMENT",
        //
        "username":"text not null",
        "nickname":"text not null",
        "password":"text not null",
        "usertype":"text not null",//COMMON,TEST,WEJH
        "web_credit":"text",
        "mobile_credit":"text",
        "pc_credit":"text"
    },
    "primarykey":"id"
}
```

#### create table

mysql

```
create table usercredit(
    id int not null AUTO_INCREMENT,
    username text not null,
    nickname text not null,
    password text not null,
    usertype text not null,
    web_credit text,
    mobile_credit text,
    pc_credit text,
    PRIMARY KEY (id)
);
```

### 用户信息模块

#### models

```
{
    "name":"userinfo",
    "table":
    {
        "id":"int not null AUTO_INCREMENT",
        //credit
        "username":"text not null",
        "jhpid":"text",
        "pwbind_jh":"text",
        "state_jh":"int",
        //pwbinds
        "pwbind_lib":"text",
        "state_lib":"int",
        "pwbind_card":"text",
        "state_card":"int",
        "pwbind_ycedu":"text",
        "state_ycedu":"int",
        "pwbind_zfedu":"text",
        "state_zfedu":"int",
        //infos
        "portrait":"text",//用户头像
        "email":"text",
        "phone":"text",
        "linkedcourse":"text", //链接键,用|分割. $based list<string>
    }
}
```

#### create table

mysql

```
create table userinfo(
    id int not null AUTO_INCREMENT,
    username text not null,
    jhpid text not null,
    pwbind_jh text not null,
    state_jh int not null,
    pwbind_lib text,
    state_lib int not null,
    pwbind_card text,
    state_card int not null,
    pwbind_ycedu text,
    state_ycedu int not null,
    pwbind_zfedu text,
    state_zfedu int not null,
    portrait text not null,
    email text,
    phone text,
    linkedcourse text,
    PRIMARY KEY (id)
);
```

### 教务系统模块

#### models
```json
{
    "name":"course",
    "table":
    {
        "id":"int not null AUTO_INCREMENT",
        //三大查询标识
        "courseid":"text not null", //课程的id
        "year":"int not null", //上课学年
        "term":"int not null", //上课学期(3为上学期，12为下学期，16为下学期)
        "name":"text",//课程名称
        "college":"text", //开课学院
        "type":"text",
        "teacher": "text",//教师名称
        "campus":"text", //校区名称
        "location":"text", //地点
        "weekrange":"text",//上课周数{1-16}表示第1~16周
        "dayofweek":"text", //星期几{0=Sunday,1=Monday...}
        "timerange":"text",//时间{1-3}表示第1~3节
        "classscore":"int", //学分
        "classhour":"int" //学时
    }
}
```

##### create table

```
create table course(
    id int not null AUTO_INCREMENT,
    courseid text not null,
    year int not null,
    term int not null,
    name text,
    college text,
    type text,
    teacher text,
    campus text,
    location text,
    weekrange text,
    dayofweek text,
    timerange text,
    classscore int,
    classhour int,
    PRIMARY KEY (id)
);
```

courseid生成方式

year + term + name + location + weekrange + dayofweek + timerange 取hashcode