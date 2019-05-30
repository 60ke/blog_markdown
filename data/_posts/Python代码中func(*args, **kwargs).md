---
title: Python代码中func(*args, **kwargs)
date: 2017-04-22 04:10:00
categories: python
tags: [python]
urlname: 48
---
这个args其实是程序员对arguments的缩写，这种缩写可以说已经成为了一种传统（各种编程语言都这么做）；而argument的中文含义即为参数


<!--more-->

这是Python函数可变参数 args及kwargs

*args表示任何多个无名参数，它是一个tuple

**kwargs表示关键字参数，它是一个dict

测试代码如下：

    def foo(*args,**kwargs):
    print 'args=',args
    print 'kwargs=',kwargs
    print '**********************'
    if __name__=='__main__':
    foo(1,2,3)
    foo(a=1,b=2,c=3)
    foo(1,2,3,a=1,b=2,c=3)
    foo(1,'b','c',a=1,b='b',c='c')

执行结果如下：


    args= (1, 2, 3)
    kwargs= {}
    **********************
    args= ()
    kwargs= {'a': 1, 'c': 3, 'b': 2}
    **********************
    args= (1, 2, 3)
    kwargs= {'a': 1, 'c': 3, 'b': 2}
    **********************
    args= (1, 'b', 'c')
    kwargs= {'a': 1, 'c': 'c', 'b': 'b'}
    **********************

