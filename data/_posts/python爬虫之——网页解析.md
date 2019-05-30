---
title: python爬虫之——网页解析
date: 2017-08-17 10:18:00
categories: python爬虫
tags: []
urlname: 55
---
常用的正则
=====

首先导入第三方包

    import re
常用的正则函数：

re.findall()
------------

re.findall()这个函数之前用的已经比较多了，除了以前提到的re.findall("",target)在“”中放入（.+?）来匹配要查找到内容，还可以结合python中 r+“”的特性，来进行正则查找，同时还可以使用多个（）来查找多个，之后再加上“”.jion(list)来实现list转字符串，然后又可以利用str.replace("","")来实现字符串的替换，talk is cheap，show you code

    import requests
    import re
    
    url = "http://		\"www.baidu.com http://www.baidu.com http://www.baidu.com http://www.baidu.com http://www.baidu.com"
    
    target_r = re.findall(r"http:(.+?)		\"",url)
    target = "".join(re.findall("http:(.+?)		\"",url)).replace("//","haha")
    print(target_r)
    print(target)
输出的结果：
['//']
haha

re.compile()
------------

    import re
    cveid = "CVE-2015-3456"
    pat = re.compile('CVE-(\d+)-\d+')
    m = pat.search(cveid)
    year = m.group(1)
    
    print(pat)
    print(m)
    print(year)
输出结果：

    re.compile('CVE-(\\d+)-\\d+')
    <_sre.SRE_Match object; span=(0, 13), match='CVE-2015-3456'>
    2015




## beautifulsoup ##

beautifulsoup 以我最近写的代码为例


    # -*- coding: utf-8 -*-
    import os
    import re
    import requests
    from bs4 import BeautifulSoup
    import json
    
    
    
    url = "http://www.huawei.com/cn/psirt/security-advisories/huawei-sa-20160706-01-openssl-cn"
    page = requests.get(url=str(url)).text
    html = requests.get(url=str(url)).content
    soup = BeautifulSoup(page,"html.parser")
    
    content = soup.find(attrs={'class':'col-sm-9 psiet-detail'})
    
    published_datetime = content.find(attrs={'id':'indexmain_0_liInieialReleaseDate'}).text
    
    a = re.findall(r'(\d+-\d+-\d+)',published_datetime)[0]
    
    last_modified_datetime = content.find(attrs={'id':'indexmain_0_liLastReleaseDate'}).text
    
    b = re.findall(r'(\d+-\d+-\d+)',last_modified_datetime)[0]
    
    name = content.find(attrs={'class':'bor-btom'}).text.strip()
    
    cvss_score = content.find(attrs={'class': 'psirt-list-out'}).find_all(attrs={"class": "psirt-set-out"})[3].find(attrs={"class":"moreinfo"}).text
    tab = soup.findAll('table')[0]
    vulnerable_software_list = []
    for tr in tab.findAll('tr'):  
        #print((tr.text))
        vulnerable_software_list.append(tr.text)
    
    print(vulnerable_software_list)

