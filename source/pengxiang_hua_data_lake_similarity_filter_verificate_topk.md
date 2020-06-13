---
title: pengxiang_hua_data_lake_similarity_filter_verificate_topk
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_filter_verificate_topk.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import heapq
* import random
* import itertools
* from data_lake.similarity.filter_verificate.verify import verify
* from utlities.heap import HeapPriorityQueue
* import math
* from utlities.time_evaluate import *
* import numpy as np

## Methods

* def topk(records,k):
* def  initial_events(size):
* def  initial_results(records,k):
* def calc_similarity(r, s):

## Code

Python example

    import heapq
    import random
    import itertools
    from data_lake.similarity.filter_verificate.verify import verify
    from utlities.heap import HeapPriorityQueue
    import math
    from utlities.time_evaluate import *
    import numpy as np
    
    @timer
    def topk(records,k):
        events = initial_events(len(records))
        results,H = initial_results(records,k)
        inverted_list = {}
    
        while len(events) > 0:
            x,px,tub = events.pop(0)
            sk = results[0][2]
    
            if tub <= sk:
                break
            w = records[x][px]
            if  w in inverted_list:
                for item in inverted_list[w]:
                    y,py = item
                    a = max(x,y)
                    b = min(x,y)
                    if (a,b) not in H and a != b:
                        sim = calc_similarity(records[a],records[b])
                        H[(a,b)] = 0
                        if sim > sk:
                            results.pop(0)
                            results.append([a,b,sim])
                            results.sort(key=lambda z:z[2])
                        sk = results[0][2]
                inverted_list[w].append([x,px])
            else:
                inverted_list[w] = [[x,px]]
            spx = 1 - (px+1)/len(records[x])
            if spx > sk:
                events.append([x,px+1,spx])
                events.sort(key=lambda z:z,reverse=True)
        for result in results:
            print(result)
    
    def  initial_events(size):
        events = []
        for i in range(size):
            event = [i,0,1.0]
            events.append(event)
        return  events
    
    def  initial_results(records,k):
        results = []
        H = {}
        length = len (records)
        while len (H) < k:
            t1, t2 = np.random.choice (list (range (length)), 2, replace=False)
            a = max (t1, t2)
            b = min (t1, t2)
            if (a, b) not in H:
                H[(a, b)] = 0
                sim = calc_similarity (records[a], records[b])
                results.append ([a, b, sim])
        results.sort(key=lambda x : x[2])
    
        return results, H
    
    
    def calc_similarity(r, s):
        s = set (s)
        r = set (r)
        similarity = float (len (s & r) / len (s | r))
        return similarity
    
    if __name__ == '__main__':
        path = r'E:\rochover\dataset\set similarity\dataset\dblp\dblp-0.2_number.txt'
        path2 = r'E:\rochover\PycharmProjects\pengxiang_hua\data_lake\test\test_number.txt'
    
        start = time.time ()
        with open (path2, 'r', encoding='utf8') as f:
            r = f.readlines ()
        records = []
        for record in r:
            temp = [eval (e) for e in record.split ()]
            records.append (temp)
        end = time.time ()
        elapsed = asMinutes (end - start)
        print ('prepare time:    ', elapsed)
    
    
        print ('->' * 10, 'starting', '->' * 10)
        topk (records, 10)
        print ('<-' * 10, 'end', '<-' * 10)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
