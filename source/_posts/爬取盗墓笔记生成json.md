---
title: 爬取盗墓笔记生成json
tags:
  - python
  - json
  - 爬虫
categories:
  - 爬虫
date: 2017-08-11 11:10:00
---

爬取盗墓笔记网站，根据章节生成json。使用requests进行网络请求，通过pyquery对网页进行解析。再把生成的json保存到本地文件。
<!-- more -->

### 代码
```python
import requests
from  pyquery import PyQuery as pq
import json

response = requests.get('http://seputu.com')
doc = pq(response.text)

title = doc('title').text()
# print(title)

dict = {}
mulu_list = []
mulu = doc('div[class=mulu]')
for item in mulu.items():
    mulu_title = item('div[class=mulu-title] center h2')
    if mulu_title:
        # print(mulu_title.text())
        chapter_list = []
        chapter = item('div[class=box] ul li a')
        for chapter_item in chapter.items():
            chapter_url = chapter_item.attr.href
            chapter_text = chapter_item.text()
            chapter_list.append({'chapter_title': chapter_text, 'chapter_url': chapter_url})
            # print(page_item_url)
            # print(page_item_text)
        mulu_list.append({"round_title": mulu_title.text(), 'round_detail': chapter_list})

dict['title'] = title
dict['content'] = mulu_list

with open('qiye.json', 'w') as f:
    json.dump(dict, f,ensure_ascii=False, indent=4)

```

一定要指定ensure_ascii为False,否则生成的json为unicode格式，不能看懂


### 生成的json

```json
{
   "content": [
       {
           "round_title": "盗墓笔记1七星鲁王宫",
           "round_detail": [
               {
                   "chapter_title": "七星鲁王 第一章 血尸",
                   "chapter_url": "http://seputu.com/biji1/1.html"
               },
               {
                   "chapter_title": "七星鲁王 第二章 五十年后",
                   "chapter_url": "http://seputu.com/biji1/2.html"
               },
               ...
               {
                   "chapter_title": "怒海潜沙 第四十六章 总结",
                   "chapter_url": "http://seputu.com/biji1/75.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记2秦岭神树",
           "round_detail": [
               {
                   "chapter_title": "秦岭神树篇 第一章 老痒出狱",
                   "chapter_url": "http://seputu.com/biji2/76.html"
               },
               ...
               {
                   "chapter_title": "云顶天宫（上） 第十五章 双层壁画",
                   "chapter_url": "http://seputu.com/biji2/130.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记3云顶天宫",
           "round_detail": [
               {
                   "chapter_title": "云顶天宫（下） 第一章 五圣雪山",
                   "chapter_url": "http://seputu.com/biji3/131.html"
               },
               ...
               {
                   "chapter_title": "盗墓笔记（另类）.mp3",
                   "chapter_url": "http://seputu.com/hesui/993.html"
               }
           ]
       }
   ],
   "title": "盗墓笔记,盗墓笔记小说全集在线阅读"
}
```