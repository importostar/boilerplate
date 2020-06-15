---
title: pengxiang_hua_data_lake_similarity_filter_verificate_adapt_top_k
date: 2020-05-07
---
Example Python program pengxiang_hua_data_lake_similarity_filter_verificate_adapt_top_k.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from data_lake.similarity.filter_verificate.verify import verify
* from utlities.heap import HeapPriorityQueue
* from utlities.time_evaluate import *
* from utlities.statistics import *
* import numpy as np

## Methods

* def adapt_top_k(records,k):
* def find_first_gt_sk(list_t,sk,start,end):
* def initial_events(records):
* def initial_result(records,k):
* def calc_similarity(r,s):
* def similarity_upper_bound_access(spx,spy):
* def similarity_upper_bound_index(x,px):
* def similarity_upper_bound_probe(x,px):
* def find_second_common_pos(x,y,px,py):

## Code

Python example

    from data_lake.similarity.filter_verificate.verify import verify
    from utlities.heap import HeapPriorityQueue
    from utlities.time_evaluate import *
    from utlities.statistics import *
    import numpy as np
    
    @timer
    def adapt_top_k(records,k):
        events = initial_events(records) #enents min-heap,每个元素有三项值，并依据第三项值排序，因为每次需要弹出最大值，故第三项值取反后存入，弹出后取反还原
        result,H = initial_result(records,k)#result min-heap
        inverted_list = {}
        flag = False
        step = 1
        while(len(events) > 0 ):
            x,px,spx = events.remove_min()
            sk = result.min()[2]
            if -spx <= sk:
                break
    
            if step < math.ceil((-spx-sk)*len(records[x])):
                step += 1
            else:
                step = math.floor ((-spx - sk) * len (records[x]))
    
            for k in range(step):
                # p = len (records[x]) - math.ceil (sk * len (records[x])) + 1
                tub = similarity_upper_bound_probe (records[x], px + k)
                if  tub <= sk:
                    break
                w = records[x][px + k]
                if w in inverted_list:
                    for j in range (len (inverted_list[w])):
                        y, py = inverted_list[w][j]
                        if len (records[x]) * sk <= len (records[y]) <= len (records[x]) / sk:
                            a = max (x, y)
                            b = min (x, y)
                            if (a, b) not in H:
                                sim = calc_similarity (records[a], records[b])
                                H[(a, b)] = 0
                                if sim > sk:
                                    result.add ([a, b, sim])
                                    result.remove_min ()
                                sk = result.min ()[2]
                    si = similarity_upper_bound_index (records[x], px+k)
                    if k == 0:
                        if  flag == False :
                            if si >= sk:
                                inverted_list[w].append ([x, px])
                            else:
                                flag = True
                    elif si >= sk:
                        inverted_list[w].append ([x, (px + k)])
                else:
                    inverted_list[w] = [[x, (px + k)]]
            spx = similarity_upper_bound_probe (records[x], px + step)
            if spx > sk:
                events.add ([x, px + step, -spx])
        print('events_size；    ',len(events))
        temp = []
        while not result.is_empty ():
            item = result.remove_min ()
            print (item)
            temp.append (item)
        path = r'E:\rochover\dataset\set similarity\dataset\dblp\dblp-0.2_number_adapt_topk.txt'
    
        with open (path, 'w', encoding='utf8') as f:
            for item in temp:
                f.writelines (str (item) + '\n')
    
    def find_first_gt_sk(list_t,sk,start,end):
        left = start
        right = end
        while (left < right):
            mid = (right-left)//2 + left
            if sk == list_t[mid][2]:
                return mid
            elif sk < list_t[mid][2]:
                right = mid - 1
            else:
                left = mid + 1
        return left
    
    
    
    def initial_events(records):
        events = HeapPriorityQueue()
        for i in range(len(records)):
            events.add([i,0,-1.0])
        return events
    
    def initial_result(records,k):
        result = HeapPriorityQueue()
        H = {}
        length = len (records)
        while len(result) < k:
            t1,t2 = np.random.choice (list (range (length)), 2,replace=False)
            a = max (t1, t2)
            b = min (t1, t2)
            if  (a,b) not in H:
                H[(a, b)] = 0
                sim = calc_similarity (records[a], records[b])
                if sim == 0:
                    sim = 0.0000000001
                result.add ([a, b ,sim])
    
        return result,H
    
    def calc_similarity(r,s):
        s = set (s)
        r = set (r)
        rs = len (s & r)
        similarity = float (rs) / (len(r)+len(s)-rs)
        return similarity
    
    def similarity_upper_bound_access(spx,spy):
        return spx*spy/(spx+spy-spx*spy)
    
    def similarity_upper_bound_index(x,px):
        return  (len (x) - px )/(len (x) + px )
    
    def similarity_upper_bound_probe(x,px):
            return 1-px/len(x)
    
    def find_second_common_pos(x,y,px,py):
        while px < len(x)-1:
            px += 1
            if x[px] in y:
                py = y.index (x[px])
                break
        return px,py
    
    
    if __name__ == '__main__':
        path = r'E:\rochover\dataset\set similarity\dataset\dblp\dblp-0.2_number.txt'
        path2 = r'E:\rochover\PycharmProjects\pengxiang_hua\data_lake\test\test_number.txt'
    
        start = time.time ()
        with open (path, 'r', encoding='utf8') as f:
            r = f.readlines ()
        records = statistics(r)
        end = time.time ()
        elapsed = asMinutes (end - start)
        print ('prepare time:    ', elapsed)
    
    
        print ('->' * 10, 'starting', '->' * 10)
        adapt_top_k (records, 1021)
        print ('<-' * 10, 'end', '<-' * 10)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
