---
layout: post
title: "[wejh]微精弘全平台后端(正在开发)-API文档"
create: 2018-12-23
update: 2018-12-23
categories: children
tags: [wejh]
description: ""
---

## API文档

> 当前服务器地址`http://39.108.120.239`

### 第一部分：用户凭证部分 

> `GET`方法已禁止，必须使用`POST`方法。

#### 地址

```
${root}/api/user
```

#### 参数

```
{
    "method":"$method:enum",//register,wejhlogin,login,autologin,changepw,changenickname
	"username":"$username:string",
	"password":"$password:string",
	"nickname":"$nickname:string",
	"devicetype":"$nickname:enum",//web,mobile,pc
	"newpassword":"$password:string",
	"credit":"$credit:string"
}
```

> devicetype 必须指定为`mobile`或`pc`或`web`否则将无法正常访问。

#### 注册

> 当method=`register`跳转至此方法。

需要提供的字段

`method`,`username`,`password`,`nickname`

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问。 |
| 403 | 用户名，密码，或者昵称为空。 |
| 403 | 用户名不符合命名规则，用户名应不包含英文特殊字符，长度在2~10位，且不能为纯数字。 |
| 403 | 密码太长或太短。 |
| 403 | 昵称不符合命名规则，昵称长度应该在2~12位。 |
| 403 | 该账号已存在。 |
| 200 | 注册账号成功。 |

> 通过此类型注册的账户账户类型始终为`common`。

输入检查

1.用户名：用户名长度需在2~10位，不能包括英文特殊字符，且不能为纯数字。
2.密码：长度在6~20位。
3.昵称：长度在2~15位。

成功返回数据

```
{
    "code":200,
    "msg":"注册账号成功。",
}
```

#### 登录

> 当method=`login`时跳转到此方法

需要提供的字段
`method`,`username`,`password`,`devicetype`

> 只有当`devicetype`为`pc`、`web`或`mobile`时才能成功登录，当前进度下`web`暂不开放。

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问。 |
| 403 | 设备类型不符合 |
| 403 | 用户名或密码为空 |
| 403 | 该用户不存在 |
| 403 | 用户密码错误 |
| 200 | 登录成功 |

```
{
	"code": 200,
	"msg": "登录成功",
	"data": {
		"username": "test1",
		"nickname": "test1",
		"credit": "e749e26edf7049448d3f555c83ad5a57",
		"usertype": "COMMON"
	}
}
```

#### 自动登录

> 当method=`autologin`时跳转到此方法

需要提供的字段

`method`,`credit`

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问。 |
| 403 | 用户凭证为空 |
| 200 | 自动登录已失效，请重新登录 |
| 402 | 自动登录失败。 |
| 403 | 自动登录已失效，请重新绑定账号。 |
| 200 | 自动登录成功 |

> 自动登录后，原来的`credit`会失效，这是为了提高安全性。

成功返回数据

```
{
    "code":200,
    "msg":"自动登录成功",
    "data":{
        "username":"test1",
        "usertype":"COMMON",
        "credit":"706637cb00ce4ab7a1c73014524d2847",
        "devicetype":"mobile"
    }
}
```

#### 修改密码

> 当method=`changpw`时跳转到此方法

需要提供的字段

`method`,`username`,`password`,`newpassword`

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 用户名，旧密码或新密码为空 |
| 402 | 该用户不存在 |
| 402 | 该用户不存在 |
| 200 | 修改密码成功 |

成功返回数据

```
{
	"code":200,
	"msg":""
}
```

--------------

这是可爱的分割线。

#### 绑定密码

##### 地址

```
${root}/api/pwbind
```

##### 参数
```
{
    "credit":"$credit",
    "bindname":"$bindname", //lib:图书馆,card:校园卡,ycedu:原创教务,zfedu:正方教务.
    "password":"$password",
}
```

```
{
    "code":200,
    "msg":"绑定%成功。" //zfedu:绑定正方成功。
}
```

> 当前只有正方教务的绑定，其他类型还在开发中。

#### 获取时间

> `GET`和`POST`方法都可以。

##### 地址

```
${root}/api/time
```

##### 返回

```
{
    "code":200,
    "msg":"获取时间成功",
    "data":{
        "year":2018,
        "term":3,//3为上学期，12为下学期，16为短学期。
        "begin":"2018-09-24",
        "end":"2019-01-27",
        "dayofweek":4,
        "week":13,
        "weeklasting":18
    }
}
```

#### 获取课表

##### 参数

```
{
    "credit":"$credit"
}
```

> 获取课表是按照服务器时间来获取的，而服务器时间可有`api/time`来获取。

##### 返回

成功

```
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