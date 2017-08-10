---
title: Pyspider爬取mzitu图片
tags:
  - python
  - pyspider
  - 爬虫
categories:
  - 爬虫
date: 2017-08-10 11:10:00
---

最近在学习爬虫技术，简单记录一下pyspider的使用。

### 安装pyspider
```shell
pip3 install pyspider
```

<!-- more -->

### 启动pyspider
安装完成后就可以直接启动了
```shell
    pyspider all
```
服务启动后，打开浏览器，在网址栏输入localhost:5000，即可进入pyspider提供的webui界面

<img  align=center src="http://image-1252244366.costj.myqcloud.com/pyspider_webui.png"/>

如果想开启一个新的任务，点击左上角的create

<img width="400" height="200" align=center src="http://image-1252244366.costj.myqcloud.com/pyspider_create_new_project.png"/>

项目创建后就进入了任务详情界面，左边可以查看每一次爬取界面的详细信息，右边是代码。

<img  align=center src="http://image-1252244366.costj.myqcloud.com/pyspider_webui_detail.png"/>

下面是具体的爬虫代码：

```python
from pyspider.libs.base_handler import *
import os


class Handler(BaseHandler):
    crawl_config = {
    }

    def mkDir(self, dir_path):
        exists = os.path.exists(dir_path)
        if not exists:
            os.makedirs(dir_path)
            return dir_path
        else:
            return dir_path

    def saveImg(self, content, path):
        f = open(path, 'wb')
        f.write(content)
        f.close()

    def __init__(self):
        self.page = 1
        self.total_page = 30
        self.base_url = "/Users/lieeber/Downloads/meizitu2/"
        self.title = ""

    @every(minutes=24 * 60)
    def on_start(self):
        while self.page <= self.total_page:
            self.crawl('http://www.mzitu.com/page/' + str(self.page), callback=self.index_page)
            self.page += 1

    @config(age=10 * 24 * 60 * 60)
    def index_page(self, response):
        aa = response.doc('div[class=postlist]')('ul[id=pins]')('li')('span')('a[target=_blank]')
        for each in aa.items():
            print(each.attr.href)
            self.crawl(each.attr.href, callback=self.index_page_each_page)

    @config(priority=2)
    def index_page_each_page(self, response):
        self.title = response.doc('title').text()
        print(self.title)
        big_page = response.doc('span[class=dots]').next('a span').text()
        for item in range(1, int(big_page) + 1):
            print(response.url + "/" + str(item))
            self.crawl(response.url + "/" + str(item), callback=self.detail_page)

    @config(priority=2)
    def detail_page(self, response):
        image_url = response.doc('div[class=main-image]')('img').attr('src')
        print(image_url)
        self.crawl(image_url, headers={'referer': 'http://www.mzitu.com/'}, callback=self.get_image_content)

    @config(priority=2)
    def get_image_content(self, response):
        image_name = response.url.split('/')[-1]
        print(image_name)
        dir_path = self.mkDir(self.base_url + self.title)
        print(dir_path)
        self.saveImg(response.content, dir_path + "/" + image_name)
```

代码写完后，就可以进入dashboard页面，更改status为running或者debug状态，点击action中的run按钮即可开启爬虫任务了。

<img  align=center src="http://image-1252244366.costj.myqcloud.com/pyspider_mzitu_item.png"/>

可以看到，图片被成功的爬取下来了。