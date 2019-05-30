---
title: ubuntu常用的一些设置
date: 2017-08-18 02:12:00
categories: Linux
tags: []
urlname: 56
---
运行程序时出现：unable to resolve host ke的解决办法：


<!--more-->


    sudo vi /etc/hosts
在hosts里面添加 127.0.0.1 localhost ke(hostname)

hostname可用

    hostname 用户名
的方法更改hostname，`vi /etc/hostname`可用永久更改hostname



ubuntu设置默认python：

    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 100
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 150

切换：

    sudo update-alternatives --config python