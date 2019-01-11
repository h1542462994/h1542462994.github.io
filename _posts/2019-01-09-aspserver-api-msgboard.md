---
layout: post
title: "[Project]tty全平台后端(正在开发)-API文档-留言板"
create: 2019-01-09
update: 2019-01-10
categories: blog
tags: [Project]
description: ""
---

## API文档-留言板

> 当前服务器地址`http://39.108.120.239`

-------

[主页](https://h1542462994.github.io/blog/2018/12/23/aspserver-index/)    [项目地址](https://github.com/TropicalTeamYard/tty.platform.aspserver)<br/>
`API系列` [API文档-用户部分](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/)  [API文档-留言板](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/)   [API文档-微精弘](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-wejh/)<br/>
`工程与部署` [MySql文档](https://h1542462994.github.io/blog/2018/12/23/aspserver-mysql/)  [部署](https://h1542462994.github.io/blog/2018/12/23/aspserver-deploy/)<br/>
`杂项` [&数据(调试用)](https://h1542462994.github.io/blog/2018/12/23/aspserver-data/)    [第三方提供的API](https://h1542462994.github.io/blog/2018/12/23/aspserver-providedapi/)<br/>
`日志` [更新日志](https://h1542462994.github.io/blog/2019/01/09/aspserver-updatelog/)<br/>
`想法&开发者提示` [留言板](https://h1542462994.github.io/blog/2019/01/03/aspserver-msgboard/)    [开发规范](https://h1542462994.github.io/blog/2019/01/11/aspserver-regular/)  

-------

#### 快速查询

[`留言板`](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/#留言板)  [添加留言](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/#添加留言)    [添加评论](#添加评论)  [更新](#更新)

-------

### 留言板

#### 地址

```
$root/api/msgboard
```

#### 参数
```csharp
"method":enum //add,addcomment,update
"credit":string //用户凭证
"id":int? //请求id,int?表示该值可为空
"time":string //时间
"content":string //请求数据
"pic":byte[] //图片数据
```

#### 添加留言

> 当method=`add`时跳转到此方法

需要提供的字段:`method`,`credit`,`content`,`pic`[可选]

样例请求:
```
url:http://39.108.120.239/api/msgboard
data:method=add&credit=43c1ce34f16240b0ad92e507065e2ac9&content=helloworld
```
返回状态码及消息:

| code | msg |
| :---: | --- |
| 400 | 无效的请求 |
| 403 | 凭证为空 |
| 403 | 无效的凭证 |
| 403 | 留言内容为空 |
| 200 | 添加留言成功 |

成功返回数据

```csharp
{
	"code": 200,
	"msg": "添加成功",
	"data": {
		"time": "2019/1/10 9:22:24",
		"msg": {
			"id": 16,
			"username": "10086",
			"time": "2019/1/10 9:22:24",
			"istop": 0,
			"islocked": 0,
			"content": "helloworld",
			"pic": null,
			"comments": []
		}
	}
}
```

#### 添加评论

> 当method=`addcomment`时跳转到此方法

需要提供的字段:`method`,`credit`,`id`,`content`

> `id`表示被添加的留言的id.

样例请求:
```
url:http://39.108.120.239/api/msgboard
data:method=addcomment&credit=43c1ce34f16240b0ad92e507065e2ac9&id=1&content=haha
```
返回状态码及消息:

| code | msg |
| :---: | --- |
| 400 | 无效的请求 |
| 403 | 凭证为空 |
| 403 | 无效的凭证 |
| 403 | 评论内容为空 |
| 200 | 添加评论成功 |

成功返回数据

```csharp
{
	"code": 200,
	"msg": "添加评论成功",
	"data": {
		"id": 2,
		"username": "10086",
		"time": "2019/1/8 15:13:04",
		"istop": 0,
		"islocked": 0,
		"content": "helloworld",
		"pic": null,
		"comments": [{
			"id": 1,
			"username": "10086",
			"time": "2019/1/10 12:50:56",
			"content": "haha"
		}, {
			"id": 2,
			"username": "10086",
			"time": "2019/1/10 12:51:06",
			"content": "haha"
		}, {
			"id": 3,
			"username": "10086",
			"time": "2019/1/10 12:51:18",
			"content": "haha"
		}]
	}
}
```

#### 更新

> 当method=`update`时跳转到此方法

需要提供的字段:`method`,`credit`,`time`

> 因缓存原因，只在最后200条记录中查询

> *mark:* `time`表示最后一次更新的时间，而不是当前的时间。

样例请求:

```
url:http://39.108.120.239/api/msgboard
data:method=update&credit=43c1ce34f16240b0ad92e507065e2ac9&time=2018/07/07%2014:00:00
```

返回状态码及消息:

| code | msg |
| :---: | --- |
| 400 | 无效的请求 |
| 403 | 凭证为空 |
| 403 | 无效的凭证 |
| 403 | 时间格式不正确 |
| 200 | 获取留言成功 |

成功返回数据

```csharp
{
	"code": 200,
	"msg": "获取留言成功",
	"data": {
		"time": "2019/1/11 23:41:44",
		"content": [{
			"id": 3,
			"username": "10086",
			"time": "2019/1/8 15:13:05",
			"istop": 0,
			"islocked": 0,
			"content": "helloworld",
			"pic": null,
			"comments": []
		}, {
			"id": 2,
			"username": "10086",
			"time": "2019/1/8 15:13:04",
			"istop": 0,
			"islocked": 0,
			"content": "helloworld",
			"pic": null,
			"comments": [{
				"id": 1,
				"username": "10086",
				"time": "2019/1/10 12:50:56",
				"content": "haha"
			}, {
				"id": 2,
				"username": "10086",
				"time": "2019/1/10 12:51:06",
				"content": "haha"
			}, {
				"id": 3,
				"username": "10086",
				"time": "2019/1/10 12:51:18",
				"content": "haha"
			}]
		}]
	}
}
```