---
title: scrapy之获取ubuntu安全公告，并将cve存储为json
date: 2017-08-22 03:33:00
categories: python爬虫
tags: [scrapy]
urlname: 58
---
创建ubuntu项目
----

    scrapy startproject ubuntu

创建spider模板
--------

    cd ubuntu
    scrapy genspider Ubuntu https://usn.ubuntu.com

    cat ubuntu/ubuntu/spiders/Ubuntu.py

    # -*- coding: utf-8 -*-
    import scrapy
    
    
    class UbuntuSpider(scrapy.Spider):
        name = 'Ubuntu'
        allowed_domains = ['https://usn.ubuntu.com']
        start_urls = ['http://https://usn.ubuntu.com/']
    
        def parse(self, response):
            pass
    ~             

编写spider
----

    # -*- coding: utf-8 -*-
    import scrapy
    from bs4 import BeautifulSoup
    import re
    import requests
    from ubuntu.items import UbuntuItem
    
    
    class UbuntuSpider(scrapy.Spider):
        name = 'Ubuntu'
        allowed_domains = ['usn.ubuntu.com']
        def start_requests(self):
            url = "https://usn.ubuntu.com/usn/"
            content = requests.get(url).text
            soup = BeautifulSoup(content,"html.parser")
            page = soup.find(attrs={"class":"right"}).text.strip()
            max_page = re.findall("Showing page 1 of (.+?) ",page)[0]
    
            start_urls = []
            for page in range(int(max_page)):
                page +=1
                url = 'https://usn.ubuntu.com/usn/?page=%s'%page
                yield scrapy.Request(url,callback=self.parse0)
                
    
        def parse0(self, response):
            # 获取公告中usn的cve_url
            cves = response.xpath("//@href").extract()
            for cve in cves:
                if cve.startswith("http://people.ubuntu.com/~ubuntu-security/cve/"):
                    item = UbuntuItem()
                    item['cve'] = cve
                    yield item
需要注意的地方：

 1. 通常需要重写start_requests()函数
 2. 导入模块语句`from ubuntu.items import UbuntuItem`
 3. 定义item`item = UbuntuItem()`注意后面的括号

存储为json
----
1.定义item

    # -*- coding: utf-8 -*-
    
    # Define here the models for your scraped items
    #
    # See documentation in:
    # http://doc.scrapy.org/en/latest/topics/items.html
    
    import scrapy
    
    
    class UbuntuItem(scrapy.Item):
        # define the fields for your item here like:
        # name = scrapy.Field()
        cve = scrapy.Field()

2.定义piplines

    # -*- coding: utf-8 -*-
    
    # Define your item pipelines here
    #
    # Don't forget to add your pipeline to the ITEM_PIPELINES setting
    # See: http://doc.scrapy.org/en/latest/topics/item-pipeline.html
    
    import json
    import codecs
    
    
    # class UbuntuPipeline(object):
    #     def process_item(self, item, spider):
    #         return item
    
    
    
    class UbuntuPipeline(object):
        def __init__(self):
            self.file = codecs.open('cve.json', 'w', encoding='utf-8')
        def process_item(self, item, spider):
            line = json.dumps(dict(item), ensure_ascii=False) + "\n"
            self.file.write(line)
            return item
        def spider_closed(self, spider):
            self.file.close()

3.spider中保存item的语句（见上面）

4.settings设置

    ITEM_PIPELINES = {
       'ubuntu.pipelines.UbuntuPipeline': 300,
    }


ps:写包含代码的文章的时候，不要用`ctrl+u`,`ctrl+o`来创建列表，会造成`ctrl+k`的代码显示不正常
====


