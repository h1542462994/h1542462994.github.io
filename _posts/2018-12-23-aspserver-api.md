---
layout: post
title: "[Project]微精弘全平台后端(正在开发)-API文档"
create: 2018-12-23
update: 2018-12-23
categories: children
tags: [Project]
description: ""
---

## API文档

> 当前服务器地址`http://39.108.120.239`

### 第一部分：用户凭证部分 

> `GET`方法已禁止，必须使用`POST`方法。

#### 地址

```csharp
${root}/api/user
```

#### 参数

```csharp
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

#### 注册【需要提供用户名的版本】

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

```csharp
{
    "code":200,
    "msg":"注册账号成功。",
}
```

#### 注册【快速版本】

> 当method=`register2`时跳转到此方法。

需要提供的字段

`method`,`password`,`nickname`

样例请求

`url`:http://39.108.120.239/api/user

`data`:method=register2&password=123456&nickname=test1

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问。 |
| 403 | 密码/昵称为空 | //prepared to update.
| 403 | 密码太长或太短 |
| 200 | 注册账户成功 |

输入检查

2.密码：长度在6~20位。
3.昵称：长度在2~15位。

成功返回数据

```csharp
{
	"code":200,
	"msg":"注册账户成功",
	"data":
	{
		"username":"10086",
		"nickname":"test1",
		"usertype":"COMMON"
	}
}
```

#### 登录

> 当method=`login`时跳转到此方法

需要提供的字段
`method`,`username`,`password`,`devicetype`

样例请求

`url`:http://39.108.120.239/api/user

`data`:method=login&username=10086&password=123456&devicetype=mobile

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

成功返回数据

```csharp
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
| 403 | 自动登录已失效，请重新登录 |
| 200 | 自动登录成功 |

> 自动登录后，原来的`credit`会失效，这是为了提高安全性。

成功返回数据

```csharp
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
| 403 | 该用户不存在 |
| 403 | 微精弘用户不能修改密码 |
| 403 | 密码错误 |
| 200 | 修改密码成功，请重新登录 |

> 修改密码后，所有自动登录都会失效，请不要忘记重新登录。

成功返回数据

```csharp
{
	"code":200,
	"msg":"修改密码成功，请重新登录"
}
```

#### 修改昵称

> 当method=`changenickname`时跳转到此方法

需要提供的字段

`method`,`credit`,`nickname`

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 用户凭证或昵称为空 |
| 403 | 自动登录已失效，请重新登录 |
| 200 | 修改昵称成功 |

#### *微精弘快速绑定及登录[准备弃用]

> 当method=`wejhlogin`时跳转到此方法

需要提供的字段

`method`,`username`,`password`,`devicetype`

> devicetype必须为`web`、`mobile`或`pc`中的一个，否则无法登录

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 用户名、密码或昵称为空 |
| 403 | 设备类型不符合 |
| 403 | 该用户不存在 |
| 403 | 用户密码错误 |
| 403 | 登录成功 |

成功返回数据

```csharp
{
	"code":200,
	"msg":"登录成功",
	"data":{
		"username":"201806061201",
		"nickname":"wejh",
		"credit":"4d393794e3214655b19b6a85ec177f59",
		"usertype":"WEJH"
	}
}
```

--------------

======这是可爱的分割线。======

### 第二部分：用户信息部分

### 2.1绑定信息

#### 地址

```
${root}/api/bind
```

#### 参数

```csharp
{
    "credit":"$credit",
    "bindname":"$bindname", //jh:精弘账号,lib:图书馆,card:校园卡,ycedu:原创教务,zfedu:正方教务.
    "password":"$password",
	"pid":"$pid"//可选
}
```

> 已完成的部分:`jh`,`zfedu`

#### 精弘(jh)

> 当bindname=`jh`时跳转到此方法

需要提供的字段

`credit`,`bindname`,`password`,`pid`

> 在这里，pid指学号。

返回状态码及消息。

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 自动登录已失效，请重新登录 |
| 403 | 学号或密码为空 |
| 403 | #upper::未注册账户 |
| 403 | #upper::绑定精弘账号失败 |
| 403 | #upper::绑定精弘账号成功 |

> `#upper::`表示需要依赖上级服务器。

成功返回信息

```csharp
{
    "code":200,
    "msg":"绑定精弘账号成功" 
}
```

#### 正方教务(zfedu)

> 需要依赖`jh`，当bindname=`zfedu`时跳转到此方法

需要提供的字段

`credit`,`bindname`,`password`

返回状态码及消息。

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 你还没有绑定精弘账号 |
| 403 | #upper::请重新绑定精弘账号 |
| 403 | 密码为空 |
| 403 | #upper::绑定正方失败 |
| 200 | #upper::绑定正方成功 |

成功返回信息

```csharp
{
	"code":200,
	"msg":"绑定正方成功"
}
```

-------------

======这是可爱的分割线======

### 2.2获取信息(指用户信息)

#### 地址

```
${root}/api/getinfo
```

#### 参数

```csharp
{
	"credit":"$credit",
	"type":"$type"//bind
}
```

#### 绑定信息

> 当type=`bind`时跳转到此方法

样例请求:

`url`:http://39.108.120.239/api/getinfo

`data`:type=bind&credit=43c1ce34f16240b0ad92e507065e2ac9

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 自动登录已失效，请重新登录 |
| 403 | 不存在该类型信息 |
| 200 | 获取成功 |

成功返回数据

```csharp
{
	"code":200,
	"msg":"获取成功",
	"data":[{
		"bindname":"jh",
		"pid":"201806061201","state":2
		},{
		"bindname":"lib",
		"pid":null,"state":0
		},{
		"bindname":"zfedu",
		"pid":null,"state":0
		},{
		"bindname":"ycedu",
		"pid":null,
		"state":0
		},{
		"bindname":"card",
		"pid":null,
		"state":0}
		]}
```

### 2.3公共信息

#### 地址

```
${root}/api/shared
```

#### 参数

```csharp
{
	"type":"$type",//user
	"query":"$query"
}
```

#### 用户信息[用户名，昵称，用户类型，用户头像]

> 当type=`user`时跳转到此方法

样例请求

`url`:http://39.108.120.239/api/shared

`data`:type=user&query=test1

> 在这里`query`指代查询用户的用户名。

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 不存在该用户 |
| 200 | 获取信息成功 |

成功返回数据

```csharp
{
	"code":200,
	"msg":"获取信息成功",
	"data":
	{
		"username":"test1",
		"nickname":"test1",
		"usertype":"COMMON","portrait":"FFD8FFE00010..."
	}
}
```

#### 获取时间

> `GET`和`POST`方法都可以。

##### 地址

```
${root}/api/time
```

##### 返回

```csharp
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

```csharp
{
    "credit":"$credit"
}
```

> 获取课表是按照服务器时间来获取的，而服务器时间可有`api/time`来获取。

##### 返回

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
