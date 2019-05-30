---
title: centos安装python3
date: 2018-07-06 10:29:00
categories: python
tags: []
urlname: 82
---
每次虚拟机的centos装python3的时候都百度，打算自己记一下了
-----------------------------------
centos官方的yum源里面有个`python34`可以使用`sudo yum install python34`来进行安装，但是我最近在清华源下载的最小版本的centos[**镜像包href**][1]没有`python34`，`python2-pip`,运行`yum provides ifconfig`的命令也不好使。。。，这个暂时也没心思细究了，自己动手丰衣足食,还是编译安装吧！


 - 下载编译安装包

    

> https://www.python.org/ftp/python python官网的ftp这里你可以找各种版本，当前时间`2018-07-06 18:00:51`官网最新版本为python3.7，然后下载编译出错了，错误代码`No module named '_ctypes'`
然后查了一下，发现有说曾经别的版本出现过这个问题，然后官方修复之类的。。。,算了我还是稳妥的下了个[python3.5][2]，官网提供的压缩包有`tgz`，`tgz.xz`的，tgz.xz压缩率更高更小。

    wget https://www.python.org/ftp/python/3.5.5/Python-3.5.5.tgz.xz
    tar -xvJf Python-3.5.5.tgz
    cd Python-3.5.5
安装编译python3所需要的依赖

    yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
***话说输入`history`查看历史命令的时候发现没有记录，然后
    `cat /etc/profile|grep HIS`
看到设置的size为1000（玛德难受）***
继续python3安装

    make
    make install
    ./configure --prefix=/usr/local/python3
    ln -s /usr/local/python3/bin/python3 /usr/bin/python
    ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3

python3的安装完成了，这时候也已经有pip3的命令了。然后pip命令，手动安装一下
下载这个：

    wget https://bootstrap.pypa.io/get-pip.py
    python(python3) get-pip.py
好了。。。


  [1]: https://mirrors.tuna.tsinghua.edu.cn/centos/7.5.1804/isos/x86_64/CentOS-7-x86_64-Minimal-1804.iso
  [2]: https://www.python.org/ftp/python/3.5.5/Python-3.5.5rc1.tar.xz