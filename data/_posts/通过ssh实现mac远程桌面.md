---
title: 通过ssh实现mac远程桌面
date: 2017-09-06 08:49:00
categories: others
tags: [mac]
urlname: 65
---
teamviewer因为电脑重启的原因，更改了远程登录的密码，但是我没有保存 所以连接不上了。。。

# 下面是解决办法：
--------

### **必要条件：可以通过ssh连接！**

 - 首先通过ssh登录mac
 - 通过下面的命令安装teamviewer

    `brew cask install  teamviewer`

 - 启动teamviewer

    `open /Applications/TeamViewer.app`

 - 截图

    `screencapture /Users/iMac/Desktop/1.png`

 - 查看图片获取密码登录即可

### **teamviewer已经登录被其它窗口挡到怎么办？**
关闭再重新打开即可！

    killall TeamViewer
    open /Applications/TeamViewer.app