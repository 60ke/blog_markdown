---
title: sublime sftp 插件安装及破解
date: 2017-11-29 03:17:00
categories: default
tags: [sublime]
urlname: 73
---
每次装完系统都需要重新安装配置sublime+python的环境，这次写个文章记一下。

1.python配置
----------
在![](http://ww1.sinaimg.cn/large/6cf740f6ly1flyr6qgoj1j211y0lcjv9.jpg这里可以创建新的环境配置

 - linux(ubuntu)：

python3.sublime-build配置：

    {
     "cmd": ["/usr/bin/python3", "-u", "$file"],
     "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
     "selector": "source.python" 
     }

 - windows：

保存的目录在`C:\Users\i5051\AppData\Roaming\Sublime Text 3\Packages\User`里面
python3.sublime-build配置：

    {
        "cmd": ["XXXXXXXXXX","-u","$file"],
        "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
        "selector": "source.python",
    }
"""
"XXXXXXXXXX"用python.exe的全路径代替
"""

 - mac：

路径：`/Users/ke/Library/Application Support/Sublime Text 3/Packages`
python3.sublime-build配置：

    {
        "cmd": ["/usr/local/bin/python3", "-u", "$file"],
        "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
        "selector": "source.python"
    }

2.必备插件
------

 - SublimeTmpl：可以自定义新建文件模板

python模板配置，在setting-user中设置：

    {
      "attr": {
        "author": "60ke",
        "email": "worileqing@163.com",
        "link": "http://www.worileqing.top",
        "version": "python3"
      },
      "date_format": "%Y-%m-%d %H:%M:%S"
    }
快捷键设置，在key—bingding中设置：

    [   
        {  
            "caption": "Tmpl: Create python", "command": "sublime_tmpl",  
            "keys": ["ctrl+alt+p"], "args": {"type": "python"}  
        },  
    ]  

 - Sftp：ssh编辑远程文件必备

部分配置：
用sublime打开文件夹，右键文件夹，在sftp的editing remote mapping中编辑设置：

    "type": "sftp",
    
    "save_before_upload": true,
    "upload_on_save": true,
    "sync_down_on_open": false,
    "sync_skip_deletes": false,
    "sync_same_age": true,
    "confirm_downloads": false,
    "confirm_sync": true,
    "confirm_overwrite_newer": false,
    
    "host": "10.0.2.30",
    "user": "root",
    "password": "111111",
    "port": "22",

 - PrettyJson:格式化Json的插件

3.sublime的sftp的插件破解
-------------------

必备插件sftp：
1，Package Control可以用来install其他package
2，sftp远程编辑文件：安装：install->sftp具体配置

sftp工具破解
    1，下载python字节码反编译工具uncompyle2  (pyc 2 py) https://github.com/wibiti/uncompyle2
    2，安装uncompyle2
    3，工具安装后的位置 E:\Python27\Scripts\uncompyle2
    4，反编译文件commands.pyc
          python uncompyle2 -o  commands.py commands.pyc
   5，注释掉函数即可 sublime.set_timeout(reg, 1)

PS:sublime的go环境开发可以使用gosublime的插件


