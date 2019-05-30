---
title: python爬取微博
date: 2017-04-05 15:22:00
categories: oldf
tags: []
urlname: 21
---
   微博算是用的比较多了，但是一条一条的翻看
太过于麻烦，无奈爬取之。
<!--more-->
- **环境：win7+python2.7；**
- python模块：request；bs4；beautifulsoup4；lxml；
- **chrome浏览器**
- 实现过程：
##  **获取cookie**：
打开chrome然后Ctrl+Shift+I调出开发者工具，点击tooggle device toolbar(Ctrl+shift+M)然后在Responsive选择合适的设备，![](http://i.imgur.com/D0MMgUl.png)我这里选择的是nexus5X，接下来打开weibo.com这时候应该看到的就是手机端网页的微博登录页面。![](http://i.imgur.com/xKxzCUN.png)在开发者工具中选中Network--Preserve log，然后登录微博。在开发者工具中找到有关m.weibo.cn的复制自己的cookie![](http://i.imgur.com/EwCHQaS.png)
##  **获取你想爬取微博的user_id**：
就是你要爬取的微博的主页网址中weibo.com/u/后面的数字部分![](http://i.imgur.com/0aANYrF.png)
## 开始利用python脚本爬取
这是python程序的源码：

```
#-*-coding:utf8-*-
import re
import string
import sys
import os
import urllib
import urllib2
from bs4 import BeautifulSoup
import requests
from lxml import etree

reload(sys) 
sys.setdefaultencoding('utf-8')
if(len(sys.argv)>=2):
    user_id = (int)(sys.argv[1])
else:
    user_id = (int)(raw_input(u"请输入user_id: "))

cookie = {"Cookie": "#your cookie"}
url = 'http://weibo.cn/u/%d?filter=1&page=1'%user_id

html = requests.get(url, cookies = cookie).content
selector = etree.HTML(html)
pageNum = (int)(selector.xpath('//input[@name="mp"]')[0].attrib['value'])

result = "" 
urllist_set = set()
word_count = 1
image_count = 1
print u'爬虫准备就绪...'

for page in range(1,pageNum+1):

  #获取lxml页面
  url = 'http://weibo.cn/u/%d?filter=1&page=%d'%(user_id,page) 
  lxml = requests.get(url, cookies = cookie).content

  #文字爬取
  selector = etree.HTML(lxml)
  content = selector.xpath('//span[@class="ctt"]')
  for each in content:
    text = each.xpath('string(.)')
    if word_count>=4:
      text = "%d :"%(word_count-3) +text+"\n\n"
    else :
      text = text+"\n\n"
    result = result + text
    word_count += 1

  #图片爬取
  soup = BeautifulSoup(lxml, "lxml")
  urllist = soup.find_all('a',href=re.compile(r'^http://weibo.cn/mblog/oripic',re.I))
  first = 0
  for imgurl in urllist:
    urllist_set.add(requests.get(imgurl['href'], cookies = cookie).url)
    image_count +=1

fo = open("/Users/Personals/%s"%user_id, "wb")
fo.write(result)
word_path=os.getcwd()+'/%d'%user_id
print u'文字微博爬取完毕'

link = ""
fo2 = open("/Users/Personals/%s_imageurls"%user_id, "wb")
for eachlink in urllist_set:
  link = link + eachlink +"\n"
fo2.write(link)
print u'图片链接爬取完毕'


if not urllist_set:
  print u'该页面中不存在图片'
else:
  #下载图片,保存在当前目录的pythonimg文件夹下
  image_path=os.getcwd()+'/weibo_image'
  if os.path.exists(image_path) is False:
    os.mkdir(image_path)
  x=1
  for imgurl in urllist_set:
    temp= image_path + '/%s.jpg' % x
    print u'正在下载第%s张图片' % x
    try:
      urllib.urlretrieve(urllib2.urlopen(imgurl).geturl(),temp)
    except:
      print u"该图片下载失败:%s"%imgurl
    x+=1

print u'原创微博爬取完毕，共%d条，保存路径%s'%(word_count-4,word_path)
print u'微博图片爬取完毕，共%d张，保存路径%s'%(image_count-1,image_path)
```
可以将上面的代码保存为wb.py然后在cmd里面运行
```
python wb.py
```
大功告成

----------



***2016/12/29 星期四 3:16:40 ***

## *补充：*
python模块的安装可以用easy_install的命令安装 例如
```
easy_install lxml
```
----------

----------
python模块pip安装：http://jingyan.baidu.com/article/e73e26c0d94e0524adb6a7ff.html
用Python写一个简单的微博爬虫: http://www.jianshu.com/p/7c5a4d7545ca
Microsoft Visual C++ Compiler for Python 2.7:
http://www.microsoft.com/en-us/download/details.aspx?id=44266
