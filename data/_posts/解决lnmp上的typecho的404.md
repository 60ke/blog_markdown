---
title: 解决lnmp上的typecho的404
date: 2018-07-04 16:27:49
categories: others
tags: [blog]
urlname: 78
---
进入nginx配置`/usr/local/nginx/conf/vhost`
将`include enable-php.conf`替换为`include enable-php-pathinfo.conf`