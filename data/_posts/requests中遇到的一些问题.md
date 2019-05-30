---
title: requests中遇到的一些问题
date: 2018-08-01 10:54:00
categories: python爬虫
tags: []
urlname: 101
---
今天使用Python的requests模拟posts时总是，无法获取到正确的结果，后来使用postman的时候，在发送请求的时候在body中奖数据类型由默认的Text改为json可以成功，但是使用postman生成的python代码，并加入了正确的cookie还是不能获得正常的返回结果。检查代码，在headers中已经添加了`'content-type': "application/json"`，但是根据代码返回的异常判断还是发送的数据有问题，最后的解决办法是，在post数据的时候，直接`data=json.dumps(data)`,之后代码正常，这样可以判断出，服务端直接接受的json在python中其实为形如dict的字符串。
最后放上代码：


```python
import requests,json


url = "http://172.31.1.31/api/realtime_news"
data = json.dumps({"begin":"2017-01-01 00:00:00","end":"","size":"10","offset":"0","data":{"keyword":[],"keyword_any":[],"keyword_not":[],"emotion":["负面"],"media_type":["print_media"],"location":[]}})
cookies = {"token":"dcd709fe-956e-11e8-9eda-001a4a16015c","user_id":"12","username1":"liushike"}
headers = {"Accept": "application/json, text/javascript, */*; q=0.01","Content-Type": "application/json","Connection": "keep-alive",}
print(type(data))
print(json.loads(requests.post(url,headers=headers,data=data,cookies=cookies).text))
```

### `requests`的params参数构造
```python
params = (
    ('devid', '99000939663350'),
)
response = requests.post('https://r.cnews.qq.com/getSubNewsChlidInterest', headers=headers, params=params, data=data)
```
```python
等同于：
from urllib.parse import urlencode
params = (
    ('devid', '99000939663350'),
)
tar = urlencode(params)
print(tar)
'devid=99000939663350'
#进而构造出 https://r.cnews.qq.com/getSubNewsChlidInterest?devid=99000939663350
requests.post('https://r.cnews.qq.com/getSubNewsChlidInterest?devid=99000939663350', headers=headers, data=data)

```
