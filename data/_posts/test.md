---
title: test
date: 2018-07-06 16:44:00
categories: others
tags: []
urlname: 83
---
```flow
st=>start: 用户登陆
op=>operation: 登陆操作
cond=>condition: 登陆成功 Yes or No?
e=>end: 进入后台

st->op->cond
cond(yes)->e
cond(no)->op
```