---
title: django框架博客开发-2
date: 2017-04-10 08:27:00
categories: python
tags: []
urlname: 36
---
django的简单介绍
-----------

 - 创建项目

    django-admin startproject myblog//项目名称；


<!--more-->


 - manage.py子命令

    python manage.py
![](http://ww1.sinaimg.cn/large/6cf740f6gy1fehmrbsqlfj20hu0hsmxh.jpg)

 - 启动服务器

    python manage.py runserver 8000//端口可以自定义
## myblog项目目录介绍 ##
myblog目录：
![](http://ww1.sinaimg.cn/mw690/6cf740f6gy1fehmzctavej20ko08y74m.jpg)
项目的一个容器
包含项目的最基本的一些配置
目录名称不建议修改

 - wsgi.py

WSGI(Python Web Server Gateway Interface)//Python服务网关接口
Python应用于web服务器之间的接口

 - urls.py

URL配置文件
django项目中所有页面都需要我们自己配置其URL

 - settings.py
项目的总配置文件
里面包含了数据库，web应用，时间等各种配置

   
    import os
    
    # Build paths inside the project like this: os.path.join(BASE_DIR, ...)//项目根目录
    BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
    
    
    # Quick-start development settings - unsuitable for production
    # See https://docs.djangoproject.com/en/1.11/howto/deployment/checklist/
    
    # SECURITY WARNING: keep the secret key used in production secret!//django项目自动生产的安全码，项目启动必不可少
    SECRET_KEY = '1z*kh0w2bqn7kg)v#lv5xw4&f2(19ckz-u=ci8)&+(ow9i(6as'
    
    # SECURITY WARNING: don't run with debug turned on in production!//debug实际应用需要关闭
    DEBUG = True
    
    ALLOWED_HOSTS = []#允许访问网站的地址
    
    
    # Application definition
    
    INSTALLED_APPS = [
        'django.contrib.admin',#管理
        'django.contrib.auth',#认证
        'django.contrib.contenttypes',#内容类型
        'django.contrib.sessions',#session缓存
        'django.contrib.messages',#消息
        'django.contrib.staticfiles',#静态目录
    ]
    
    MIDDLEWARE = [					#中间键，django自带的工具集
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
    ]
    
    ROOT_URLCONF = 'myblog.urls'	#URL的根配置文件
    
    TEMPLATES = [					#模版，在django里是一个个的html文件
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [],
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]
    
    WSGI_APPLICATION = 'myblog.wsgi.application'
    
    
    # Database
    # https://docs.djangoproject.com/en/1.11/ref/settings/#databases
    
    DATABASES = {				#数据库配置
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }
    
    
    # Password validation
    # https://docs.djangoproject.com/en/1.11/ref/settings/#auth-password-validators
    
    AUTH_PASSWORD_VALIDATORS = [		#密码认证
        {
            'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
        },
    ]
    
    
    # Internationalization
    # https://docs.djangoproject.com/en/1.11/topics/i18n/
    
    LANGUAGE_CODE = 'en-us'
    
    TIME_ZONE = 'UTC'
    
    USE_I18N = True
    
    USE_L10N = True
    
    USE_TZ = True
    
    
    # Static files (CSS, JavaScript, Images)
    # https://docs.djangoproject.com/en/1.11/howto/static-files/
    
    STATIC_URL = '/static/'

 - _init_.py
python中声明模块的文件
内容默认为空