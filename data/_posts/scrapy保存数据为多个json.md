---
title: scrapy保存数据为多个json
date: 2017-08-23 06:26:33
categories: python爬虫
tags: [scrapy]
urlname: 60
---
定义pipline：
----------

    # -*- coding: utf-8 -*-
    
    # Define your item pipelines here
    #
    # Don't forget to add your pipeline to the ITEM_PIPELINES setting
    # See: http://doc.scrapy.org/en/latest/topics/item-pipeline.html
    
    
    # class VmwarePipeline(object):
    #     def process_item(self, item, spider):
    #         return item
    
    import json
    import codecs
    
    
    class VmwarePipeline(object):
        def process_item(self, item, spider):
            self.file = codecs.open('%s.json'%item['vid'], 'w', encoding='utf-8')
            line = json.dumps(dict(item), ensure_ascii=False) + "\n"
            self.file.write(line)
            return item
        def spider_closed(self, spider):
            self.file.close()

PS：scrapy中spiders的解析不能执行的问题
---
目前为止遇到的情况有两种

 1. 解析函数本身存在问题，解析错误导致不能继续传递
 2. 解析的网址不在定义的`allowed_domains`中（这个比较坑，因为scrapy对于是否在`allowed_domains`的判断不够准确，没有必要的话最好不写这个`allowed_domains`）