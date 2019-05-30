---
title: VMware安装MacOS 
date: 2017-04-05 15:18:00
categories: oldf
tags: []
urlname: 20
---
---
title: VMware安装MacOS 
date: 2017-01-05 16:51:55
tags: mac
---
## 准备工作：
VMware12 
OX 10.12 Sierra镜像cdr
Unlocker208--VMware上的Mac补丁
（bios intelVT开启）
**工具地址**：链接：
<!--more-->
http://pan.baidu.com/s/1nv0iiZB 密码：f1tw
**VMware Workstation 12序列号**: 5A02H-AU243-TZJ49-GTC7K-3C61N 
## 安装过程
1. 安装VMware
2. 安装mac补丁
   解压unlocker208，右键win-install.cmd以管理员运行，然后等待cmd窗口自己关闭，unlocker208安装完成
1. 安装VMware里面的mac
   上述工作准备完成后新建虚拟机里面就会多出Apple Mac OS X(M)选项，安转即可
1. 不可恢复错误解决问题解决 mac安转完成打开出现提示不可恢复错误，此时进入虚拟机安装目录用记事本类的编辑器，编辑macOS 10.12.vmx加入以下代码：
`smc.version = "0"`
**完工**
## 补充
VMware优化：http://blog.csdn.net/whitehack/article/details/47074403/