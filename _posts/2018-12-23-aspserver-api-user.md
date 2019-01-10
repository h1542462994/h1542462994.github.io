---
layout: post
title: "[Project]tty全平台后端(正在开发)-API文档-用户部分"
create: 2018-12-23
update: 2019-01-10
categories: blog
tags: [Project]
description: ""
---

## API文档

> 当前服务器地址`http://39.108.120.239`

-------

#### 系列文档

[主页](https://h1542462994.github.io/blog/2018/12/23/aspserver-index/)    [项目地址](https://github.com/TropicalTeamYard/tty.platform.aspserver)

`API系列` [API文档-用户部分](https://h1542462994.github.io/blog/2018/12/23/aspserver-api-user/)  [API文档-留言板](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-msgboard/)   [API文档-微精弘](https://h1542462994.github.io/blog/2019/01/09/aspserver-api-wejh/)

`工程与部署` [MySql文档](https://h1542462994.github.io/blog/2018/12/23/aspserver-mysql/)  [部署](https://h1542462994.github.io/blog/2018/12/23/aspserver-deploy/)

`杂项` [&数据(调试用)](https://h1542462994.github.io/blog/2018/12/23/aspserver-data/)   [第三方提供的API](https://h1542462994.github.io/blog/2018/12/23/aspserver-providedapi/)


`日志` [更新日志](https://h1542462994.github.io/blog/2019/01/09/aspserver-updatelog/)

`想法&开发者提示` [留言板](https://h1542462994.github.io/blog/2019/01/03/aspserver-msgboard/)

-------

#### 快速查询

[`用户凭证`](#第一部分用户凭证部分)  

> [&注册(准备弃用)](#注册)    [注册2](#注册2)   [登录](#登录)  [自动登录](#自动登录)  [修改密码](#修改密码)    [修改昵称](#修改昵称)    [&微精弘快速绑定及登录](#微精弘快速绑定及登录)

[`用户信息`](#第二部分用户信息部分)

> [`绑定`](#21绑定)  [精弘_jh](#精弘_jh)    [正方教务_zfedu](#正方教务_zfedu)

> [`获取用户信息`](#22获取用户信息)    [绑定信息](#绑定信息)  [用户基础信息](#用户基础信息)


> [`获取公共信息`](#23获取公共信息)   [用户公共信息](#用户公共信息)

> [`设置用户信息`](#24设置用户信息)

-------

### 第一部分：用户凭证部分 

> `GET`方法已禁止，必须使用`POST`方法。

#### 地址

```csharp
$root/api/user
```

#### 参数

```csharp
method:enum //register,wejhlogin,login,autologin,changepw,changenickname
username:string
password:string
nickname:string
devicetype:enum //web,mobile,pc
newpassword:string
credit:string
```

> devicetype 必须指定为`mobile`或`pc`或`web`否则将无法正常访问。

#### 注册

> *waring:* 该接口准备弃用。

> 当method=`register`跳转至此方法。

需要提供的字段

`method`,`username`,`password`,`nickname`

样例请求

```
url:http://39.108.120.239/api/user
data:method=register&username=test1&password=123456&nickname=test1
```

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

#### 注册2

> 当method=`register2`时跳转到此方法。

需要提供的字段

`method`,`password`,`nickname`

样例请求

```
url:http://39.108.120.239/api/user
data:method=register2&password=E10ADC3949BA59ABBE56E057F20F883E&nickname=test1
```

> 密码请求时需要经过MD5加密，否则无法通过密码验证。

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

```
url:http://39.108.120.239/api/user
data:method=login&username=10086&password=E10ADC3949BA59ABBE56E057F20F883E&devicetype=mobile
```

> 只有当`devicetype`为`pc`、`web`或`mobile`时才能成功登录，当前进度下`web`暂不开放。

> 密码请求时需要经过MD5加密，否则无法通过密码验证。

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

样例请求

```
url:http://39.108.120.239/api/user
data:method=autologin&credit=118fad6b0d19442b94924ead72e01bdf
```

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

样例请求

```
url:http://39.108.120.239/api/user
data:method=changepw&username=10086&password=E10ADC3949BA59ABBE56E057F20F883E&newpassword=E10ADC3949BA59ABBE56E057F20F883E
```

> 密码请求时需要经过MD5加密，否则无法通过密码验证。

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

> *waring:* 该方法准备最近弃用，届时将合并到到`userinfo.setinfo`方法。

需要提供的字段

`method`,`credit`,`nickname`

样例请求

```
url:http://39.108.120.239/api/user
data:method=changenickname&credit=118fad6b0d19442b94924ead72e01bdf&nickname=test2
```

返回状态码及消息

| code | msg |
| :---: | --- |
| 400 | 无效的访问 |
| 403 | 用户凭证或昵称为空 |
| 403 | 自动登录已失效，请重新登录 |
| 200 | 修改昵称成功 |

#### 微精弘快速绑定及登录

> 当method=`wejhlogin`时跳转到此方法

> *waring:* 因接口分离导致的复杂性，准备将其弃用，并合并到`login`方法.

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


### 第二部分：用户信息部分

### 2.1绑定

#### 地址

```
$root/api/bind
```

#### 参数

```csharp
credit:string
bindname:enum //jh:精弘账号,lib:图书馆,card:校园卡,ycedu:原创教务,zfedu:正方教务.
password:string
pid:string//可选
```

> 已完成的部分:`jh`,`zfedu`

#### 精弘_jh

> 当bindname=`jh`时跳转到此方法

需要提供的字段

`credit`,`bindname`,`password`,`pid`

> 在这里，pid指学号。

样例请求

```
url:http://39.108.120.239/api/bind
data:bindname=jh&credit=118fad6b0d19442b94924ead72e01bdf&password=123456&pid=201806061777
```

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

#### 正方教务_zfedu

> 需要依赖`jh`，当bindname=`zfedu`时跳转到此方法

需要提供的字段

`credit`,`bindname`,`password`

样例请求

```
url:http://39.108.120.239/api/bind
data:bindname=zfedu&credit=118fad6b0d19442b94924ead72e01bdf&password=123456
```

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

### 2.2获取用户信息

#### 地址

```
$root/api/getinfo
```

#### 参数

```csharp
credit:string
type:enum //bind,base
```

#### 绑定信息

> 当type=`bind`时跳转到此方法

需要提供的字段: `type`,`credit`

样例请求:

```
url:http://39.108.120.239/api/getinfo
data:type=bind&credit=43c1ce34f16240b0ad92e507065e2ac9
```

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
	]
}
```

#### 用户基础信息

> 当type=`base`时跳转到此方法

需要提供的字段: `type`,`credit`

样例请求:

```
url:http://39.108.120.239/api/getinfo
data:type=base&credit=43c1ce34f16240b0ad92e507065e2ac9
```

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
	"code": 200,
	"msg": "获取成功",
	"data": {
		"username": "10086",
		"nickname": "test1",
		"usertype": "COMMON",
		"portrait": "default::unset",
		"email": "",
		"phone": ""
	}
}
```

> 当`portrait`为`default::unset`时，表示其没有设置头像，设置头像后，返回一串Base64十六进制字符串。

### 2.3获取公共信息

#### 地址

```
$root/api/shared
```

#### 参数

```csharp
type:enum,//user
query:string
```

#### 用户公共信息

> 当type=`user`时跳转到此方法

样例请求

```
url:http://39.108.120.239/api/shared
data:type=user&query=test1
```

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
	"data":{
		"username":"10086",
		"nickname":"test1",
		"usertype":"COMMON","portrait":"default::unset","premission_msgboard":0
	}
}
```

> 这是用户公开的信息，这个和`user.getinfo::base`会少一些字段。

> 当`portrait`为`default::unset`时，表示其没有设置头像，设置头像后，返回一串Base64十六进制字符串。

#### 用户公共信息MD5

> 当type=`usermd5`时跳转到此方法

样例请求

```
url:http://39.108.120.239/api/shared
data:type=usermd5&query=test1
```

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
	"data":"1B3E45BE5A40AA2881C8D309C41A95C7"
}
	
```

> 这是用户公开的信息，这个和`user.getinfo::base`会少一些字段。

> 当`portrait`为`default::unset`时，表示其没有设置头像，设置头像后，返回一串Base64十六进制字符串。

#### 获取时间

> 此结构只开放`GET`方法

> *waring:* 该方法最近将合并到`api.shared::time`。

地址

```
$root/api/time
```

样例请求

```
url:http://39.108.120.239/api/time
```

返回

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

#### 2.4设置用户信息

地址

```
$root/api/setinfo
```

参数

```csharp
credit:string,
email:string, //可选参数
portrait:string, //可选参数
phone:string //可选参数
```

样例请求

```
url:http://39.108.120.239/api/setinfo
data:credit=118fad6b0d19442b94924ead72e01bdf&email=lalala@cht. com&portrait=AESD532YND632...&phone=1111111111
```

返回

```json
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

> 在这里返回数据若为`2`表示修改成功，若为`1`表示修改失败，若为`0`表示未修改。