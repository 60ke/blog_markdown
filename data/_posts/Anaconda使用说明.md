---
title: Anaconda使用说明
date: 2017-04-26 10:07:04
categories: python
tags: [python]
urlname: 51
---
Anaconda常用的命令：
--------------

 - -conda list 查看安装了哪些包。
 - conda env list 或 conda info -e 查看当前存在哪些虚拟环境
 - conda update conda 检查更新当前conda
 - conda -V 查看conda版本


<!--more-->

创建使用Python虚拟环境：
-------------

    conda create -n your_env_name python=X.X（2.7、3.6等）

打开命令行输入`python --version`可以检查当前python的版本。

使用如下命令即可 激活你的虚拟环境(即将python的版本改变)。

    Linux:  source activate your_env_name(虚拟环境名称)
    
    Windows: activate your_env_name(虚拟环境名称)


对虚拟环境中安装额外的包：
-------------

    使用命令`conda install -n your_env_name [package]`即可安装package到your_env_name中

关闭虚拟环境(即从当前环境退出返回使用PATH环境中的默认python版本)：
---------------------------------------

   使用如下命令即可。

 

      Linux: source deactivate
    
       Windows: deactivate

删除虚拟环境：
-------

   使用命令`conda remove -n your_env_name(虚拟环境名称) --all`， 即可删除。

删除环境中的某个包：
----------

   使用命令`conda remove --name $your_env_name  $package_name` 即可。
