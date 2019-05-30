---
title: django框架博客开发-3
date: 2017-04-10 09:18:20
categories: default
tags: []
urlname: 37
---
创建应用
----

 - 进入manage.py同级目录
 - 命令行输入 python manage.py startapp blog
 - 添加应用名到settings.py中的INATALLED_APPS里


<!--more-->


![](http://ww1.sinaimg.cn/mw690/6cf740f6gy1feho7m3dahj209105x0sm.jpg)
 - 目录结构
 ![](http://ww1.sinaimg.cn/mw690/6cf740f6ly1fehp6vi63tj207w0b074v.jpg)
 - migrations
数据移植（迁移）模块
 - admin.py
该应用的后台管理系统配置
 - apps.py
该应用的一些配置
Django—1.9以后自动生成
 - models.py

数据模块
使用orm框架
类似于MVC结构中的Models

 - test.py
自动化测试模块
Django提供了自动化测试功能
在这里编写测试脚本（语句）
 - views.py
执行响应的代码所在模块
代码逻辑处理的主要地点
项目中大部分代码均在这里编写

创建第一个页面（响应）
----
编辑blog.views添加以下代码

        from django.http import HttpResponse
    def index(reques):
    	return HttpResponse('Hello,World')

 - 配置URL
打开myblog下的urls.py

![](http://ww1.sinaimg.cn/mw690/6cf740f6ly1fehp929yl0j209w05e3ye.jpg)

 - 打开sever，在浏览器输入网址打开页面
![](http://ww1.sinaimg.cn/mw690/6cf740f6ly1fehpcmv9vaj20au03tt8n.jpg)