---
layout: title
title: paramiko 执行sudo
date: 2019-05-28 12:00:26
tags:
---

```python
import paramiko
ssh = paramiko.SSHClient()
    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
host_ips = "127.0.0.1"
username = "admin"
password = "admin"
port = 22
ssh.connect(host_ip,port,username,password)
stdin, stdout, stderr = ssh.exec_command("sudo -S -p '' service redis restart;")
#stdout.read()可以获取输出内容

```

注意执行带有 `sudo`的 `ssh.exec_command()`时需要在命令前加 `sudo -S -p '' ` 