---
title: python对于词频的统计和排序
date: 2017-08-29 03:00:00
categories: python
tags: []
urlname: 62
---
以文件名字为product.txt的文件为例：
-----------------------

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    # @Date    : 2017-08-29 10:48:30
    # @Author  : 60ke (worileqing@163.com)
    # @Link    : http://www.worileqing.top
    # @Version : $Id$
    
    import os
    
    with open("product.txt","r") as f:
    	content = f.read().split('\n')
    d = dict()
    for s in content:
    	d[s]=d.get(s,0)+1
    print(d)
    print(len(content))
    print(len(d))
    print(sorted(d.items(),key=lambda item:item[1],reverse=True))
    #reverse=True将结果改为降序

PS:这个词频统计按行分开，对于小说类的成段文字可以参考下面的
----
1.代码来自：http://zwustudy.iteye.com/blog/2236094

    #coding=utf-8  
    ''''' 
    Created on 2015年8月15日 
    统计一篇英文文章各个单词出现的词频，并按单次的词频从大到小输出 
    @author: minmin 
    '''  
    import re  
    import collections  
      
    ''''' 
    从文件中读取内容，统计词频 
    '''  
    def count_word(path):  
        result = {}  
        with open(path) as file_obj:  
            all_the_text = file_obj.read()  
            #大写转小写  
            all_the_text = all_the_text.lower()  
            #正则表达式替换特殊字符  
            all_the_text = re.sub("\"|,|\.", "", all_the_text)  
              
            for word in all_the_text.split():  
                if word not in result:  
                    result[word] = 0  
                result[word] += 1   
                  
            return result  
          
      
    ''''' 
    以词频倒序 
    '''  
    def sort_by_count(d):  
        #字典排序  
        d = collections.OrderedDict(sorted(d.items(), key = lambda t: -t[1]))  
        return d  
      
    if __name__ == '__main__':  
        file_name = "..\my father.txt"  
      
        dword = count_word(file_name)  
        dword = sort_by_count(dword)  
          
        for key,value in dword.items():  
            print key + ":%d" % value  

![输出结果][1]


  [1]: http://dl2.iteye.com/upload/attachment/0111/0365/737162f7-33ef-32a3-9077-1ba1e135300c.png


2.代码来自http://blog.csdn.net/walkingalien/article/details/54292643

    # -*- coding: utf-8 -*-
    import sys,string,json
    reload(sys)
    sys.setdefaultencoding('utf8')
    
    fr=open('xyj.txt','r')
    characters=[]
    stat={}
    
    for line in fr:
        line=line.strip()
    
        if len(line)==0:
           continue
    
        #print type(line)
        line=unicode(line)
    
        #print type(line)
        for x in xrange(0,len(line)):
            if line[x] in [' ','\t','\n','，','.','。','！','：','“','”','？']:
                continue
            if not line[x] in characters:
                characters.append(line[x])
            if not stat.has_key(line[x]):
                stat[line[x]]=0
            stat[line[x]]+=1
    
    fw=open('result.json','w')
    fw.write(json.dumps(stat))
    fw.close()
    
    stat=sorted(stat.iteritems(),key=lambda d:d[1],reverse=True )
    
    print type(characters[0])
    for x in xrange(0,20):
        print characters[x]
    print '********************************************'
    print type(stat[0][0])
    for x in xrange(0,20):
        print stat[x][0],stat[x][1]
    fw=open('result.csv','w')
    for item in stat:
        fw.write(item[0]+':'+str(item[1])+'\n')
    fw.close()
    
    
    fr.close()  
输出：

    <type 'unicode'>
    ﻿
    吴
    承
    恩
    著
    第
    一
    回
    灵
    根
    育
    孕
    源
    流
    出
    心
    性
    修
    持
    大
    ********************************************
    <type 'unicode'>
    道 10023
    不 7984
    了 7144
    一 7079
    那 6934
    我 6575
    是 5907
    行 5474
    来 5431
    他 5297
    个 5206
    你 5086
    的 4971
    者 4887
    有 3909
    大 3603
    得 3514
    这 3481
    去 3377
    上 3260
    [Finished in 19.7s]