---
title: PySpider爬取糗事百科文章和图片
tags:
  - python
  - pyspider
  - 爬虫
categories:
  - 爬虫
date: 2016-10-10 15:20:00
---

### 摘要

爬取糗事百科的文章，有些文章含有图片，需要把图片也保存下来，同时保存用户的头像，通过用户的昵称来命名文件夹，同一个用户的段子保存在同一个目录下。

<!-- more -->

下面是具体的爬虫代码：

```python
from pyspider.libs.base_handler import *
import os


class Handler(BaseHandler):
    crawl_config = {
    }

    def __init__(self):
        self.base_dir = "/Users/lieeber/Downloads/qiushibaike/"

    def mkDir(self, dir_path):
        exists = os.path.exists(dir_path)
        if not exists:
            os.makedirs(dir_path)
        return dir_path

    def saveImg(self, content, path):
        with open(path, 'wb') as f:
            f.write(content)

    def saveText(self, content, path):
        with open(path, 'w') as f:
            f.write(content)

    @every(minutes=15)
    def on_start(self):
        for i in range(1, 14):
            self.crawl('https://www.qiushibaike.com/8hr/page' + str(i), callback=self.index_page)

    @config(age=10 * 24 * 60 * 60)
    def index_page(self, response):
        list_article = response.doc('div[class^="article block untagged mb15"]')
        for item in list_article.items():
            item_article_url = item('a[class=contentHerf]').attr.href
            print(item_article_url)
            self.crawl(item_article_url, callback=self.detail_article_page)

    @config(priority=2)
    def detail_article_page(self, response):
        # print(response.text)
        content = response.doc('div[class=content]').text()
        print(content)
        user_info = response.doc('div[class="author clearfix"]')
        img_src = user_info('img[src^="https://pic.qiushibaike.com/system/avtnew"]').attr('src')
        user_name = user_info('a h2').text()
        self.mkDir(self.base_dir + user_name)

        print(img_src)
        print(user_name)
        self.crawl(img_src, callback=self.get_user_avatar, save={'user_name': user_name})
        self.saveText(content, self.base_dir + user_name + "/" + user_name + ".txt")
        content_src = response.doc('div[class=thumb] img').attr('src')
        if content_src:
            print(content_src)
            self.crawl(content_src, callback=self.get_content_img, save={'user_name': user_name})

    @config(priority=2)
    def get_content_img(self, response):
        image_name = response.url.split('/')[-1]
        user_name = response.save['user_name']
        self.saveImg(response.content, self.base_dir + user_name + "/" + image_name)

    @config(priority=2)
    def get_user_avatar(self, response):
        image_name = response.url.split('/')[-1]
        user_name = response.save['user_name']
        self.saveImg(response.content, self.base_dir + user_name + "/" + user_name + ".jpg")
```

当某个方法需要使用上一个方法的数据时，往self.crawl()函数中添加参数save={'key':'value'}，下一个方法通过response.save['key']就能正确拿到value了。