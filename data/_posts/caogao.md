---
title: caogao
date: 2017-09-06 06:46:00
categories: default
tags: []
urlname: 64
---
# python 爬虫
## **1.获取网页内容**
### **1.1不包含js代码网页**
对于静态网站，我们可以使用`urllib`,`urllib2`,`requests`，来获取网页的源代码；获取到的源代码，一般与我们在浏览器右键查看网页源代码看到的内容一致

##### 免登录，构造post的爬虫
[CNVD](file:///C:\Users\i5051\Desktop\python爬虫\crawl.py)
### **1.2包含js代码网页**

通过前端的js代码生成get，post请求

##### 模拟新浪微博登录爬虫：

[微博](file:///C:\Users\i5051\Desktop\python爬虫\login.py)


## 2.**对网页内容的解析**
### 常用第三方库
`BS4`     以dict的形式对网页进行解析

`lxml`    xml树状形解析网页

`requests`    强大的第三方库

### **框架**  
`scrapy`

爬虫
[vmware](file:///C:\Users\i5051\Desktop\python爬虫\VMware.py)
## **3.数据存储**
### 3.1存储为指定格式：`txt`，`json`，`csv`等等
### 3.2存储到数据库：`mysql`，`mongodb`

