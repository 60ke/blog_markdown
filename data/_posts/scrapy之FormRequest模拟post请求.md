---
title: scrapy之FormRequest模拟post请求
date: 2018-01-02 07:36:19
categories: python爬虫
tags: []
urlname: 74
---
先放代码吧，以后闲了再完善


----------


    def start_requests(self):
        url = "http://www.hebzx.gov.cn/specialnews.aspx?meetingtype=009001"
        yield scrapy.Request(url,callback=self.parse0)
    def parse0(self,response):
        formdata = {"__EVENTTARGET":"AspNetPager1","__EVENTARGUMENT":"2"}
        return scrapy.FormRequest.from_response(
                    response,
                    formdata=formdata,
                    callback=self.parse1
                )       
    def parse1(self,response):
        print("1111111111111")
        print(response.text)