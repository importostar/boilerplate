---
title: use_korean_at_python_2_x
date: 2020-05-07
---
Example Python program use_korean_at_python_2_x.py

## Modules

* import sys
* import urllib
* import json

## Code

Python example

    # -*- coding: utf-8 -*-
    # 명시적으로 아래 코드는 utf-8임을 알림
    import sys
    
    test_string = '한글 python'
    print test_string
    
    # unicode decoding 출력 해보기, Error
    # print str(unicode(test_string))
    # UnicodeDecodeError: 'ascii' codec can't decode byte 0xed in position 0: ordinal not in range(128)
    
    # 명시적으로 인코딩
    print test_string.decode('utf-8').encode('utf-8')
    
    # unicode decoding 할 때 기본인코딩
    reload(sys)
    sys.setdefaultencoding('utf-8')
    print str(unicode(test_string))
    
    # url encoding
    # 한글 관련 파라미터 전송시
    import urllib
    
    # url path에 들어가면 %20이 들어가는 quote
    print urllib.quote(test_string)
    # %ED%95%9C%EA%B8%80%20python
    
    # 폼 데이터 전송시는 +로 변환되는 quote_plus
    print urllib.quote_plus(test_string)
    # %ED%95%9C%EA%B8%80+python
    
    # dict에 한글
    d = {}
    d["key"] = test_string
    print d
    
    # dict 한글 출력
    import json
    print json.dumps(d, ensure_ascii=False)
    print json.dumps(d, ensure_ascii=False, indent=4)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
