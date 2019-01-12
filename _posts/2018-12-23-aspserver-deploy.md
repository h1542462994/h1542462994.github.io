---
layout: post
title: "[Project]tty全平台后端(正在开发)-部署"
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

## 部署服务器

#### On Unbuntu 18.04

> *error:* 请跳过此部分内容，因为该项目开发者(cht)无法解决在linux系统上的部署问题。

注册Microsoft key和产品仓储

```bush
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
```

安装依赖项

```bush
sudo dpkg -i packages-microsoft-prod.deb
```

安装 .NET SDK

```bush
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1
```

验证SDK安装情况

```bush
dotnet --info
```

启动项目

```bush
dotnet ${name}.dll
```

安装代理服务器ngnix

```bush
sudo apt-get install nginx
vim /etc/ngnix/sites-available/default
```

编辑server
```vim
server{
    listen 80;
    server_name localhost;
    location /{
        proxy_pass ${location};
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Conncection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

安装守护进程

```
sudo apt-get install supervisor
```

修改配置

```
cd /etc/supervisor/conf.d/
touch ${name}.conf
vim text.conf
```

修改内容
```
[program:ShareYunSourse]   
command=dotnet ShareYunSourse.Web.dll 
directory=/usr/ShareYunSourse
environment=ASPNETCORE__ENVIRONMENT=Production
user=www-data 
stopsignal=INT
autostart=true 
autorestart=true 
startsecs=1
stderr_logfile=/usr/log/ShareYunSourse.err.log
stdout_logfile=/usr/log/ShareYunSourse.out.log
```

