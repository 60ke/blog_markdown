---
title: python之有道翻译
date: 2017-04-18 14:46:00
categories: python
tags: [python]
urlname: 40
---
Talk is cheap ， show you code


<!--more-->


    import urllib.request
    import urllib.parse
    import json
    import time
    '''
    head = {}
    head['User-Agent'] = 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36'
    '''
    while True :
        content = input('输入要翻译的内容(输入q!退出程序)：')
        if content == 'q!' :
            break
        url = 'http://fanyi.youdao.com/translate?smartresult=dict&smartresult=rule&smartresult=ugc&sessionFrom=https://www.baidu.com/link'
        data = {}
        data['type']= 'AUTO'
        data['i'] = content
        data['doctype'] = 'json'
        data['xmlVersion'] = '1.8'
        data['keyfrom'] = 'fanyi.web'
        data['ue'] ='UTF-8'
        data['action'] ='FY_BY_ENTER'
        data['typoResult'] ='true'
        data = urllib.parse.urlencode(data).encode('utf-8')
    
    
        req = urllib.request.Request(url,data)
        req.add_header('User-Agent' , 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36')
        response = urllib.request.urlopen(req)
        html = response.read().decode('utf-8')
        target = json.loads(html)
        print('翻译结果为：%s' %target["translateResult"][0][0]["tgt"])
        time.sleep(1)



