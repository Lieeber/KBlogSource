---
title: Scrapy爬取顶点小说
tags:
  - python
  - scrapy
  - 爬虫
categories:
  - 爬虫
date: 2016-10-13 15:10:00
---

scrapy是非常常用的python爬虫框架，使用的异步模式，加快了我们的爬取速度，能大大提高我们的爬虫效率。

### 安装scrapy
```shell
pip3 install scrapy
```

<!-- more -->

### 启动pyspider
安装完成后，在命令行输入
```shell
    scrapy startproject XXXXX
```
就创建了一个scrapy爬虫工程，我们用pycharm打开这个工程。

<img  align=center src="http://image-1252244366.costj.myqcloud.com/scrapy_scrapy_dingdian.png"/>

entrypoint.py文件是我们自己创建的，是告诉scrapy等下需要爬取哪个文件。

```python
from scrapy.cmdline import execute
execute(['scrapy', 'crawl', 'dingdian'])
```
在spider目录下面创建dingdian.py。

```python
import re
from urllib.parse import urljoin

import os
import scrapy
from pyquery import PyQuery as pq
from scrapy.http import Request

class Myspider(scrapy.Spider):
    name = 'dingdian'
    allowed_domain = ['x23us.com']
    bash_url = 'http://www.11kt.cn/list/'
    bashurl = '.html'
    base_dir = '/Users/lieeber/Downloads/xiaoshuo/'

    def mkDir(self, dir_path):
        exists = os.path.exists(dir_path)
        if not exists:
            os.makedirs(dir_path)
            return dir_path
        else:
            return dir_path

    def start_requests(self):
        for i in range(1, 11):
            url = self.bash_url + str(i) + '_1' + self.bashurl
            yield Request(url, self.parse, meta={'item': i})

    def parse(self, response):
        doc = pq(response.text)
        max_num = doc('a[class=last]').text()
        item = response.meta['item']
        # print(item)

        for num in range(2, int(max_num) + 1):
            url = self.bash_url + str(item) + "_" + str(num) + ".html"
            # print(url)
            yield Request(url, self.get_name)

    def get_name(self, response):
        print(response.url)
        doc = pq(response.text)
        tds = doc('tr[bgcolor="#FFFFFF"] td:first-child')
        # print(tds)
        for td in tds.items():
            a = td('a')
            novel_url = a.attr('href')
            novel_name = a.text()
            yield Request(novel_url, callback=self.get_chapterurl,
                          meta={'novelname': novel_name, 'novelurl': novel_url})

    def get_chapterurl(self, response):
        novel_name = response.meta['novelname']
        novel_url = response.meta['novelurl']
        # print(novel_url)
        # print(novel_name)
        doc = pq(response.text)
        # item = DingdianItem()
        # item['name'] = novel_name
        # item['novelurl'] = novel_url
        category = doc('table[id=at] tr:first-child a').eq(0).text()
        author = doc('table[id=at] tr:first-child td').eq(1).text()
        novel_index = doc('p[class=btnlinks] a[class=read]').attr('href')
        # print(novel_index)
        # print(category)
        # print(author)
        # item['category'] = category
        # item['author'] = author
        # item['name_id'] = name_id
        # return item

        yield Request(novel_index, callback=self.get_novel_chapter,
                      meta={'novelname': novel_name, 'novelurl': novel_url, 'category': category, 'author': author})

    def get_novel_chapter(self, response):
        novel_url = response.meta['novelurl']
        novel_name = response.meta['novelname']
        category = response.meta['category']
        author = response.meta['author']
        # print(novel_url)
        doc = pq(response.text)
        a_list = doc('tr td[class=L] a')
        count = 1
        for a in a_list.items():
            href = a.attr('href')
            chapter_title = a.text()
            # print(href)
            # print(chapter_title)
            chapter_url = urljoin(response.url, href)
            # print(chapter_url)
            yield Request(chapter_url, callback=self.get_novel_text,
                          meta={'novelname': novel_name, 'novelurl': novel_url, 'category': category, 'author': author,
                                'chapter_title': chapter_title, 'count': count})
            count += 1

    def get_novel_text(self, response):
        novel_url = response.meta['novelurl']
        novel_name = response.meta['novelname'].replace('/', '——').strip()
        category = response.meta['category'].replace('/', '').strip()
        author = response.meta['author'].replace('/', '').strip()
        chapter_title = response.meta['chapter_title'].replace('/', '').strip()
        count = response.meta['count']
        doc = pq(response.text)
        contents = doc('dd[id=contents]')
        contents('span').replace_all('br')
        # print(contents)
        aa = contents.text().replace(' ', '')

        dir_path = self.base_dir + "/" + category + "/" + novel_name + "_" + author + "/"

        self.mkDir(dir_path)

        with open(dir_path + str(count) + "、" + chapter_title + ".txt", 'w') as f:
            f.write(aa)

```

代码写完后，运行entrypoint.py文件，就能够开启爬虫了。

<img  align=center src="http://image-1252244366.costj.myqcloud.com/scrapy_project_dingdian_result.png"/>

可以看到，我们已经成功把小说爬取下来了，由于爬取数量太多，只爬取了一小部分。。