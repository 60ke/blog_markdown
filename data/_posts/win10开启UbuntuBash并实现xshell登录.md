---
title: win10开启UbuntuBash并实现xshell登录
date: 2017-04-26 09:18:00
categories: others
tags: []
urlname: 50
---
看到win10内置ubuntubash没忍住，又把系统换成了win10


<!--more-->

一，开启Bash
--------

 1. 把系统设置改为开发人员模式
    ![](http://ww1.sinaimg.cn/large/6cf740f6gy1ff06qeqmyqj20m10hijry.jpg)
 2. 经控制面板进入程序开启Ubuntu子系统
    ![](http://ww1.sinaimg.cn/large/6cf740f6gy1ff06tnov4wj20md0fpq3y.jpg)
 3. 打开cmd输入bash开始下载Ps:不翻墙，正常情况下是无法下载的下面是解决下载的办法
    1.更改系统设置的区域为香港特别行政区
    2.更改本地dns为微软的dns：4.2.2.1; 4.2.2.2
 等待下载完成就好：
![](http://ww1.sinaimg.cn/large/6cf740f6gy1ff070e3hgxj20k50e1whq.jpg)

二，开启ssh
-------

 1. 设置root密码：
打开bash默认root登陆，用一下命令设置root密码：

    passwd root

 2. 开启ssh

    service ssh start

 3. 设置sshd

   

     vi etc/ssh/sshd_config

将PasswordAuthentication改为yes，PermitRootLogin改为yes
PS：如果（密匙登陆的情况）出现could not load host key的错误可以用dpkg-reconfigure openssh-server 生成


