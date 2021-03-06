---
layout: post
title: "[Project]tty全平台后端(正在开发)-第三方提供的API"
create: 2018-12-23
update: 2018-12-23
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

## 需要使用的api及其说明

------

### 1.精弘用户中心

> 该接口使用`get`来请求。

#### 地址

```json
{
    "jh.user":"http://user.jh.zjut.edu.cn/api.php"
}
```

#### 登录

```json
{
    "app":"passport",
    "action":"login",
    "passport":"$username",
    "password":"$password"
}
```

返回数据

错误1（未注册）

```json
{
    "state":"error",
    "info":"通行证（学号）不存在或者未注册，如未注册，请注册后重新登陆"
}
```

成功

```json
{
    "state":"success",
    "info":"登录成功",
    "data":{
        "pid":"201806061201",
        "email":"t1542462994@outlook.com",
        "currentUidCount":"0",
        "availableUidCount":"3",
        "lastLoginTime":"1544883861",
        "lastLoginIP":"10.128.69.69",
        "activeTime":"1534913073",
        "activeIP":"172.16.9.101",
        "type":"1",
        "zjutmail":null
    }
}
```

### 2.微信端微精弘后台

#### 登录

> 该接口使用`get`来请求。

```json
{

}
```

成功

```json
{
	"errcode": 200,
	"errmsg": "登陆成功",
	"data": {
		"user": {
			"uno": "201806061201",
			"ext": {
				"school_info": {
					"name": null,
					"gender": 0,
					"grade": null,
					"college": null,
					"major": null,
					"class": null
				},
				"wechat_info": {
					"avatar": null,
					"nickname": null,
					"subscribe": false
				},
				"terms": {
					"score_term": "2017\/2018(1)",
					"class_term": "2017\/2018(1)",
					"exam_term": "2017\/2018(1)"
				},
				"passwords_bind": {
					"jh_password": 1,
					"card_password": 1,
					"lib_password": 1,
					"yc_password": 0,
					"zf_password": 0
				}
			},
			"updated_at": "2018-12-11 06:05:33",
			"created_at": "2018-12-11 06:05:33",
			"id": 45
		},
		"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjQ1LCJpc3MiOiJodHRwczovL3Rlc3Quc2VydmVyLndlamguaW1jci5tZS9hcGkvbG9naW4iLCJpYXQiOjE1NDQ1MDgzMzMsImV4cCI6MTU0NDU5NDczMywibmJmIjoxNTQ0NTA4MzMzLCJqdGkiOiI5TEVSVXdMWUFuOEt6RjlJIn0.wkjz4MpQDd-RcXmNpaEC7cM6LA0Pdr71OdPgB46QRY8"
	},
	"redirect": null
}
```

#### 获取时间

##### 地址

https://server.wejh.imcr.me/api/time

成功

```json
{
	"errcode": 1,
	"errmsg": "获取时间成功",
	"data": {
		"term": "2018\/2019(1)",
		"month": "12",
		"week": 13,
		"day": 4,
		"is_begin": true
	},
	"redirect": null
}
```

### 3.正方教务系统

> 该接口使用`get`来请求。

### 查询课表

#### 地址

http://api.jh.zjut.edu.cn/student/classZf.php

#### 入参

```csharp
{
    "username":"$username", //学号
    "password":"$password", //密码
    "year":"$year", //学年(2017)
    "term":"$term", //学期(3为上学期，12为下学期，16为短学期)
}
```

失败

```csharp
{
	"status": "error",
	"msg": "参数错误"
}
```

```csharp
{
	"status": "error",
	"msg": "用户名或密码错误"
}
```

成功

