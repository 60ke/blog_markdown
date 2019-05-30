---
title: iterm2
date: 2018-12-13 14:07:00
categories: Mac
tags: []
urlname: 108
---
# iterm2的美化
> https://www.cnblogs.com/soyxiaobi/p/9695931.html

# iterm2实现上传下载

## 安装lrzsz
`brew install lrzsz`

## 下载zmoden脚本
在https://github.com/mmastrac/iterm2-zmodem上将iterm2-send-zmodem.sh 和 iterm2-recv-zmodem.sh脚本下载下来并放到/usr/local/bin/目录下，注意赋予脚本执行的权限

## 配置iterm2 Trigger

打开iterm2 ------  同时按 command和,键 -----》 Profiles ------》  Default -----》 Advanced -----》 Triggers的Edit按钮，在弹出的界面配置以下参数

    Regular expression:\*\*B0100
    Action: Run Silent Coprocess
    Parameters: /usr/local/bin/iterm2-send-zmodem.sh

    Regular expression:\*\*B00000000000000
    Action: Run Silent Coprocess
    Parameters: /usr/local/bin/iterm2-recv-zmodem.sh
