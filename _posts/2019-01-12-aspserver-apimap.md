---
layout: post
title: "[Project]tty全平台后端(正在开发)-API映射表"
create: 2019-01-12
update: 2019-01-12
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

### 用户凭证

#### 注册

```
url:http://39.108.120.239/api/user
data:method=register&username=test1&password=123456&nickname=test1
```

```csharp
{
    "code":200,
    "msg":"注册账号成功。",
}
```

#### 注册2

```
url:http://39.108.120.239/api/user
data:method=register2&password=E10ADC3949BA59ABBE56E057F20F883E&nickname=test1
```

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

```
url:http://39.108.120.239/api/user
data:method=login&username=10086&password=E10ADC3949BA59ABBE56E057F20F883E&devicetype=mobile
```

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

```
url:http://39.108.120.239/api/user
data:method=autologin&credit=118fad6b0d19442b94924ead72e01bdf
```

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

```
url:http://39.108.120.239/api/user
data:method=changepw&username=10086&password=E10ADC3949BA59ABBE56E057F20F883E&newpassword=E10ADC3949BA59ABBE56E057F20F883E
```

```csharp
{
	"code":200,
	"msg":"修改密码成功，请重新登录"
}
```

#### 修改昵称

```
url:http://39.108.120.239/api/user
data:method=changenickname&credit=118fad6b0d19442b94924ead72e01bdf&nickname=test2
```

```csharp
{
	"code":200,
	"msg":"修改昵称成功"
}
```

#### 微精弘快速绑定及登录

> 已弃用

### 用户信息

### 2.2获取用户信息

```
url:http://39.108.120.239/api/getinfo
data:type=bind&credit=43c1ce34f16240b0ad92e507065e2ac9
```

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
	]
}
```

#### 用户基础信息

```
url:http://39.108.120.239/api/getinfo
data:type=base&credit=43c1ce34f16240b0ad92e507065e2ac9
```

```csharp
{
	"code": 200,
	"msg": "获取成功",
	"data": {
		"username": "10086",
		"nickname": "test1",
		"usertype": "COMMON",
		"portrait": "default::unset",
		"email": "",
		"phone": ""
        "permission_msgboard":0
	}
}
```

### 2.3获取公共信息

#### 用户公共信息

```
url:http://39.108.120.239/api/shared
data:type=user&query=test1
```

```csharp
{
	"code":200,
	"msg":"获取信息成功",
	"data":[{
		"username":"10086",
		"nickname":"test1",
		"usertype":"COMMON",
        "portrait":"default::unset",
	}]
}
```

#### 用户公共信息MD5

```
url:http://39.108.120.239/api/shared
data:type=usermd5&query=['10086','10087','10088']
```

```csharp
{
	"code":200,
	"msg":"获取信息成功",
	"data":[{
		"username":"10086","md5":"CCC8263BE1056CC88382FBD983E0B674"
		}]
	}
```

### 2.4设置用户信息

```
url:http://39.108.120.239/api/setinfo
data:credit=118fad6b0d19442b94924ead72e01bdf&email=lalala@cht. com&portrait=AESD532YND632...&phone=1111111111
```

```csharp
{
    "code":200,
    "msg":"修改信息成功",
    "data":{
		"e_email":2,
		"e_portrait":2,
		"e_phone":2
    }
}
```