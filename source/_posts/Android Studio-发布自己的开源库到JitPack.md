---
title: 发布自己的开源库到JitPack
tags:
  - Android studio
  - JitPack
categories:
  - Android studio
date: 2018-2-15 12:28:15
---

&emsp;&emsp;之前我们使用过jCenter,虽然也很简单，步骤也只有简单几步，不过与JitPack比起来，还是显得太麻烦了。看看JitPack发布开源库的流程有多简单。
<!-- more -->
###  创建项目 
通过Android studio 创建开源库，然后上传到github.
### 登录网站 
打开 http://jitpack.io ,使用github登录账号，在输入框中输入你的项目的github地址。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fspvea5y1vj214y0hvabr.jpg)
### 发布版本
可以看到下面有一个Version，如果你没有发布release，这里默认显示的是master，如果需要显得正式一点，可以每次修改重新发布一个版本，提交release更新版本号。

在github中打开你的项目，点击release。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fspvhn7wlnj20xb05nmxq.jpg)
然后创建一个新的release，这里创建了一个v1.2的版本，并简单描述了这次改动。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fspvjjd8nnj20od0lkwfs.jpg)
然后再JitPack就可以看到这次修改的release了。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fspvkzpq0tj20kn0aagly.jpg)
我们点击Get it。
### 引入并使用
然后JitPack自动帮我们生成了开源库的地址。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fspvm6j708j20la0h6myn.jpg)
按照提示在android studio中引入即可。