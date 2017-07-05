---
title: Hexo使用上的一些小tips
tags:
  - Markdown
  - Hexo
categories:
  - 博客
date: 2017-05-15 12:39:04
---

### 更换next主题的背景
1. 将喜欢的背景图放到project-->themes-->next-->source-->images目录下。
2. 打开project-->themes-->next-->source-->css-->_custom-->custom.styl文件，加入代码<br>
`body { background:url(/images/imagename.jpg);}`
3. 重新编译项目就OK了。

<!-- more -->

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
