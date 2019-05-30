---
title: python对字典进行划分
date: 2017-09-01 10:39:27
categories: python
tags: [python基础]
urlname: 63
---
code
----

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    # @Date    : 2017-09-01 15:38:11
    # @Author  : 60ke (worileqing@163.com)
    # @Link    : http://www.worileqing.top
    # @Version : $Id$
    
    import os
    list = ['a1','a2','a3','b1','b2','b3','c1']
    num = len(list)
    data = {}
    for i in range(num):
    	try:
    		print(data['%s'%list[i][0]])
    	except:
    		data['%s'%list[i][0]]=[]
    	if list[i][0] in data:
    		data['%s'%list[i][0]].append(list[i])
    print(data)

result：
----

['a1']
['a1', 'a2']
['b1']
['b1', 'b2']
{'a': ['a1', 'a2', 'a3'], 'b': ['b1', 'b2', 'b3'], 'c': ['c1']}