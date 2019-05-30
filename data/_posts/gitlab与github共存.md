---
title: gitlab与github共存
date: 2018-07-05 10:02:20
categories: default
tags: []
urlname: 81
---
## gitlab与github共存 ##

 1. 生成公私匙

    `ssh-keygen -t rsa -C "邮箱地址"`
因为生成的时候有个默认的名字，所以注意修改名字使其共存

 2. 添加公匙
登录gitlab或者github，添加公匙

 3. 在.ssh文件下配置config（重点！！！）
`vim config`

    Host git.goldeneye.org.cn
     HostName git.goldeneye.org.cn
     User git
     IdentityFile /c/Users/i5051/.ssh/gitlab
    
    Host github.com
     HostName github.com
     User git
     IdentityFile /c/Users/i5051/.ssh/github


