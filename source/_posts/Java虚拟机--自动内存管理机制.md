---
title: Java的自动内存管理机制
tags:
  - Java
  - Java虚拟机
categories:
  - Java
date: 2017-03-11 10:31:04
---
### 运行时数据区域
Java虚拟机在执行Java程序时会把它管理的内存划分为几个不同的数据区域。每个区域有各自的用途，并且创建和销毁的时间都会有所不同，有的区域随着虚拟机进程的启动而存在，有些区域则依赖用户线程的启动和结束而建立和销毁。以下是Java虚拟机所管理的几个运行时数据区域。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsoe263y0vj20dr0b1ju7.jpg)
<!-- more -->
1. 程序计数器
    - 每个线程都有自己独立的程序计数器，用来记录下一条要执行的字节码指令，分支，循环，跳转，异常处理，线程恢复等基础功能。此内存区域是唯一一个在Java虚拟机规范中没有规定任何OutOfMemoryError情况的区域。
2. Java虚拟机栈
    - 虚拟机栈是线程私有的，每个方法在执行时都会创建一个栈帧，用来存储局部变量表，操作数栈，动态链接，方法出口等信息。每一个方法从调用到执行完成，就对应着一个栈帧在虚拟机中入栈到出栈的过程。
    - 局部变量表存放各种基本数据类型，对象引用和returnAddress类型，其中64位长度的double和long数据会占用2个局部变量空间。
    - 局部变量表所需的内存空间在编译期间就完成了分配，在方法运行期间不会改变。
    - stackoverflowerror：线程请求的栈深度大于虚拟机允许的深度。outofmemoryerror：虚拟机栈可以动态扩展，但是扩展时无法申请到足够的内存。
3. 本地方法栈
    - 虚拟机栈执行Java方法，而本地方法栈则为虚拟机使用到的native方法服务。
    - 本地方法栈也会抛出StackOverFlowError和OutOfMemoryError异常。



### Markdown语法中实现添加脚注功能
hexo默认的渲染组件，是不能实现添加脚注功能的，因此需要安装新的渲染组件。
```
$ npm un hexo-renderer-marked --save
$ npm i hexo-renderer-markdown-it --save
```

打开项目_config.yml文件，在文中添加
```
markdown:
  render:
    html: true
    xhtmlOut: false
    breaks: false
    linkify: true
    typographer: true
    quotes: '“”‘’'
  plugins:
    - markdown-it-footnote
    - markdown-it-sup
    - markdown-it-sub
    - markdown-it-abbr
  anchors:
    level: 2
    collisionSuffix: 'v'
    permalink: true
    permalinkClass: header-anchor
    permalinkSymbol: ¶
```
重新编译后就可以使用脚注了。

测试发现，直接跑hexo server没有效果，需要发布后才能看到脚注的实现效果。

脚注的使用方法可以在[<font color=#0099ff>Markdown语法的使用</font>](http://www.lieeber.com/2017/01/22/markdown%E8%AF%AD%E6%B3%95%E7%9A%84%E4%BD%BF%E7%94%A8/ "Markdown语法的使用")中查看。


