---
title: bash问题解决
date: 2017-11-26 12:48:32
categories: others
tags: []
urlname: 72
---
解决 [执行中]http: ../sysdeps/posix/getaddrinfo.c:2603：getaddrinfo: 假设 ‘IN6_IS_ADDR_V4MAPPED (sin6->sin6_addr.s6_addr32)’ 失败的问题
------------------------------------------------------------------------


Important Note: Existing Ubuntu 14.04 instances are NOT automatically upgraded to 16.04: You must manually upgrade your instance to Ubuntu 16.04 in one of two ways:

Remove & Replace (recommended)
Upgrade In-Place
Remove & replace
If you're currently running an Ubuntu 14.04 instance, we recommend removing and replacing your existing instance with a fresh new Ubuntu 16.04 instance.

WARNING: The instructions below will delete your existing distro and any of the files you've stored in the Linux filesystem. Therefore, be sure to copy/move any Linux files you want to keep, for example, to a Windows folder (e.g. /mnt/c/temp/wslbackup/...) BEFORE removing and replacing your instance!

To remove and re-install your Ubuntu instance, run the following commands from a Cmd/PowerShell Console.

C:\> lxrun /uninstall /full /y
...
C:\> lxrun /install
The lxrun /install command above will then download and install a fresh new copy of Ubuntu 16.04 onto your machine.

Upgrade In-Place
If your Ubuntu instance is particularly complex to configure, you can opt to upgrade it in-place, though this may not result in an optimal instance.

If you opt to upgrade your instance in-place, use Ubuntu's instructions for upgrading an existing instance:

$ sudo do-release-upgrade

具体可参考：https://blogs.msdn.microsoft.com/commandline/2017/04/11/windows-10-creators-update-whats-new-in-bashwsl-windows-console/