```csharp
{
	"status": "success",
	"msg": [{
		"cd_id": "19832", //课程id
		"cdmc": "教404", //上课教室(场地名称？)
		"jc": "1-2节",  
		"jcor": "1-2", //第几节上课
		"jcs": "1-2",
		"jgh_id": "1166",
		"jgpxzd": "1",
		"jxb_id": "6CDD0B1E70ED68EBE053A11310AC0090", //教学班id
		"jxbmc": "线性代数-0010", //教学班名称
		"kch_id": "101", 
		"kcmc": "线性代数", //课程名称
		"khfsmc": "考查", //考核方式名称
		"listnav": "false",
		"localeKey": "zh_CN",
		"oldjc": "3",
		"oldzc": "65535",
		"pageable": true,
		"pkbj": "1",
		"rangeable": true,
		"rsdzjs": 0,
		"sxbj": "1",
		"totalResult": "0",
		"xm": "金建国", //教师姓名
		"xnm": "2018", //学年名
		"xqdm": "0",
		"xqh_id": "01",
		"xqj": "1",
		"xqjmc": "星期一",//星期几
		"xqm": "3",
		"xqmc": "朝晖校区",//校区名称
		"xsdm": "01",
		"xslxbj": "◆",
		"zcd": "1-16周",
		"zcmc": "副教授",
		"zyfxmc": "无方向",
        //这些字段是后来开发者为了方便理解添加的字段
		"name": "线性代数:金建国", //课程名称
		"collage": "", //开课学院 *谁把college拼错了?
		"classinfo": "1-16周:星期1(1-2) 教404;", //课程信息
		"classtype": "考查", //课程类型"未安排"/"考查"/"考试"
		"classscore": 2,//学分
		"classhuor": 32//学时 *谁把hour拼错了?
    }]
}
```

### 查询成绩

#### 地址

http://api.jh.zjut.edu.cn/student/scoresZf.php

#### 参数

```csharp
username=201312341234 //[学号]
password=xxxxx //[密码]
year=2017 //[学年]
term=3 //[学期, 3为上学期，12为下学期, 16为短学期]
```

#### 结果

成功

```csharp
{
    "status": "success",
    "msg": [
        {
            "bh_id": "081201452007", 
            "bj": "中文1403", //班级
            "cj": "92", //成绩
            "cjsfzf": "否",
            "jg_id": "08",
            "jgmc": "人文学院",
            "jgpxzd": "1",
            "jsxm": "方爱武", //教师姓名
            "jxb_id": "158685",
            "jxbmc": "158685",
            "kcbj": "主修",
            "kch": "G108136",
            "kch_id": "22342",
            "kcmc": "台港澳暨海外华文文学", //课程名称
            "kkbmmc": "人文学院",
            "ksxz": "正常考试",
            "listnav": "false",
            "localeKey": "zh_CN",
            "njdm_id": "2014",
            "njmc": "2014",
            "pageable": true,
            "rangeable": true,
            "row_id": "1",
            "sfxwkc": "否",
            "totalResult": "6",
            "xb": "女",
            "xbm": "2",
            "xf": "2", //学分
            "xh": "201400000123",
            "xh_id": "927126",
            "xm": "姓名",
            "xnm": "2016",
            "xnmmc": "2016-2017",
            "xqm": "12",
            "xqmmc": "2",
            "zyh_id": "520",
            "zymc": "中国语言文学类",
            "term": "2016/2017(2)",
            "name": "台港澳暨海外华文文学",
            "classprop": "主修",
            "classscore": "92",
            "classhuor": "92",
            "classcredit": 32
        },
        {
            "bh_id": "081201452007",
            "bj": "中文1403",
            "cj": "92",
            "cjsfzf": "否",
            "jg_id": "08",
            "jgmc": "人文学院",
            "jgpxzd": "1",
            "jsxm": "褚蓓娟",
            "jxb_id": "158624",
            "jxbmc": "158624",
            "kcbj": "主修",
            "kch": "G108142",
            "kch_id": "16027",
            "kcmc": "外国文学Ⅱ",
            "kkbmmc": "人文学院",
            "ksxz": "正常考试",
            "listnav": "false",
            "localeKey": "zh_CN",
            "njdm_id": "2014",
            "njmc": "2014",
            "pageable": true,
            "rangeable": true,
            "row_id": "2",
            "sfxwkc": "否",
            "totalResult": "6",
            "xb": "女",
            "xbm": "2",
            "xf": "2.5",
            "xh": "201400000123",
            "xh_id": "927126",
            "xm": "姓名",
            "xnm": "2016",
            "xnmmc": "2016-2017",
            "xqm": "12",
            "xqmmc": "2",
            "zyh_id": "520",
            "zymc": "中国语言文学类",
            "term": "2016/2017(2)",
            "name": "外国文学Ⅱ",
            "classprop": "主修",
            "classscore": "92",
            "classhuor": "92",
            "classcredit": 40
        },
        // ...
    ]
}
```