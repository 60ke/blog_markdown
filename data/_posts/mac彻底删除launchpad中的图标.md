---
title: mac彻底删除launchpad中的图标
date: 2018-09-14 08:52:00
categories: others
tags: []
urlname: 105
---
之前因为wifi的问题装了许多从网络上面下载的dmg软件，之后发现有些软件在卸载之后图标依然存在于启动台，下面是解决办法。


### 第一步：找到com.apple.dock.launchpad文件夹：

打开一个folder，按`command+shift+G`，在前往当中输入地址/private/var/folders，然后在里边自己尝试找到com.apple.dock.launchpad这个文件夹，我的路径是，省略号处应该大家都不一样，所以慢慢找，总之最后找到名为com.apple.dock.launchpad的文件夹。

### 第二步：找到数据库，获取其路径：

打开com.apple.dock.launchpad 文件夹

之后有一个db文件夹，再点进去有一个文件叫db,它就是我们要找的数据库。
### 第三步：开始对数据库进行操作

打开终端：cd到刚才拷贝的路径
然后输入：
`sqlite3 db "delete from apps where title='应用名称';"&&killall Dock`

注意要将应用名称处替换成你要删除的图标的名称，然后回车即可