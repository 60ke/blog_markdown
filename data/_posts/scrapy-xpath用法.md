---
title: scrapy-xpath用法
date: 2017-08-22 02:04:10
categories: python爬虫
tags: [scrapy,xpath]
urlname: 57
---
转载自http://www.cnblogs.com/huhuuu/p/3701017.html　　
Scrapy是基于python的开源爬虫框架，使用起来也比较方便。具体的官网档：http://doc.scrapy.org/en/latest/

　　之前以为了解python就可以直接爬网站了，原来还要了解HTML，XML的基本协议，在了解基础以后，在了解下xpath的基础上，再使用正则表达式(python下的re包提供支持)提取一定格式的信息（比如说url），就比较容易处理网页了。

　　xpath是Scrapy下快速提取特定信息（如title,head,href等）的一个接口。


<!--more-->


　　

　　几个简单的例子：

　　/html/head/title: 选择HTML文档<head>元素下面的<title> 标签。
　　/html/head/title/text(): 选择前面提到的<title> 元素下面的文本内容
　　//td: 选择所有 <td> 元素
　　//div[@class="mine"]: 选择所有包含 class="mine" 属性的div 标签元素

 

　　基本的路径意义：

　　

表达式	描述
nodename	选取此节点的所有子节点。
/	从根节点选取。
//	从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。
.	选取当前节点。
..	选取当前节点的父节点。
@	选取属性。
　　

 

　　具体的使用实例：

　　比如对http://www.dmoz.org/Computers/Programming/Languages/Python/Books/ 网站提取特定的信息

　　1）、先在第一层tutorial文件夹下，在cmd中输入： scrapy shell http://www.dmoz.org/Computers/Programming/Languages/Python/Books/  

　　2）、现在比如我们需要抓取该网页的tittle，由于前面的shell命令已经实例化了一个selector的对象sel， 就输入 sel.xpath('//title') 获取了网页的标题。

　　3）、比如我们想要知道该网页下的www.****.com形式的链接，可以使用xpath 结合正则表达式re提取信息，输入   sel.xpath('//@href').re("www.[0-9a-zA-Z]+\.com")