输出结果

    ['\n\n产品名称\n\n\n版本号\n\n\n修复版本号\n\n', '\n\n9032\n\n\nV100R001C00\n\n\nV100R001C00SPC101\n\n', '\n\n\xa0Agile Controller-Campus\n\n\nV100R001C00\n\n\nUpgrade to V100R002C10SPC400\n\n', '\n\nV100R002C00\n\n', '\n\nV100R002C10\n\n\nV100R002C10SPC400\n\n', '\n\nAnyOffice\n\n\nV200R002C20\n\n\nUpgrade to V200R006C00\n\n', '\n\nV200R003C00\n\n', '\n\nV200R005C00\n\n', '\n\n\xa0AR510\n\n\nV200R005C30\n\n\nUpgrade to V200R008C20\n\n', '\n\n\xa0BH620\n\n\nV100R001C00\n\n\nV100R001C00SPC106\xa0 \n\n', '\n\n\xa0BH620 V2\n\n\nV100R002C00\n\n\nV100R002C00SPC301B010\n\n', '\n\n\xa0CH221\n\n\nV100R001C00\n\n\nV100R001C00SPC266\n\n', '\n\nCH225 V3\n\n\nV100R001C00\n\n\nV100R001C00SPC102\n\n', '\n\nE5372s\n\n\nE5372s-32TCPU-V200R001B290D23SP00C00\n\n\nE5372s-32TCPU-V200R001B290D25SP00C00 \n\n', '\n\nE5377Bs\n\n\nE5377Bs-605TCPU-V200R001B305D09SP00C00\n\n\nE5377Bs-605TCPU-V200R001B313D13SP00C00\n\n', '\n\nE5786s\n\n\nE5786s-32aTCPU-V200R001B313D15SP00C00\n\n\nE5786s-32aTCPU-V200R001B313D17SP00C00\n\n', '\n\nE5878s\n\n\nE5878s-32TCPU-V200R001B305D11SP00C00\n\n\nE5878s-32TCPU-V200R001B313D13SP00C00 \n\n', '\n\nE6000 Chassis\n\n\nV100R001C00\n\n\nV100R001C00SPC501B010\n\n', '\n\nE9000 Chassis\n\n\nV100R001C00\n\n\nV100R001C00SPC296\n\n', '\n\nEEM\n\n\nV200R007C00\n\n\nUpgrade to V200R008C10\n\n', '\n\nV200R007C10\n\n', '\n\nV200R007C20\n\n', '\n\nV200R008C00\n\n', '\n\neLog\n\n\nV200R005C00\n\n\nV200R005C00SPC101\n\n', '\n\neSDK Platform \n\n\nV100R005C30\n\n\nUpgrade to V100R005C60\n\n', '\n\neSight Network\n\n\nV300R003C20\n\n\nV300R003C20SPC106\n\n', '\n\nV300R005C00\n\n\nV300R005C00SPC302\n\n', '\n\neSpace IVS\n\n\neSpace IVS V100R001C02SPC100\n\n\nUpgrade to eSpace VCN3000 V100R001C01SPC132\n\n', '\n\nEudemon8000E-X8\n\n\nV300R001C01\n\n\nV300R001C01SPCA00\n\n', '\n\nV500R001C00\n\n\nUpgrade to V500R002C00SPC100\n\n', '\n\nFireHunter6000\n\n\nV100R001C20\n\n\nV100R001C20SPC101\n\n', '\n\nFusionAccess\n\n\nV100R003C00\n\n\nUpgrade to V100R006C00\n\n', '\n\nV100R005C10\n\n', '\n\nV100R005C20\n\n', '\n\nV100R005C30\n\n', '\n\nFusionInsight HD\n\n\nV100R002C50\n\n\nUpgrade to V100R002C60SPC200\n\n', '\n\nFusionInsight\n\n\nFusionInsight V100R002C30\n\n\nUpgrade to FusionInsight HD V100R002C60SPC200\n\n', '\n\nFusionManager\n\n\nFusionManager V100R003C10\n\n\nUpgrade to FusionSphere OpenStack V100R006C00RC3B036\n\n', '\n\nFusionManager V100R005C00\n\n', '\n\nFusionManager V100R005C10SPC700\n\n', '\n\nFusionManager V100R006C00\n\n', '\n\nFusionStorage DSware\n\n\nFusionStorage DSware V100R003C02\n\n\nUpgrade to FusionStorage V100R003C30U1SPC001\n\n', '\n\nFusionStorage DSware V100R003C30\n\n\nUpgrade to FusionStorage V100R003C30U1SPC001\n\n', '\n\nFusionStorage\n\n\nV100R003C00\n\n\nUpgrade to V100R003C30U1SPC001\n\n', '\n\nG710-C00\n\n\nV100R001C92B118\n\n\nV100R001C92B135\n\n', '\n\nHG253s V2-20\n\n\nV100R001C205B027\n\n\nV100R001C205B052\n\n', '\n\nHG255s-10\n\n\nV100R001C163B013\n\n\nV100R001C163B026\n\n', '\n\xa0\n            HiSTBAndroid\n\n\nV600R001C00SPC060\n\n\xa0\n            V600R001C00CP0013\n\n', '\n\niBMC\n\n\nV100R002C10\n\n\nUpgrade to \xa0V200R002C10\n\n', '\n\nV100R002C30\n\n', '\n\nIVS\n\n\nIVS V100R002C10\n\n\nUpgrade to eSpace VCN3000 V100R002C10SPC108\n\n', '\n\nLogCenter\n\n\nV100R001C10\n\n\nUpgrade to V100R001C20SPC102\n\n', '\n\nV100R001C20\n\n\nV100R001C20SPC102\n\n', '\n\nMT992-10\n\n\nMV100R001C01B002\n\n\nV100R001C01B019\n\n', '\n\nOceanStor 18500\n\n\nV100R001C10\n\n\nUpgrade to V100R001C30SPC201\n\n', '\n\nOceanStor 18800 V3\n\n\nV300R003C00\n\n\nUpgrade to V300R003C10SPC100\n\n', '\n\nOceanStor 2860 V3\n\n\nOceanStor 2860 V3 V300R001C00T\n\n\nUpgrade to OceanStor 2800 V300R003C20\n\n', '\n\nOceanStor 5600 V3\n\n\nV300R001C00\n\n\nUpgrade to \xa0V300R003C10SPC100\n\n', '\n\nOceanStor 5600 V3\n\n\nV300R003C00\n\n\nUpgrade to V300R003C10SPC100\n\n', '\n\nOceanStor 5600 V3\n\n\nV300R003C10\n\n\nV300R003C10SPC100\n\n', '\n\nOceanStor 5800 V3\n\n\nV300R002C00\n\n\nUpgrade to V300R003C10SPC100\n\n', '\n\nOceanStor 9000\n\n\nO\xa0 V100R001C01\n\n\nUpgrade to V300R005C00SPC170\n\n', '\n\nV100R001C30\n\n\nOV300R005C00SPC170\n\n', '\n\nOceanStor 9000E\n\n\nOceanStor 9000E V100R001C01\n\n\nUpgrade to OceanStor 9000 V300R005C00SPC170\n\n', '\n\nOceanStor 9000E V100R002C00\n\n', '\n\nOceanStor 9000E V100R002C19\n\n', '\n\nOceanStor Backup \xa0Software\n\n\nV100R002C00\n\n\nV100R002C00LHWS01SPC100\n\n', '\n\nOceanStor BCManager\n\n\nV100R005C00\n\n\nUpgrade to V200R001C00\n\n', '\n\nOceanStor CSE\n\n\nOceanStor CSE V100R002C00LSFM01B010\n\n\nUpgrade to OceanStor Onebox V100R002C00LSFM01SPC108\n\n', '\n\nOceanStor HVS85T\n\n\nOceanStor HVS85T V100R001C30\n\n\nOceanStor 18500 V100R001C30SPC201\n\n', '\n\nOceanStor HVS85T\n\n\nOceanStor HVS85T V100R001C30\n\n\nOceanStor 18500 V100R001C30SPC201\n\n', '\n\nOceanStor N8500\n\n\nV200R001C09\n\n\nV200R001C09SPC506\n\n', '\n\nV200R001C91\n\n\nV200R001C91SPC902\n\n', '\n\nPolicy Center\n\n\nPolicy Center V100R003C00\n\n\nUpgrade to Agile Controller-Campus V100R002C10SPC400\xa0 \n\n', '\n\nPolicy Center V100R003C10\n\n', '\n\nPublic Cloud Solution\n\n\nPublic Cloud Solution OpsTools 1.0.3\n\n\nPublic Cloud Solution 1.0.9\n\n', '\n\nPublic Cloud Solution V100R001C00\n\n', '\n\nRH1288 V3\n\n\nV100R003C00SPC100\n\n\nV100R003C00SPC613\n\n', '\n\nRH2285H V2\n\n\nV100R002C00\n\n\nV100R002C00SPC505\n\n', '\n\nRH5885 V2\n\n\nV100R001C00\n\n\nUpgrade to V100R001C02SPC302\n\n', '\n\nRH5885 V3\n\n\nV100R003C00\n\n\nUpgrade to V100R003C10SPC102\n\n', '\n\nV100R003C01\n\n\nUpgrade to V100R003C10SPC102\n\n', '\n\nRH8100 V3\n\n\nV100R003C00\n\n\nV100R003C00SPC207\n\n', '\n\nSoftVCN\n\n\nV100R002C20\n\n\nV100R002C20SPC100\n\n', '\n\npeedport Hybrid\n\n\nV100R001C01B021\n\n\nUpgrade to V100R001C03B012\n\n', '\n\nUSG9560\n\n\nUSG9560 V300R001C20\n\n\nUpgrade to USG9500 V500R001C30\n\n', '\n\nUSG9560 V300R002C00\n\n\nUpgrade to USG9500 V500R001C30\xa0 \n\n', '\n\nVCM\n\n\nV100R001C10\n\n\nV100R001C10SPC006\n\n', '\n\nVCM5010\n\n\nVCM5010 V100R002C20\n\n\nUpgrade to VCM5020 V100R002C20\n\n', '\n\nXH320\n\n\nXH320 V100R001C00\n\n\nUpgrade to Tecal X6000 V100R001C02\n\n', '\n\nXH620\n\n\nXH620 V100R001C00\n\n\nUpgrade to XH620 V3 V100R003C00\n\n']

 ## 补充 ##
以前用BeautifulSoup一直用的"html.parser"的解析器，今天补充一下其他的
http://bbs.csdn.net/topics/392161042?list=lz
