---
title: pengxiang_hua_data_lake_test_test
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_test_test.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from data_lake.similarity.filter_verificate.verify import verify
* import  math

## Methods

* def calc_similarity(x, y):

## Code

Python example

    from data_lake.similarity.filter_verificate.verify import verify
    import  math
    
    
    
    
    
    path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number.txt'
    path2 = r'E:\rochover\PycharmProjects\pengxiang_hua\data_lake\test\test_number.txt'
    
    with open (path, 'r', encoding='utf8') as f:
        r = f.readlines()
    records = []
    for record in r:
        temp = [int (e) for e in record.split ()]
        records.append(temp)
    
    def calc_similarity(x, y):
        s = set (records[x])
        r = set (records[y])
        result = float (len (s & r) / len (s | r))
        return result
    
    
    path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number_all_pairs_0.8.txt'
    with open(path,'r',encoding='utf8') as f:
        result =  f.readlines()
    records_all_pairs = []
    for record in result:
        temp = record.split('\n')[0]
        x, y, _ = temp.split (',')
        x = x.replace ('(', '')
        records_all_pairs.append((int (x), int (y)))
    
    
    path = r'E:\rochover\dataset\set similarity\dataset\orkut\orkut_number_topk_0.8.txt'
    # dblp-0.2_number_topk_0.8  dblp-0.2_number_adapt_topk_0.8
    with open(path,'r',encoding='utf8') as f:
        result =  f.readlines()
    records_topk = []
    for record in result:
        temp = record.split('\n')[0]
        x,y,_ = temp.split(',')
        x = x.replace('[','')
        records_topk.append((int(x),int(y)))
    
    t = set(records_all_pairs).difference (set(records_topk))
    t2 = set(records_topk).difference (set(records_all_pairs))
    
    print(len(t))
    for r in list(t):
        x,y = r
        sitar = calc_similarity(x,y)
        print(r,sitar)
    
    print(len(t2))
    for r in list(t2):
        x,y = r
        sitar = calc_similarity(x,y)
        print(r,sitar)
        print(records[x])
        print (records[y])
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
