---
title: python requests post
date: 2020-05-07
---
Example Python program python-requests-post.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import requests
* import json

## Code

Python example

    import requests
    
    payload = {'key1': 'value1', 'key2': 'value2'}
    
    r = requests.post("https://httpbin.org/post", data=payload)
    print(r.text)
    
    # using tuples
    
    payload_tuples = [('key1', 'value1'), ('key1', 'value2')]
    r1 = requests.post('https://httpbin.org/post', data=payload_tuples)
    payload_dict = {'key1': ['value1', 'value2']}
    r2 = requests.post('https://httpbin.org/post', data=payload_dict)
    print(r1.text)
    
    
    import json
    
    url = 'https://api.github.com/some/endpoint'
    payload = {'some': 'data'}
    
    r = requests.post(url, data=json.dumps(payload))
    
    
    url = 'https://api.github.com/some/endpoint'
    payload = {'some': 'data'}
    
    r = requests.post(url, json=payload)
    
    
    # Post a multipart encoded file
    
    url = 'https://httpbin.org/post'
    files = {'file': open('report.xls', 'rb')}
    
    r = requests.post(url, files=files)
    r.text
    
    
    url = 'https://httpbin.org/post'
    files = {'file': ('report.xls', open('report.xls', 'rb'), 'application/vnd.ms-excel', {'Expires': '0'})}
    
    r = requests.post(url, files=files)
    r.text
    
    
    url = 'https://httpbin.org/post'
    files = {'file': ('report.csv', 'some,data,to,send\nanother,row,to,send\n')}
    
    r = requests.post(url, files=files)
    r.text
    
    # It is strongly recommended that you open files in binary mode. This is because Requests may attempt to provide the 
    # Content-Length header for you, and if it does this value will be set to the number of bytes in the file. Errors may occur # if you open the file in text mode.

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
