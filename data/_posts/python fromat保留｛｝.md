---
title: python fromat保留｛｝
date: 2018-07-13 03:41:14
categories: default
tags: []
urlname: 84
---
今天写程序执行

    cmd = "ps -ef|grep {}|awk \'{print $2}\'|xargs kill -9"
    cmd.format(11)
结果报错：

    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    KeyError: 'print $2'
正确的写法：
    cmd = "ps -ef|grep {}|awk \'{{print $2}}\'|xargs kill -9"
    cmd.format(11)