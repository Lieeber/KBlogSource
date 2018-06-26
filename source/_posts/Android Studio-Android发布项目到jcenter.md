---
title: Android发布项目到jCenter
tags:
  - Android studio
  - jCenter
categories:
  - Android studio
date: 2018-2-10 12:18:15
---

&emsp;&emsp;对于一些常用的工具类，我们经常会在很多项目中都使用到，如果每个项目中都对这些代码进行拷贝，确实是一件比较麻烦的事情；另外，我们经常会创造一些比较实用的项目，也希望能够拿这些项目去帮助别人。因此，将自己的工具类或者项目开源是一个很必要的事情。

&emsp;&emsp;android studio中引入第三方库，基本都是来自于jcenter仓库，我们也可以把自己的项目放到jcenter仓库。

下面是具体的操作流程
<!-- more -->
### 注册bintray.com账号。
1. 进入https://bintray.com/，注册账号。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsoyyn80fyj20rx0euaqp.jpg)
3. 注意jcenter的首页如上图所示，我们应该点击右边的‘Singn Up Here’进行注册，因为左边的对应的的是用户，30天免费期过后是需要付费的。
4. 注册并登录后点击右上角View Profile，再点击左上角的Edit，然后可以看到以下界面。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsp1f8j38aj20td0fl0tv.jpg)
5. 点击API Key获取到属于你个人的API Key
6. 点击Repositories，创建一个叫做maven的仓库
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsp1gm6xl9j20hy0ja75a.jpg)
###  在项目中引入bintray-release
1. 打开project的build.gradle文件
```java
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.3'
        classpath 'com.novoda:bintray-release:0.8.0'
    }
}
```
2. 将需要上传的library的build.gradle中添加如下配置。
```java
apply plugin: 'com.novoda.bintray-release'
.....
publish {
    userOrg = 'lieeber1'//bintray.com用户名
    groupId = 'com.lieeber'//jcenter上的路径
    artifactId = 'jcenterlibrary'//项目名称
    publishVersion = '1.1.0'//版本号
    desc = 'you can write everything whatever you want.'//描述
    website = 'https://github.com/lieeber/demolibrary'//网站
}
```
完成上面的配置后，就准备上传了。
### 上传
1. mac执行下面的代码
```java
    ./gradlew clean build bintrayUpload
    -PbintrayUser=lieeber1
    -PbintrayKey=xxxxxxxxxxxxxxxxxxxxxx
    -PdryRun=false
```
2. windows执行以下代码
```java
    gradlew clean build bintrayUpload -PbintrayUser=lieeber -PbintrayKey=xxxxxxxxxxxxxxxxxxxxxx -PdryRun=false
```
上传完成后，可以通过 https://bintray.com/你的用户名/maven对访问刚刚上传的仓库。（我这里是https://bintray.com/lieeber1/maven）
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsp1l5pin9j20po0jpwfu.jpg)
但是到了这一步，不代表我们的仓库就能在项目中进行引用了，我们还需要添加到jcenter，并且通过人工审核之后才能正常使用。
点击仓库，打开仓库详情。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsp1lnlypmj20xf0jz41a.jpg)
点击右下角的Add to jCenter.在提交页面，需要你描述一下你的仓库，填完之后，提交并等待人工审核。通过之后，你就可以成功在项目中引入你的仓库了。

比如我这个仓库的引用地址为：implementation 'com.lieeber:jcenterlibrary:1.1.0'。


