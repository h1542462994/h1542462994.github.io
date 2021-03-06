---
layout: post
title: "[Project]tty全平台后端(正在开发)-API文档-微精弘"
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

## API文档-留言板

> 当前服务器地址`http://39.108.120.239`

#### 获取课表

参数

```csharp
{
    "credit":"$credit"
}
```

> 获取课表是按照服务器时间来获取的，而服务器时间可有`api/time`来获取。

返回

成功

```csharp
{
	"code": 200,
	"msg": "获取课表成功。",
	"data": [{
		"id": 0,
		"courseid": "19832",
		"year": 2018,
		"term": 3,
		"name": "线性代数",
		"college": "",
		"type": "考查",
		"teacher": "金建国",
		"campus": "朝晖校区",
		"location": "教404",
		"weekrange": "1-16",
		"dayofweek": "1",
		"timerange": "1-2",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "6D910A62D3DC31D9E053A11310ACD644",
		"year": 2018,
		"term": 3,
		"name": "大学英语",
		"college": "",
		"type": "考试",
		"teacher": "阮晓亮",
		"campus": "朝晖校区",
		"location": "文605",
		"weekrange": "1-16",
		"dayofweek": "1",
		"timerange": "3-4",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "19815",
		"year": 2018,
		"term": 3,
		"name": "高等数学Ⅰ",
		"college": "",
		"type": "考试",
		"teacher": "练晓鹏",
		"campus": "朝晖校区",
		"location": "教201",
		"weekrange": "1-16",
		"dayofweek": "1",
		"timerange": "6-7",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "19818",
		"year": 2018,
		"term": 3,
		"name": "程序设计基础C",
		"college": "",
		"type": "考试",
		"teacher": "潘清",
		"campus": "朝晖校区",
		"location": "教204",
		"weekrange": "1-16",
		"dayofweek": "2",
		"timerange": "1-2",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "19822",
		"year": 2018,
		"term": 3,
		"name": "人体健康与疾病",
		"college": "",
		"type": "未安排",
		"teacher": "陈艳",
		"campus": "朝晖校区",
		"location": "教301",
		"weekrange": "1-16",
		"dayofweek": "2",
		"timerange": "10-11",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "19832",
		"year": 2018,
		"term": 3,
		"name": "中国近现代史纲要",
		"college": "",
		"type": "考查",
		"teacher": "颜桂珍",
		"campus": "朝晖校区",
		"location": "教404",
		"weekrange": "1-16",
		"dayofweek": "3",
		"timerange": "1-2",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "19815",
		"year": 2018,
		"term": 3,
		"name": "高等数学Ⅰ",
		"college": "",
		"type": "考试",
		"teacher": "练晓鹏",
		"campus": "朝晖校区",
		"location": "教201",
		"weekrange": "1-16",
		"dayofweek": "3",
		"timerange": "3-4",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "6D910A62D3DC31D9E053A11310ACD644",
		"year": 2018,
		"term": 3,
		"name": "大学英语",
		"college": "",
		"type": "考试",
		"teacher": "阮晓亮",
		"campus": "朝晖校区",
		"location": "文605",
		"weekrange": "1-16",
		"dayofweek": "3",
		"timerange": "6-7",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "19827",
		"year": 2018,
		"term": 3,
		"name": "程序设计基础C",
		"college": "",
		"type": "考试",
		"teacher": "潘清",
		"campus": "朝晖校区",
		"location": "教307",
		"weekrange": "1-16",
		"dayofweek": "4",
		"timerange": "3-4",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": null,
		"year": 2018,
		"term": 3,
		"name": "体育",
		"college": "",
		"type": "未安排",
		"teacher": "王德明",
		"campus": "朝晖校区",
		"location": "未排地点",
		"weekrange": "1-16",
		"dayofweek": "4",
		"timerange": "6-7",
		"classscore": 2,
		"classhour": 32
	}, {
		"id": 0,
		"courseid": "19815",
		"year": 2018,
		"term": 3,
		"name": "高等数学Ⅰ",
		"college": "",
		"type": "考试",
		"teacher": "练晓鹏",
		"campus": "朝晖校区",
		"location": "教201",
		"weekrange": "1-8",
		"dayofweek": "5",
		"timerange": "6-7",
		"classscore": 2,
		"classhour": 32
	}]
}
```