---
layout: post
title: "[Markdown]基础篇：语法高亮预览"
date: 2018-12-08
categories: blog
tags: [Markdown]
description: "学习Markdown"
---

#### 摘要

一般来说，markdown编译器都支持主流编程语言和一些特殊语言的代码高亮。

想要知道代码高亮到底显示成什么样子？你可以从我的github上下载此文件，放到编辑器里，看一看代码高亮的情况，在这里，我将会测试基础的代码高亮语法。

#### 相关文章

入门篇：[开始学习markdown](https://h1542462994.github.io/blog/2018/12/08/learn-markdown1/)

基础篇：语法高亮预览

#### 相关测试

> 注意，三个反括号为了防止转义，我用`()`包起来了，但是并不影响阅读。

已测试：无格式，cpp(C++)，cs(C#)，css，html，js(javascript)，json，liquid，xml，math(LaTex)

---

##### 无格式

```
(```)
测试文本1
//测试文本2
/*测试文本3*/
(```)
```

显示效果
```
测试文本1
//测试文本2
/*测试文本3*/
```

---

##### cpp(C++)

```
(```cpp)
#include<iostream>

using namespace std;
int main()
{
	cout << "hello world!" << endl;
	return 0;
}
(```)
```

显示效果
```cpp
#include<iostream>

using namespace std;
int main()
{
	cout << "hello world!" << endl;
	return 0;
}
```

---

##### cs(C#)

```
(```cs)
using System;
namespace Demo1()
{
	public static class Program
	{
		static void Main()
		{
			Console.WriteLine("hello world!");
		}
	}
}
(```)
```

显示效果
```cs
using System;
namespace Demo1()
{
	public static class Program
	{
		static void Main()
		{
			Console.WriteLine("hello world!");
		}
	}
}
```

---

##### css

```
(```css)
.tags {
	margin-bottom: -5px;
}

.tags a,
.tags .tag
{
	dispaly: inline-block;
	border: 1px solid rgba(255,255,255,0.8)
	border-radius: 999em;
	padding: 0 10px;
	color: #ffffff;
	line-height: 24px;
	font-size: 12px;
	text-decoration: none;
	margin: 0 1px;
	margin-bottom: 6px;
}
(```)
```

显示效果
```css
.tags {
	margin-bottom: -5px;
}

.tags a,
.tags .tag
{
	dispaly: inline-block;
	border: 1px solid rgba(255,255,255,0.8)
	border-radius: 999em;
	padding: 0 10px;
	color: #ffffff;
	line-height: 24px;
	font-size: 12px;
	text-decoration: none;
	margin: 0 1px;
	margin-bottom: 6px;
}
```

---

##### html

```
(```html)
<span class="sr-only">Toggle navigation</span>
<span class="icon-bar"></span>
<span class="icon-bar"></span>
<span class="icon-bar"></span>
(```)
```

显示效果
```html
<span class="sr-only">Toggle navigation</span>
<span class="icon-bar"></span>
<span class="icon-bar"></span>
<span class="icon-bar"></span>
```

---

##### js(javascript)

```
(```js)
function printhello(){
	console.log('hello world!');
}
(```)
```

显示效果
```js
function printhello(){
	console.log('hello world!');
}
```

---

##### json

```
(```json)
{
	"name": "张三",
	"grade": 80,
	"values": {
		"height": 167
		"tag": "此人的标签"
	}
}
(```)
```

显示效果
```json
{
	"name": "张三",
	"grade": 80,
	"values": {
		"height": 167
		"tag": "此人的标签"
	}
}
```

---

{% raw %}
##### liquid

```
(```liquid)
{% for index in (1..5) %}
index={{ index }}
{% endfor %}
(```)
```

显示效果
```liquid
{% for index in (1..5) %}
index={{ index }}
{% endfor %}
```

{% endraw %}

---

##### xml

```
(```xml)
<?xml version="1.0" encoding="UTF-8"?>
<student>
	<name>张三</name>
	<grade>80</grade>
	<values>
		<height>167</height>
		<tag>此人的tag</tag>
	</values>
</student>
(```)
```

显示效果
```xml
<?xml version="1.0" encoding="UTF-8"?>
<student>
	<name>张三</name>
	<grade>80</grade>
	<values>
		<height>167</height>
		<tag>此人的tag</tag>
	</values>
</student>
```

##### math(LaTex)

```
(```math)
1.\int\sqrt\frac{1+x}{1-x}dx
(```)
```

> 当前网站无法显示数学公式。

显示效果
```math
1.\int\sqrt\frac{1+x}{1-x}dx
```