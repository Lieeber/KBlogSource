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
               {
                   "chapter_title": "七星鲁王 第三章 瓜子庙",
                   "chapter_url": "http://seputu.com/biji1/3.html"
               },
               {
                   "chapter_title": "七星鲁王 第四章 尸洞",
                   "chapter_url": "http://seputu.com/biji1/4.html"
               },
               {
                   "chapter_title": "七星鲁王 第五章 水影",
                   "chapter_url": "http://seputu.com/biji1/5.html"
               },
               {
                   "chapter_title": "七星鲁王 第六章 积尸地",
                   "chapter_url": "http://seputu.com/biji1/6.html"
               },
               {
                   "chapter_title": "七星鲁王 第七章 一百多个人头",
                   "chapter_url": "http://seputu.com/biji1/7.html"
               },
               {
                   "chapter_title": "七星鲁王 第八章 山谷",
                   "chapter_url": "http://seputu.com/biji1/8.html"
               },
               {
                   "chapter_title": "七星鲁王 第九章 古墓",
                   "chapter_url": "http://seputu.com/biji1/9.html"
               },
               {
                   "chapter_title": "七星鲁王 第十章 影子",
                   "chapter_url": "http://seputu.com/biji1/10.html"
               },
               {
                   "chapter_title": "七星鲁王 第十一章 七星棺",
                   "chapter_url": "http://seputu.com/biji1/11.html"
               },
               {
                   "chapter_title": "七星鲁王 第十二章 门",
                   "chapter_url": "http://seputu.com/biji1/12.html"
               },
               {
                   "chapter_title": "七星鲁王 第十三章 02200059",
                   "chapter_url": "http://seputu.com/biji1/13.html"
               },
               {
                   "chapter_title": "七星鲁王 第十四章 闷油瓶",
                   "chapter_url": "http://seputu.com/biji1/14.html"
               },
               {
                   "chapter_title": "七星鲁王 第十五章 屁",
                   "chapter_url": "http://seputu.com/biji1/15.html"
               },
               {
                   "chapter_title": "七星鲁王 第十六章 小手",
                   "chapter_url": "http://seputu.com/biji1/16.html"
               },
               {
                   "chapter_title": "七星鲁王 第十七章 洞",
                   "chapter_url": "http://seputu.com/biji1/17.html"
               },
               {
                   "chapter_title": "七星鲁王 第十八章 大树",
                   "chapter_url": "http://seputu.com/biji1/18.html"
               },
               {
                   "chapter_title": "七星鲁王 第十九章 女尸",
                   "chapter_url": "http://seputu.com/biji1/19.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十章 钥匙",
                   "chapter_url": "http://seputu.com/biji1/20.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十一章 青眼狐尸",
                   "chapter_url": "http://seputu.com/biji1/21.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十二章 八重宝函",
                   "chapter_url": "http://seputu.com/biji1/22.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十三章 棺椁",
                   "chapter_url": "http://seputu.com/biji1/23.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十四章 活尸",
                   "chapter_url": "http://seputu.com/biji1/24.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十五章 玉俑",
                   "chapter_url": "http://seputu.com/biji1/25.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十六章 紫玉匣子",
                   "chapter_url": "http://seputu.com/biji1/26.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十七章 谎言",
                   "chapter_url": "http://seputu.com/biji1/27.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十八章 火",
                   "chapter_url": "http://seputu.com/biji1/28.html"
               },
               {
                   "chapter_title": "七星鲁王 第二十九章 紫金匣",
                   "chapter_url": "http://seputu.com/biji1/29.html"
               },
               {
                   "chapter_title": "怒海潜沙 第一章 蛇眉铜鱼",
                   "chapter_url": "http://seputu.com/biji1/30.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二章 双层墓墙",
                   "chapter_url": "http://seputu.com/biji1/31.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三章 大风暴",
                   "chapter_url": "http://seputu.com/biji1/32.html"
               },
               {
                   "chapter_title": "怒海潜沙 第四章 海鬼",
                   "chapter_url": "http://seputu.com/biji1/33.html"
               },
               {
                   "chapter_title": "怒海潜沙 第五章 老照片",
                   "chapter_url": "http://seputu.com/biji1/34.html"
               },
               {
                   "chapter_title": "怒海潜沙 第六章 海南",
                   "chapter_url": "http://seputu.com/biji1/35.html"
               },
               {
                   "chapter_title": "怒海潜沙 第七章 女人",
                   "chapter_url": "http://seputu.com/biji1/36.html"
               },
               {
                   "chapter_title": "怒海潜沙 第八章 变天了",
                   "chapter_url": "http://seputu.com/biji1/37.html"
               },
               {
                   "chapter_title": "怒海潜沙 第九章 鬼船",
                   "chapter_url": "http://seputu.com/biji1/38.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十章 枯手",
                   "chapter_url": "http://seputu.com/biji1/39.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十一章 甲板",
                   "chapter_url": "http://seputu.com/biji1/40.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十二章 三叔的谎言",
                   "chapter_url": "http://seputu.com/biji1/41.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十三章 海猴子",
                   "chapter_url": "http://seputu.com/biji1/42.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十四章 永兴岛",
                   "chapter_url": "http://seputu.com/biji1/43.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十五章 胖子",
                   "chapter_url": "http://seputu.com/biji1/44.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十六章 开会",
                   "chapter_url": "http://seputu.com/biji1/45.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十七章 头发",
                   "chapter_url": "http://seputu.com/biji1/46.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十八章 大量头发",
                   "chapter_url": "http://seputu.com/biji1/47.html"
               },
               {
                   "chapter_title": "怒海潜沙 第十九章 大瓷罐",
                   "chapter_url": "http://seputu.com/biji1/48.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十章 甬道",
                   "chapter_url": "http://seputu.com/biji1/49.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十一章 箭",
                   "chapter_url": "http://seputu.com/biji1/50.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十二章 第一次解迷",
                   "chapter_url": "http://seputu.com/biji1/51.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十三章 继续解迷",
                   "chapter_url": "http://seputu.com/biji1/52.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十四章 开棺",
                   "chapter_url": "http://seputu.com/biji1/53.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十五章 一个人",
                   "chapter_url": "http://seputu.com/biji1/54.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十六章 瓷画",
                   "chapter_url": "http://seputu.com/biji1/55.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十七章 无题",
                   "chapter_url": "http://seputu.com/biji1/56.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十八章 继续无题",
                   "chapter_url": "http://seputu.com/biji1/57.html"
               },
               {
                   "chapter_title": "怒海潜沙 第二十九章 石碑",
                   "chapter_url": "http://seputu.com/biji1/58.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十章 池底",
                   "chapter_url": "http://seputu.com/biji1/59.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十一章 二十年前",
                   "chapter_url": "http://seputu.com/biji1/60.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十二章 奇门遁甲",
                   "chapter_url": "http://seputu.com/biji1/61.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十三章 生门",
                   "chapter_url": "http://seputu.com/biji1/62.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十四章 连环",
                   "chapter_url": "http://seputu.com/biji1/63.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十五章 血字",
                   "chapter_url": "http://seputu.com/biji1/64.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十六章 脱困",
                   "chapter_url": "http://seputu.com/biji1/65.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十七章 盗洞",
                   "chapter_url": "http://seputu.com/biji1/66.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十八章 禁婆",
                   "chapter_url": "http://seputu.com/biji1/67.html"
               },
               {
                   "chapter_title": "怒海潜沙 第三十九章 混战",
                   "chapter_url": "http://seputu.com/biji1/68.html"
               },
               {
                   "chapter_title": "怒海潜沙 第四十章 墙洞",
                   "chapter_url": "http://seputu.com/biji1/69.html"
               },
               {
                   "chapter_title": "怒海潜沙 第四十一章 珊瑚树",
                   "chapter_url": "http://seputu.com/biji1/70.html"
               },
               {
                   "chapter_title": "怒海潜沙 第四十二章 困境",
                   "chapter_url": "http://seputu.com/biji1/71.html"
               },
               {
                   "chapter_title": "怒海潜沙 第四十三章 炸弹",
                   "chapter_url": "http://seputu.com/biji1/72.html"
               },
               {
                   "chapter_title": "怒海潜沙 第四十四章 脱皮",
                   "chapter_url": "http://seputu.com/biji1/73.html"
               },
               {
                   "chapter_title": "怒海潜沙 第四十五章 脱出",
                   "chapter_url": "http://seputu.com/biji1/74.html"
               },
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
               {
                   "chapter_title": "秦岭神树篇 第二章 六角铃铛",
                   "chapter_url": "http://seputu.com/biji2/77.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三章 跟踪",
                   "chapter_url": "http://seputu.com/biji2/78.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第四章 继续跟踪",
                   "chapter_url": "http://seputu.com/biji2/79.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第五章 偷听",
                   "chapter_url": "http://seputu.com/biji2/80.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第六章 挖掘",
                   "chapter_url": "http://seputu.com/biji2/81.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第七章 夹子沟",
                   "chapter_url": "http://seputu.com/biji2/82.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第八章 猴子",
                   "chapter_url": "http://seputu.com/biji2/83.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第九章 石人",
                   "chapter_url": "http://seputu.com/biji2/84.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十章 哲罗鲑",
                   "chapter_url": "http://seputu.com/biji2/85.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十一章 人头",
                   "chapter_url": "http://seputu.com/biji2/86.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十二章 地下河",
                   "chapter_url": "http://seputu.com/biji2/87.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十三章 黄泉的瀑布",
                   "chapter_url": "http://seputu.com/biji2/88.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十四章 深潭",
                   "chapter_url": "http://seputu.com/biji2/89.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十五章 休息",
                   "chapter_url": "http://seputu.com/biji2/90.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十六章 爬",
                   "chapter_url": "http://seputu.com/biji2/91.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十七章 尸阵",
                   "chapter_url": "http://seputu.com/biji2/92.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十八章 鬼吹灯",
                   "chapter_url": "http://seputu.com/biji2/93.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第十九章 骨头的故事",
                   "chapter_url": "http://seputu.com/biji2/94.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十章 火龙阵",
                   "chapter_url": "http://seputu.com/biji2/95.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十一章 秦岭神树",
                   "chapter_url": "http://seputu.com/biji2/96.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十二章 继续爬",
                   "chapter_url": "http://seputu.com/biji2/97.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十三章 裂痕",
                   "chapter_url": "http://seputu.com/biji2/98.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十四章 摔死",
                   "chapter_url": "http://seputu.com/biji2/99.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十五章 祭祀",
                   "chapter_url": "http://seputu.com/biji2/100.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十六章 螭蛊",
                   "chapter_url": "http://seputu.com/biji2/101.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十七章 凌空",
                   "chapter_url": "http://seputu.com/biji2/102.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十八章 麒麟竭",
                   "chapter_url": "http://seputu.com/biji2/103.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第二十九章 逼近",
                   "chapter_url": "http://seputu.com/biji2/104.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十章 老套路",
                   "chapter_url": "http://seputu.com/biji2/105.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十一章 鬼雾",
                   "chapter_url": "http://seputu.com/biji2/106.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十二章 偷袭",
                   "chapter_url": "http://seputu.com/biji2/107.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十三章 和解",
                   "chapter_url": "http://seputu.com/biji2/108.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十四章 大胆假设，小...",
                   "chapter_url": "http://seputu.com/biji2/109.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十五章 失控",
                   "chapter_url": "http://seputu.com/biji2/110.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十六章 坍塌",
                   "chapter_url": "http://seputu.com/biji2/111.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十七章 日记",
                   "chapter_url": "http://seputu.com/biji2/112.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十八章 真像",
                   "chapter_url": "http://seputu.com/biji2/113.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第三十九章 烛九阴",
                   "chapter_url": "http://seputu.com/biji2/114.html"
               },
               {
                   "chapter_title": "秦岭神树篇 第四十章 脱出",
                   "chapter_url": "http://seputu.com/biji2/115.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第一章 新的消息",
                   "chapter_url": "http://seputu.com/biji2/116.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第二章 二００七年第一...",
                   "chapter_url": "http://seputu.com/biji2/117.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第三章 镜儿宫",
                   "chapter_url": "http://seputu.com/biji2/118.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第四章 多了一个",
                   "chapter_url": "http://seputu.com/biji2/119.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第五章 最初的迷题",
                   "chapter_url": "http://seputu.com/biji2/120.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第六章 简单答案",
                   "chapter_url": "http://seputu.com/biji2/121.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第七章 潘子",
                   "chapter_url": "http://seputu.com/biji2/122.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第八章 新的团伙",
                   "chapter_url": "http://seputu.com/biji2/123.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第九章 九龙抬尸",
                   "chapter_url": "http://seputu.com/biji2/124.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第十章 营山村",
                   "chapter_url": "http://seputu.com/biji2/125.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第十一章 困境",
                   "chapter_url": "http://seputu.com/biji2/126.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第十二章 百足龙",
                   "chapter_url": "http://seputu.com/biji2/127.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第十三章 缝隙（上）",
                   "chapter_url": "http://seputu.com/biji2/128.html"
               },
               {
                   "chapter_title": "云顶天宫（上） 第十四章 缝隙（下）",
                   "chapter_url": "http://seputu.com/biji2/129.html"
               },
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
               {
                   "chapter_title": "云顶天宫（下） 第二章 自杀行为",
                   "chapter_url": "http://seputu.com/biji3/132.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三章 雪崩",
                   "chapter_url": "http://seputu.com/biji3/133.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四章 昆仑胎",
                   "chapter_url": "http://seputu.com/biji3/134.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第五章 胎洞灵宫",
                   "chapter_url": "http://seputu.com/biji3/135.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第六章 灵宫大殿",
                   "chapter_url": "http://seputu.com/biji3/136.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第七章 博弈",
                   "chapter_url": "http://seputu.com/biji3/137.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第八章 骚动",
                   "chapter_url": "http://seputu.com/biji3/138.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第九章 墙串子",
                   "chapter_url": "http://seputu.com/biji3/139.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十章 百足龙神",
                   "chapter_url": "http://seputu.com/biji3/140.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十一章 夹层",
                   "chapter_url": "http://seputu.com/biji3/141.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十二章 藏尸阁",
                   "chapter_url": "http://seputu.com/biji3/142.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十三章 排道",
                   "chapter_url": "http://seputu.com/biji3/143.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十四章 进入排道",
                   "chapter_url": "http://seputu.com/biji3/144.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十五章 火山口（上）...",
                   "chapter_url": "http://seputu.com/biji3/145.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十六章 火山口（下）...",
                   "chapter_url": "http://seputu.com/biji3/146.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十七章 门殿（一）",
                   "chapter_url": "http://seputu.com/biji3/147.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十八章 门殿（二）",
                   "chapter_url": "http://seputu.com/biji3/148.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第十九章 门殿（三）",
                   "chapter_url": "http://seputu.com/biji3/149.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十章 门殿（四）",
                   "chapter_url": "http://seputu.com/biji3/150.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十一章 护城河",
                   "chapter_url": "http://seputu.com/biji3/151.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十二章 殉葬渠",
                   "chapter_url": "http://seputu.com/biji3/152.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十三章 无聊暗号...",
                   "chapter_url": "http://seputu.com/biji3/153.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十四章 水下的排...",
                   "chapter_url": "http://seputu.com/biji3/154.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十五章 猴头烧",
                   "chapter_url": "http://seputu.com/biji3/155.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十六章 记号",
                   "chapter_url": "http://seputu.com/biji3/156.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十七章 一个新的...",
                   "chapter_url": "http://seputu.com/biji3/157.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十八章 无法言喻...",
                   "chapter_url": "http://seputu.com/biji3/158.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第二十九章 十年前的...",
                   "chapter_url": "http://seputu.com/biji3/159.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十章 影子的道路...",
                   "chapter_url": "http://seputu.com/biji3/160.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十一章 永无止境...",
                   "chapter_url": "http://seputu.com/biji3/161.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十二章 胖子的枚...",
                   "chapter_url": "http://seputu.com/biji3/162.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十三章 倒斗和量...",
                   "chapter_url": "http://seputu.com/biji3/163.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十四章 来自海底...",
                   "chapter_url": "http://seputu.com/biji3/164.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十五章 犀照",
                   "chapter_url": "http://seputu.com/biji3/165.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十六章 出口",
                   "chapter_url": "http://seputu.com/biji3/166.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十七章 闷油瓶第...",
                   "chapter_url": "http://seputu.com/biji3/167.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十八章 蛇眉铜鱼...",
                   "chapter_url": "http://seputu.com/biji3/168.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第三十九章 唯一的出...",
                   "chapter_url": "http://seputu.com/biji3/169.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四十章 “守护神”的...",
                   "chapter_url": "http://seputu.com/biji3/170.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四十一章 谍中谍",
                   "chapter_url": "http://seputu.com/biji3/171.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四十二章 千手观音...",
                   "chapter_url": "http://seputu.com/biji3/172.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四十三章 围攻",
                   "chapter_url": "http://seputu.com/biji3/173.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四十四章 天与地的...",
                   "chapter_url": "http://seputu.com/biji3/174.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四十五章 永远无法...",
                   "chapter_url": "http://seputu.com/biji3/175.html"
               },
               {
                   "chapter_title": "云顶天宫（下） 第四十六章 休整之后...",
                   "chapter_url": "http://seputu.com/biji3/176.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第一章 三叔的醒来",
                   "chapter_url": "http://seputu.com/biji3/177.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二章 往事不堪回首...",
                   "chapter_url": "http://seputu.com/biji3/178.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第三章 Who Are You?...",
                   "chapter_url": "http://seputu.com/biji3/179.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第四章 血尸古墓",
                   "chapter_url": "http://seputu.com/biji3/180.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第五章 怪脸",
                   "chapter_url": "http://seputu.com/biji3/181.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第六章 让人无法接受...",
                   "chapter_url": "http://seputu.com/biji3/182.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第七章 四目九天娘娘...",
                   "chapter_url": "http://seputu.com/biji3/183.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第八章 西沙的前奏",
                   "chapter_url": "http://seputu.com/biji3/184.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记4蛇沼鬼城",
           "round_detail": [
               {
                   "chapter_title": "蛇沼鬼城（上） 第九章 录像带",
                   "chapter_url": "http://seputu.com/biji4/185.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十章 裘德考",
                   "chapter_url": "http://seputu.com/biji4/186.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十一章 青铜的丹炉...",
                   "chapter_url": "http://seputu.com/biji4/187.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十二章 星盘",
                   "chapter_url": "http://seputu.com/biji4/188.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十三章 西沙的真相...",
                   "chapter_url": "http://seputu.com/biji4/189.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十四章 深海",
                   "chapter_url": "http://seputu.com/biji4/190.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十五章 浮尸",
                   "chapter_url": "http://seputu.com/biji4/191.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十六章 沉船",
                   "chapter_url": "http://seputu.com/biji4/192.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十七章 哨子棺",
                   "chapter_url": "http://seputu.com/biji4/193.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十八章 尿",
                   "chapter_url": "http://seputu.com/biji4/194.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第十九章 机关",
                   "chapter_url": "http://seputu.com/biji4/195.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十章 虫脑",
                   "chapter_url": "http://seputu.com/biji4/196.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十一章 黑暗中的...",
                   "chapter_url": "http://seputu.com/biji4/197.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十二章 抉择",
                   "chapter_url": "http://seputu.com/biji4/198.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十三章 上帝的十...",
                   "chapter_url": "http://seputu.com/biji4/199.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十四章 死而复生...",
                   "chapter_url": "http://seputu.com/biji4/200.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十五章 重启",
                   "chapter_url": "http://seputu.com/biji4/201.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十六章 出院",
                   "chapter_url": "http://seputu.com/biji4/202.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十七章 画面",
                   "chapter_url": "http://seputu.com/biji4/203.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十八章 第十一个...",
                   "chapter_url": "http://seputu.com/biji4/204.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（上） 第二十九章 尾声",
                   "chapter_url": "http://seputu.com/biji4/205.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第一章 稀客",
                   "chapter_url": "http://seputu.com/biji4/206.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二章 新的线索",
                   "chapter_url": "http://seputu.com/biji4/207.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三章 录像带里的老...",
                   "chapter_url": "http://seputu.com/biji4/208.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四章 完全混乱",
                   "chapter_url": "http://seputu.com/biji4/209.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第五章 录像带的真正...",
                   "chapter_url": "http://seputu.com/biji4/210.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第六章 来自地狱的请...",
                   "chapter_url": "http://seputu.com/biji4/211.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第七章 鬼楼",
                   "chapter_url": "http://seputu.com/biji4/212.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第八章 306",
                   "chapter_url": "http://seputu.com/biji4/213.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第九章 线索",
                   "chapter_url": "http://seputu.com/biji4/214.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十章 计划",
                   "chapter_url": "http://seputu.com/biji4/215.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十一章 盗墓笔记",
                   "chapter_url": "http://seputu.com/biji4/216.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十二章 文锦的笔记...",
                   "chapter_url": "http://seputu.com/biji4/217.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十三章 黑暗",
                   "chapter_url": "http://seputu.com/biji4/218.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十四章 惊变",
                   "chapter_url": "http://seputu.com/biji4/219.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十五章 重逢",
                   "chapter_url": "http://seputu.com/biji4/220.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十六章 营地",
                   "chapter_url": "http://seputu.com/biji4/221.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十七章 出发",
                   "chapter_url": "http://seputu.com/biji4/222.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十八章 文锦的口信...",
                   "chapter_url": "http://seputu.com/biji4/223.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第十九章 再次出发",
                   "chapter_url": "http://seputu.com/biji4/224.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十章 迷路",
                   "chapter_url": "http://seputu.com/biji4/225.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十一章 魔鬼城",
                   "chapter_url": "http://seputu.com/biji4/226.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十二章 魔鬼的呼...",
                   "chapter_url": "http://seputu.com/biji4/227.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十三章 沙海沉船...",
                   "chapter_url": "http://seputu.com/biji4/228.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十四章 西王母罐...",
                   "chapter_url": "http://seputu.com/biji4/229.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十五章 鬼头",
                   "chapter_url": "http://seputu.com/biji4/230.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十六章 启示录",
                   "chapter_url": "http://seputu.com/biji4/231.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十七章 第一场雨...",
                   "chapter_url": "http://seputu.com/biji4/232.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十八章 向绿洲进...",
                   "chapter_url": "http://seputu.com/biji4/233.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第二十九章 向绿洲进...",
                   "chapter_url": "http://seputu.com/biji4/234.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十章 第二场雨（上...",
                   "chapter_url": "http://seputu.com/biji4/235.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十一章 第二场雨...",
                   "chapter_url": "http://seputu.com/biji4/236.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十二章 青苔下的...",
                   "chapter_url": "http://seputu.com/biji4/237.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十三章 青苔下的...",
                   "chapter_url": "http://seputu.com/biji4/238.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十四章 蛇骨（上）...",
                   "chapter_url": "http://seputu.com/biji4/239.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十五章 蛇骨（中）...",
                   "chapter_url": "http://seputu.com/biji4/240.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十六章 蛇骨（下）...",
                   "chapter_url": "http://seputu.com/biji4/241.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十七章 沼泽魔域...",
                   "chapter_url": "http://seputu.com/biji4/242.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十八章 沼泽魔域...",
                   "chapter_url": "http://seputu.com/biji4/243.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第三十九章 沼泽魔域...",
                   "chapter_url": "http://seputu.com/biji4/244.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四十章 狂蟒之灾",
                   "chapter_url": "http://seputu.com/biji4/245.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四十一章 蛇王",
                   "chapter_url": "http://seputu.com/biji4/246.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四十二章 蛇沼鬼城...",
                   "chapter_url": "http://seputu.com/biji4/247.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四十三章 蛇沼鬼城...",
                   "chapter_url": "http://seputu.com/biji4/248.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四十四章 蛇沼鬼城...",
                   "chapter_url": "http://seputu.com/biji4/249.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四十五章 尸体的脚...",
                   "chapter_url": "http://seputu.com/biji4/250.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（中） 第四十六章 蛇的阴谋...",
                   "chapter_url": "http://seputu.com/biji4/251.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记5谜海归巢",
           "round_detail": [
               {
                   "chapter_title": "蛇沼鬼城（下） 第一章 追击",
                   "chapter_url": "http://seputu.com/biji5/252.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二章 消失了",
                   "chapter_url": "http://seputu.com/biji5/253.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三章 信号烟",
                   "chapter_url": "http://seputu.com/biji5/254.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第四章 无声的山谷",
                   "chapter_url": "http://seputu.com/biji5/255.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第五章 石像",
                   "chapter_url": "http://seputu.com/biji5/256.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第六章 石像的朝向",
                   "chapter_url": "http://seputu.com/biji5/257.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第七章 破裂",
                   "chapter_url": "http://seputu.com/biji5/258.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第八章 第一夜：大雾",
                   "chapter_url": "http://seputu.com/biji5/259.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第九章 第一夜：手链",
                   "chapter_url": "http://seputu.com/biji5/260.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十章 第一夜：丛林鬼...",
                   "chapter_url": "http://seputu.com/biji5/261.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十一章 第一夜：逼近...",
                   "chapter_url": "http://seputu.com/biji5/262.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十二章 第一夜：偷袭...",
                   "chapter_url": "http://seputu.com/biji5/263.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十三章 第一夜：冲突...",
                   "chapter_url": "http://seputu.com/biji5/264.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十四章 第一夜：追击...",
                   "chapter_url": "http://seputu.com/biji5/265.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十五章 第一夜：搏斗...",
                   "chapter_url": "http://seputu.com/biji5/266.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十六章 黎明：血光之...",
                   "chapter_url": "http://seputu.com/biji5/267.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十七章 黎明：寂静的...",
                   "chapter_url": "http://seputu.com/biji5/268.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十八章 第二夜：再次...",
                   "chapter_url": "http://seputu.com/biji5/269.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第十九章 第二夜：秘密...",
                   "chapter_url": "http://seputu.com/biji5/270.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十章 第二夜：反推...",
                   "chapter_url": "http://seputu.com/biji5/271.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十一章 第二夜：它...",
                   "chapter_url": "http://seputu.com/biji5/272.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十二章 第二夜：盲...",
                   "chapter_url": "http://seputu.com/biji5/273.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十三章 第二夜：影...",
                   "chapter_url": "http://seputu.com/biji5/274.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十四章 黎明：转移...",
                   "chapter_url": "http://seputu.com/biji5/275.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十五章 第三夜：浮...",
                   "chapter_url": "http://seputu.com/biji5/276.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十六章 第三夜：似...",
                   "chapter_url": "http://seputu.com/biji5/277.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十七章 第三夜：蛇...",
                   "chapter_url": "http://seputu.com/biji5/278.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十八章 第三夜：捕...",
                   "chapter_url": "http://seputu.com/biji5/279.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第二十九章 第三夜：暗...",
                   "chapter_url": "http://seputu.com/biji5/280.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十章 第三夜：泥潭...",
                   "chapter_url": "http://seputu.com/biji5/281.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十一章 第三夜：藏...",
                   "chapter_url": "http://seputu.com/biji5/282.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十二章 第三夜：又...",
                   "chapter_url": "http://seputu.com/biji5/283.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十三章 第三夜：宿...",
                   "chapter_url": "http://seputu.com/biji5/284.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十四章 第三夜：沼...",
                   "chapter_url": "http://seputu.com/biji5/285.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十五章 第三夜：鬼...",
                   "chapter_url": "http://seputu.com/biji5/286.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十六章 第三夜：雾...",
                   "chapter_url": "http://seputu.com/biji5/287.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十七章 第三夜：窥...",
                   "chapter_url": "http://seputu.com/biji5/288.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十八章 第三夜：毒...",
                   "chapter_url": "http://seputu.com/biji5/289.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第三十九章 第三夜：蛇...",
                   "chapter_url": "http://seputu.com/biji5/290.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第四十章 第三夜：获救...",
                   "chapter_url": "http://seputu.com/biji5/291.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第四十一章 第三夜：入...",
                   "chapter_url": "http://seputu.com/biji5/292.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第四十二章 第三夜：避...",
                   "chapter_url": "http://seputu.com/biji5/293.html"
               },
               {
                   "chapter_title": "蛇沼鬼城（下） 第四十三章 第三夜：录...",
                   "chapter_url": "http://seputu.com/biji5/294.html"
               },
               {
                   "chapter_title": "谜海归巢 第一章 集结号",
                   "chapter_url": "http://seputu.com/biji5/295.html"
               },
               {
                   "chapter_title": "谜海归巢 第二章 深入",
                   "chapter_url": "http://seputu.com/biji5/296.html"
               },
               {
                   "chapter_title": "谜海归巢 第三章 记号",
                   "chapter_url": "http://seputu.com/biji5/297.html"
               },
               {
                   "chapter_title": "谜海归巢 第四章 三选一",
                   "chapter_url": "http://seputu.com/biji5/298.html"
               },
               {
                   "chapter_title": "谜海归巢 第五章 真相",
                   "chapter_url": "http://seputu.com/biji5/299.html"
               },
               {
                   "chapter_title": "谜海归巢 第六章 颠覆",
                   "chapter_url": "http://seputu.com/biji5/300.html"
               },
               {
                   "chapter_title": "谜海归巢 第七章 囚禁",
                   "chapter_url": "http://seputu.com/biji5/301.html"
               },
               {
                   "chapter_title": "谜海归巢 第八章 会合",
                   "chapter_url": "http://seputu.com/biji5/302.html"
               },
               {
                   "chapter_title": "谜海归巢 第九章 记号的终点",
                   "chapter_url": "http://seputu.com/biji5/303.html"
               },
               {
                   "chapter_title": "谜海归巢 第十章 炼丹室",
                   "chapter_url": "http://seputu.com/biji5/304.html"
               },
               {
                   "chapter_title": "谜海归巢 第十一章 机关",
                   "chapter_url": "http://seputu.com/biji5/305.html"
               },
               {
                   "chapter_title": "谜海归巢 第十二章 近了",
                   "chapter_url": "http://seputu.com/biji5/306.html"
               },
               {
                   "chapter_title": "谜海归巢 第十三章 终点",
                   "chapter_url": "http://seputu.com/biji5/307.html"
               },
               {
                   "chapter_title": "谜海归巢 第十四章 天石",
                   "chapter_url": "http://seputu.com/biji5/308.html"
               },
               {
                   "chapter_title": "谜海归巢 第十五章 等待",
                   "chapter_url": "http://seputu.com/biji5/309.html"
               },
               {
                   "chapter_title": "谜海归巢 第十六章 继续等待",
                   "chapter_url": "http://seputu.com/biji5/310.html"
               },
               {
                   "chapter_title": "谜海归巢 第十七章 离开",
                   "chapter_url": "http://seputu.com/biji5/311.html"
               },
               {
                   "chapter_title": "谜海归巢 第十八章 陷坑",
                   "chapter_url": "http://seputu.com/biji5/312.html"
               },
               {
                   "chapter_title": "谜海归巢 第十九章 水壶",
                   "chapter_url": "http://seputu.com/biji5/313.html"
               },
               {
                   "chapter_title": "谜海归巢 第二十章 尾声（第一季大结...",
                   "chapter_url": "http://seputu.com/biji5/314.html"
               },
               {
                   "chapter_title": "第二季 引子 第一章 盗墓笔记",
                   "chapter_url": "http://seputu.com/biji5/315.html"
               },
               {
                   "chapter_title": "第二季 引子 第二章 讨论",
                   "chapter_url": "http://seputu.com/biji5/316.html"
               },
               {
                   "chapter_title": "第二季 引子 第三章 第二张老照片",
                   "chapter_url": "http://seputu.com/biji5/317.html"
               },
               {
                   "chapter_title": "第二季 引子 第四章 同病相怜之人",
                   "chapter_url": "http://seputu.com/biji5/318.html"
               },
               {
                   "chapter_title": "第二季 引子 第五章 再次出发",
                   "chapter_url": "http://seputu.com/biji5/319.html"
               },
               {
                   "chapter_title": "第二季 引子 第六章 继承",
                   "chapter_url": "http://seputu.com/biji5/320.html"
               },
               {
                   "chapter_title": "第二季 引子 第七章 影子传说",
                   "chapter_url": "http://seputu.com/biji5/321.html"
               },
               {
                   "chapter_title": "第二季 引子 第八章 照片的谜团",
                   "chapter_url": "http://seputu.com/biji5/322.html"
               },
               {
                   "chapter_title": "第二季 引子 第九章 档案",
                   "chapter_url": "http://seputu.com/biji5/323.html"
               },
               {
                   "chapter_title": "第二季 引子 第十章 老鼠",
                   "chapter_url": "http://seputu.com/biji5/324.html"
               },
               {
                   "chapter_title": "第二季 引子 第十一章 面人",
                   "chapter_url": "http://seputu.com/biji5/325.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记6阴山古楼",
           "round_detail": [
               {
                   "chapter_title": "阴山古楼 第一章 起源",
                   "chapter_url": "http://seputu.com/biji6/326.html"
               },
               {
                   "chapter_title": "阴山古楼 第二章 古怪的村子",
                   "chapter_url": "http://seputu.com/biji6/327.html"
               },
               {
                   "chapter_title": "阴山古楼 第三章 火灾",
                   "chapter_url": "http://seputu.com/biji6/328.html"
               },
               {
                   "chapter_title": "阴山古楼 第四章 变故",
                   "chapter_url": "http://seputu.com/biji6/329.html"
               },
               {
                   "chapter_title": "阴山古楼 第五章 巡山",
                   "chapter_url": "http://seputu.com/biji6/330.html"
               },
               {
                   "chapter_title": "阴山古楼 第六章 水牛头沟",
                   "chapter_url": "http://seputu.com/biji6/331.html"
               },
               {
                   "chapter_title": "阴山古楼 第七章 古坟",
                   "chapter_url": "http://seputu.com/biji6/332.html"
               },
               {
                   "chapter_title": "阴山古楼 第八章 老头",
                   "chapter_url": "http://seputu.com/biji6/333.html"
               },
               {
                   "chapter_title": "阴山古楼 第九章 盘马老爹",
                   "chapter_url": "http://seputu.com/biji6/334.html"
               },
               {
                   "chapter_title": "阴山古楼 第十章 坐下来谈",
                   "chapter_url": "http://seputu.com/biji6/335.html"
               },
               {
                   "chapter_title": "阴山古楼 第十一章 味道",
                   "chapter_url": "http://seputu.com/biji6/336.html"
               },
               {
                   "chapter_title": "阴山古楼 第十二章 盘马的回忆",
                   "chapter_url": "http://seputu.com/biji6/337.html"
               },
               {
                   "chapter_title": "阴山古楼 第十三章 心理战",
                   "chapter_url": "http://seputu.com/biji6/338.html"
               },
               {
                   "chapter_title": "阴山古楼 第十四章 那是一个魔湖",
                   "chapter_url": "http://seputu.com/biji6/339.html"
               },
               {
                   "chapter_title": "阴山古楼 第十五章 中邪",
                   "chapter_url": "http://seputu.com/biji6/340.html"
               },
               {
                   "chapter_title": "阴山古楼 第十六章 计划",
                   "chapter_url": "http://seputu.com/biji6/341.html"
               },
               {
                   "chapter_title": "阴山古楼 第十七章 似曾相识",
                   "chapter_url": "http://seputu.com/biji6/342.html"
               },
               {
                   "chapter_title": "阴山古楼 第十八章 脑筋急转弯",
                   "chapter_url": "http://seputu.com/biji6/343.html"
               },
               {
                   "chapter_title": "阴山古楼 第十九章 虹吸效应",
                   "chapter_url": "http://seputu.com/biji6/344.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十章 湖底",
                   "chapter_url": "http://seputu.com/biji6/345.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十一章 湖底的古寨",
                   "chapter_url": "http://seputu.com/biji6/346.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十二章 捞起来的怪物...",
                   "chapter_url": "http://seputu.com/biji6/347.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十三章 铁块",
                   "chapter_url": "http://seputu.com/biji6/348.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十四章 流水行程",
                   "chapter_url": "http://seputu.com/biji6/349.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十五章 心理战2",
                   "chapter_url": "http://seputu.com/biji6/350.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十六章 风雨无阻",
                   "chapter_url": "http://seputu.com/biji6/351.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十七章 雨中魔影",
                   "chapter_url": "http://seputu.com/biji6/352.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十八章 魔湖的诡异",
                   "chapter_url": "http://seputu.com/biji6/353.html"
               },
               {
                   "chapter_title": "阴山古楼 第二十九章 独自下水",
                   "chapter_url": "http://seputu.com/biji6/354.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十章 老树蜇头",
                   "chapter_url": "http://seputu.com/biji6/355.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十一章 水底的灯光",
                   "chapter_url": "http://seputu.com/biji6/356.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十二章 瑶家大院",
                   "chapter_url": "http://seputu.com/biji6/357.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十三章 绿光",
                   "chapter_url": "http://seputu.com/biji6/358.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十四章 成真",
                   "chapter_url": "http://seputu.com/biji6/359.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十五章 影子的真面目...",
                   "chapter_url": "http://seputu.com/biji6/360.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十六章 后半部分在地...",
                   "chapter_url": "http://seputu.com/biji6/361.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十七章 胖子的小聪明...",
                   "chapter_url": "http://seputu.com/biji6/362.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十八章 玉脉",
                   "chapter_url": "http://seputu.com/biji6/363.html"
               },
               {
                   "chapter_title": "阴山古楼 第三十九章 奇洞",
                   "chapter_url": "http://seputu.com/biji6/364.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十章 洞里的问题",
                   "chapter_url": "http://seputu.com/biji6/365.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十一章 封闭空间",
                   "chapter_url": "http://seputu.com/biji6/366.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十二章 假设",
                   "chapter_url": "http://seputu.com/biji6/367.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十三章 挖出来的是什...",
                   "chapter_url": "http://seputu.com/biji6/368.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十四章 石中人",
                   "chapter_url": "http://seputu.com/biji6/369.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十五章 这里的石头",
                   "chapter_url": "http://seputu.com/biji6/370.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十六章 异变",
                   "chapter_url": "http://seputu.com/biji6/371.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十七章 怪物",
                   "chapter_url": "http://seputu.com/biji6/372.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十八章 火炭",
                   "chapter_url": "http://seputu.com/biji6/373.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十九章 有三十五个",
                   "chapter_url": "http://seputu.com/biji6/374.html"
               },
               {
                   "chapter_title": "阴山古楼 第四十九章 有三十五个",
                   "chapter_url": "http://seputu.com/biji6/375.html"
               },
               {
                   "chapter_title": "阴山古楼 第五十章 脱出",
                   "chapter_url": "http://seputu.com/biji6/376.html"
               },
               {
                   "chapter_title": "阴山古楼 第五十一章 二叔",
                   "chapter_url": "http://seputu.com/biji6/377.html"
               },
               {
                   "chapter_title": "阴山古楼 第五十二章 开心",
                   "chapter_url": "http://seputu.com/biji6/378.html"
               },
               {
                   "chapter_title": "阴山古楼 第五十三章 很像的寨子",
                   "chapter_url": "http://seputu.com/biji6/379.html"
               },
               {
                   "chapter_title": "阴山古楼 第五十四章 镜像阴谋",
                   "chapter_url": "http://seputu.com/biji6/380.html"
               },
               {
                   "chapter_title": "阴山古楼 第五十五章 不速之客",
                   "chapter_url": "http://seputu.com/biji6/381.html"
               },
               {
                   "chapter_title": "阴山古楼 第五十六章 使坏",
                   "chapter_url": "http://seputu.com/biji6/382.html"
               },
               {
                   "chapter_title": "邛笼石影 第一章 兜圈",
                   "chapter_url": "http://seputu.com/biji6/383.html"
               },
               {
                   "chapter_title": "邛笼石影 第二章 老档案",
                   "chapter_url": "http://seputu.com/biji6/384.html"
               },
               {
                   "chapter_title": "邛笼石影 第三章 笔迹",
                   "chapter_url": "http://seputu.com/biji6/385.html"
               },
               {
                   "chapter_title": "邛笼石影 第四章 找到了",
                   "chapter_url": "http://seputu.com/biji6/386.html"
               },
               {
                   "chapter_title": "邛笼石影 第五章 拍卖会",
                   "chapter_url": "http://seputu.com/biji6/387.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记7邛笼石影",
           "round_detail": [
               {
                   "chapter_title": "盗墓笔记7 第一章 拍卖",
                   "chapter_url": "http://seputu.com/biji7/388.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二章 霍霍霍霍（一）",
                   "chapter_url": "http://seputu.com/biji7/389.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二章 霍霍霍霍（二）",
                   "chapter_url": "http://seputu.com/biji7/390.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三章 收藏界的盛宴",
                   "chapter_url": "http://seputu.com/biji7/391.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四章 回忆（上）",
                   "chapter_url": "http://seputu.com/biji7/392.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五章 回忆（下）",
                   "chapter_url": "http://seputu.com/biji7/393.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第六章 点天灯",
                   "chapter_url": "http://seputu.com/biji7/394.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第七章 大闹天宫",
                   "chapter_url": "http://seputu.com/biji7/395.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第八章 霍秀秀",
                   "chapter_url": "http://seputu.com/biji7/396.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第九章 样式雷（上）",
                   "chapter_url": "http://seputu.com/biji7/397.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十章 奇怪的形容",
                   "chapter_url": "http://seputu.com/biji7/398.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十一章 考古队、楼和镜...",
                   "chapter_url": "http://seputu.com/biji7/399.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十二章 似是故人来",
                   "chapter_url": "http://seputu.com/biji7/400.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十三章 背负着一切的麒...",
                   "chapter_url": "http://seputu.com/biji7/401.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十四章 同居生活",
                   "chapter_url": "http://seputu.com/biji7/402.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十五章 背负着一切的麒...",
                   "chapter_url": "http://seputu.com/biji7/403.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十六章 鱼在我这里",
                   "chapter_url": "http://seputu.com/biji7/404.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十七章 长驱直入的秘密...",
                   "chapter_url": "http://seputu.com/biji7/405.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十八章 背负着一切的麒...",
                   "chapter_url": "http://seputu.com/biji7/406.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第十九章 信的故事",
                   "chapter_url": "http://seputu.com/biji7/407.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十章 史上最大盗墓活...",
                   "chapter_url": "http://seputu.com/biji7/408.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十一章 史上最大盗墓...",
                   "chapter_url": "http://seputu.com/biji7/409.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十二章 史上最大盗墓...",
                   "chapter_url": "http://seputu.com/biji7/410.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十三章 世上最大奇怪...",
                   "chapter_url": "http://seputu.com/biji7/411.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十三章 世上最大奇怪...",
                   "chapter_url": "http://seputu.com/biji7/412.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十四章 逆反心理",
                   "chapter_url": "http://seputu.com/biji7/413.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十五章 进入正题",
                   "chapter_url": "http://seputu.com/biji7/414.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十六章 夹喇嘛",
                   "chapter_url": "http://seputu.com/biji7/415.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十七章 样式雷（下）",
                   "chapter_url": "http://seputu.com/biji7/416.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十八章 计划",
                   "chapter_url": "http://seputu.com/biji7/417.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第二十九章 四川和分别",
                   "chapter_url": "http://seputu.com/biji7/418.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十章 流水",
                   "chapter_url": "http://seputu.com/biji7/419.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十一章 巢（上）",
                   "chapter_url": "http://seputu.com/biji7/420.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十二章 巢（下）",
                   "chapter_url": "http://seputu.com/biji7/421.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十三章 双线（一）",
                   "chapter_url": "http://seputu.com/biji7/422.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十三章 双线（二）",
                   "chapter_url": "http://seputu.com/biji7/423.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十四章 小头发",
                   "chapter_url": "http://seputu.com/biji7/424.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十五章 怪家伙",
                   "chapter_url": "http://seputu.com/biji7/425.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十六章 头发（一）",
                   "chapter_url": "http://seputu.com/biji7/426.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十六章 头发（二）",
                   "chapter_url": "http://seputu.com/biji7/427.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十七章 花鼓戏（一）",
                   "chapter_url": "http://seputu.com/biji7/428.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十七章 花鼓戏（二）",
                   "chapter_url": "http://seputu.com/biji7/429.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十八章 毛刺",
                   "chapter_url": "http://seputu.com/biji7/430.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十九章 寄生（一）",
                   "chapter_url": "http://seputu.com/biji7/431.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第三十九章 寄生（二）",
                   "chapter_url": "http://seputu.com/biji7/432.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十章 来自广西的提示...",
                   "chapter_url": "http://seputu.com/biji7/433.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十一章 奇怪铁盘上的...",
                   "chapter_url": "http://seputu.com/biji7/434.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十二章 浮雕补完",
                   "chapter_url": "http://seputu.com/biji7/435.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十三章 秘密",
                   "chapter_url": "http://seputu.com/biji7/436.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十四章 提示的诀窍",
                   "chapter_url": "http://seputu.com/biji7/437.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十五章 进入机关之内...",
                   "chapter_url": "http://seputu.com/biji7/438.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十五章 进入机关之内...",
                   "chapter_url": "http://seputu.com/biji7/439.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十六章 吊",
                   "chapter_url": "http://seputu.com/biji7/440.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十七章 黑毛",
                   "chapter_url": "http://seputu.com/biji7/441.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十八章 蛇咬",
                   "chapter_url": "http://seputu.com/biji7/442.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第四十九章 密码",
                   "chapter_url": "http://seputu.com/biji7/443.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十章 解开密码（一）",
                   "chapter_url": "http://seputu.com/biji7/444.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十章 解开密码（二）",
                   "chapter_url": "http://seputu.com/biji7/445.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十一章 成功者（一）",
                   "chapter_url": "http://seputu.com/biji7/446.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十一章 成功者（二）",
                   "chapter_url": "http://seputu.com/biji7/447.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十一章 成功者（三）",
                   "chapter_url": "http://seputu.com/biji7/448.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十二章 死亡错误",
                   "chapter_url": "http://seputu.com/biji7/449.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十三章 冷静（一）",
                   "chapter_url": "http://seputu.com/biji7/450.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十三章 冷静（二）",
                   "chapter_url": "http://seputu.com/biji7/451.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十四章 绝望",
                   "chapter_url": "http://seputu.com/biji7/452.html"
               },
               {
                   "chapter_title": "盗墓笔记7 第五十五章 轮回恐惧之面...",
                   "chapter_url": "http://seputu.com/biji7/453.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记8大结局",
           "round_detail": [
               {
                   "chapter_title": "盗墓笔记8 第一章（一）",
                   "chapter_url": "http://seputu.com/biji8/454.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第一章（二）",
                   "chapter_url": "http://seputu.com/biji8/455.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二章（一）",
                   "chapter_url": "http://seputu.com/biji8/456.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二章（二）",
                   "chapter_url": "http://seputu.com/biji8/457.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三章（一）",
                   "chapter_url": "http://seputu.com/biji8/458.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三章（二）",
                   "chapter_url": "http://seputu.com/biji8/459.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四章（一）",
                   "chapter_url": "http://seputu.com/biji8/460.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四章（二）",
                   "chapter_url": "http://seputu.com/biji8/461.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五章（二）",
                   "chapter_url": "http://seputu.com/biji8/462.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五章（一）",
                   "chapter_url": "http://seputu.com/biji8/463.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六章（一）",
                   "chapter_url": "http://seputu.com/biji8/464.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六章（二）",
                   "chapter_url": "http://seputu.com/biji8/465.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七章（一）",
                   "chapter_url": "http://seputu.com/biji8/466.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七章（二）",
                   "chapter_url": "http://seputu.com/biji8/467.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第八章（一）",
                   "chapter_url": "http://seputu.com/biji8/468.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第八章（二）",
                   "chapter_url": "http://seputu.com/biji8/469.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第九章（一）",
                   "chapter_url": "http://seputu.com/biji8/470.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第九章（二）",
                   "chapter_url": "http://seputu.com/biji8/471.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十章（一）",
                   "chapter_url": "http://seputu.com/biji8/472.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十章（二）",
                   "chapter_url": "http://seputu.com/biji8/473.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十一章（一）",
                   "chapter_url": "http://seputu.com/biji8/474.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十一章（二）",
                   "chapter_url": "http://seputu.com/biji8/475.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十二章（一）",
                   "chapter_url": "http://seputu.com/biji8/476.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十二章（二）",
                   "chapter_url": "http://seputu.com/biji8/477.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十三章（一）",
                   "chapter_url": "http://seputu.com/biji8/478.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十三章（二）",
                   "chapter_url": "http://seputu.com/biji8/479.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十四章（一）",
                   "chapter_url": "http://seputu.com/biji8/480.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十四章（二）",
                   "chapter_url": "http://seputu.com/biji8/481.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十五章（一）",
                   "chapter_url": "http://seputu.com/biji8/482.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十五章（二）",
                   "chapter_url": "http://seputu.com/biji8/483.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十六章（一）",
                   "chapter_url": "http://seputu.com/biji8/484.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十六章（二）",
                   "chapter_url": "http://seputu.com/biji8/485.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十七章（一）",
                   "chapter_url": "http://seputu.com/biji8/486.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十七章（二）",
                   "chapter_url": "http://seputu.com/biji8/487.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十八章（一）",
                   "chapter_url": "http://seputu.com/biji8/488.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十八章（二）",
                   "chapter_url": "http://seputu.com/biji8/489.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第十九章",
                   "chapter_url": "http://seputu.com/biji8/490.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十章",
                   "chapter_url": "http://seputu.com/biji8/491.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十一章",
                   "chapter_url": "http://seputu.com/biji8/492.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十二章",
                   "chapter_url": "http://seputu.com/biji8/493.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十三章",
                   "chapter_url": "http://seputu.com/biji8/494.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十四章",
                   "chapter_url": "http://seputu.com/biji8/495.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十五章",
                   "chapter_url": "http://seputu.com/biji8/496.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十六章",
                   "chapter_url": "http://seputu.com/biji8/497.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十七章",
                   "chapter_url": "http://seputu.com/biji8/498.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十八章",
                   "chapter_url": "http://seputu.com/biji8/499.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第二十九章",
                   "chapter_url": "http://seputu.com/biji8/500.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十章",
                   "chapter_url": "http://seputu.com/biji8/501.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十一章",
                   "chapter_url": "http://seputu.com/biji8/502.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十二章",
                   "chapter_url": "http://seputu.com/biji8/503.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十三章",
                   "chapter_url": "http://seputu.com/biji8/504.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十四章",
                   "chapter_url": "http://seputu.com/biji8/505.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十五章",
                   "chapter_url": "http://seputu.com/biji8/506.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十六章",
                   "chapter_url": "http://seputu.com/biji8/507.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十七章",
                   "chapter_url": "http://seputu.com/biji8/508.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十八章",
                   "chapter_url": "http://seputu.com/biji8/509.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第三十九章",
                   "chapter_url": "http://seputu.com/biji8/510.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十章",
                   "chapter_url": "http://seputu.com/biji8/511.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十一章",
                   "chapter_url": "http://seputu.com/biji8/512.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十二章",
                   "chapter_url": "http://seputu.com/biji8/513.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十三章",
                   "chapter_url": "http://seputu.com/biji8/514.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十四章",
                   "chapter_url": "http://seputu.com/biji8/515.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十五章",
                   "chapter_url": "http://seputu.com/biji8/516.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十六章",
                   "chapter_url": "http://seputu.com/biji8/517.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十七章",
                   "chapter_url": "http://seputu.com/biji8/518.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十八章",
                   "chapter_url": "http://seputu.com/biji8/519.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第四十九章",
                   "chapter_url": "http://seputu.com/biji8/520.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十章",
                   "chapter_url": "http://seputu.com/biji8/521.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十一章",
                   "chapter_url": "http://seputu.com/biji8/522.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十二章",
                   "chapter_url": "http://seputu.com/biji8/523.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十三章",
                   "chapter_url": "http://seputu.com/biji8/524.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十四章",
                   "chapter_url": "http://seputu.com/biji8/525.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十五章",
                   "chapter_url": "http://seputu.com/biji8/526.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十六章",
                   "chapter_url": "http://seputu.com/biji8/527.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十七章",
                   "chapter_url": "http://seputu.com/biji8/528.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十八章",
                   "chapter_url": "http://seputu.com/biji8/529.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第五十九章",
                   "chapter_url": "http://seputu.com/biji8/530.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十章",
                   "chapter_url": "http://seputu.com/biji8/531.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十一章",
                   "chapter_url": "http://seputu.com/biji8/532.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十二章",
                   "chapter_url": "http://seputu.com/biji8/533.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十三章",
                   "chapter_url": "http://seputu.com/biji8/534.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十四章",
                   "chapter_url": "http://seputu.com/biji8/535.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十五章",
                   "chapter_url": "http://seputu.com/biji8/536.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十六章",
                   "chapter_url": "http://seputu.com/biji8/537.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十七章",
                   "chapter_url": "http://seputu.com/biji8/538.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十八章",
                   "chapter_url": "http://seputu.com/biji8/539.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第六十九章",
                   "chapter_url": "http://seputu.com/biji8/540.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十章",
                   "chapter_url": "http://seputu.com/biji8/541.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十一章",
                   "chapter_url": "http://seputu.com/biji8/542.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十二章",
                   "chapter_url": "http://seputu.com/biji8/543.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十三章",
                   "chapter_url": "http://seputu.com/biji8/544.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十四章",
                   "chapter_url": "http://seputu.com/biji8/545.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十五章",
                   "chapter_url": "http://seputu.com/biji8/546.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十六章",
                   "chapter_url": "http://seputu.com/biji8/547.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十七章",
                   "chapter_url": "http://seputu.com/biji8/548.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十八章",
                   "chapter_url": "http://seputu.com/biji8/549.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第七十九章",
                   "chapter_url": "http://seputu.com/biji8/550.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第八十章",
                   "chapter_url": "http://seputu.com/biji8/551.html"
               },
               {
                   "chapter_title": "盗墓笔记8 第八十一章",
                   "chapter_url": "http://seputu.com/biji8/552.html"
               }
           ]
       },
       {
           "round_title": "藏海花在线试读",
           "round_detail": [
               {
                   "chapter_title": "藏海花 第一章 起源",
                   "chapter_url": "http://seputu.com/zanghaihua/591.html"
               },
               {
                   "chapter_title": "藏海花 第二章 第一件怪事（上）",
                   "chapter_url": "http://seputu.com/zanghaihua/592.html"
               },
               {
                   "chapter_title": "藏海花 第三章 第一件怪事（下）",
                   "chapter_url": "http://seputu.com/zanghaihua/593.html"
               },
               {
                   "chapter_title": "藏海花 第四章 第二件怪事",
                   "chapter_url": "http://seputu.com/zanghaihua/594.html"
               },
               {
                   "chapter_title": "藏海花 第五章 轮回的开端(1)",
                   "chapter_url": "http://seputu.com/zanghaihua/595.html"
               },
               {
                   "chapter_title": "藏海花 第五章 轮回的开端(2) - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/596.html"
               },
               {
                   "chapter_title": "藏海花 第六章 命运的重启(1) - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/597.html"
               },
               {
                   "chapter_title": "藏海花 第六章 命运的重启(2) - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/598.html"
               },
               {
                   "chapter_title": "藏海花 第七章 西藏油画(1) - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/599.html"
               },
               {
                   "chapter_title": "藏海花 第七章 西藏油画(2) - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/600.html"
               },
               {
                   "chapter_title": "藏海花 第八章 一座喇嘛庙(1) - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/601.html"
               },
               {
                   "chapter_title": "藏海花 第八章 一座喇嘛庙(2) - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/602.html"
               },
               {
                   "chapter_title": "藏海花 第九章 关于闷油瓶的关键线...",
                   "chapter_url": "http://seputu.com/zanghaihua/603.html"
               },
               {
                   "chapter_title": "藏海花 第十章 闷油瓶的往事 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/604.html"
               },
               {
                   "chapter_title": "藏海花 第十一章 比黄金还贵的黄金...",
                   "chapter_url": "http://seputu.com/zanghaihua/605.html"
               },
               {
                   "chapter_title": "藏海花 第十二章 进入雪山 - 盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/606.html"
               },
               {
                   "chapter_title": "藏海花 第十三章 关于世界终极的笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/607.html"
               },
               {
                   "chapter_title": "藏海花 第十四章 极限的秘密 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/608.html"
               },
               {
                   "chapter_title": "藏海花 第十五章 雪山里的神秘部落...",
                   "chapter_url": "http://seputu.com/zanghaihua/609.html"
               },
               {
                   "chapter_title": "藏海花 第十六章 守护者 - 盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/610.html"
               },
               {
                   "chapter_title": "藏海花 第十七章 冰封的神湖 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/611.html"
               },
               {
                   "chapter_title": "藏海花 第十八章 尸香 - 盗墓笔记",
                   "chapter_url": "http://seputu.com/zanghaihua/612.html"
               },
               {
                   "chapter_title": "藏海花 第十九章 阎王骑尸 - 盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/613.html"
               },
               {
                   "chapter_title": "藏海花 第二十章 独立于其他文明的...",
                   "chapter_url": "http://seputu.com/zanghaihua/614.html"
               },
               {
                   "chapter_title": "藏海花 第二十一章 闷油瓶出现了 -...",
                   "chapter_url": "http://seputu.com/zanghaihua/615.html"
               },
               {
                   "chapter_title": "藏海花 第二十二章 召唤胖子 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/616.html"
               },
               {
                   "chapter_title": "藏海花 第二十三章 西藏的天罗地网...",
                   "chapter_url": "http://seputu.com/zanghaihua/617.html"
               },
               {
                   "chapter_title": "藏海花 第二十四章 惊人的细节 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/618.html"
               },
               {
                   "chapter_title": "藏海花 第二十五章 不知道从何而来...",
                   "chapter_url": "http://seputu.com/zanghaihua/619.html"
               },
               {
                   "chapter_title": "藏海花 第二十六章 与张家人正面交...",
                   "chapter_url": "http://seputu.com/zanghaihua/620.html"
               },
               {
                   "chapter_title": "藏海花 第二十七章 七个吴邪 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/621.html"
               },
               {
                   "chapter_title": "藏海花 第二十八章 艰难的选择 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/622.html"
               },
               {
                   "chapter_title": "藏海花 第二十九章 分崩离析的张家...",
                   "chapter_url": "http://seputu.com/zanghaihua/623.html"
               },
               {
                   "chapter_title": "藏海花 第三十章 汪藏海的千年伏笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/624.html"
               },
               {
                   "chapter_title": "藏海花 第三十一章 胖子的实力(1) ...",
                   "chapter_url": "http://seputu.com/zanghaihua/625.html"
               },
               {
                   "chapter_title": "藏海花 第三十一章 胖子的实力(2) ...",
                   "chapter_url": "http://seputu.com/zanghaihua/626.html"
               },
               {
                   "chapter_title": "藏海花 第三十二章 胖子的保险措施...",
                   "chapter_url": "http://seputu.com/zanghaihua/627.html"
               },
               {
                   "chapter_title": "藏海花 第三十三章 差点死了 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/628.html"
               },
               {
                   "chapter_title": "藏海花 第三十四章 奇怪的变动 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/629.html"
               },
               {
                   "chapter_title": "藏海花 第三十五章 人全部都消失了...",
                   "chapter_url": "http://seputu.com/zanghaihua/630.html"
               },
               {
                   "chapter_title": "藏海花 第三十六章 喇嘛庙封引 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/631.html"
               },
               {
                   "chapter_title": "藏海花 第三十七章 枚举之王 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/632.html"
               },
               {
                   "chapter_title": "藏海花 第三十八章 脱身(1) - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/633.html"
               },
               {
                   "chapter_title": "藏海花 第三十八章 脱身(2) - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/634.html"
               },
               {
                   "chapter_title": "藏海花 第三十九章 血竭 - 盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/635.html"
               },
               {
                   "chapter_title": "藏海花 第四十章 误会 - 盗墓笔记",
                   "chapter_url": "http://seputu.com/zanghaihua/636.html"
               },
               {
                   "chapter_title": "藏海花 第四十一章 黄粱一梦 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/637.html"
               },
               {
                   "chapter_title": "藏海花 第四十二章 张海杏 - 盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/638.html"
               },
               {
                   "chapter_title": "藏海花 第四十三章 闷油瓶十三岁 -...",
                   "chapter_url": "http://seputu.com/zanghaihua/639.html"
               },
               {
                   "chapter_title": "藏海花 第四十四章 放野 - 盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/640.html"
               },
               {
                   "chapter_title": "藏海花 第四十五章 离奇的墓穴 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/641.html"
               },
               {
                   "chapter_title": "藏海花 第四十六章 倒挂着的棺材 -...",
                   "chapter_url": "http://seputu.com/zanghaihua/642.html"
               },
               {
                   "chapter_title": "藏海花 第四十七章 问题的所在 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/643.html"
               },
               {
                   "chapter_title": "藏海花 第四十八章 奇怪的机关 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/644.html"
               },
               {
                   "chapter_title": "藏海花 第四十九章 临卡 - 盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/645.html"
               },
               {
                   "chapter_title": "藏海花 第五十章 泥浆池 - 盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/646.html"
               },
               {
                   "chapter_title": "藏海花 第五十一章 他们的发现 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/647.html"
               },
               {
                   "chapter_title": "藏海花 第五十二章 绝境 - 盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/648.html"
               },
               {
                   "chapter_title": "藏海花 第五十三章 爆炸之后的意外...",
                   "chapter_url": "http://seputu.com/zanghaihua/649.html"
               },
               {
                   "chapter_title": "藏海花 第五十四章 快速出发 - 盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/650.html"
               },
               {
                   "chapter_title": "藏海花 第五十五章 往回走 - 盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/651.html"
               },
               {
                   "chapter_title": "藏海花 第五十六章 喇嘛庙 - 盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/652.html"
               },
               {
                   "chapter_title": "藏海花 第五十七章 之前的情况 - 盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/653.html"
               },
               {
                   "chapter_title": "藏海花 第五十八章 山下面的东西 -...",
                   "chapter_url": "http://seputu.com/zanghaihua/654.html"
               },
               {
                   "chapter_title": "藏海花2 第一章 问题的所在_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/655.html"
               },
               {
                   "chapter_title": "藏海花2 第二章 奇怪的机关_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/656.html"
               },
               {
                   "chapter_title": "藏海花2 第三章 临卡_藏海花2在线阅...",
                   "chapter_url": "http://seputu.com/zanghaihua/657.html"
               },
               {
                   "chapter_title": "藏海花2 第四章 泥浆池_藏海花2在线...",
                   "chapter_url": "http://seputu.com/zanghaihua/658.html"
               },
               {
                   "chapter_title": "藏海花2 第五章 脚下的古城_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/659.html"
               },
               {
                   "chapter_title": "藏海花2 第六章 他们的发现_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/660.html"
               },
               {
                   "chapter_title": "藏海花2 第七章 绝境_藏海花2在线阅...",
                   "chapter_url": "http://seputu.com/zanghaihua/661.html"
               },
               {
                   "chapter_title": "藏海花2 第八章 之后的意外_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/662.html"
               },
               {
                   "chapter_title": "藏海花2 第九章 快速出发_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/663.html"
               },
               {
                   "chapter_title": "藏海花 第十章 往回走_藏海花2在线...",
                   "chapter_url": "http://seputu.com/zanghaihua/664.html"
               },
               {
                   "chapter_title": "藏海花2 第十一章 喇嘛庙_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/665.html"
               },
               {
                   "chapter_title": "藏海花2 第12章 之前的情况_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/666.html"
               },
               {
                   "chapter_title": "藏海花2 第十三章 山下面的东西_藏...",
                   "chapter_url": "http://seputu.com/zanghaihua/667.html"
               },
               {
                   "chapter_title": "藏海花2 第十四章 青铜门的奥秘_藏...",
                   "chapter_url": "http://seputu.com/zanghaihua/668.html"
               },
               {
                   "chapter_title": "藏海花2 第十五章 影子_藏海花2在线...",
                   "chapter_url": "http://seputu.com/zanghaihua/669.html"
               },
               {
                   "chapter_title": "藏海花2 第十六章 青铜门开_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/670.html"
               },
               {
                   "chapter_title": "藏海花2 第十七章 不可能存在的洞穴...",
                   "chapter_url": "http://seputu.com/zanghaihua/671.html"
               },
               {
                   "chapter_title": "藏海花2 第十八章 青铜门后_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/672.html"
               },
               {
                   "chapter_title": "藏海花2 第十九章 终极的秘密_藏海...",
                   "chapter_url": "http://seputu.com/zanghaihua/673.html"
               },
               {
                   "chapter_title": "藏海花2 第二十章 无法理解的谜语_...",
                   "chapter_url": "http://seputu.com/zanghaihua/674.html"
               },
               {
                   "chapter_title": "藏海花2 第二十一章 张家的内部体系...",
                   "chapter_url": "http://seputu.com/zanghaihua/675.html"
               },
               {
                   "chapter_title": "藏海花2 第二十二章 最大的秘密_藏...",
                   "chapter_url": "http://seputu.com/zanghaihua/676.html"
               },
               {
                   "chapter_title": "藏海花2 第二十三章 麒麟血_藏海花...",
                   "chapter_url": "http://seputu.com/zanghaihua/677.html"
               },
               {
                   "chapter_title": "藏海花2 第二十四章 换种思维方式_...",
                   "chapter_url": "http://seputu.com/zanghaihua/678.html"
               },
               {
                   "chapter_title": "藏海花2 第二十五章 来这里的理由_...",
                   "chapter_url": "http://seputu.com/zanghaihua/679.html"
               },
               {
                   "chapter_title": "藏海花2 第二十六章 真正的仇恨_藏...",
                   "chapter_url": "http://seputu.com/zanghaihua/680.html"
               },
               {
                   "chapter_title": "藏海花2 第二十七章 无比混乱的局面...",
                   "chapter_url": "http://seputu.com/zanghaihua/681.html"
               },
               {
                   "chapter_title": "藏海花2 第二十八章 那个巨大的东西...",
                   "chapter_url": "http://seputu.com/zanghaihua/682.html"
               },
               {
                   "chapter_title": "藏海花2 第二十九章 所有相关的细节...",
                   "chapter_url": "http://seputu.com/zanghaihua/683.html"
               },
               {
                   "chapter_title": "藏海花2 第三十章 改变立场的原因_...",
                   "chapter_url": "http://seputu.com/zanghaihua/684.html"
               },
               {
                   "chapter_title": "藏海花2 第三十一章 对付那群东西_...",
                   "chapter_url": "http://seputu.com/zanghaihua/685.html"
               },
               {
                   "chapter_title": "藏海花2 第三十二章 出现_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/686.html"
               },
               {
                   "chapter_title": "藏海花2 第三十三章 三个要素齐备_...",
                   "chapter_url": "http://seputu.com/zanghaihua/687.html"
               },
               {
                   "chapter_title": "藏海花2 第二部第三十四章 有点感觉...",
                   "chapter_url": "http://seputu.com/zanghaihua/688.html"
               },
               {
                   "chapter_title": "藏海花2 第三十五章 石头脑袋_藏海...",
                   "chapter_url": "http://seputu.com/zanghaihua/689.html"
               },
               {
                   "chapter_title": "藏海花2 第三十六章 炸了_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/690.html"
               },
               {
                   "chapter_title": "藏海花2 第三十七章 阎王的秘密_藏...",
                   "chapter_url": "http://seputu.com/zanghaihua/691.html"
               },
               {
                   "chapter_title": "藏海花2 第三十八章 小哥_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/692.html"
               },
               {
                   "chapter_title": "藏海花2 第三十九章 小哥和胖子说了...",
                   "chapter_url": "http://seputu.com/zanghaihua/693.html"
               },
               {
                   "chapter_title": "藏海花2 第四十章 掉落_藏海花2在线...",
                   "chapter_url": "http://seputu.com/zanghaihua/694.html"
               },
               {
                   "chapter_title": "藏海花2 第四十一章 车间_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/695.html"
               },
               {
                   "chapter_title": "藏海花2 第四十二章 尸王_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/696.html"
               },
               {
                   "chapter_title": "藏海花2 第四十三章 白沙_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/697.html"
               },
               {
                   "chapter_title": "藏海花2 第四十四章 宗教_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/698.html"
               },
               {
                   "chapter_title": "藏海花2 第四十五章 重启_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/699.html"
               },
               {
                   "chapter_title": "藏海花2 第四十六章 陷阱_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/700.html"
               },
               {
                   "chapter_title": "藏海花2 第四十七章 原因_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/701.html"
               },
               {
                   "chapter_title": "藏海花2 第四十八章 解密_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/702.html"
               },
               {
                   "chapter_title": "藏海花2 第四十九章 脱出_藏海花2在...",
                   "chapter_url": "http://seputu.com/zanghaihua/703.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第一章 失踪_盗墓笔记9在...",
                   "chapter_url": "http://seputu.com/zanghaihua/704.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第十五章 密谈_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/705.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第十六章 袭击_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/706.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第十七章 逃亡_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/707.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第十八章 路人甲_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/708.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第十九章 尸体_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/709.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十章 通道_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/710.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十一章 地下河_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/711.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十二章 危机_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/712.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十三章 相遇_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/713.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十四章 回忆(上)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/714.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十五章 回忆(中)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/715.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十六章 回忆（下）_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/716.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十七章 鉴_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/717.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十八章 鬼打墙_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/718.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第二十九章 生病_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/719.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十章 冲突_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/720.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十一章 松达剌人_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/721.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十二章 绝密档案_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/722.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十三章 扎营_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/723.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十四章 麒麟吼_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/724.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十五章 变故_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/725.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十六章 狼群围猎_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/726.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十七章 时间之轴_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/727.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十八章 回忆_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/728.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第三十九章 蓝光_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/729.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十章 血脸_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/730.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十一章 鬼脸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/731.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十二章 坠崖_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/732.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十三章 会师_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/733.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十四章 殒玉_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/734.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十五章 怪石_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/735.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十六章 记忆之门_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/736.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十七章 合作_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/737.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十八章 真相_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/738.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第四十九章 摸金校尉_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/739.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十章 情义_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/740.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十一章 下水_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/741.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十二章 攀岩_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/742.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十三章 棺椁_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/743.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十四章 鬼语_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/744.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十五章 应声虫_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/745.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十六章 大萝卜_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/746.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十七章 火龙_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/747.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十八章 生死一线_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/748.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第五十九章 殉葬坑_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/749.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十章 孩尸_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/750.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十一章 二叔_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/751.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十二章 不吹灯_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/752.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十三章 不存在的三角...",
                   "chapter_url": "http://seputu.com/zanghaihua/753.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十四章 出路_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/754.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十五章 死亡_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/755.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十六章 尸煞_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/756.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十七章 做戏_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/757.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十八章 改造_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/758.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第六十九章 石棺_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/759.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十章 粽子_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/760.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十一章 利用_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/761.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十二章 悬尸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/762.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十三章 青铜棺_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/763.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十四章 黑影_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/764.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十五章 洞口_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/765.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十六章 疗伤_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/766.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十七章 分析_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/767.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十八章 金黑子_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/768.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第七十九章 龙抬头_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/769.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第八十章 夜光_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/770.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第八十一章 丧魂灯_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/771.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第八十二章 青铜人俑_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/772.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第八十三章 三叔_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/773.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第八十四章 送行_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/774.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第八十五章 狼窟_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/775.html"
               },
               {
                   "chapter_title": "昆仑狼窟 第八十六章 生死雪域_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/776.html"
               },
               {
                   "chapter_title": "无声之城 第一章 祖宅_盗墓笔记9在...",
                   "chapter_url": "http://seputu.com/zanghaihua/777.html"
               },
               {
                   "chapter_title": "无声之城 第二章 出逃_盗墓笔记9在...",
                   "chapter_url": "http://seputu.com/zanghaihua/778.html"
               },
               {
                   "chapter_title": "无声之城 第五章 张博士_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/779.html"
               },
               {
                   "chapter_title": "无声之城 第六章 雅布达_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/780.html"
               },
               {
                   "chapter_title": "无声之城 第七章 出卖_盗墓笔记9在...",
                   "chapter_url": "http://seputu.com/zanghaihua/781.html"
               },
               {
                   "chapter_title": "无声之城 第八章 打架_盗墓笔记9在...",
                   "chapter_url": "http://seputu.com/zanghaihua/782.html"
               },
               {
                   "chapter_title": "无声之城 第九章 金算子_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/783.html"
               },
               {
                   "chapter_title": "无声之城 第十章 鬼梭梭_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/784.html"
               },
               {
                   "chapter_title": "无声之城 第十一章 扎营_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/785.html"
               },
               {
                   "chapter_title": "无声之城 第十二章 沉沙_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/786.html"
               },
               {
                   "chapter_title": "无声之城 第十三章 绿洲_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/787.html"
               },
               {
                   "chapter_title": "无声之城 第十四章 考察队_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/788.html"
               },
               {
                   "chapter_title": "无声之城 第十五章 叛变_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/789.html"
               },
               {
                   "chapter_title": "无声之城 第十六章 人头_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/790.html"
               },
               {
                   "chapter_title": "无声之城 第十七章 魔鬼蔓藤_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/791.html"
               },
               {
                   "chapter_title": "无声之城 第十八章 仙人掌_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/792.html"
               },
               {
                   "chapter_title": "无声之城 第十九章 丛林怪物_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/793.html"
               },
               {
                   "chapter_title": "无声之城 第二十章 离开_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/794.html"
               },
               {
                   "chapter_title": "无声之城 第二十一章 基因力量_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/795.html"
               },
               {
                   "chapter_title": "无声之城 第二十二章 无声爱情_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/796.html"
               },
               {
                   "chapter_title": "无声之城 第二十三章 寄生_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/797.html"
               },
               {
                   "chapter_title": "无声之城 第二十四章 红头蝎_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/798.html"
               },
               {
                   "chapter_title": "无声之城 第二十五章 地窖_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/799.html"
               },
               {
                   "chapter_title": "无声之城 第二十六章 封石_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/800.html"
               },
               {
                   "chapter_title": "无声之城 第二十七章 尸玉_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/801.html"
               },
               {
                   "chapter_title": "无声之城 第二十八章 移动的入口_盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/802.html"
               },
               {
                   "chapter_title": "无声之城 第二十九章 磁场效应_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/803.html"
               },
               {
                   "chapter_title": "无声之城 第三十章 空间扭曲_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/804.html"
               },
               {
                   "chapter_title": "无声之城 第三十一章 黑瘤_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/805.html"
               },
               {
                   "chapter_title": "无声之城 第三十二章 争锋相对_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/806.html"
               },
               {
                   "chapter_title": "无声之城 第三十三章 拔_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/807.html"
               },
               {
                   "chapter_title": "无声之城 第三十四章 骗局_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/808.html"
               },
               {
                   "chapter_title": "无声之城 第三十五章 迷雾重重_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/809.html"
               },
               {
                   "chapter_title": "无声之城 第三十六章 麒麟石柱_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/810.html"
               },
               {
                   "chapter_title": "无声之城 第三十七章 大地黑蟒_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/811.html"
               },
               {
                   "chapter_title": "无声之城 第三十八章 流沙_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/812.html"
               },
               {
                   "chapter_title": "无声之城 第三十九章 蛇窝_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/813.html"
               },
               {
                   "chapter_title": "无声之城 第四十章 人头蛇_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/814.html"
               },
               {
                   "chapter_title": "无声之城 第四十一章 ZOJP_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/815.html"
               },
               {
                   "chapter_title": "无声之城 第四十二章 意外消息_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/816.html"
               },
               {
                   "chapter_title": "无声之城 第四十三章 寻找_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/817.html"
               },
               {
                   "chapter_title": "无声之城 第四十四章 炖牛肉_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/818.html"
               },
               {
                   "chapter_title": "无声之城 第四十五章 腐尸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/819.html"
               },
               {
                   "chapter_title": "无声之城 第四十六章 将错就错_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/820.html"
               },
               {
                   "chapter_title": "无声之城 第四十七章 门外有鬼_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/821.html"
               },
               {
                   "chapter_title": "无声之城 第四十八章 骸骨_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/822.html"
               },
               {
                   "chapter_title": "无声之城 第四十九章 炸药_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/823.html"
               },
               {
                   "chapter_title": "无声之城 第五十章 地洞_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/824.html"
               },
               {
                   "chapter_title": "无声之城 第五十一章 小金毛_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/825.html"
               },
               {
                   "chapter_title": "无声之城 第五十二章 德国目标_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/826.html"
               },
               {
                   "chapter_title": "无声之城 第五十三章 爆炸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/827.html"
               },
               {
                   "chapter_title": "无声之城 第五十四章 机关铃铛_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/828.html"
               },
               {
                   "chapter_title": "无声之城 第五十五章 麒麟吐珠(上)...",
                   "chapter_url": "http://seputu.com/zanghaihua/829.html"
               },
               {
                   "chapter_title": "无声之城 第五十六章 麒麟吐珠(下)...",
                   "chapter_url": "http://seputu.com/zanghaihua/830.html"
               },
               {
                   "chapter_title": "无声之城 第五十七章 地形_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/831.html"
               },
               {
                   "chapter_title": "无声之城 第五十八章 红丹_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/832.html"
               },
               {
                   "chapter_title": "无声之城 第五十九章 血尸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/833.html"
               },
               {
                   "chapter_title": "无声之城 第六十章 幻象_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/834.html"
               },
               {
                   "chapter_title": "无声之城 第六十一章 青铜鼎_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/835.html"
               },
               {
                   "chapter_title": "无声之城 第六十二章 寻尸带_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/836.html"
               },
               {
                   "chapter_title": "无声之城 第六十三章 尸魁_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/837.html"
               },
               {
                   "chapter_title": "无声之城 第六十四章 水流洞_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/838.html"
               },
               {
                   "chapter_title": "无声之城 第六十五章 侮辱_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/839.html"
               },
               {
                   "chapter_title": "无声之城 第六十六章 中招_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/840.html"
               },
               {
                   "chapter_title": "无声之城 第六十七章 中毒(上)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/841.html"
               },
               {
                   "chapter_title": "无声之城 第六十八章 中毒(下)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/842.html"
               },
               {
                   "chapter_title": "无声之城 第六十九章 石蜡壁画_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/843.html"
               },
               {
                   "chapter_title": "无声之城 第七十章 十八层地狱_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/844.html"
               },
               {
                   "chapter_title": "无声之城 第七十一章 古尸(上)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/845.html"
               },
               {
                   "chapter_title": "无声之城 第七十二章 古尸(下)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/846.html"
               },
               {
                   "chapter_title": "无声之城 第七十三章 漠视_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/847.html"
               },
               {
                   "chapter_title": "无声之城 第七十四章 分头行动_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/848.html"
               },
               {
                   "chapter_title": "无声之城 第七十五章 意外之敌_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/849.html"
               },
               {
                   "chapter_title": "无声之城 第七十六章 孤立无援_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/850.html"
               },
               {
                   "chapter_title": "无声之城 第七十九章 变鬼_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/851.html"
               },
               {
                   "chapter_title": "无声之城 第八十章 朱砂_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/852.html"
               },
               {
                   "chapter_title": "无声之城 第八十一章 裂变_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/853.html"
               },
               {
                   "chapter_title": "无声之城 第八十二章 地下十七层_盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/854.html"
               },
               {
                   "chapter_title": "无声之城 第八十三章 天宝琉璃双龙...",
                   "chapter_url": "http://seputu.com/zanghaihua/855.html"
               },
               {
                   "chapter_title": "无声之城 第八十四章 天宝琉璃双龙...",
                   "chapter_url": "http://seputu.com/zanghaihua/856.html"
               },
               {
                   "chapter_title": "无声之城 第八十五章 报应_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/857.html"
               },
               {
                   "chapter_title": "无声之城 第八十六章 闷油瓶_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/858.html"
               },
               {
                   "chapter_title": "无声之城 第八十七章 悬空棺_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/859.html"
               },
               {
                   "chapter_title": "无声之城 第八十八章 深入地底_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/860.html"
               },
               {
                   "chapter_title": "无声之城 第八十九章 黄泉阴兵_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/861.html"
               },
               {
                   "chapter_title": "无声之城 第九十章 环形空间_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/862.html"
               },
               {
                   "chapter_title": "无声之城 第九十一章 天梯_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/863.html"
               },
               {
                   "chapter_title": "无声之城 第九十二章 间歇泉_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/864.html"
               },
               {
                   "chapter_title": "无声之城 第九十三章 夜宿_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/865.html"
               },
               {
                   "chapter_title": "巫山妖棺 第一章 接应驼队_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/866.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二章 钥匙_盗墓笔记9在...",
                   "chapter_url": "http://seputu.com/zanghaihua/867.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三章 暗流涌动_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/868.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四章 夜探祖宅(上)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/869.html"
               },
               {
                   "chapter_title": "巫山妖棺 第五章 夜探祖宅(中)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/870.html"
               },
               {
                   "chapter_title": "巫山妖棺 第六章 夜探祖宅(下)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/871.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七章 古尸研究室_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/872.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八章 家中起尸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/873.html"
               },
               {
                   "chapter_title": "巫山妖棺 第九章 混乱迷途_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/874.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十章 上京_盗墓笔记9在...",
                   "chapter_url": "http://seputu.com/zanghaihua/875.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十一章 仙丹_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/876.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十二章 解宅_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/877.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十三章 看押_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/878.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十四章 女鬼_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/879.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十五章 古怪_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/880.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十六章 双龙_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/881.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十七章 巫峡_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/882.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十八章 水鬼_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/883.html"
               },
               {
                   "chapter_title": "巫山妖棺 第十九章 进山_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/884.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十章 豺熊_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/885.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十一章 古寨_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/886.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十二章 雨夜_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/887.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十三章 追踪_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/888.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十四章 鬼雷山_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/889.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十五章 走蛟_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/890.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十六章 乱坟沟_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/891.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十七章 无头人影_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/892.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十八章 监视_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/893.html"
               },
               {
                   "chapter_title": "巫山妖棺 第二十九章 沼泽_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/894.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十章 上树_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/895.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十一章 人棺_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/896.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十二章 钻尸洞_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/897.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十三章 红凶_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/898.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十四章 龙隐_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/899.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十五章 拆雷_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/900.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十六章 抗战基地_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/901.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十七章 鼠王（上）_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/902.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十八章 鼠王（下）_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/903.html"
               },
               {
                   "chapter_title": "巫山妖棺 第三十九章 白龙罩玉骨_盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/904.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十章 盗洞_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/905.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十一章 鬼军_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/906.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十二章 鼠祸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/907.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十三章 连接_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/908.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十四章 废斗_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/909.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十五章 入斗开棺_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/910.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十六章 双头凶煞_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/911.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十七章 汉奸_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/912.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十八章 机关_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/913.html"
               },
               {
                   "chapter_title": "巫山妖棺 第四十九章 殉葬坑_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/914.html"
               },
               {
                   "chapter_title": "巫山妖棺 第五十章 红孩儿_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/915.html"
               },
               {
                   "chapter_title": "巫山妖棺 第五十一章 替死鬼_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/916.html"
               },
               {
                   "chapter_title": "巫山妖棺 第五十二章 反现象_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/917.html"
               },
               {
                   "chapter_title": "巫山妖棺 第五十三章 密室(上)_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/918.html"
               },
               {
                   "chapter_title": "巫山妖棺 第六十五章 真假难辨_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/919.html"
               },
               {
                   "chapter_title": "巫山妖棺 第六十六章 杀心_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/920.html"
               },
               {
                   "chapter_title": "巫山妖棺 第六十七章 九生九死锁_盗...",
                   "chapter_url": "http://seputu.com/zanghaihua/921.html"
               },
               {
                   "chapter_title": "巫山妖棺 第六十八章 火烧_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/922.html"
               },
               {
                   "chapter_title": "巫山妖棺 第六十九章 飞蚁王_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/923.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十章 塌陷_盗墓笔记9...",
                   "chapter_url": "http://seputu.com/zanghaihua/924.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十一章 破釜沉舟_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/925.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十二章 绝壁惊魂_盗墓...",
                   "chapter_url": "http://seputu.com/zanghaihua/926.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十三章 点灯_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/927.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十四章 夺命棺_盗墓笔...",
                   "chapter_url": "http://seputu.com/zanghaihua/928.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十五章 过去_盗墓笔记...",
                   "chapter_url": "http://seputu.com/zanghaihua/929.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十六章 疑心暗鬼",
                   "chapter_url": "http://seputu.com/zanghaihua/930.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十七章 交心",
                   "chapter_url": "http://seputu.com/zanghaihua/931.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十八章 双脸",
                   "chapter_url": "http://seputu.com/zanghaihua/932.html"
               },
               {
                   "chapter_title": "巫山妖棺 第七十九章 密室机关",
                   "chapter_url": "http://seputu.com/zanghaihua/933.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十章 石龙",
                   "chapter_url": "http://seputu.com/zanghaihua/934.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十一章 真假胎",
                   "chapter_url": "http://seputu.com/zanghaihua/935.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十二章 邪",
                   "chapter_url": "http://seputu.com/zanghaihua/936.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十三章 不死",
                   "chapter_url": "http://seputu.com/zanghaihua/937.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十四章 破门",
                   "chapter_url": "http://seputu.com/zanghaihua/938.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十五章 道斗",
                   "chapter_url": "http://seputu.com/zanghaihua/939.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十六章 龙胎",
                   "chapter_url": "http://seputu.com/zanghaihua/940.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十七章 疑魂",
                   "chapter_url": "http://seputu.com/zanghaihua/941.html"
               },
               {
                   "chapter_title": "巫山妖棺 第八十八章 黑龙盘尸",
                   "chapter_url": "http://seputu.com/zanghaihua/942.html"
               },
               {
                   "chapter_title": "第八十九章 黑蛟",
                   "chapter_url": "http://seputu.com/zanghaihua/943.html"
               },
               {
                   "chapter_title": "第九十章 打捞",
                   "chapter_url": "http://seputu.com/zanghaihua/944.html"
               },
               {
                   "chapter_title": "巫山妖棺 第九十一章 蜘蛛扣",
                   "chapter_url": "http://seputu.com/zanghaihua/945.html"
               },
               {
                   "chapter_title": "巫山妖棺 第九十二章 山崩",
                   "chapter_url": "http://seputu.com/zanghaihua/946.html"
               },
               {
                   "chapter_title": "巫山妖棺 第九十三章 获救",
                   "chapter_url": "http://seputu.com/zanghaihua/947.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二章",
                   "chapter_url": "http://seputu.com/zanghaihua/948.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第三章",
                   "chapter_url": "http://seputu.com/zanghaihua/949.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第四章",
                   "chapter_url": "http://seputu.com/zanghaihua/950.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第五章",
                   "chapter_url": "http://seputu.com/zanghaihua/951.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第六章",
                   "chapter_url": "http://seputu.com/zanghaihua/952.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第七章",
                   "chapter_url": "http://seputu.com/zanghaihua/953.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第八章",
                   "chapter_url": "http://seputu.com/zanghaihua/954.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第九章",
                   "chapter_url": "http://seputu.com/zanghaihua/955.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十章",
                   "chapter_url": "http://seputu.com/zanghaihua/956.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十一章",
                   "chapter_url": "http://seputu.com/zanghaihua/957.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十二章",
                   "chapter_url": "http://seputu.com/zanghaihua/958.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十三章",
                   "chapter_url": "http://seputu.com/zanghaihua/959.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十四章",
                   "chapter_url": "http://seputu.com/zanghaihua/960.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十五章",
                   "chapter_url": "http://seputu.com/zanghaihua/961.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十六章",
                   "chapter_url": "http://seputu.com/zanghaihua/962.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十七章",
                   "chapter_url": "http://seputu.com/zanghaihua/963.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十八章",
                   "chapter_url": "http://seputu.com/zanghaihua/964.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第十九章",
                   "chapter_url": "http://seputu.com/zanghaihua/965.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十章",
                   "chapter_url": "http://seputu.com/zanghaihua/966.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十一章",
                   "chapter_url": "http://seputu.com/zanghaihua/967.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十二章",
                   "chapter_url": "http://seputu.com/zanghaihua/968.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十三章",
                   "chapter_url": "http://seputu.com/zanghaihua/969.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十四章",
                   "chapter_url": "http://seputu.com/zanghaihua/970.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十五章",
                   "chapter_url": "http://seputu.com/zanghaihua/971.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十六章",
                   "chapter_url": "http://seputu.com/zanghaihua/972.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十七章",
                   "chapter_url": "http://seputu.com/zanghaihua/973.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十八章",
                   "chapter_url": "http://seputu.com/zanghaihua/974.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第二十九章",
                   "chapter_url": "http://seputu.com/zanghaihua/975.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第四十章",
                   "chapter_url": "http://seputu.com/zanghaihua/976.html"
               },
               {
                   "chapter_title": "盗墓笔记9大结局 第四十一章",
                   "chapter_url": "http://seputu.com/zanghaihua/977.html"
               },
               {
                   "chapter_title": "第四十二章",
                   "chapter_url": "http://seputu.com/zanghaihua/978.html"
               },
               {
                   "chapter_title": "第四十三章",
                   "chapter_url": "http://seputu.com/zanghaihua/979.html"
               },
               {
                   "chapter_title": "第四十四章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/980.html"
               },
               {
                   "chapter_title": "第四十五章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/981.html"
               },
               {
                   "chapter_title": "第四十六章",
                   "chapter_url": "http://seputu.com/zanghaihua/982.html"
               },
               {
                   "chapter_title": "第四十七章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/983.html"
               },
               {
                   "chapter_title": "第四十八章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/984.html"
               },
               {
                   "chapter_title": "第四十九章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/985.html"
               },
               {
                   "chapter_title": "第五十章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/986.html"
               },
               {
                   "chapter_title": "第五十一章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/987.html"
               },
               {
                   "chapter_title": "第五十三章 尾声_盗墓笔记9在线阅...",
                   "chapter_url": "http://seputu.com/zanghaihua/989.html"
               },
               {
                   "chapter_title": "第五十二章_盗墓笔记9在线阅读",
                   "chapter_url": "http://seputu.com/zanghaihua/988.html"
               }
           ]
       },
       {
           "round_title": "盗墓笔记 贺岁篇",
           "round_detail": [
               {
                   "chapter_title": "南派三叔-南派三叔作品",
                   "chapter_url": "http://seputu.com/hesui/553.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 起源",
                   "chapter_url": "http://seputu.com/hesui/554.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 棺材",
                   "chapter_url": "http://seputu.com/hesui/555.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 往事",
                   "chapter_url": "http://seputu.com/hesui/556.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 移棺",
                   "chapter_url": "http://seputu.com/hesui/557.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 错误",
                   "chapter_url": "http://seputu.com/hesui/558.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 开棺",
                   "chapter_url": "http://seputu.com/hesui/559.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 乾坤",
                   "chapter_url": "http://seputu.com/hesui/560.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 里面",
                   "chapter_url": "http://seputu.com/hesui/561.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 黑水",
                   "chapter_url": "http://seputu.com/hesui/562.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 深渊",
                   "chapter_url": "http://seputu.com/hesui/563.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 螺蛳",
                   "chapter_url": "http://seputu.com/hesui/564.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 商量",
                   "chapter_url": "http://seputu.com/hesui/565.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 小溪",
                   "chapter_url": "http://seputu.com/hesui/566.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 影子",
                   "chapter_url": "http://seputu.com/hesui/567.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 杀杀",
                   "chapter_url": "http://seputu.com/hesui/568.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 窥探",
                   "chapter_url": "http://seputu.com/hesui/569.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 二叔",
                   "chapter_url": "http://seputu.com/hesui/570.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 阿琴",
                   "chapter_url": "http://seputu.com/hesui/571.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 传说",
                   "chapter_url": "http://seputu.com/hesui/572.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 石灰",
                   "chapter_url": "http://seputu.com/hesui/573.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 族谱",
                   "chapter_url": "http://seputu.com/hesui/574.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 安氏",
                   "chapter_url": "http://seputu.com/hesui/575.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 大雨",
                   "chapter_url": "http://seputu.com/hesui/576.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 物体",
                   "chapter_url": "http://seputu.com/hesui/577.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 死亡",
                   "chapter_url": "http://seputu.com/hesui/578.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 目的",
                   "chapter_url": "http://seputu.com/hesui/579.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 设局",
                   "chapter_url": "http://seputu.com/hesui/580.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 猎物",
                   "chapter_url": "http://seputu.com/hesui/581.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 真相",
                   "chapter_url": "http://seputu.com/hesui/582.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 秘密",
                   "chapter_url": "http://seputu.com/hesui/583.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 尾声",
                   "chapter_url": "http://seputu.com/hesui/584.html"
               },
               {
                   "chapter_title": "盗墓笔记 贺岁篇 后记",
                   "chapter_url": "http://seputu.com/hesui/585.html"
               },
               {
                   "chapter_title": "《盗墓笔记》电视剧启动 吴秀波陈坤疑...",
                   "chapter_url": "http://seputu.com/hesui/586.html"
               },
               {
                   "chapter_title": "盗墓笔记电视剧来了！胡歌演男主角",
                   "chapter_url": "http://seputu.com/hesui/587.html"
               },
               {
                   "chapter_title": "【最炫盗墓风】盗墓笔记X最炫民族风X...",
                   "chapter_url": "http://seputu.com/hesui/588.html"
               },
               {
                   "chapter_title": "《盗墓笔记》带你探寻云顶天宫",
                   "chapter_url": "http://seputu.com/hesui/589.html"
               },
               {
                   "chapter_title": "《盗墓笔记》电影版人物表",
                   "chapter_url": "http://seputu.com/hesui/590.html"
               },
               {
                   "chapter_title": "《盗墓笔记》中真实存在的27件奇葩物...",
                   "chapter_url": "http://seputu.com/hesui/990.html"
               },
               {
                   "chapter_title": "古代人的“盗墓笔记”",
                   "chapter_url": "http://seputu.com/hesui/991.html"
               },
               {
                   "chapter_title": "《盗墓笔记》烂成渣http://seputu.co...",
                   "chapter_url": "http://seputu.com/hesui/992.html"
               },
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