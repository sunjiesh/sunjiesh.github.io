---

layout: post 
title: "Python3 Urllib使用" 
date: 2019-04-17 10:00:00 +0800
categories: Python
---


```

from urllib import request
from urllib import parse
import json

data = {}
data['key1'] = 'value1'
data['key2'] = 'value2'
request_gateway_with_post(data)

def request_get(data):
    params = parse.urlencode(data)
    url = 'http://localhost:8080/test?' + params
    resp = request.urlopen(url)
    json_obj = json.loads(resp.read().decode())
    return json_obj

def request_post(data):
    params = parse.urlencode(data)
    params = params.encode('ascii')
    url = 'http://localhost:8080/test'
    resp = request.urlopen(url=url,data=params)
    json_obj = json.loads(resp.read().decode())
    #print('json=' + str(json_obj))
    return json_obj
 ```
