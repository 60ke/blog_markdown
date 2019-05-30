---
title: ubuntu中安装R和Rstudio
date: 2017-06-12 14:24:45
categories: others
tags: []
urlname: 53
---
转载自 作者：会心一击
出处：http://www.cnblogs.com/lijingchn/

1. 安装R

1.1 首先添加镜像源

sudo gedit /etc/apt/sources.list
加入新镜像源：
deb http://cran.rstudio.com/bin/linux/ubuntu trusty/
1.2 运行命令下载公钥

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 51716619E084DAB9
然后更新一下
sudo apt-get update
1.3 安装R

sudo apt-get install r-base
然后验证是否安装成功：在终端输入R，出现R的信息则安装成功。

2. 安装Rstudio

2.1 安装

首先，去下载对应自己系统的安装文件: http://www.rstudio.com/products/rstudio/download/，然后执行一下步骤。

　　

sudo apt-get install gdebi-core
sudo apt-get install libapparmor1  # Required only for Ubuntu, not Debian

sudo gdebi 下载的Rstudio的deb安装包
2.2 在Rstudio里安装ggplot2

安装ggplot2包之前需要先安装其它的依赖包：' plyr ' , ' digest ' , ' gtable ' , ' reshape2 ' , ' scales ' , ' proto ' , 在Rstudio的命令窗口分别执行以下命令。 

　　

复制代码
install.packages('plyr')
install.packages('digest')
install.packages('gtable')
install.packages('reshape2')
install.packages('scales')
install.packages('proto')
复制代码
然后，安装 ‘ ggplot2 ' 包 , 安装成功后就可以使用了。

install.packages('ggplot2')
 

