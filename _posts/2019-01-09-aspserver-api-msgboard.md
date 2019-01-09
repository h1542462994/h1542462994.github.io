---
layout: post
title: "[Project]微精弘全平台后端(正在开发)-API文档-留言板"
create: 2019-01-09
update: 2019-01-09
categories: blog
tags: [Project]
description: ""
---

## API文档-留言板

> 当前服务器地址`http://39.108.120.239`

-------

#### 系列文档

[主页](https://h1542462994.github.io/blog/2018/12/23/aspserver-index/)

`API系列` [API文档-用户部分](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/)  [API文档-留言板](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/)   [API文档-微精弘](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-wejh/)

`工程与部署` [MySql文档](https://h1542462994.github.io/blog/2018/12/23/aspserver-mysql/)  [部署](https://h1542462994.github.io/blog/2018/12/23/aspserver-deploy/)

`杂项` [*数据(调试用)](https://h1542462994.github.io/blog/2018/12/23/aspserver-data/)

`日志` [更新日志](https://h1542462994.github.io/blog/2019/01/09/aspserver-updatelog/)

`想法&开发者提示` [留言板](https://h1542462994.github.io/blog/2019/01/03/aspserver-msgboard/)

-------

#### 快速查询

[`留言板`](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/#留言板)  [添加留言](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/#添加留言)

-------

### 留言板

#### 地址

```
${root}/api/msgboard
```

#### 参数
```csharp
{
	"method":"string"//add,remove,add-comment,remove-comment,update,getnew,getupdateid
	"credit":"string"//用户凭证
	"id":"int"//请求id
	"subid":"int"//副id
	"content":"string"//请求数据
	"pic":"byte[]"//图片数据
}
```

#### 添加留言

> 当method=`add`时跳转到此方法

需要提供的字段:`method`,`credit`,`content`,`pic`[可选]

样例请求:

`url`:http://39.108.120.239/api/msgboard

`data`:method=add&credit=43c1ce34f16240b0ad92e507065e2ac9&content=hello%32world

返回状态码及消息:

| code | msg |
| :---: | --- |
| 400 | 无效的请求 |

成功返回数据

```