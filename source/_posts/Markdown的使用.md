---
title: Markdown的使用
tags:
  - Markdown
categories:
  - 博客
date: 2017-01-22 12:39:04
---

MarkDown语法比较简单，能够很轻松的学会，但如果搭配html的语法使用，能够实现更多复杂的效果。

### 标题

在文字前面添加#即可实现标题效果
`# 一级标题`
`## 二级标题`
`### 三级标题`
依此类推，总共可以创建六级标题

<!-- more -->

### 引用文字
在文字前添加>
> 这是一级引用
>>这是二级引用
>>> 这是三级引用

语法：
`> 这是一段引用。`

### 添加超连接

这是一个跳转到博客首页的连接[<font color=#0099ff>首页</font>](http://www.lieeber.com/ "我的首页")
语法：`[首页](http://www.lieeber.com/ "我的首页")`


### 添加图片

<img width="150" height="150" align=center src="http://www.lieeber.com/images/lieeber.jpg"/>

语法：
1. `![图片](https://mgpath/xxx.jpg)`
2. `<img width="150" height="150" align=center src="mgpath/xxx.jpg"/>`

第一种是使用的Markdown自带的添加语法，无法控制图片的大小和位置，第二种是html的语法，可以指定图片的大小和位置，不过对于Markdown语法，我们可以结合div来控制图片的位置。

```
<div align=center>
![图片](https://mgpath/xxx.jpg)
</div>
```

### 分割线
***
语法：`***`

### 列表

#### 无序列表
- one
- two
- three

语法：`在需要列表样式的文字前添加"-"或者"*"`

#### 有序列表
1. one
2. two
3. three

语法：`在需要列表样式的文字前添加"1."，依次增加。`

### 粗体与斜体

**这个是粗体**

*这个是斜体*

语法：
`**这个是粗体**`
`*这个是斜体*`

### 表格

| 书籍         | 价格   |  作者    |
| ---------   | -----: | :----:  |
| 金瓶梅       | ￥30  |   小明   |
| 西厢记       | ￥49  |   小华   |
| 计算机原理    | ￥50  |  韩梅梅  |

语法：
```
| 书籍         | 价格   |  作者    |
| ---------   | -----: | :----:  |
| 金瓶梅       | \￥30  |   小明   |
| 西厢记       | \￥49  |   小华   |
| 计算机原理    | \￥50  |  韩梅梅  |

* ------:为右对齐。 
* :------为左对齐。 
* :------:为居中对齐。 
* -------为使用默认居中对齐
```

### 阅读全文
`<!-- more -->`

### 代码块：

#### 单行代码块：
`public static void main(String args)`
语法：在代码块左右分别添加一个&acute;

#### 多行代码块
```
public static void main(String ..args){
    System.out.println("hello Markdown!")
}
```
语法：在代码块左右分别添加三个&acute;

### 删除线
~~这是一条被删除文本~~
语法：`~~这是一条被删除文本~~`

### 脚注
这是一个脚注[^1]。
语法：
```
这是一个脚注[^1]。
脚注须使用数字，然后再文章末尾加上"[^1]: 脚注内容"即可
```
### 实现页面内跳转
[锚点](#index)
<br>
<span id = "index">跳转到这里</span><br>
语法：
```
[锚点](#index)
<span id = "index">跳转到这里</span>
```

### 配合html,css使用
#### 设置字体颜色，样式，大小等
<font face="黑体">我是黑体字</font></br>
<font face="微软雅黑">我是微软雅黑</font></br>
<font face="STCAIYUN">我是华文彩云</font></br>
<font color=#0099ff size=5 face="黑体">color=#0099ff size=72 face="黑体"</font></br>
<font color=#00ffff size=4>color=#00ffff</font></br>
<font color=gray size=10>color=gray</font></br>
语法：
```
<font face="黑体">我是黑体字</font></br>
<font face="微软雅黑">我是微软雅黑</font></br>
<font face="STCAIYUN">我是华文彩云</font></br>
<font color=#0099ff size=5 face="黑体">color=#0099ff size=72 face="黑体"</font></br>
<font color=#00ffff size=4>color=#00ffff</font></br>
<font color=gray size=10>color=gray</font></br>
```

html样式可以和Markdown语法组合起来使用，比如可以指定超链接的颜色。<br>
这是一个跳转到博客首页的连接[<font color=#0099ff>首页</font>](http://www.lieeber.com/ "我的首页")
语法：`这是一个跳转到博客首页的连接[<font color=#0099ff>首页</font>](http://www.lieeber.com/ "我的首页")`
#### 设置背景色
<table><tr><td bgcolor=orange>黄色背景：orange</td></tr></table>


[^1]: 脚注内容