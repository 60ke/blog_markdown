---
title: 通过路由器自定义host与连接设备共享host
date: 2017-04-05 15:13:00
categories: oldf
tags: []
urlname: 19
---
次奥
<!--more-->
## 过程
我的路由器是newifi现在刷的是Pandorabox是基于openwrt的路由系统，系统集成的dhcp/dns服务可以自定义host![](http://i.imgur.com/wjaVIrT.png)。用winscp连接路由上传我们的host文件到路由，然后在路由设置里的额外的hosts文件打钩，填入我们刚刚的host。然后ssh连接路由输入命令
`/etc/init.d/dnsmasq restart`
Ps：如果是电脑本地的dns不能使用自定义的，需要改为路由器的dns，其实直接改为自动获取dns就行了。
## host