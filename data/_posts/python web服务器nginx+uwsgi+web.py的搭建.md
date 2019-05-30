---
title: python web服务器nginx+uwsgi+web.py的搭建
date: 2016-02-09 04:37:00
categories: python
tags: []
urlname: 34
---
1、环境配置
python至少升级到2.6.6版本
安装nginx

    #rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm
    #yum install nginx


<!--more-->


安装MySQL数据库

    #yum -y install mysql mysql-server mysql-devel libdbi-dbd-mysql 
    #service mysqld start 
    #chkconfig mysqld on

    安装MySQLdb ( mysql-python ) 
    #easy_install mysql-python
    安装web.py ( 官网 ) 
    #easy_install web.py
    安装uwsgi ( 官网 ) 
    #easy_install uwsgi

2、 配置uwsgi 
uwsgi 的配置文件 可支持xml yaml ini等格式。这里使用ini格式的配置文件。默认路径为/etc/uwsgi.ini。

    [uwsgi] 
    #使用动态端口，启动后将端口号写入以下文件中
    socket = /tmp/uwsgi_vhosts.sock
    #也可以指定使用固定的端口
    #socket=127.0.0.1:9090 
    pidfile=/var/run/uwsgi.pid 
    daemonize=/var/log/uwsgi.log 
    
    master=true 
    vhost=true 
    gid=root
    uid=root
    
    #性能相关的一些参数，具体内容查看官网文档
    workers=10
    max-requests=5000 
    limit-as=512
3、 创建uwsgi开机自启动脚本，便于进行系统管理
   

     vi /etc/init.d/uwsgi，内容如下：
        #! /bin/sh  
        
        PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin  
        DESC="uwsgi daemon"  
        NAME=uwsgi  
        DAEMON=/usr/bin/uwsgi  
        CONFIGFILE=/etc/$NAME.ini  
        PIDFILE=/var/run/$NAME.pid  
        SCRIPTNAME=/etc/init.d/$NAME  
        
        set -e  
        [ -x "$DAEMON" ] || exit 0  
        
        do_start() {  
           $DAEMON $CONFIGFILE || echo -n "uwsgi already running"  
        }  
        
        do_stop() {  
           $DAEMON --stop $PIDFILE || echo -n "uwsgi not running"  
           rm -f $PIDFILE  
           echo "$DAEMON STOPED."  
        }  
        
        do_reload() {  
           $DAEMON --reload $PIDFILE || echo -n "uwsgi can't reload"  
        }  
        
        do_status() {  
           ps aux|grep $DAEMON  
        }  
        
        case "$1" in  
         status)  
           echo -en "Status $NAME: \n"  
           do_status  
         ;;  
         start)  
           echo -en "Starting $NAME: \n"  
           do_start  
         ;;  
         stop)  
           echo -en "Stopping $NAME: \n"  
           do_stop  
         ;;  
         reload|graceful)  
           echo -en "Reloading $NAME: \n"  
           do_reload  
         ;;  
         *)  
           echo "Usage: $SCRIPTNAME {start|stop|reload}" >&2  
           exit 3  
         ;;  
        esac  
        
        exit 0
    将脚本属性修改为可执行： 
        #chmod 755 /etc/init.d/uwsgi
        启用开机自动启动： 
        #chkconfig uwsgi on
        启动uwsgi服务： 
        #service uwsgi start 
        

4、 配置nginx下的uwsgi站点 
    例如新增以下一个站点uwsgi。 
    vi /etc/nginx/conf.d/uwsgi.conf, 内容：
   

     server { 
          listen  9091; 
          server_name  localhost; 
          root /www/uwsgi; 
          index index.html index.htm; 
          access_log logs/uwsgi.log; 
          error_log logs/uwsgi.log; 
          location / { 
            #使用动态端口
            uwsgi_pass unix:///tmp/uwsgi_vhosts.sock;
            #uwsgi_pass 127.0.0.1:9090; 
    
        include uwsgi_params; 
        uwsgi_param UWSGI_SCRIPT index;   #默认载入的脚本文件
        uwsgi_param UWSGI_PYHOME $document_root; 
        uwsgi_param UWSGI_CHDIR  $document_root; 
      } 
    }
    启动Nginx服务 
    #service nginx start 
    #chkconfig nginx on

5、编写Hello Word！

    #vim index.py 
    脚本名称和上面nginx虚机配置的uwsgi_param UWSGI_SCRIPT参数要一致
    不使用web.py框架的写法：
    01
    #!/usr/bin/python
    02
    import os
    03
    import sys
    
    06
    def application(environ, start_response):
    07
        status = '200 OK'
    08
        output = 'Hello World!'
    09
        response_headers = [('Content-type', 'text/plain'),
    10
                        ('Content-Length', str(len(output)))]
    11
        start_response(status, response_headers)
    12
        return [output]
    使用web.py框架的写法：
    #!/usr/bin/env python
    # -*- coding: utf-8 -*-  
    
    import web
    
    urls = (
      '/t', 'test', #测试
      '/', 'home'
    )
    
    app = web.application(urls, globals())
    #返回wsgi接口，application 是 wsgi app入口函数
    application = app.wsgifunc()
    
    class test:
      '测试'	  
    
      def GET(self):
        # 开发测试用
        referer = web.ctx.env.get('HTTP_REFERER', 'http://google.com')
        client_ip = web.ctx.env.get('REMOTE_ADDR')
        host = web.ctx.env.get('host')
        fullpath = web.ctx.fullpath
        user_agent = web.ctx.env.get('HTTP_USER_AGENT')
    
        data = ""
        data += 'Client: %s<br/>\n' % client_ip
        data += 'User-agent: %s<br/>\n' % user_agent
        data += 'FullPath: %s<br/>\n' % fullpath
        data += 'Referer: %s<br/>\n' % referer
    
        return data
    
      def POST(self):
        pass
    
    class home:
      '根目录请求的处理'		
      def GET(self):
        return "Hello Web.py"
    
      def POST(self):
        return self.GET()
    
    #定义404错误显示内容  
    def notfound():  
        return web.notfound("Sorry, the page you were looking for was not found.")  
    
    app.notfound = notfound  
    if __name__ == "__main__":
      app.run()

6、重新载入python脚本
   

     #service uwsgi reload
        或者
        #python index.py 9092

表示使用index.py脚本在9092端口新开启一个web服务监听
这样你写的hello word就生效了，现在可以在浏览器输入你的ip地址+端口来访问python web内容了


