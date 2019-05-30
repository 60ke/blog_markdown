---
title: python基础之生成器，迭代器，高阶函数
date: 2017-04-18 08:31:00
categories: python
tags: [python]
urlname: 38
---
thumb,no
## 高阶函数 ##

    def add(x,y,f):
        return f(x)+(y)
    add(3,(-4),abs)//    7


<!--more-->


## 迭代器 ##
example:1
    for i in range(5)
        print(i)  
        
        0
        1
        2    
        3
        4

example:2

    xinxi = { "name" : "60ke",
              "age"  : "23",
              "hobby" : "challenge"
            }
    for each in xinxi:
        print(each,xinxi[each])

example:3

    string = "I Love Hard"
    it = iter(string)
    while True:
        try:
            each = next(it)
        except StopIteration://notice Aa
            break
        print(each)        //for each in string


## 生成器 ##

yield，相当于挂起的return


    def MYGEN():
        print('生成器被执行！')
        yield 1
        yield 2
    mygen = MYGEN()
![](http://ww1.sinaimg.cn/mw690/6cf740f6ly1feqv95pwefj209m076748.jpg)
 

在yield1之前加入 return 0 测试

![](https://ws1.sinaimg.cn/mw690/6cf740f6ly1feqvai03t0j20a706odft.jpg)


无限输出菲波那切数列：
    def fibs():
    	a=0
    	b=1
    	while True:
    		a,b=b,a+b
    		yield a
    for each in fibs():
        print(each)



看图思考


![](https://ws1.sinaimg.cn/large/6cf740f6ly1feqw323fr7j20nf0aw0t7.jpg)


    a = {s:s%3==0 for s in range(10)}
    print(a)

    {0: True, 1: False, 2: False, 3: True, 4: False, 5: False, 6: True, 7: False, 8: False, 9: True}



暴走的括号：
------

    
    b = {i for i in [1,1,12,3,2,23,3]}
    c = {i for i in (1,1,12,3,2,23,3)}
    d = {i for i in {1,1,12,3,2,23,3}}
    f = (i for i in {1,1,12,3,2,23,3})
    g = (i for i in (1,1,12,3,2,23,3))
    h = (i for i in [1,1,12,3,2,23,3])
    j = [i for i in (1,1,12,3,2,23,3)]
    k = [i for i in {1,1,12,3,2,23,3}]
    n = [i for i in [1,1,12,3,2,23,3]]
    print(b,c,d,f,g,h,j,k,n)

输出结果：

    {1, 2, 3, 12, 23} {1, 2, 3, 12, 23} {1, 2, 3, 12, 23} <generator object <genexpr> at 0x0000000002BB3468> <generator object <genexpr> at 0x0000000002BB34C0> <generator object <genexpr> at 0x0000000002BB3518> [1, 1, 12, 3, 2, 23, 3] [1, 2, 3, 12, 23] [1, 1, 12, 3, 2, 23, 3]
    >>> 


    >>> f = (i for i in {1,1,12,3,2,23,3})
    >>> next(f)
    1
    >>> next(f)
    2
    >>> next(f)
    3
    >>> next(f)
    12
    >>> 

总结:小括号与逗号可以创建生成器

[IMG]https://ws1.sinaimg.cn/large/6cf740f6ly1feqwzla4h6j20b60g0gls.jpg[/IMG]
