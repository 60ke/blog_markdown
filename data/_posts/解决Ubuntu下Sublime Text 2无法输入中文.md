---
title: 解决Ubuntu下Sublime Text 2无法输入中文
date: 2017-06-11 04:57:48
categories: others
tags: []
urlname: 52
---
ubuntu16.04下sublime text 2无法输入中文的问题


<!--more-->

 - 保存下面的代码到文件sublime_imfix.c(位于~目录，即主文件夹目录)

    #include <gtk/gtkimcontext.h>
    void gtk_im_context_set_client_window (GtkIMContext *context,
             GdkWindow    *window)
    {
     GtkIMContextClass *klass;
     g_return_if_fail (GTK_IS_IM_CONTEXT (context));
     klass = GTK_IM_CONTEXT_GET_CLASS (context);
     if (klass->set_client_window)
       klass->set_client_window (context, window);
     g_object_set_data(G_OBJECT(context),"window",window);
     if(!GDK_IS_WINDOW (window))
       return;
     int width = gdk_window_get_width(window);
     int height = gdk_window_get_height(window);
     if(width != 0 && height !=0)
       gtk_im_context_focus_in(context);
    }

 - 将上一步的代码编译成共享库libsublime-imfix.so
然后将libsublime-imfix.so拷贝到sublime_text所在文件夹,修改文件/usr/bin/subl的内容

 

    cd ~
    gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
    sudo mv libsublime-imfix.so /opt/sublime_text_2/
将

    #!/bin/sh
    /opt/sublime_text_2/sublime_text "$@"

修改为

    #!/bin/sh
    LD_PRELOAD=/opt/sublime_text_2/libsublime-imfix.so exec /opt/sublime_text_2/sublime_text "$@"

