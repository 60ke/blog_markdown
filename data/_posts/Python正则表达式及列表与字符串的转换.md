---
title: Python正则表达式及列表与字符串的转换
date: 2017-04-19 09:19:00
categories: python
tags: [python,正则]
urlname: 41
---
## Talk is cheap ， show you code ##


<!--more-->


    import re
    hao = ('<h4><a data-bid="1004608738" data-eid="qd_C40" href="//book.qidian.com/info/1004608738" target="_blank">圣墟</a></h4>')
    target = re.findall(r'target="_blank">(.+?)</a>', hao)
    print(target)
    print(type(target))
    print ("".join(target))
    
    a = 'worileqing'
    li = list(a)
    print(type(a))
    print(type(a))
    print(li)
    print(li[5])




输出：

    ['圣墟']
    <class 'list'>
    圣墟
    <class 'str'>
    <class 'str'>
    ['w', 'o', 'r', 'i', 'l', 'e', 'q', 'i', 'n', 'g']
    e

参考：
    ![](https://ws1.sinaimg.cn/large/6cf740f6ly1fes3zi3i4ij20hc0engnl.jpg)

## re.findall与re.compile ##
测试代码

re.findall
----------

    import re
    a = "wodiddjfkj"
    b = re.findall(r"d.+?k",a)
    c = re.findall(r"d(.+?)k",a)
    print(b)
    print(c)
输出：

    ['diddjfk']
    ['iddjf']

re.compile
----

    import re
    a = "wodiddjfkj"
    b = re.compile(r"d.+?k")
    c = b.findall(a)
    print(b)
    print(c)
输出：

    re.compile('d.+?k')
    ['diddjfk']
## url解码： ##
测试代码：

    import urllib.parse
    print(urllib.parse.unquote("%E6%B5%8B%E8%AF%95abc"))

输出：

    测试abc

## url编码： ##
测试代码：

    import urllib.parse
    print(urllib.parse.quote("测试abc"))

输出：

    %E6%B5%8B%E8%AF%95abc

## 补充 ##
用(.+?)来匹配任意字符中“.”是不包含/n的所以。。。
解决办法：
用([\s\S]*)来表示

    bb = re.findall("2\.([\s\S]*)",aa))
表示的是匹配aa中"2."之后的所有内容