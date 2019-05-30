---
title: python模块之difflib字符串，相似度差异比较
date: 2017-11-23 09:18:00
categories: python
tags: []
urlname: 71
---
最近要做redhat的版本比较，本来以为和ubuntu没差多少，之后才发现，redhat的yum源里面只放了一个当前的版本号，比如如果你安装的是vim7，之后vim升级到vim8，那么yum源里面只有一个vim8之前的vim7不能够通过yum源来获取了 这样一来，如果补丁包的版本不是最新的话，是无法通过yum源来直接获得软件的信息的，我们只能通过`yum list installed|grep (相关的包名的一部分字符串)`来查询。。。
说了这么多有点扯远了。开始说正事：
difflib模块：
介绍：This module provides classes and functions for comparing sequences. It can be used for example, for comparing files, and can produce difference information in various formats, including HTML and context and unified diffs. For comparing directories and files, see also, the filecmp module.

具体用法可以看这里：
https://docs.python.org/3/library/difflib.html?highlight=ndiff
今天只说字符串的相似度用法.

    difflib.get_close_matches(word, possibilities, n=3, cutoff=0.6)
    Return a list of the best “good enough” matches. word is a sequence for which close matches are desired (typically a string), and possibilities is a list of sequences against which to match word (typically a list of strings).
    
    Optional argument n (default 3) is the maximum number of close matches to return; n must be greater than 0.
    
    Optional argument cutoff (default 0.6) is a float in the range [0, 1]. Possibilities that don’t score at least that similar to word are ignored.
    
    The best (no more than n) matches among the possibilities are returned in a list, sorted by similarity score, most similar first.
    
    >>>
    >>> get_close_matches('appel', ['ape', 'apple', 'peach', 'puppy'])
    ['apple', 'ape']
    >>> import keyword
    >>> get_close_matches('wheel', keyword.kwlist)
    ['while']
    >>> get_close_matches('pineapple', keyword.kwlist)
    []
    >>> get_close_matches('accept', keyword.kwlist)
    ['except']
get_close_matches()函数，括号里面的参数依次是：目标字符串，要匹配的列表，匹配结果的个数限制，匹配相似度（0-1）。如果未满足要求则返回空列表。
